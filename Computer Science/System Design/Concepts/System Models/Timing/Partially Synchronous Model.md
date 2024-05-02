---
tags:
  - system-model/timing
relates to:
  - "[[System Model]]"
---
***Partial synchrony*** means that a system behaves like a synchronous system ***most of the time***, but it sometimes exceeds the bounds for network delay, [[Process Pauses|process pauses]], and [[Time-Of-Day Clocks|clock drift]].

This is a realistic model of many systems: most of the time, networks and processes are quite well behaved - otherwise we would never be able to get anything done - but we have to reckon with the fact that any timing assumptions may be shattered occasionally. When this happens, network delay, pauses, and clock error may become arbitrarily large.