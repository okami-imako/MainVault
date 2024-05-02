---
tags:
  - system-model/timing
relates to:
  - "[[System Model]]"
---
The ***synchronous model*** assumes bounded network delay, bounded process pauses, and bounded clock error. 

This does not imply exactly synchronized clocks or zero network delay; it just means you know that network delay, [[Process Pauses|pause]], and [[Time-Of-Day Clocks|clock drift]] will never exceed some fixed upper bound.

The synchronous model is ***not a realistic model*** of most practical systems, because unbounded delays and pauses do occur.