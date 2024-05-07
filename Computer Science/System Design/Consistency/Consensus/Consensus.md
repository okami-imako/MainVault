---
tags:
  - consistency-guarantee
---
The consensus problem is normally formalized as follows: one or more nodes may ***propose*** values, and the consensus algorithm ***decides*** on one of those values.

In this formalism, a consensus algorithm must satisfy the following properties:
- ***Uniform Agreement*** - no two nodes decide differently
- ***Integrity*** - no node decides twice
- ***Validity*** - if a node decides value $v$, then $v$ was proposed by some node
- ***Termination*** - every node that does not crash eventually decides some value

The ***uniform agreement*** and ***integrity*** properties define the core idea of consensus: everyone decides on the same outcome, and once you have decided, you cannot change your mind. 

The ***validity*** property exists mostly to rule out trivial solutions: for example, you could have an algorithm that always decides null, no matter what was proposed; this algorithm would satisfy the ***agreement*** and ***integrity*** properties, but not the ***validity*** property.

If you don’t care about fault tolerance, then satisfying the first three properties is easy: you can just hardcode one node to be the ***“dictator”***, and let that node make all of the decisions. However, if that one node fails, then the system can no longer make any decisions. This is, in fact, what we saw in the case of [[Two-Phase Commit]].

The ***termination*** property formalizes the idea of [[Fault Tolerance]]. It essentially says that a consensus algorithm cannot simply sit around and do nothing forever - in other words, it must make progress. Even if some nodes fail, the other nodes must still reach a decision. (Termination is a [[Liveness|liveness property]], whereas the other three are [[Safety|safety properties]])

The system model of consensus assumes that when a node “crashes,” it suddenly disappears and never comes back.

Most consensus algorithms assume that there are no [[Byzantine Faults]]
# Applications
- Leader election
- Atomic commit/rollback of distributed [[Transaction|transactions]]