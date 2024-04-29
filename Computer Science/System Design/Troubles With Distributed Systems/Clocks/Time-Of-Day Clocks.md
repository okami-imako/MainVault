---
tags:
  - clock
relates to:
  - "[[Unreliable Clocks]]"
---
A ***time-of-day clock*** does what you intuitively expect of a clock: it returns the ***current date and time*** according to some calendar (also known as wall-clock time). 

For example, `clock_gettime(CLOCK_REALTIME)` on Linux and `System.currentTimeMillis()` in Java return the number of seconds (or milliseconds) since the epoch: ***midnight UTC on January 1, 1970***, according to the Gregorian calendar, not counting leap sec‐ onds. Some systems use other dates as their reference point.

Time-of-day clocks are usually synchronized with [[NTP]], which means that a timestamp from one machine (ideally) means the same as a timestamp on another machine.

# Problems
- If the local clock is too far ahead of the NTP server, it may be forcibly reset and appear to ***jump back*** to a previous point in time. These jumps, as well as the fact that they often ignore leap seconds, make time-of-day clocks ***unsuitable*** for measuring elapsed time.
- Time-of-day clocks have also historically had quite a coarse-grained resolution, e.g., moving forward in steps of 10 ms on older Windows systems. On recent systems, this is less of a problem.