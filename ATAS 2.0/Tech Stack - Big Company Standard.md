Programming
- Why Big Company like to use Java?

Python

Java
- OOP


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
	- N+1 查询问题（性能杀手）

Third Party


Standard
ISO20022
