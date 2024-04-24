---
tags:
  - partitioning/rebalancing
relates to:
  - "[[Rebalancing Partitions]]"
---
Idea is that the system tries to keep each partition's size to be inside of a preconfigured range.
- When partition becomes too big - it is split in half and one half may be taken by another node
- When partition becomes too small - it is merged with another partition

This process is similar to [[B-Tree]]

Total number of partitions adapts to the overall data volume
- Smol data - not many partitions - low overhead
- Big data - a lot of partitions

## Interesting Detail
When database is just started - there is no data
That means that it will start off with a single partition

I.e. until the data volume reaches a certain threshold, all requests will have to be handled by one node while others sit idle

Some databases allow ***pre-splitting*** - configuring an initial set of partitions on an empty database. That requires from you knowledge of the future data distribution