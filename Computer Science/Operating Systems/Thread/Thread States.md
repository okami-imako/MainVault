---
tags:
  - operating-system
relates to:
  - "[[Thread]]"
---
A ***thread*** can be in one of three states:
- *Running* - a process is running on a cpu
- *Ready* - a process is ready to run, but it isn't running at the moment
- *Blocked* - a process has performed some kind of operation that makes it not ready to run until some other event takes place (e.g. I/O request)
![[process-states.png]]