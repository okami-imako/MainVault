---
tags:
  - transactions/isolation
relates to:
  - "[[Serializable Snapshot Isolation]]"
---
You also need to consider the case when one transaction updates the data already read by another transaction

The control mechanism is similar to [[Index-Range Locking]] except that [[Serializable Snapshot Isolation|SSI]] doesn't block other transactions.

![[DetectingWritesAfterReads.png]]

1) Transactions 42 and 43 both read the same data. If there is an index on `shift_id`, the database can use the index entry for 1234 to record that fact (if there is no index, the info can be kept at the table level and later vacuumed)
2) When transaction 42 updates the data, it can see through the index, that it was read by transaction 43, so it notifies 43 about the fact that the data it has previously read may become out-of-date.
3) Then transaction 43 does the same
4) Transaction 42 is the first one to commit
5) Database recognizes that transaction 42 has committed, so it aborts the transaction 43