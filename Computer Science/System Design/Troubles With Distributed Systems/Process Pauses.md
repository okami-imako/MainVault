---
tags:
  - distributed-systems/problem
---
Say you have a database with a [[Leader-Based Replication|single leader]] per partition. Only the leader is allowed to accept writes.

![[Lease]]

## Similar Problem:
![[DistributedLock.png]]

Solution - [[Fencing Token]]