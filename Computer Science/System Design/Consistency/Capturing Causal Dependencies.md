---
tags:
  - consistency-guarantee
relates to:
  - "[[Causal Consistency]]"
---
In order to maintain causality, you need to know which operation [[Happens Before|happened before]] which other operation.

This is a partial order: [[Concurrency|concurrent]] operations may be processed in any order, but if one operation ***happened before*** another, then they must be processed in that order on every replica. Thus, when a replica processes an operation, it must ensure that all causally preceding operations (all operations that happened before) have already been processed; if some preceding operation is missing, the later operation must wait until the preceding operation has been processed.