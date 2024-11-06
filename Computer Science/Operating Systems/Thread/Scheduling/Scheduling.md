---
tags:
  - operating-system
  - multithreading
relates to:
  - "[[Thread]]"
---
![[scheduling-loop-1.png]]Basically [[Thread Control Block|TCBs]] make their ways through the queues: 
*ready queue* -> *cpu* -> *time slice expired* -> *ready queue*

Scheduler is interacting with the *ready queue*
The other queues are being managed by the [[Device Driver|device drivers]]

Conceptually, the *scheduling loop* of the [[Operating System]] looks as follows:
![[scheduling-loop-2.png]]

Note that with single [[CPU]] only one thing can run at a time. That means that the OS gives up control on the processor to the user thread

How does the OS get control back?
- [[Internal Events]]: thread returns control voluntarily
- *External* events: thread gets kicked out