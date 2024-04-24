---
tags:
  - partitioning
  - index
---
The idea is to construct a ***global index*** (rather then [[Partitioning Secondary Indexes By Document|local index]]) and distribute it across partitions.

![[PartitioningSecondaryIndexByTerm.png]]

In the example above the red cars from all partitions appear under the `color:red` entry in the index, but the index itself is partitioned so that colors from *a* to *r* are stored on partition 0, and colors from *s* to *r* appear on partition 1. the same goes for `make` attribute

This kind of index is called ***term partitioned***, because the [[Term|term]] we are looking for determines the partition of the index.

We can partition the index
- by the [[Partitioning By Key Range|term itself]] - effective range queries
- by the [[Partitioning By Hash Of Key|hash of the term]] - more distributed load

# Advantages
Advantage over [[Partitioning By Key Range]] is that you don't need to scatter over all partitions

# Disadvantages
Writes are more complicated. A single write now affects multiple partitions (every term in the document/row might be located on different node). In order to always keep the index up-to-date you have to implement [[Distributed Transactions|distributed transactions]] across all partitions affected by the write - which is not supported by most databases.

# Related Topics
- [[Partitioning And Secondary Indexes]]