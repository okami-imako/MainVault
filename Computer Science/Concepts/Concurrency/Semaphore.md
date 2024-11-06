---
tags:
  - concept
  - concurrency
---
***Semaphore*** is a generalized [[Mutex]]. It represents a number with 2 possible operations:
- `dec()` - waits for the semaphore to become positive and then decrements it
- `inc()` - increments the semaphore