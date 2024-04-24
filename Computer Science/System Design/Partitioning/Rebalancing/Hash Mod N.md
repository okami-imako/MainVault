---
tags:
  - partitioning/rebalancing
relates to:
  - "[[Rebalancing Partitions]]"
  - "[[Partitioning By Hash Of Key]]"
---
Hash Mod N is an approach to deciding which partition the key will go to in a [[Partitioning By Hash Of Key]] strategy

In a nutshell you take a mod (%) of the hash value and that's the index of partition.
If you have 10 partitions - you calculate `hash % 10`

The problem with this approach is that if the number of nodes changes, the keys have to move - you don't want to move the keys more than you have to.