---
tags:
  - operating-system
relates to:
  - "[[Address Space]]"
---
We break the entire [[Virtualization|virtual]] [[Address Space]] into equal sized chunks - ***pages***

All ***pages*** have the same size, so it is easy to place them in memory.

**Hardware** translates address using [[Page Table]]
- Each ***page*** has a separate `base`
- The `bound` is the ***page*** size
- Special hardware registers stores pointer to page table

![[paging.png]]