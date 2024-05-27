---
tags:
  - "#consistency-guarantee/sync"
relates to:
  - "[[Heterogeneous distributed transactions]]"
---
Most non-trivial systems have a bunch of datastores: [[OLTP]] database, [[Cache]], [[Full Text Search]] index and a [[Data Warehouse]]

In that cases changes in database records need to be propagated to the other systems.

- [[Dual Writes]]
- [[Change Data Capture]]