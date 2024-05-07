---
tags:
  - consistency-guarantee/consensus
relates to:
  - "[[Consensus]]"
  - "[[Distributed Transactions]]"
---
***Two-phase commit*** is an algorithm for achieving atomic transaction commit across multiple nodes - i.e., to ensure that either all nodes commit or all nodes abort.

![[Pasted image 20240507181114.png]]

***Coordinator*** is often implemented as a library within the application that is requesting the transaction, but it can also be a separate running process or service

# Algorithm
___
 >Database nodes are called ***participants*** in the transaction
1) 2PC transaction begins with application reading and writing data by initiating a *single-node transaction* on each participant
2) When the app is ready to commit, ***coordinator*** sends a ***prepare*** request to each of the nodes, asking them whether they are able to commit.
3) Participant makes sure that it can definitely commit the transaction ***under any circumstances***. This includes writing all transaction data to disk (crash, a power failure, or running out of disk space is not an acceptable excuse for refusing to commit later), and checking for any conflicts or constraint violations. By replying `yes` to the *coordinator*, the node ***promises*** to commit the transaction without error if requested.
3) *Coordinator* receives responses from all participants and makes the final decision on whether to commit (only if all participants replied `yes`) or abort the transaction. The coordinator must persist this decision so that it knows which way it decided in case of crashes. This is called the ***commit point***
4) Once the decision has been written to disk, the ***commit*** or ***abort*** request is sent to all participants. If this request fails, or times out, the coordinator ***must retry forever until it succeeds***. If a participant has crashed in the meantime, the transaction will be committed when it recovers.

## Key points
- If any of the ***prepare*** requests fail or time out, the coordinator aborts the transaction
- If any of the ***commit*** or ***abort*** requests fail or time out, the coordinator retries indefinitely

## Coordinator Failure
If coordinator fails before sending the ***prepare*** request - participants can safely abort. But once the participant has received a ***prepare*** request and replied `yes`, it can no longer abort by itself - it must wait to hear back from the coordinator. This state of participant is called ***in doubt*** or ***uncertain***
![[Pasted image 20240507183641.png]]

That's why coordinator must write his decision to disk before sending the commit/abort requests - so that it can recover it after restart from crash and resolve all participants that are [[In-Doubt Transaction|in-doubt]]