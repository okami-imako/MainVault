---
tags:
  - operating-system
relates to:
  - "[[Process]]"
---
Different processes may need a way to communicate with one another.

# Communication through files
---
One process (*producer*) writes to a [[File|file]] while the other process (*consumer*) reads what the first one wrote

Very expensive

# In-Memory Queue
---
Kernel can maintain an in-memory blocking queue that one process writes to and another reads from

## POSIX/Unix PIPE
Pipe is an implementation of in-memory queue pattern
- *Producer* tries to write. When buffer is full, it **blocks**
- *Consumer* tries to read. When buffer is empty, it **blocks**

```c
int pipe(int fileds(2));
```
- Allocates two new [[File Descriptor|file descriptors]] in the process
- Writes to `fileds[1]` read from `fileds[0]`
- Implemented as a fixed-size queue

Kernel knows when to wake up blocked process
- If *consumer* is blocked, kernel wakes hip up when *producer* writes
- If *producer* is blocked, kernel wakes him up when *consumer* reads

After last *write* descriptor is closed, reads return only *EOF*
After last *read* descriptor is closed, writes generate *SIGPIPE* signals