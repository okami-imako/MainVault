---
tags:
  - transactions/isolation
relates to:
  - "[[Serializable]]"
---
Genius, right?

Reasons to why this is actually a valid approach:
- RAM became cheap, in many cases you can store the whole dataset in memory, which makes executing transactions much faster
- [[Online Transaction Processing|OTLP]] transactions are usually short and make a small number of reads and writes. By contrast, long-running analytic queries are typically read-only, so they can bu run on a consistent snapshot outside of the serial execution loop

***Serial Execution*** is, in a sense, [[Pessimistic Concurrency Control|pessimistic]] to extreme - each transaction has a lock on the entire database
## Gocha
In such setup the database can't afford having *interactive* transactions - ping-ponging requests from the db to application code so that the application code can perform some logic (like checks) and then perform a write for example.

Interactive transactions would kill the throughput

Because of that usually the application must submit the entire transaction code to the db ahead of time as a [[Stored Procedures|stored procedure]]

![[InteractiveTransaction.png]]

___
You can [[Scalability|scale]] via [[Partitioning]]. If you can split the data so that each transaction won't have to leave a single partition that is. Otherwise the stored procedure would have to be executed ***with locks*** across multiple partitions, which is slow of course.
This is viable for simple key-value storage, but if you have secondary indexes, you require a lot of cross-partition coordination [[Partitioning And Secondary Indexes]]

# Summary
Serial execution of transactions has become a viable way of achieving serializable isolation within certain constraints:
- Every transaction must be small and fast, because it takes only one slow transaction to stall all transaction processing.
- It is limited to use cases where the active dataset can fit in memory. Rarely accessed data could potentially be moved to disk, but if it needed to be accessed in a single-threaded transaction, the system would get very slow, or [[Anti-Caching]] could be used - abort the transaction, asynchronously fetch the data into memory while continuing to process other transactions, and then restart the transaction when the data has been loaded.
- Write throughput must be low enough to be handled on a single CPU core, or else transactions need to be partitioned without requiring cross-partition coordination.
- Cross-partition transactions are possible, but there is a hard limit to the extent to which they can be used.