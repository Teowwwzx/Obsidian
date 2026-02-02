Annotations

## @Entity
Tell JPA, this stock object is a db table
Affect: StockRepository can't detect this class, error: `Not a managed type`

## @Id
Tell JPA, this is primary key

## @GeneratedValue (Optional but recommended)
Tell JPA, help me generate ID, doesn't need me to setID manually.