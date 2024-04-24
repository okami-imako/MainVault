---
tags:
  - replication
---
Unfortunately, if an application reads from an asynchronous follower, it may see outdated information if the follower has fallen behind. This leads to apparent inconsistencies in the database: if you run the same query on the leader and a follower at the same time, you may get different results, because not all writes have been reflected in the follower. This inconsistency is just a temporary state - if you stop writing to the database and wait a while, the followers will eventually catch up and become ***consistent*** with the leader. For that reason, this effect is known as ***eventual consistency*** 

The term “***eventually***” is deliberately vague: in general, there is no limit to how far a replica can fall behind.

# Related Topics
- [[Replication Lag]]