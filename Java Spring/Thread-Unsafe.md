
# Race Condition
**本质逻辑是：非原子性操作 (Non-atomic Operation)。** 你的 `buy` 方法包含了：**1. 读 -> 2. 改 -> 3. 写**。 只要这三步不是一气呵成的（中间可以被别人插足），它就是 Thread-Unsafe 的。

想象一下，只剩 **1 个** 苹果时，**线程 A** 和 **线程 B** 同时进来了：

1. **时间点 0.01ms:** 线程 A 问数据库：“还有多少？” 数据库说：“还有 **1** 个”。
    
2. **时间点 0.01ms:** 线程 B 问数据库：“还有多少？” 数据库说：“还有 **1** 个”（注意：A 还没来得及减）。
    
3. **时间点 0.02ms:** 线程 A 很高兴：“太好了，买它！” 于是计算 `1 - 1 = 0`。
    
4. **时间点 0.03ms:** 线程 B 也很高兴：“太好了，买它！” 于是计算 `1 - 1 = 0`。
    
5. **时间点 0.04ms:** 线程 A 把 **0** 写回数据库。
    
6. **时间点 0.05ms:** 线程 B 把 **0** 写回数据库。
    

**结果：** 两个人都觉得买了苹果，都发了货，但库存只减了 1 次。 **放大来看：** 你那 1000 个线程里，有几百次这样的“同时读取、互相覆盖”，导致明明卖了几百个苹果，库存却只像蜗牛一样慢慢减了 80 个。


![[Pasted image 20260203013100.png]]

![[Pasted image 20260203013142.png]]

![[Pasted image 20260203012748.png]]

![[Pasted image 20260203012726.png]]



## Synchronized
Mutual Exclusion Lock 互斥锁: This piece of code only can have one thread go in at a time.

### Distributed Lock
Java 的 `synchronized` 只能锁住**当前的 JVM**。如果服务器 A 和服务器 B 同时收到订单，它们各自的 `synchronized` 互不干扰，依然会同时改数据库。

- Atomicity
	- [[Redis]]
		1. Server A : `SET lock_key unique_value NX PX 30000`
			- `NX` 的意思是：只有当 `lock_key` 不存在时才成功（保证只有一个成功）。
		    - `PX` 是过期时间（防止服务器 A 挂了导致锁永远不释放）。
		2.  Result
			- 如果 Redis 返回 OK，服务器 A 拿到钥匙，开始操作数据库。
			- 如果服务器 B 也来领钥匙，Redis 发现 `lock_key` 已经存在，返回 Fail。服务器 B 只能等待或重试。
	- [[Zookeeper]]

![[Pasted image 20260203013034.png]]

![[Pasted image 20260203013155.png]]

💡
“有没有更高效的方法？不要让大家傻排队，但又要保证安全？”

### 悲观锁 (Pessimistic Lock)
像是银行柜台取钱。柜员处理你的业务时，把窗口牌子一挂“暂停服务”，后面的人只能干等，直到你办完。特点：安全，但慢。

`SELECT * FROM stock WHERE id = 1 FOR UPDATE;`
(重点是 `FOR UPDATE`，这会触发数据库的行锁)。

```
public interface StockRepository extends JpaRepository<Stock, Long> {

    // 关键注解：PESSIMISTIC_WRITE 代表写锁 (排他锁)
    @Lock(LockModeType.PESSIMISTIC_WRITE)
    @Query("SELECT s FROM Stock s WHERE s.id = :id")
    Optional<Stock> findByIdWithLock(Long id);
}
```

```
@Service
public class OrderService {
    // 必须加 @Transactional，因为数据库锁必须在事务内才有效！
    // 锁会在事务提交(commit)的那一刻自动释放
    @Transactional 
    public String buy(Long stockId) {
        // 使用我们刚写的带锁查询
        // 这一行执行时，如果已经有别人锁了，当前线程就会在这里“卡住”等待
        Stock stock = stockRepository.findByIdWithLock(stockId).orElseThrow();

        if (stock.getQuantity() > 0) {
            try { Thread.sleep(5); } catch (InterruptedException e) {} 
            
            stock.setQuantity(stock.getQuantity() - 1);
            stockRepository.save(stock);
            
            // 事务结束时，锁自动释放
            return "SUCCESS";
        } else {
            return "FAIL";
        }
    }
}
```

### 乐观锁 (Optimistic Lock)
大家都可以下单，但如果那一秒价格变了，你的单子就会被拒（Reject），你需要重新下单。特点：快，但可能失败。

- **查：** 我读出数据，发现 `version = 1`。
    
- **改：** 我想把库存 -1。
    
- **写：** 我告诉数据库：“把库存 -1，**前提是现在的 version 还是 1**”。
    
    - 如果数据库发现 version 已经是 2 了（被别人改过了）：**更新失败，抛出异常。**
        
    - 如果 version 还是 1：更新成功，把 version 变成 2。

---

# Visibility
- **现象：** 线程 A 修改了一个全局变量，线程 B 却看不见，依然在用旧的值。
    
- **Why：** 现代 CPU 有 L1/L2 缓存。线程 A 可能只改了自己的 CPU 缓存，没写回主内存（Main Memory）。
    
- **解决方法：** 使用 `volatile` 关键字（你之前问过的那个词！）。

# Instruction Reordering
- 为了优化性能，编译器或 CPU 会自作聪明地乱改你的代码顺序。
    
- **例子：** 你写的是 `a = 1; b = 2;`，CPU 觉得先执行 `b = 2` 更快。在单线程没问题，但在多线程下，如果线程 B 依赖 `a` 的值来判断 `b` 是否可用，就会瞬间崩掉。
    
- **解决方法：** 还是 `volatile`（它能建立内存屏障，禁止乱排）。

# Deadlock
- **现象：** 线程 A 拿着锁 1 想要锁 2，线程 B 拿着锁 2 想要锁 1。大家都不松手，系统直接卡死。
    
- **Why：** 锁的申请顺序不一致导致的逻辑闭环。


# Extra Knowledge
## Distributed Database
- [[Sharding]]
- [[Paxos]] / [[Raft]]