---
tags:
  - transactions/isolation
relates to:
  - "[[Serializable]]"
---
***Serializable Snapshot Isolation*** algorithm is a very promising approach.

It provides full *serializability* while having only a small performance penalty compared to the [[Repeatable Read|snapshot isolation]]

***Serializable Snapshot Isolation*** follows the principle of the [[Optimistic Concurrency Control]]

As the name suggests, it is based on [[Snapshot Isolation]] - all reads within a transaction are made from a consistent snapshot of the database. On top of that, SSI adds an algorithm for detecting serialization conflicts among writes and determining which transactions to abort

The algorithm should [[Detecting Stale MVCC reads|detect stale reads]] and [[Detecting Writes That Affect Prior Reads|detect that writes have affected recent reads]]

# Disadvantages
- It performs badly if there is high contention (many transactions trying to access the same objects), as this leads to a high proportion of transactions needing to abort. If the system is already close to its maxi‐ mum throughput, the additional transaction load from retried transactions can make performance worse.

# Advantages
- Due to the absence of locks, transactions that abort don't impact the throughput
- Read-Only transactions are never locked