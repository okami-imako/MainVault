---
tags:
  - operating-system
relates to:
  - "[[Scheduling]]"
---
Examples of *Internal Events*:
- Blocking on I/O
- Waiting on a *signal* from other thread
- `yield()` - volunteer to give up [[CPU]]

```c
void pthread_yield(void);
void sched_yield(void);
```