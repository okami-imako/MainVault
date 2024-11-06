---
tags:
  - operating-system
---
***Socket*** is an abstraction for one endpoint of a network connection

It looks like a [[File|file]] with a [[File Descriptor|file descriptor]]
- Corresponds to a network connection (two queues)
- *write* adds to output queue
- *read* removes from its input queue
- Some operations do now work (*lseek*)

## Assumptions
- Reliable
	- Write to a [[File]] -> Read it back. Nothing is lost
	- Write to a ([[TCP]]) socket -> Read from the other side 
- In order (sequential)
	- Write X then write Y -> read gets X then read gets Y

## Connection procedure
Server creates a special kind of *socket* - ***server socket***
- Has file descriptor
- Can't read or write
It has two operations:
- `listen()` - start allowing clients to connect
- `accept()` - create a new *socket* for a particular client

![[connection-procedure.png]]

5-tuple identifies each connection:
1) Source [[IP|ip address]]
2) Destination [[IP|ip address]]
3) Source *Port Number*
4) Destination *Port Number*
5) Protocol

***Server port*** is often well known:
- 80 (web), 443 (secure web), etc.