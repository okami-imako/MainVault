---
tags:
  - operating-system
  - multithreading
relates to:
  - "[[Thread]]"
---
***Context Switch*** is the process of saving the state of the running [[Thread|thread]] so that it can be restored and resume execution later ([[Thread Control Block]]), and then restoring a different, previously saved, thread

![[context-switch.png]]

Too frequent ***Context Switches*** result in a big portion of [[CPU]] time being wasted.