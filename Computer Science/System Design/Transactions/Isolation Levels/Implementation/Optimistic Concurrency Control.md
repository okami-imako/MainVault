---
tags:
  - concurrency
  - transactions/isolation
relates to:
  - "[[Concurrency]]"
---
***Optimistic Concurrency Control*** mechanism is based on principle that if anything might possibly go wrong, proceed anyway in the hope that everything turns out alright. When transaction wants to commit, the database checks whether anything bad happened. If so, the transaction is aborted and has to be retried
___
Performs badly if there is high contest on the given object, as it leads to most of transactions being aborted and retried. If the system is near capacity, the additional transaction load might become the final nail in the coffin.

However, if there is enough spare capacity, and the contention between transactions is not too high, ***optimistic concurrency control*** techniques tend to perform better than [[Pessimistic Concurrency Control|pessimistic ones]]