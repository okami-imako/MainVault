---
tags:
  - partitioning
relates to:
  - "[[Partitioning]]"
  - "[[Request Routing]]"
---
***ZooKeeper*** is a coordination service that keeps track of the cluster metadata.

Each node registers itself in ***ZooKeeper***, and ***ZooKeeper*** maintains the mapping of partitions to the nodes.

Any partition-aware clients such as [[Request Routing|routing tier]] may subscribe to ***ZooKeeper*** in order to receive updates.

Whenever a partition changes ownership, or node leaves or joins the cluster, ***ZooKeeper*** notifies everyone.

![[ZooKeeper.png]]