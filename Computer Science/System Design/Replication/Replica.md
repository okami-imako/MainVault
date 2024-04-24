---
tags:
  - replication
  - concept
---
Each node that stores a copy of the database is called a *replica*

Every write to the database needs to be processed by every replica; otherwise, the replicas would no longer contain the same data.

The most common solution for this is [[Leader-Based Replication|leader-based replication]]

# Related Topics
- [[Replication]]