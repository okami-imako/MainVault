---
tags:
  - partitioning
  - concept
---
Splitting a big database into smaller subsets called *partitions* so that different partitions can be assigned to different nodes (also known as *sharding*).

Normally each single record belongs to ***exactly one*** partition.

The main reason for partitioning is [[Scalability|scalability]]. Different partitions can be placed on different nodes in a [[Shared Nothing|shared nothing]] cluster. Thus, a large dataset can be distributed across many disks, and the query load may be distributed across many processors.

Partitioning is combined with [[Replication]]. This may look like this:
![[PartitioningAndReplication.png]]

Each partition leader is being assigned to one node and its followers are being assigned to other nodes. That way each node may be a leader of some partitions and a follower for others.