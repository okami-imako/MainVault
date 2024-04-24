---
tags:
  - replication
  - concept
---
Means keeping a copy of the same data ([[Replica|replica]]) on several different nodes, potentially in different locations. Replication provides redundancy: if some nodes are unavailable, the data can still be served from the remaining nodes. Replication can also help improve performance.

Reasons for replication:
- To keep data geographically close to your users (and thus reduce latency)
- To allow the system to continue working even if some of its parts have failed (and thus increase availability)
- To scale out the number of machines that can serve read queries (and thus increase read throughput)

Replication can be [[Synchronous|synchronous]] and [[Asynchronous|asynchronous]]

![[SyncAndAsyncReplication.png]]