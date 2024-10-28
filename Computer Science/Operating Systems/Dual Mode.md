---
tags:
  - operating-system
---
[[Hardware]] provides at least 2 modes:
- Kernel mode
- User mode

Certain operations are prohibited in *user mode* (changing the [[Paging|page table pointer]], disabling interrupts, interacting directly with hardware, writing to kernel memory)

![[dual-mode.png]]

User -> Kernel mode transitions happens because of:
- [[System Call]]
- [[Interrupt]]
- [[Trap]] or [[Exception]]