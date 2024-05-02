---
tags:
  - consistency-guarantee
---
A database may provide both [[Serializability]] and [[Linearizability]], and this combination is known as ***strict serializability*** or ***strong one-copy serializability (strong-1SR)***

Implementations of serializability based on [[Two-Phase Locking]] or [[Actual Serial Execution]]  are typically linearizable.

However, [[Serializable Snapshot Isolation]] is not linearizable: by design, it makes reads from a consistent snapshot, to avoid lock contention between readers and writers. The whole point of a consistent snapshot is that it does not include writes that are more recent than the snapshot, and
thus reads from the snapshot are not linearizable.