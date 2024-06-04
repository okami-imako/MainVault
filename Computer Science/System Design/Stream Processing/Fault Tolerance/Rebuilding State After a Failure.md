---
tags:
  - stream-processing/fault-tolerance
relates to:
  - "[[Stream Processing]]"
  - "[[Fault Tolerance]]"
---
Any stream process that requires state (window aggregations, tables, indexes used for joins) must ensure that this state can be recovered after a failure.

1) Keep state local to the stream processor, and replicate it periodically. Then, when the stream processor is recovering from a failure, the new task can read the replicated state and resume processing without data loss.
2) In some cases, it may not be necessary to replicate the state, because it can be rebuilt from the input stream. For example, if the state consists of aggregations over a fairly short window, it may be fast enough to simply replay the input events corresponding to that window.