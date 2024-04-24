---
tags:
  - partitioning/rebalancing
relates to:
  - "[[Partitioning]]"
---
Things may happen that can lead to the need for data/requests to be moved from one node to another. The process of moving load from one node in the cluster to another is called ***rebalancing***.

Usual requirements for rebalancing:
- Must be fair
- The system should continue to server reads and writes
- The amount of data moved between nodes should be minimized

Strategies for rebalancing:
- How not to do it [[Hash Mod N]]
- [[Fixed Amount Of Partitions]]: ***size of partition*** is proportionate to the ***size of the dataset***
- [[Dynamic Partitioning]] - ***amount of partitions*** is proportionate to the ***size of the dataset***
- [[Partitioning Proportionately To Nodes]] - ***amount of partitions*** is proportionate to the ***amount of nodes***