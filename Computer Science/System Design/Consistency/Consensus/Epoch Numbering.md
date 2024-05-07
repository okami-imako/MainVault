---
tags:
  - consistency-guarantee/consensus
relates to:
  - "[[Consensus]]"
---
It looks like you can't really come up with a [[Consensus]] algorithm, which won't use ***leaders*** internally.

>This is too bad, because when you have leader, you forfeit the ***Termination*** property, thus, making your system not [[Fault Tolerance|fault tolerant]]

However most of the consensus protocols ***don't guarantee*** that the leader is unique. They make a weaker guarantee:
>The protocol defines an ***epoch number*** and guarantees that within each epoch, the leader is unique

# Algorithm
1) Every time the leader is thought to be dead, a vote is started to elect a new leader. This election is given an incremented epoch number, and thus epoch numbers are [[Total Order|totally ordered]] and monotonically increasing. If there is a conflict between two different leaders in two different epochs, then the leader with the higher epoch number wins
2) For every decision that a leader wants to make, it must send the proposed value to the other nodes and wait for a [[Quorum]] of nodes to respond in favor of the proposal. A node votes in favor of a proposal only if it is not aware of any other leader with a higher epoch.

## Key Insight
We have two rounds of voting:
1) Leader's election
2) Vote on a leader's proposal

***Quorum*** for those two votes must overlap
> This means that in every vote on a leader's proposal there is at least one node that has also participated in the latest leader election. Thus, if during vote on proposal higher-epoch leader hasn't been discovered, then current leader is safe to assume, that he still holds the title.

# Limitations
- Making all nodes to participate in the vote on proposals is basically ***Synchronous [[Replication]]***, which is more safe, but has worse performance then asynchronous one
- Consensus systems always require a strict majority to operate
- Adding/Removing nodes is tricky. Something called [[Dynamic Membership]] can be used
- Sensitive to network problems - algos use timeouts to detect dead nodes. If the network is unreliable, nodes are falsely announced dead and, nodes can spend time more time electing new leaders, then doing actual work