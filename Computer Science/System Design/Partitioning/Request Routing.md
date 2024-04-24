---
tags:
  - partitioning
  - routing
relates to:
  - "[[Partitioning]]"
  - "[[Rebalancing Partitions]]"
  - "[[Service Discovery]]"
---
When the data is [[Partitioning|scattered across the nodes]] and is [[Rebalancing Partitions|moved from time to time]] how does client decide which node to connect to?

This question is a part of a more general topic called [[Service Discovery]]

There are multiple approaches to this problem:
- Forward the request from node to node via [[Round Robin]] until it ends up on a node which owns the partition with the data, then pass the reply in reverse order
- Have some kind of router
- Make clients be aware of partitions and the assignments of the partitions to the nodes. That way they can connect directly to the node they want

![[RequestRouting.png]]

Anyway, how does the entity, that performs the routing, learn about the changes in the partition assignment?
- [[ZooKeeper]]
- *Gossip Protocol* - first schema in the picture. Doesn't require external dependency on smth like ***ZooKeeper***
- Use routing tier that learns about the partition mapping directly from the cluster nodes