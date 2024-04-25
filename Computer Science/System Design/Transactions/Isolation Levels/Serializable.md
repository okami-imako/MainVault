---
tags:
  - transactions/isolation
relates to:
  - "[[ACID - Isolation]]"
---
In theory ***serializable*** isolation level shouldn't allow ***any*** anomalies.

It guarantees that even though transactions may execute in parallel, the end result is the same as if they had executed *serially* - no [[Race Condition|race conditions]]

There are 3 main strategies for implementing this *dream* isolation level:
- [[Actual Serial Execution]]
- [[Two-Phase Locking]]
- [[Serializable Snapshot Isolation]]