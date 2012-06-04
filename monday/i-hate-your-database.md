# Why I hate your database

- Misuse
- Ignorance
- Lies

Use different dbs for different occasions.

- Types of db
    - Relational/Document/Key-value
    - Graph, object, spatial, time-series, search... and many more

### Quick theory

- ACID: Atomicity, Consistency, Isolation, Durability
    - Atomicity: No half done transactions
    - Consistency: Validation
    - Isolation: I can't corrupt the data as transactions isolate from
      eachother
    - Durability: I don't lose my data!
- CAP: Consistency, Availability, Paritition Tolerance
    - Only ever 2 of 3 (well)

### Relational DBs

- Common pitfalls: standard abuse of column types. Poor querying.
- MySQL - many features, can't use them all at once. Can't have transactions
  and full text search. Poor query optimiser. Oracle (that's a good reason not
  to use it...).
    - Can be very fast for some operations?
- Sqlite
    - no integrity checking (being fixed)
    - Certain table alterations don't work
    - No concurrent access
    - Low overhead
    - Portable
    - Good at what it does, but don't abuse it for more than that!
- Postgres
    - Slow default configuration
    - Harder to learn?
    - Too many features?
    - Awesomely reliable
    - Not much to complain about really...

### Document databases

- advantages
    - no fixed schema
    - low entry barrier
    - closer to python datatypes
- problems
    - immature
    - no transactions
    - no integrity checking
- Schemas are **not** a bad thing! They can help you.

### Key value store

- Simple to use
- Traits:
    - Horizontal scaling
    - Exceedingly fast
    - There is only one way to query it
    - Batch/map-reduce queries
    - No transactions

### Spatial

- Strange beasts
- Knowledge of projections useful
- Spatial indexes really speed up some problems
- Generally add-on to an existing DB
- Not necessary if you don't really need them

### Filesystems

- Heirachical key-value store
- Multiple writers for appends
- Supports very large files

### Graph Databases

- Neo4j
- Brilliant for efficient neighbour queries
- Not much use for anything else.

### Round robin

- Deliberately lose old data
- Useful for logging or stats

### Final thoughts

- Very unlikely all your data fits into one paradigm.
- Just "buying a bigger server" actually gets you most of the way there... Only
  scale horizontally if you absolutely have to.
- If it sounds too good to be true, it probably is.
