---
tags:
  - stream-processing/fault-tolerance
relates to:
  - "[[Stream Processing Fault Tolerance]]"
---
***Checkpointing*** is an approach when you periodically generate rolling checkpoints of state and write them to durable storage.

If a stream operator crashes, it can restart from its most recent checkpoint and discard any output generated between the last checkpoint and the crash.