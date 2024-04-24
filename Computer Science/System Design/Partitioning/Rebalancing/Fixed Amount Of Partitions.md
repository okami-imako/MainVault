---
tags:
  - partitioning/rebalancing
relates to:
  - "[[Rebalancing Partitions]]"
---
Create a lot more partitions than there are nodes.

For example 10 nodes and 100 partitions.

That way when a node joins the party, it can gradually steal partitions from the other nodes. And vice versa - when the node leaves the cluster, it distributes partitions among other nodes

![[FixedAmountOfPartitions.png]]

## Problems
- You should choose high enough value to accommodate growth
- To many partitions bring management overhead
- May be hard to choose the right amount if the total size of the dataset is unpredictable