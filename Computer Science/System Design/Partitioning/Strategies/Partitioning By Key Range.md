---
tags:
  - partitioning/strategy
---
In case of a [[Key-Value Datastore|key-value datastore]] if the key is sortable you can assign each partition a continuous range of keys. Then by looking at the key you would know, which partition it belongs to. You can even go directly to the node that partition belongs to, if you know which one it is - just like picking up the right encyclopedia chapter of the bookshelf.
![[PartitioningByKeyRange.png]]

Data may not be evenly distributed, partitions should adapt.

Within each partition data keys could be sorted ([[SSTables]], [[LSM-Trees]])

# Related Topics
- [[Computer Science/System Design/Partitioning/Partitioning]]