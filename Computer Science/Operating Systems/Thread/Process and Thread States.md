---
tags:
  - operating-system
relates to:
  - "[[Thread]]"
  - "[[Process]]"
---
A [[Thread]] or a [[Process]] can be in one of five states:
- *New* - the thread/process is created
- *Ready* - the thread/process is waiting to run
- *Running* - the thread/process is running - instructions are being executed
- *Waiting* - the thread/process has performed some kind of operation that makes it not ready to run until some other event takes place (e.g. I/O request)
- *Terminated* - the thread/process has finished execution
![[thread-states.png]]