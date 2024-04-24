---
tags:
  - replication/anomaly
---
If user makes several requests and gets served by different replicas with different replication lags - he can see things ***go back in time***

![[MonotonicReads.png]]

Monotonic reads is a guarantee that this kind of anomaly does not happen. It’s a lesser guarantee than strong consistency, but a stronger guarantee than [[Eventual Consistency|eventual consistency]]

One way of achieving monotonic reads is to make sure that each user always makes their reads from the same replica