---
tags:
  - consistency-guarantee/sync
relates to:
  - "[[Keeping Systems In Sync]]"
  - "[[Replication Log]]"
---
***Change Data Capture (CDC)*** is the process of observing all data changes written to a database and extracting them in a form in which they can [[Replication|replicated]] to other systems

![[Pasted image 20240524154744.png]]

# Implementation
CDC makes one database the leader and turns the others into followers. A [[Log-Based Message Broker]] is well suited for transporting the change events from the source database, since it preserves the ordering of messages
- ***Triggers*** - performance overhead
- Parsing the [[Replication Log]] - more robust, but handling schema changes may be tricky
CDC is usually [[Asynchronous]], but that comes with all the problems of the [[Replication Lag]]

## Initial Snapshot
When you connect a [[Derived Data System]] to the database that already has some data, just replaying the log of recent changes is not enough to consume the whole db.

Thus, if you don't have the entire log history - create a [[Snapshot|consistent snapshot]] of the db which corresponds to some offset in the ***replication log***.

## Log Compaction
Using [[Log Compaction]] db can manage to keep the latest update of each record with some kind of primary key

The same idea works in the context of ***log-based message brokers*** and ***CDC***

Now, whenever you want to rebuild a ***derived data system***, you can start a new ***consumer*** from offset 0 of the ***log-compacted topic***, and sequentially scan over all messages in the log

