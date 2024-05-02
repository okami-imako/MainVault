---
tags:
  - replication
relates to:
  - "[[Leader-Based Replication]]"
---
How does a node know that it is still leader (that it hasn’t been declared dead by the others), and that it may safely accept writes?

One option is for the leader to obtain a ***lease*** from the other nodes, which is similar to a lock with a timeout. Only one node can hold the lease at any one time - thus, when a node obtains a lease, it knows that it is the leader for some amount of time, until the lease expires. In order to remain leader, the node must periodically renew the lease before it expires. If the node fails, it stops renewing the lease, so another node can take over when it expires.

You can imagine the request-handling loop looking something like this:
```java
while(true) {
	request = getIncomingRequest();

	if (lease.expiryTimeMillis - System.currentTimeMillis() < 10000) {
		lease = lease.renew();
	}

	if (lease.isValid()) {
		process(request)
	}
}
```

## What’s wrong with this code? 
___
1) Firstly, it’s relying on [[Time-Of-Day Clocks|synchronized clocks]]: the expiry time on the lease is set by a different machine (where the expiry may be calculated as the current time plus 30 seconds, for example), and it’s being compared to the local system clock. If the clocks are out of sync by more than a few seconds, this code will start doing strange things.
2) The program may be suspended just before the `process(request)` call. In that case the lease may be already expired by the time the program wakes up.

There are many cases in which the process may be stopped and won't even know about it:
- [[Garbage Collection]]
- In a virtualized environment, a virtual machine may be *suspended*
- Laptop's lead can be closed
- [[Context Switch]]
- Synchronize disk access
- SIGSTOP - SIGCONT