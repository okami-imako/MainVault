---
tags:
  - consistency-guarantee
---
Ordering is recurring theme:
- The main purpose of the leader in [[Leader-Based Replication|single-leader replication]] is to determine the ***order of writes*** in the [[Replication Log|replication log]]. If there is no single leader, [[Write Conflict Resolution|conflicts can occur]] due to the [[Concurrency|concurrent]] nature of the operations
- [[Serializability]] is about ensuring that [[Transaction|transactions]] behave as if they were executed in ***some sequential order***
- Timestamps and clocks may be used as an attempt to order events - [[Unreliable Clocks]]