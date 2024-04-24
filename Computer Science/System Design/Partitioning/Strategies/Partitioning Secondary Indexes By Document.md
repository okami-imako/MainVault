---
tags:
  - partitioning
  - index
---
# Description
Each [[Partitioning|partition]] has it's own [[Secondary Indexes|secondary index]] - easy-peasy.

![[PartitioningSecondaryIndexByDocument.png]]
Document-Partitioned index is also known as *local index* 

# Advantages
Effective writes - indexes and indexed data are located on the same node

# Disadvantages
In order to read you have to scatter across all partitions, which may get expensive

# Related Topics
- [[Partitioning And Secondary Indexes]]