---
tags:
  - transactions/isolation
relates to:
  - "[[Serializable]]"
  - "[[Lock]]"
---
Have a [[Lock|lock]] on each object in the database
- ***Read*** can happen only if nobody is writing to the object.
- ***Write*** can happen only if nobody is writing to the object and nobody is reading from the object.

Opposing to the [[Repeatable Read]] mantra of ***2PL*** is:
- *Readers block Writers*
- *Writers block both Readers and Writers*

Having so many locks in use may lead to often [[Deadlock|deadlocks]]

>Usually database automatically detects deadlocks between transactions and aborts one of them so that the others can make progress. The aborted transaction should retry.

2PL follows the [[Pessimistic Concurrency Control]] .
# Problem
1. Due to the interactive nature of modern applications, databases running 2PL can have quite unstable latencies and can be very slow at [[Percentiles|high percentiles]]
2. We still have a problem of [[Phantom Read|phantoms]]. To fix it we can use a technique called [[Predicate Locks|predicate locks]]