---
tags:
  - transactions/isolation
relates to:
  - "[[ACID - Isolation]]"
---
# Forbidden Anomalies
---
- [[Dirty Write]]
- [[Dirty Read]]
- [[Read Skew]]
- [[Phantom Read]]
# Description
---
In most databases ***Repeatable Read*** isolation level is implemented using [[Snapshot Isolation|snapshots]]

Mantra of the ***Repeatable Read***:
- *Readers never block Writers*
- *Writers never block Readers*