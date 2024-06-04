---
tags:
  - stream-processing/fault-tolerance
relates to:
  - "[[Stream Processing]]"
  - "[[Fault Tolerance]]"
---
Our goal is to discard the partial output of any failed tasks so that they can be safely retried without taking effect twice. [[Atomic Commit|Distributed transactions]] are one way of achieving that goal, but another way is to rely on [[Idempotence]]

Even if an operation is ***not naturally idempotent***, it can often be made ***idempotent*** with a bit of extra metadata. For example, when consuming messages from Kafka, every message has a persistent, monotonically increasing ***offset***. When writing a value to an external database, you can include the ***offset*** of the message that triggered the last write with the value. Thus, you can tell whether an update has ***already been applied***, and ***avoid performing*** the same update again.