---
tags:
  - replication
---
Some data storage systems have decided to ***abandon*** the concept of leaders allowing each replica to accept writes.

In some systems the client ***directly*** sends the writes to all replicas, while in the others the write distribution is being performed by the ***coordinator*** node, but it doesn't ensure the order of writes.

In case when one node goes down, what would happen in a leader-based replication is a [[Failover]], but in a leaderless setup there is no such thing as a failover.
![[LeaderlessReplication.png]]

When the node goes back up it may contain ***stale data*** due to the fact that it has missed some writes. What we can do is to make client read from ***several*** nodes in parallel, and then decide which data is most up to date by looking at the version number.

How does stale node catch up?
- ***Read Repair***. Client reads from multiple nodes and detects that one node is out of date, then client writes to that node. If some data is being read rarely, we end up with reduced [[Durability|durability]]
- ***Anti-Entropy Process***. Background process is constantly looking for diffs between replicas and copies missing data. Unlike the [[Replication Log]] it doesn't copy writes in any particular order and there may be significant delay before the data is copied.

# [[Quorum]] for reading and writing
If we have $n$ nodes and write is considered successful if $w$ nodes process it, then if on reads we query $r$ nodes and $r > n - w$ ($n-w$ can be viewed as the maximum amount of nodes that may not have processed the write), then at least one of the $r$ nodes we are reading from will contain an up-to-date data.

If fewer then required $r$ or $w$ nodes are available, then reads or writes are going to fail.

## Sloppy Quorum
If for example due to the network failure the client is cut off from the majority of the nodes and can't meet the quorum anymore there is a ***trade-off*** to be made
- return errors for all request that don't reach the quorum of $w$ or $r$ nodes?
- accept the writes anyway but send them to some nodes that are reachable but aren't among the $n$ nodes the value usually lives on?

The latter is called a ***sloppy quorum*** - you may lock yourself out of your house, but you can ask the neighbor to sit on their couch temporarily.

Once the network problem is fixed, any writes that one node temporarily accepted on someone's behalf are sent to the "home" node - ***hinted handoff*** (*once you find the keys to your house again, the neighbor politely asks you to get out*)

The sloppy quorum loses the quorum's guarantee. If you read from $r$ nodes you can receive a stale value, but any value is stored on ***some*** $w$ nodes.

# Related Topics
- [[Replication]]