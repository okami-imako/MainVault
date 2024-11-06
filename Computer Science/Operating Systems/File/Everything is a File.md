---
tags:
  - operating-system
  - posix
  - unix
---
[[Unix]]/[[Posix]] follow an interesting idea of "*everything is a file*":
- Files on disk
- Devices (terminals, printers...)
- Networking (sockets)
- Local interprocess communication (pipes, sockets)

It is based on system calls `open()`, `read()`, `write()`, `close()` and additional `ioctl()` for custom configuration.