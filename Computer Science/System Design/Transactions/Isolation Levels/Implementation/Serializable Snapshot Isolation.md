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
