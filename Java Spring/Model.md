Annotations

## @Entity
This stock object is a database table
Affect: StockRepository can't detect this class, error: `Not a managed type`

## @Id
Primary key

## @GeneratedValue (Optional but recommended)
Tell JPA, help me generate ID, doesn't need me to setID manually.
`GenerationType.AUTO` mean [^1]Hibernate follow database type to choose (in [^2]H2 normally is 自增序列)

|ID Data Type|`GenerationType.AUTO` Strategy (Commonly Used)|How it Works|
|:--|:--|:--|
|**`long` or `int`**|**Identity/Sequence/Table** (Database-specific auto-increment)|The database (like H2, MySQL, or PostgreSQL) handles generating the next sequential number.|
|**`UUID` (String or Java `UUID` type)**|**UUID Generation Strategy**|Since a UUID (Universally Unique Identifier) is a 128-bit value (a long, unique string) and cannot be "auto-incremented," Hibernate's provider will typically use a mechanism to generate a unique UUID either in the application layer or by calling a database function (like `UUID()` in MySQL or `gen_random_uuid()` in PostgreSQL). **The database does not sequentially count them.**|


# Data Type

| Data Type                | Descriptions                                                                                                                                                                                                                                                                                                               | Example                                                                                                 |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| String                   | **Immutability:** `str = "a" + "b" + "c"`, Java will create few String object temporarily which wasted RAM.                                                                                                                                                                                                                |                                                                                                         |
| StringBuilder            | It turn to a dynamic draft which allow to modify original text without produce some garbage in RAM.                                                                                                                                                                                                                        |                                                                                                         |
|                          |                                                                                                                                                                                                                                                                                                                            |                                                                                                         |
| Int 32 bits (4 byte)     | Max cover 21 billions                                                                                                                                                                                                                                                                                                      |                                                                                                         |
| BigDecimal               | Pros: To avoid floating points issues like float<br>- **When to use:** Price, balance, finance calculation                                                                                                                                                                                                                 |                                                                                                         |
|                          |                                                                                                                                                                                                                                                                                                                            |                                                                                                         |
| UUID                     | Unorder<br>`a0eebc-99...`<br><br>**Pros**<br>**Cons**                                                                                                                                                                                                                                                                      | [[Page Splitting]]<br>                                                                                  |
| long 64 bits (8 byte)    | [[Primitive type  基础类型]]<br><br>Order<br>`1,2,3,4,5`<br><br>Pure number stored in RAM, fast performance but can't be **null.** It Covered from -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807<br><br>**Pros**<br>**Memory Optimization:** [[B-Tree 索引]]<br><br>**Cons**<br>                                       | High performance calculation inside a method or a loop. It stored in RAM [[Stack]] instead of [[Heap]]. |
| Long                     | [[Wrapped Object 包装类对象]]<br><br>Order<br>`1,2,3,4,5`<br><br>**Pros:**<br>**Nullability:** Creating new user, not yet stored in database. Now the program is `null` instead of `0`<br><br>**Generics:** Java collection does not support primitive type like `List` or `Set`. You can't write `List<long>`<br><br>**Cons:** |                                                                                                         |
|                          |                                                                                                                                                                                                                                                                                                                            |                                                                                                         |
| Set                      | Pro: To avoid duplicated data inside a set.<br>- noDuplicatedSet = {"a", "b"}                                                                                                                                                                                                                                              |                                                                                                         |
|                          |                                                                                                                                                                                                                                                                                                                            |                                                                                                         |
| HashDictionary           | Key-pair value and the performance O(1)<br>- Cons: More memory, no order when retrieved                                                                                                                                                                                                                                    |                                                                                                         |
| LinkedHashDictionary     | Pros: Store with timestamp<br>- Cons: Used more memory than HashDictionary                                                                                                                                                                                                                                                 |                                                                                                         |
| ConccurentHashDictionary | Pros: Can modify the same Dictionary at the same time<br>- Cons: More complex architecture<br>                                                                                                                                                                                                                             |                                                                                                         |
|                          |                                                                                                                                                                                                                                                                                                                            |                                                                                                         |
|                          |                                                                                                                                                                                                                                                                                                                            |                                                                                                         |


# Indexing

| Type                 | Description | Example |
| -------------------- | ----------- | ------- |
| Clustered Index 聚簇索引 |             |         |
| Tree                 |             |         |
| [[B-Tree 索引]]        |             |         |
| B + Tree             |             |         |

# Algorithms

| Snowflake |     |
| --------- | --- |
|           |     |














[^1]: Hibernate is a JPA (Java Persistence API) implementation and an Object Relational Mapping (ORM) framework
[^2]: H2 is a database. It is a lightweight, open-source relational database.
