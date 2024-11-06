---
tags:
  - operating-system
---
High-level API for files in [[Posix]] are ***streams***

***Stream*** is an unformatted sequence of bytes

This API is wrapping a low-level [[File Descriptor]] API which
## API
---
```c
#include <stdio.h>
FILE *fopen(const char *filename, const char *mode);
int fclose(FILE *fp);
```

If the system call fails we receive a `NULL`

`FILE*` contains:
- [[File Descriptor]] from call to `open()`
- Buffer (array)
- Lock (in case multiple threads use the `FILE` concurrently)
- ...