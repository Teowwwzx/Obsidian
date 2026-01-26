#### 1. 架构思维 (Architectural Logic)

- **CAP 定理 (Consistency, Availability, Partition Tolerance)**：这是分布式系统的“宪法”。你需要理解为什么在 Grab 这种“严肃行业”里，有时要牺牲一点点“数据一致性”来换取“系统永不宕机” 。
    
- **去中心化架构 (Gossip Protocol)**：学习节点之间是如何“聊天”并同步状态的。
    

#### 2. 数据处理 (Data Handling)

- **数据分区 (Data Partitioning & Consistent Hashing)**：这正是你提到的 **"Decoupling into small pieces"** 。学习 Cassandra 如何通过哈希算法把千万条订单平均分配到不同的服务器上 。
    
- **副本策略 (Replication Factor)**：如何确保同一份数据在不同地方有备份，保证“大家的食物”不会因为服务器起火而丢失 。
    

#### 3. 读写性能 (Performance)

- **LSM-Tree (Log-Structured Merge-Tree)**：这是 Cassandra 写入速度极快的核心秘密。它把随机写入变成了顺序写入，效率接近 $O(1)$ 。
    
- **CQL (Cassandra Query Language)**：虽然长得像 SQL，但它的逻辑完全不同。你需要学习如何基于“查询模式”来设计表，而不是基于“实体关系”。
    

#### 4. 高级维护 (DevOps 视角)

- **Compaction（压缩合并）**：学习系统如何自动清理旧数据，保持磁盘整洁 。
    
- **一致性级别 (Quorum, Local_One)**：在代码层面，你可以控制这笔交易需要多少个节点确认才算成功 。