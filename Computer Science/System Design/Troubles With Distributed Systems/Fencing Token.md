---
tags:
  - distributed-systems/problem
relates to:
  - "[[Process Pauses]]"
---
To solve the following problem:
![[DistributedLock.png]]

We can implement something called ***fencing token***
![[FencingToken.png]] 

Datastore takes an active role in validating the token

***Fencing Token*** is usually some number that monotonically increases every time the lock is acquired. Hence, [[Total Order]] of the `acquire lock` operations is required