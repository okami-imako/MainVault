---
tags:
  - operating-system
relates to:
  - "[[Scheduling]]"
---
[[Thread]] may ***yield*** in order to voluntarily give up [[CPU]] to another thread

![[yield.png]]

```c
run_new_thread() {
	newThread = PickNewThread();
	switch(curThread, newThread);
	ThreadHouseKeeping(); // Do cleanup
}
```

How does dispatcher *switch*?
- Save anything next thread may trash: PC, regs, stack pointer
- Maintain isolation for each thread

```
Switch(tCur,tNew) {
	// Unload old thread
	TCB[tCur].regs.r7 = CPU.r7;
	...
	TCB[tCur].regs.r0 = CPU.r0;
	TCB[tCur].regs.sp = CPU.sp;
	TCB[tCur].regs.retpc = CPU.retpc; // return addr

	// Load and execute new thread
	CPU.r7 = TCB[tNew].regs.r7;
	...
	CPU.r0 = TCB[tNew].regs.r0;
	CPU.sp = TCB[tNew].regs.sp;
	CPU.retpc = TCB[tNew].regs.retpc;
	return; // return to CPU.retpc
}
```

![[switch.png]]
> There aren't 2 different `switch()` routines like on the picture in reality - it is one routine that changes jumps to another stack
