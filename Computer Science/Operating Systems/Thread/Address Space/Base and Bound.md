---
tags:
  - operating-system
relates to:
  - "[[Address Space]]"
---
The [[Operating System|OS]] loads the thread's ***address space*** into physical memory region starting at address `base` and ending at `bound` and then whenever thread tries to access some memory address, it is being checked to be greater than `base` and less then `bound`. 

`base` and `bound` values are being stored in special registers.

There are 2 options to address translation:
- All the addresses are being translated when the program is loaded. That way there is no overhead in runtime, because no translation is being performed at this stage.
- You add an *adder* on **hardware** level that translates the addresses on the fly.

This is a ***Hardware*** based check

![[base-and-bound.png]]

The issue with the approach is that as the **OS** loads and offloads ***threads*** it has to deal with a big [[Fragmentation|fragmentation]] problem