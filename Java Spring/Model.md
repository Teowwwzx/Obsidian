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


# Java Data Type

| Data Type | Descriptions | Example |
| --------- | ------------ | ------- |
|           |              |         |




[^1]: Hibernate is a JPA (Java Persistence API) implementation and an Object Relational Mapping (ORM) framework
[^2]: H2 is a database. It is a lightweight, open-source relational database.
