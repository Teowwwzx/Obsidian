### 4. 还有什么大厂代码标准？(The Big Tech Checklist)

除了上面说的，如果你想进 Google/Bybit，你的代码还需要具备以下特质：

#### A. 依赖注入 (Dependency Injection)

- **做法：** 永远不要在函数内部手动创建 `db = SessionLocal()`。
    
- **标准：** 使用 FastAPI 的 `Depends(get_db)`。这让你的代码易于测试（测试时可以注入一个假的内存数据库）。
    

#### B. 类型提示 (Type Hinting) —— 必须严格！

- **不要写：** `def process(data):` (不知道 data 是什么)
    
- **要写：** `def process(data: UserCreateSchema) -> UserResponseSchema:`
    
- **工具：** 你的 IDE 会变聪明，而且可以用 `mypy` 进行静态检查。
    

#### C. 结构化日志 (Structured Logging)

- **禁止：** `print("Error happened")` (在服务器日志里这行字毫无意义)
    
- **标准：**
    
    Python
    
    ```
    import logging
    logger.info("Creating user", extra={"user_id": 123, "ip": "1.2.3.4"})
    ```
    
    大厂会把日志收集到 ELK 系统里，可以通过 `user_id` 搜出这个人所有的操作记录。
    

#### D. 环境变量 (Configuration)

- **禁止：** 把密码写死在代码里 `password = "123456"`。
    
- **标准：** 使用 `app/core/config.py` 读取 `.env` 文件。