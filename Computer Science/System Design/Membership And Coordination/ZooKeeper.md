---
tags:
  - partitioning
relates to:
  - "[[Partitioning]]"
  - "[[Request Routing]]"
---
***ZooKeeper*** is a coordination service that keeps track of the cluster metadata.

ZooKeeper implements a [[Consensus]] algorithm, thus, providing [[Total Order Broadcast]] and [[Linearizability|linearizable]] operations

If an application grows to thousands of nodes, trying to perform majority votes over so many nodes would be terribly inefficient. Instead, ZooKeeper runs on a fixed number of nodes (usually three or five), and performs its majority votes among those nodes while supporting a potentially large number of clients.

Normally, the kind of data managed by ZooKeeper is quite slow-changing (current cluster leader, partition mapping, etc.)

ZooKeeper is a key-value datastore, which stores it's data in-memory with periodical flushes to the disk
# Features
## Partition Mapping
___
Each node registers itself in ***ZooKeeper***, and ***ZooKeeper*** maintains the mapping of partitions to the nodes.

Any partition-aware clients such as [[Request Routing|routing tier]] may subscribe to ***ZooKeeper*** in order to receive updates.

Whenever a partition changes ownership, or node leaves or joins the cluster, ***ZooKeeper*** notifies everyone.

![[ZooKeeper.png]]

## [[Linearizability|Linearizable]] [[Atomicity|atomic]] operations
___
Using at atomic [[Compare And Set]] operation, you can implement a [[Lock]] service (usually as a [[Lease]])

## [[Total Order|Total ordering]] of operations
___
When some resource is protected by a lock or a lease, you need a [[Fencing Token]] to prevent conflicts in case of process pauses. ZooKeeper [[Total Order|Totally Orders]] all `acquire lock` operations and give each operation a monotonically increasing *transaction ID* (`zxid`) and *version number* (`cversion`)

## [[Failure]] detection
___
Clients maintain a long-lived session on ZooKeeper servers, and they periodically exchange heartbeats to check that the other node is still alive.

Even if the connection is temporarily interrupted, or a ZooKeeper node fails, the session remains active.

However, if the heartbeats cease for a duration that is longer than the session timeout, ZooKeeper declares the session to be dead. Any locks held by a session can be configured to be automatically released when the session times out

## Change notifications
___
A client can subscribe to updates from ZooKeeper and listen for events like:
- New node joining the cluster
- Another node's failure

## Service Discovery
___
ZooKeeper is often used for ![[Service Discovery]]
## Membership Service
___
A membership service determines which nodes are currently alive and live members of a cluster. 

[[Detecting Faults]] is a tricky problem, however, if you couple [[Failure]] detection with [[Consensus]], nodes can come to an agreement about which nodes should be considered alive or not