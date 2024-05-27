---
tags:
  - consistency-guarantee/sync
relates to:
  - "[[Keeping Systems In Sync]]"
---
Application code can just write to all places explicitly.

# Problem
![[Pasted image 20240524151500.png]]
Unless you have something like version vectors ([[Write Conflict Resolution]]), you will not notice that [[Concurrency|concurrent]] events occurred - one will just overwrite the other one silently

Also [[Fault Tolerance]] is in question. Ensuring that all writes either succeed or fail is very expensive - [[Two-Phase Commit]]