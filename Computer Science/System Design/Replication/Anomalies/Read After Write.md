---
tags:
  - replication/anomaly
---
When new data is submitted, it must be sent to the leader, but when the user views the data, it can be read from a follower.

With asynchronous replication if the user views the data shortly after making a write, the new data may not yet have reached the replica - ***bad***.

![[ReadAfterWrite.png]]

In this situation, we need ***read-after-write*** consistency
This is a guarantee that if the user reloads the page, they will always see any updates ***they*** submitted ***themselves***.

There are a lot of techniques:
- When reading something that the user may have modified, read it from the leader; otherwise, read it from a follower.
- Track the time of the last update and, for one minute after the last update, make all reads from the leader.
- The client can remember the timestamp of its most recent write - then the system can ensure that the replica serving any reads for that user reflects updates at least until that timestamp.