---
tags:
  - distributed-system
  - architecture
---
One of the big ideas in building distributed systems is ***Building a Reliable System from Unreliable Components***

This may sound counter intuitive, but it actually does make sense

For example:
- [[Error-Correction|error-correcting]] algorithms that allow restoring data if bits get flipped by the interference
- [[Internet Protocol|IP]] is unreliable - it may drop, delay, duplicate or reorder packets. [[Transmission Control Protocol|TCP]] provides a more reliable transport layer on top of IP.

There is a limit to how reliable the system can be though.

>error-correcting codes can deal with only a small number of flipped bits
>TCP can't magically remove network delays