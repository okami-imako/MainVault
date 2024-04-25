---
tags:
  - transactions/isolation
relates to:
  - "[[Serializable Snapshot Isolation]]"
---
[[Snapshot Isolation]] is usually implemented by ***multi-version concurrency control*** (MVCC)

![[DetectingStaleMVCCReads.png]]
To detect serializability issues, when the transaction wants to commit, the database checks whether any of the ignored writes have been committed. If so, the transaction must be aborted.