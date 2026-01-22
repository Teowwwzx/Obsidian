System Design
- Distributed Application
	- Java
		- Spring Cloud
- Caching
	- Redis (Hit Rate, Cache Miss)
	- Stock price data in every second are stored in Redis instead of write the db
		- Ehcache, Caffeine
- Messaging
	- Python
		- Celery + Worker
	- Java
		- Apache Kafka
		- RabbitMQ, Active MQ
- Database
	- RDBMS: PostgreSQL, Oracle, MySQL
		- Store Money, Order (Why?)
	- Object Storage: AWS S3, Azure Blob, Cloudinary
		- Suitable for Image, PDF (Why?)
	- NoSQL: MongoDB, Cassandra
		- Un-structure data: comments
	- Common Types:
		- Arrays
		- Linked List
		- Stacks
		- Queues
		- HashMaps (Dictionaries)
		- Trees
		- Big I Notation?

Programming
- Why Big Company like to use Java?

Python

Java
- [[OOP]]
- Framework
	- Spring
	- It's a massive ecosystem instead a single tool
	- ICO (Inversion of Control - 控制反转)
		- Before have to create "new" for an object manually (new UserService()). In Spring, it will insert an object for you and this is called Dependency Injection（依赖注入）
	- AOP (Aspect Oriented Programming - 切面编程)
		- A lot of 函数 required logged. Instead of writing logger.info() in each 函数, why not just write a 切面 to make it execute before the 函数 is running.
		- This is excellent while dealing which bank transactional


Database
- ACID
	- Atomicity（原子性）：Either transaction successful, either failed.
	- Consistency（一致性）：Before & After the transaction, balance of both accounts must be correct.
	- Isolation（隔离性）：Two transactions happened in the same time would not disrupt each.
	- Durability（持久性）：Once saved, won't be missed out even electricity shortage.
- SQL (Structured Query Language)
	- SELECT, JOIN, INDEXES, Transactions
- ORM (Object-Relational Mapping)
	- A bridge that reflect the "object" into the "table"
	- WHY?
		- Is suffer to write SQL in JAVA
			- WHY?
	- Main Framework in JAVA
		- Hibernate
		- JPA (Java Persistence API)
	- Main Framework in Python
		- SQLAlchemy
		- user.save() -> INSERT INTO users ...
	- ==N+1 查询问题（性能杀手）==

Third Party

Testing
- Test-Driven Development (TTD): Write test code first, then functional code
Python
- Pytest
Java
- JUnit


Standard
ISO20022
