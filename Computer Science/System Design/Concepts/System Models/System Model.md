---
tags:
  - distributed-systems
relates to:
  - "[[Fault]]"
---
In order to write algorithms that do not depend much on the details of the hardware and software, we need to *formalize* the kinds of ***faults***, that we expect to happen in a system

We do this by defining a ***system model***, which is an abstraction that describes what things an algorithm may assume.

# Timing System Models
- [[Synchronous Model]]
- [[Partially Synchronous Model]]
- [[Asynchronous Model]]

# Nodes System Models
- [[Crash-Stop Faults]]
- [[Crash-Recovery Faults]]
- [[Byzantine Faults]]