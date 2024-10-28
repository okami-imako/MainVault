---
tags:
  - concept
---
# Definition 1
**Multiple** operations are ***concurrent*** if there is no [[Happens Before|happens before]] relationship between them.

# Definition 2
**Multiple** operations are ***concurrent*** if there is no guarantee on how they will be scheduled:
- Will run one by one to completion
- Will be interleaved
- Will be executed in parallel

---
❗❗ ***Concurrency*** is not [[Parallelism]] ❗❗