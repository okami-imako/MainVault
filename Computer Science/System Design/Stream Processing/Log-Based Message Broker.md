---
tags:
  - stream-processing
relates to:
  - "[[Message Broker]]"
---
***Log-Based Message Broker*** is a hybrid, combining the durable storage approach of databases with the low-latency notification facilities of messaging

[[Producer]] sends a message by appending it to the end of the [[Log]]
[[Consumer]] receives messages by reading the log sequentially. If *consumer* reaches the end of the log, it waits for a notification that a new message has been appended

In order to scale to higher [[Throughput]], the log can be [[Partitioning|partitioned]]
Within each *partition*, the broker assigns a monotonically increasing sequence number, or ***offset***, to every message.

![[Pasted image 20240518172128.png]]

In order to achieve [[Durability]], the partitions can also be [[Replication|replicated]]