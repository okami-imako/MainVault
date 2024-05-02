---
tags:
  - system-model/timing
relates to:
  - "[[System Model]]"
---
In this model, an algorithm is ***not allowed to make any timing assumptions*** - in fact, it does not even have a clock (so it cannot use timeouts). Some algorithms can be designed for the asynchronous model, but it is very restrictive.