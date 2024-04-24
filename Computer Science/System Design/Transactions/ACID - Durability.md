---
tags:
  - transactions/acid
relates to:
  - "[[ACID Properies]]"
---
***Durability*** is a gurantee the database gives you that once the transaction is [[Commit|committed]], any data it has written is not forgotten, even if there is a hardware fault or the database crashes.

It can be achieved via writing to disk, keeping a [[Write-Ahead Log]] and [[Replication|replicating]] data to other nodes.