---
tags:
  - concurrency
  - transactions/isolation
relates to:
  - "[[Concurrency]]"
  - "[[Mutual Exclusion]]"
---
***Pessimistic Concurrency Control*** mechanism is based on principle that if anything might possibly go wrong (for example some transaction holds a lock on the object), it's better to wait until the situation is safe again before doing anything.