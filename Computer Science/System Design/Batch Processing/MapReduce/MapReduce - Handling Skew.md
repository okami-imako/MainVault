---
tags:
  - batch-processing/map-reduce
relates to:
  - "[[MapReduce]]"
---
The pattern of “bringing all records with the same key to the same place” breaks down if there is a very large amount of data related to a single key. 

Such disproportionately active database records are known as ***linchpin objects*** or ***hot keys***.

There are algorithms aimed at compensating
# Skewed Join
___
1) Run a sampling job to determine which keys are hot
2) When performing the actual join, the ***mappers*** send any records relating to a hot key to one of several ***reducers***, chosen at ***random*** (in contrast to conventional MapReduce, which chooses a reducer deterministically based on a hash of the key).
3) If there is a [[Reduce-Side Join]] going on, then records relating to the hot key need to be replicated to ***all*** reducers handling that key.
4) Apply another reduce to the outputs of all reducers that have worked on the ***hot key***
## Sharded join
Practically the same as the ***skewed join***, but requires the ***hot keys*** to be specified explicitly rather than using a sampling job