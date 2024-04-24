---
tags:
  - partitioning/rebalancing
relates to:
  - "[[Rebalancing Partitions]]"
---
Idea is to have a fixed number of partitions ***per node***

In this case the ***size of partitions*** grows with the ***size of the dataset*** while the amount of nodes ***remains unchanged***, but when you ***increase*** the number of nodes, the partitions become ***smaller*** again

Basically the algorithm may look like this:
1) New node joins the cluster
2) It randomly chooses a fixed amount of partitions
3) Splits them in half
4) Takes ownership of every half of each partitions while leaving the other half of each partition in place

This algo may be unfair, but it smoothes out in the long run