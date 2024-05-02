---
tags:
  - consistency-guarantee
---
The idea behind ***linearizability*** is to make a system appear as if there were only one copy of the data and all operations on it are atomic.

>In a linearizable system, as soon as one client successfully completes a write, all clients reading from the database must be able to see the value just written.

***Linearizability*** is a recency guarantee on reads and writes of a register (an individual object). It doesn’t group operations together into [[Transaction|transactions]], so it does not prevent problems such as [[Write Skew]], unless you take additional measures.

# Example
![[Linearizability.png]]
- First client B sent a request to read x, then client D sent a request to set x to 0, and then client A sent a request to set x to 1. Nevertheless, the value returned to B’s read is 1 (the value written by A). This is okay: it means that the database ***first*** processed D’s write, ***then*** A’s write, and ***finally*** B’s read. Although this is not the order in which the requests were sent, it’s an acceptable order, because the three requests are [[Concurrency|concurrent]]. Perhaps B’s read request was slightly delayed in the network, so it only reached the database after the two writes.
- Client B’s read returned 1 before client A received its response from the database, saying that the write of the value 1 was successful. This is also okay: it doesn’t mean the value was read before it was written, it just means the `ok` response from the database to client A was slightly delayed in the network.
- This model doesn’t assume any transaction isolation: another client may change a value at any time. For example, C first reads 1 and then reads 2, because the value was changed by B between the two reads. An atomic [[Compare And Set]] (cas) operation can be used to check the value hasn’t been concurrently changed by another client: B and C’s cas requests succeed, but D’s cas request fails (by the time the database processes it, the value of x is no longer 0).
- The final read by client B (in a shaded bar) is not linearizable. The operation is concurrent with C’s cas write, which updates x from 2 to 4. In the absence of other requests, it would be okay for B’s read to return 2. However, client A has already read the new value 4 before B’s read started, so B is not allowed to read an older value than A.