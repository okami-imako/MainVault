---
tags:
  - consistency-guarantee/sync
---
***Event Sourcing*** is a powerful technique that involves storing all changes to the application state as a [[Log]] of ***change events***

Difference from [[Change Data Capture]]:
- In ***CDC*** the application mutates the db and a log of changes is extracted from the db at a low level. The application does not need to be aware that CDC is happening
- In ***Event Sourcing*** application must explicitly write [[Immutability]] events to an event log. Events are designed to reflect things that happened at the application level, rather than low-level state changes

***Event Sourcing*** distinguishes ***events*** from ***commands***.

When user's request initially arrives - it may still fail due to the constraint check. This is called a ***command***

At the point when the event is generated, it becomes a ***fact***
# Example
---
***CDC***: one entry was deleted from the enrollments table, and one cancellation reason was added to the student feedback table
***Event Sourcing***: student cancelled their course enrollment 

# Limitations
---
## Log Compaction
[[Log Compaction]] isn't as straightforward as in ***CDC*** - events are modeled at a higher level and represent an intent rather than full record overwrite. Thus, later events typically don't overwrite prior ones.
# [[Read After Write]]
Consumption of the event log is usually [[Asynchronous]]. That means that when you create an event and than perform a read from a derived view, you can see stale data

## Immutability
While [[Immutability]] has a lot of benefits, in workloads with a high rate of updates and deletes, the immutable history may grow very large.

Besides performance reasons, there are situations when you have to delete something for administrative reasons:
- Deleting user's personal information
- Containing sensitive data leak
# Big Ideas
---
- ***Event Sourcing*** carries more data, that would be inaccessible when using plain db - user adds an item to the cart and then removes it 
- ***Event Sourcing*** allows to separate the form in which data is written from the form it is read
- ***Event Sourcing*** allows creating several different derived read views