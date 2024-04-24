---
tags:
  - replication/anomaly
---
- Event A comes ***before*** the event B.
- Someone listens to both events through the replicas. 
- First replica receives event B before the second replica receives event A
- Someone sees event B come before event A - ***bad***

![[ConsistentPrefixReads.png]]

Preventing this kind of anomaly requires another type of guarantee: ***consistent prefix reads***

This guarantee says that if a sequence of writes happens in a ***certain order***,
then anyone reading those writes will see them appear in the ***same order***.

This is a particular problem in [[Computer Science/System Design/Partitioning/Partitioning|partitioned (sharded)]] databases

One solution is to make sure that any writes that are causally related to each other are written to the same partition—but in some applications that cannot be done efficiently. There are also algorithms that explicitly keep track of causal dependencies ([[Capturing The Happens Before Relationship]])