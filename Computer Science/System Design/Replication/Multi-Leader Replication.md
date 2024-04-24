---
tags:
  - replication
---
# Description
The problem with [[Leader-Based Replication]] is that all writes must go through the leader. If the leader is unavailable, the system stops serving writes. 

The natural thing to do would be to allow multiple nodes to handle writes. This setup is called ***multi-leader*** configuration. 

All of the rules stay mostly the same. 
- Leader must forward writes to all followers
- Each leader acts as a follower to all other leaders

# Example
## 🔌Multiple Datacenters
Multi-leader replication could be beneficial if you have multiple datacenters. In a vanilla setup only one datacenter would contain a leader. This means that all write requests have to be forwarded to this datacenter.

Switching to multi-leader setup we can tolerate failure of one datacenter and have a leader closer to some of the users

![[MultiLeaderReplication.png]]

## 📱Offline Clients
If you have an app, that may go offline and needs to be able to continue server updates (Calendar App), the local db will act as a leader and sync up with the cloud when the opportunity is given.

## 🧑‍🤝‍🧑Collaborative Editing
Real-time collaborative editing applications allow several people to edit a document
simultaneously.
This problem has a lot in common with a database replication problem.
When one user edits the document, the changes are flushed to it's local working copy and then are being synced to the cloud.
To guarantee that there won't be any editing conflicts, you can make each user acquire a lock on the document in order to perform changes - this hammers the throughput though.
What you actually want is to make the unit of change as small as possible, perhaps a single keystroke. But in that case the means of [[Write Conflict Resolution]] should be set up.

# Issues
The same data could be concurrently modified on multiple leaders. Those conflicts need to be resolved somehow.

# Topology
A replication [[Topology|topology]] describes the communication paths along which writes are propagated from one node to another.
![[MutliLeaderReplicationTopology.png]]
To avoid infinite replication in [[Circular Topology|circular topology]] each replication packet is tagged with the ID of replica from which it came. When replica encounters a packet that is tagged with it's own ID, it doesn't forward it to the next replica. 

In circular and [[Start Topology|start topology]] if one node goes down, the flow of replication is interrupted. It is possible to set up a path around the failed node, but it is mostly performed manually. [[All-To-All Topology|All-To-All topology]] doesn't have such problems.

The all-to-all topology also may have problems due to the fact that some links of the network may be slower then the others.
![[MultiLeaderAllToAllTopology.png]]
This problem is similar to the [[Consistent Prefix Reads]] problem. To order those events correctly a technique called [[Versioned Vectors|versioned vectors]] can be used.
# Related Topics
- [[Replication]]
- [[Leader-Based Replication]]
- [[Write Conflict Resolution]]