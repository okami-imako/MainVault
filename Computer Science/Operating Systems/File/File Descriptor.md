---
tags:
  - operating-system
relates to:
  - "[[File]]"
---
Low-level file I/O:
```c
#include <fcntl.h>
#include <unistd.h>
#include <sys/types.h>

int open(const char *filename, int flags [, mode_t mode])
int create(const char *filename, mode_t mode)
int close(int filedes)
```

Integer returned from `open()` is a ***file descriptor***
- `open()` system call created an *open file description* entry in system-wide table of open files
- *Open file description* object in the kernel represents an instance of an open file

Primary reason for returning ***file descriptors*** instead of literal file structures is *security* - the [[Operating System|OS]] doesn't allow you to modify/access things you are not supposed to

[[Operating System]] maintains a table which maps ***file descriptors*** to the *open file description* which contains such info as file location on disk, offset of where you are reading from...y