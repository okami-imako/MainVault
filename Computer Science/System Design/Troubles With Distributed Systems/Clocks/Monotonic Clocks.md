---
tags:
  - clock
relates to:
  - "[[Unreliable Clocks]]"
---
A ***monotonic clock*** is suitable for measuring a ***duration*** (time interval), such as a timeout or a service’s response time: `clock_gettime(CLOCK_MONOTONIC)` on Linux and `System.nanoTime()` in Java are monotonic clocks, for example. The name comes from the fact that they are ***guaranteed*** to always ***move forward*** (whereas a [[Time-Of-Day Clocks]] may jump back in time).

The ***absolute time*** of such clock is ***meaningless***. 

> It may be bounded to the amount if time that have elapsed since the computer has started

[[NTP]] may adjust the frequency at which the monotonic clock moves forward (this is known as ***slewing*** the clock) if it detects that the computer’s local quartz is moving faster or slower than the NTP server. 

NTP cannot cause the monotonic clock to jump forward or backward.

The resolution of monotonic clocks is usually quite good: on most systems they can measure time intervals in microseconds or less.

In a distributed system, using a monotonic clock for measuring elapsed time (e.g., timeouts) is usually fine, because it doesn’t assume any synchronization between dif‐ ferent nodes’ clocks and is not sensitive to slight inaccuracies of measurement.