---
tags:
  - operating-system
  - unix
relates to:
  - "[[Process]]"
---
[[Unix]] exposes a ***process api*** through [[System Call|system calls]].
Every *process* is created by another *process*.
The first *process* is created by the kernel and is called ***root process***

### `exit()`
---
```c
void exit(int status);
```

Parent process will receive the `status`
Any `status` other then zero is considered to be an error

### `fork()` system call
---
The `fork()` system call is used to create a new process.

It is really weird:
```C
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(int argc, char *argv[]) {
	printf("hello world (pid:%d)\n", (int) getpid());
	int rc = fork();
	if (rc < 0) {
		// fork failed
		fprintf(stderr, "fork failed\n");
		exit(1);
	} else if(rc == 0){
		// child (new process)
		printf("hello, I am child (pid:%d)\n", (int) getpid());
	else {
		// parent goes down this path (main)
		printf("hello, I am parent of %d (pid:%d)\n", rc, (int) getpid());
	}
	return 0;
}
```

```
prompt> ./p1
hello world (pid:29146)
hello, I am parent of 29147 (pid:29146)
hello, I am child (pid:29147)
prompt>
```

Basically the `fork()` system call creates an (almost) exact copy of the calling process. That means that  to the OS, it now looks like there are two copies of the program `p1` running, and both are about to return from the `fork()` system call. That means that the newly crated process doesn't start running from the beginning of the `main()` - it just comes to life as if it had called the `fork()` itself.

The child will have its own copy of the address space, registers, its own PC...

The output of `p1` is *not deterministic* - the [[Scheduler|OS scheduler]] determines which process runs at a given moment in time; because it is complex, we cannot make strong assumptions about what will happen.

### `wait()` system call
---
The `wait()` system call is used by parent to wait on a child:
```C
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(int argc, char *argv[]) {
	printf("hello world (pid:%d)\n", (int) getpid());
	int rc = fork();
	if (rc < 0) {
		fprintf(stderr, "fork failed\n");
		exit(1);
	} else if(rc == 0){
		printf("hello, I am child (pid:%d)\n", (int) getpid());
	else {
		in rc_wait = wait(NULL)
		printf("hello, I am parent of %d (rc_wait:%d) (pid:%d)\n", rc, rc_wait, (int) getpid());
	}
	return 0;
}
```

Call to `wait()` delays the execution until the child finishes running:
```
prompt> ./p2
hello world (pid:29266)
hello, I am child (pid:29267)
hello, I am parent of 29267 (rc_wait:29267) (pid:29266)
prompt>
```

The output becomes *deterministic*

> There are cases when `wait()` returns before the child exits - read the man page

### `exec()` system call
___
The `exec()` system call is used to running a program that is different from the calling program:
```C
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <sys/wait.h>

int main(int argc, char *argv[]) {
	printf("hello world (pid:%d)\n", (int) getpid());
	int rc = fork();
	if (rc < 0) {
		// fork failed; exit
		fprintf(stderr, "fork failed\n");
		exit(1);
	} else if (rc == 0) { 
		// child (new process)
		printf("hello, I am child (pid:%d)\n", (int) getpid());
		char *myargs[3];
		myargs[0] = strdup("wc");   // program: "wc" (word count)
		myargs[1] = strdup("p3.c"); // argument: file to count
		myargs[2] = NULL;           // marks end of array
		execvp(myargs[0], myargs);  // runs word count
		printf("this shouldn’t print out");
	else {              
		// parent goes down this path (main)
		int rc_wait = wait(NULL);
		printf("hello, I am parent of %d (rc_wait:%d) (pid:%d)\n", rc, rc_wait, (int) getpid());
	}
	return 0;
}
```

```
prompt> ./p3
hello world (pid:29383)
hello, I am child (pid:29384)
29 107 1030 p3.c
hello, I am parent of 29384 (rc_wait:29384) (pid:29383)
prompt>
```

`exec()` takes the name of the executable and some arguments. It *loads* code (and static data) from that executable and overwrites its current code segment (and current static data) with it

The *heap* and *stack* and other parts of the memory space of the program are re-initialized

It doesn't create a new process - it ***transforms*** the currently running one.

*Successful* call to `exec()` never returns.