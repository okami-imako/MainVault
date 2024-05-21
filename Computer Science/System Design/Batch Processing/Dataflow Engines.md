---
tags:
  - batch-processing
---
In order to fix the problems with [[Materialization of Intermediate State]] of [[MapReduce]] several new execution engines for distributed batch computations were developed known as ***dataflow engines***

They handle an entire workflow as one job

Instead of using mappers and reducers, these engines use more generalized ***operators***. The dataflow engine provides several different options for connecting one operator's output to another's input:
- [[Partitioning|Repartition]] and sort records by key - enables [[Map-Side Join#Sort-Merge joins]]
- Partition, but skip the sorting - enables [[Map-Side Join#Partitioned hash joins]]
- Just send one operator's output to the other's input - [[Map-Side Join#Broadcast hash joins]]

# Advantages
- Sorting is only performed where it's needed
- No unnecessary map tasks
- All joins and data dependencies are explicitly declared allowing scheduler to make locality optimizations
- No i/o to [[HDFS]]
- Operators can start executing as soon as their input us ready