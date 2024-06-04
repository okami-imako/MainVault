---
tags:
  - stream-processing/fault-tolerance
relates to:
  - "[[Stream Processing]]"
  - "[[Fault Tolerance]]"
---
***Tolerating Fault*** in stream processing job is not an easy task.

While [[Batch Processing]] jobs tolerate faults fairly easy by constantly retrying due to the fact that the input is immutable, that doesn't apply to ***stream processing***  because a stream is infinite and so you can never finish processing it

Approaches to fault tolerance in ***stream processing*** are:
- [[Microbatching]]
- [[Checkpointing]]
> Both ***Microbatching*** and ***Checkpointing*** provide the same [[Exactly Once]] semantics as batch processing. However if stream processor has [[Side Effect|side effects]] to message processing, the framework is not able to discard the results of those side effects
- [[Atomic Commit]]
- [[Relying On Idempotence]]
- [[Rebuilding State After a Failure]]