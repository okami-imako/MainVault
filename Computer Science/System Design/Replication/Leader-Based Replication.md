---
tags:
  - replication
relates to:
  - "[[Replication]]"
---
Works as follows:
1) One of the [[Replica|replicas]] is designated to be a *leader* (also known as *master* or *primary*). When clients want to write to the database, they must send their requests to the leader, which first writes the new data to its local storage.
2) The other replicas are known as *followers* (*read replicas*, *slaves*, *secondaries*, or *hot standbys*). Whenever the leader writes new data to its local storage, it also sends the data change to all of its followers as part of a [[Replication Log|replication log]] or *change stream*. Each follower takes the log from the leader and updates its local copy of the database accordingly, by applying all writes in the same order as they were processed on the leader.
3) When a client wants to read from the database, it can query either the leader or any of the followers. However, writes are only accepted on the leader (the followers are read-only from the client’s point of view).

![[LeaderBasedReplication.png]]

How to achieve high availability with leader-based replication?
- Follower Failure: [[Catch-Up Recovery]]
- Leader Failure: [[Failover]]

# Properties
You are assigning the decision-making capability to a single node. Such database is able to provide [[Linearizability|linearizable]] operations, uniqueness constraints, [[Total Order|totally ordered]] [[Replication Log]] and more

However, if that single leader fails, or if a network interruption makes the leader unreachable, such a system becomes unable to make any progress. There are three ways of handling that situation:
1) Wait for the leader to recover, and accept that the system will be blocked in the meantime. This approach does not fully solve [[Consensus]], because it does not satisfy the ***termination*** property
2) Manually fail over by getting humans to choose a new leader node and reconfigure the system to use it - ***consensus by "Act of God"***. The speed of failover is limited by the speed at which humans can act
3) Use an algorithm to automatically choose a new leader. This approach requires a consensus algorithm