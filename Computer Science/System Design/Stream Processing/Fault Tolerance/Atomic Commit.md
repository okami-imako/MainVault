---
tags:
  - stream-processing/fault-tolerance
relates to:
  - "[[Stream Processing Fault Tolerance]]"
---
In order to give the appearance of [[Exactly Once]] processing in the presence of faults, we need to ensure that all outputs and [[Side Effect|side effects]] of processing an event take effect if and only if the processing is successful.

The idea is very similar to [[Distributed Transactions]] and [[Two-Phase Commit]]

In this kind of restricted environment it is possible to implement such an atomic commit facility efficiently.