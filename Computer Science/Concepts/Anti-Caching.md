---
tags:
  - concept
relates to:
  - "[[Transaction]]"
---
To overcome the restriction that all data fit in main memory, a technique called ***anti-caching*** can be used, where [[Cold Data|cold data]] is moved to disk in a transactionally-safe manner as the database grows in size. Because data initially resides in memory, an anti-caching architecture reverses the traditional storage hierarchy of disk-based systems. Main memory is now the primary storage device.

# Useful Links
- [technique proposal](https://www.vldb.org/pvldb/vol6/p1942-debrabant.pdf)