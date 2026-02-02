Annotations

## @Entity
Tell JPA, this stock object is a database table
Affect: StockRepository can't detect this class, error: `Not a managed type`

## @Id
Tell JPA, this is primary key

## @GeneratedValue (Optional but recommended)
Tell JPA, help me generate ID, doesn't need me to setID manually.
`GenerationType.AUTO` mean Hibernate follow database type to choose (in H2 normally is 自增序列)

> [^1]Hibernate persistence provider will inspect the database you are connected to (e.g., MySQL, PostgreSQL, H2) and automatically select the most suitable and efficient method for generating primary key values.
> 
> Hibernate defaults to is using an **auto-increment sequence**. This is a mechanism where the database automatically assigns the next sequential number as the ID for a new record.

[^1]: 
