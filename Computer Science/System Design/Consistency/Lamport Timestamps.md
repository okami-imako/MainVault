---
tags:
  - consistency-guarantee
---
***Lamport Timestamp*** is a simple method for generating sequence numbers that is [[Causal Consistency|consistent with causality]]

![[Pasted image 20240506195533.png]]
Each node has a ***unique identifier***, and each node keeps a counter of the number of operations it has processed

Two nodes may sometimes have the same counter value, but by including the ***node ID*** in the timestamp, each timestamp is made unique

# Rule
---
if you have two timestamps, the one with a ***greater counter*** value is the ***greater*** timestamp; if the counter values are ***the same***, the one with the ***greater node ID*** is the ***greater*** timestamp.

Every node and every client keeps track of the ***maximum*** counter value it has seen so far, and includes that maximum on every request. When a node receives a request or response with a maximum counter value greater than its own counter value, it immediately increases its own counter to that maximum.

>In the picture client A receives a counter value of 5 from node 2, and then sends that maximum of 5 to node 1. At that time, node 1’s counter was only 1, but it was immediately moved forward to 5, so the next operation had an incremented counter value of 6.

# Summary
As long as the maximum counter value is carried along with every operation, this scheme ensures that the ordering from the ***Lamport timestamps*** is *consistent with causality*, because every causal dependency results in an increased timestamp.

***Lamport timestamps*** are sometimes confused with [[Capturing The Happens Before Relationship|version vectors]]

Although there are some similarities, they have a different purpose: ***version vectors*** can distinguish *whether two operations are concurrent or whether one is causally dependent on the other*, whereas ***Lamport timestamps*** always enforce a [[Total Order|total ordering]]. From the total ordering of Lamport timestamps you cannot tell whether two operations are [[Concurrency|concurrent]] or whether they are [[Causal Consistency|causally dependent]]. The advantage of Lamport timestamps over version vectors is that they are more compact.