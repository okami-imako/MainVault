---
tags:
  - operating-system
---
***Thread*** is an abstraction exposed by the [[Operating System]] that represents a *virtualized* processor.

***Thread*** contains program counter, registers, execution flags, stack, memory state.

A ***Thread*** is executing on a processor when it is *resident* in the processor *registers*. *Resident* means the *registers* hold the context of the ***thread***. A ***thread*** is *suspended* when its state is *not loaded* into the *registers*.

# Why Threads?
[[Operating System]] must handle multiple things at once
