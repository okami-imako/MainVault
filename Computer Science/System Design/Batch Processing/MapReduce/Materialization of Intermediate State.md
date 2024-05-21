---
tags:
  - batch-processing/map-reduce
relates to:
  - "[[MapReduce]]"
---
In order to pipe the output of one [[MapReduce]] job to the input of another job you need to set the output dir of the first as the input dir of the second. On top of that the second job has to wait until the first job completes

This setup is reasonable if the output of one job is treated as input to a bunch of different jobs (including jobs developed by other teams). Such publishing of data to a well-known location in the distributed filesystem allows [[Loose Coupling]]

However, in many cases, you know that the output of one job is only ever used as input to one other job, which is maintained by the same team. In that case the files on the distributed filesystem are simply ***intermediate state*** - a means of passing data from one job to the next.

The process of writing out this intermediate state to files is called ***materialization***. By contrast [[Unix]] pipes do not fully materialize intermediate state, instead the [[stream]] the output to the input using only a small in-memory buffer

# Downsides
- A MapReduce job can only start when all tasks in the preceding jobs have completed
- Mappers are often redundant: they just read back the same file that was just written by a reducer. If the reducer output was partitioned and sorted in the same way as mapper output, then reducers could be chained together directly.
- Storing intermediate state in a distributed filesystem means replication, which is a huge overkill