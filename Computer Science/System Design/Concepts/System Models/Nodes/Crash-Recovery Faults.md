---
tags:
  - system-model/nodes
relates to:
  - "[[System Model]]"
---
We assume that nodes may crash at any moment, and perhaps start responding again after some unknown time.

In the ***crash-recovery model***, nodes are assumed to have stable storage (i.e., nonvolatile disk storage) that is preserved across crashes, while the in-memory state is assumed to be lost