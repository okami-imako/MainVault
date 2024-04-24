---
tags:
  - replication
  - recovery
---
One of the followers needs to be promoted to be the new leader ([[Consensus]]), clients need to be reconfigured to send their writes to the new leader, and the other followers need to start consuming data changes from the new leader. This process is called *failover*.