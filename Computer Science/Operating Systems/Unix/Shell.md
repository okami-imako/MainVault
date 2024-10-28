---
tags:
  - operating-system
  - unix
relates to:
  - "[[Process API]]"
---
The ***shell*** is just a [[User Program|user program]]. It shows you a *prompt* and then waits for you to type something into it:
1) You type a command (.e. the name of the executable + args)
2) ***Shell*** finds the *executable*
3) ***Shell*** calls `fork()` to create a new child process
4) Child process calls `exec()` to run the command
5) ***Shell*** call `wait()` and waits for it to return
6) ***Shell*** prints the *prompt* again