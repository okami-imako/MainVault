---
tags:
  - consistency-guarantee
relates to:
  - "[[Total Order]]"
---
# Problem
[[Lamport Timestamps]] are not sufficient to solve common problems in distributes systems

## Example
***Rule***: Username of the user must be unique

At first glance - if two accounts with the same username are created, pick the one with the lower timestamp as the winner

However when the node is processing a write, it doesn't know if any other node is processing a write with the same username, but it steel needs to decide ***right now*** if write should succeed or fail.

## Problem Statement
[[Total Order]] of operations only emerges after you have collected all of the operations

In order to implement uniqueness constraint for usernames you need to know when the total order of operations is finalized

# Total Order Broadcast
***Total order broadcast*** is usually described as a protocol for exchanging messages between nodes. Informally, it requires that two safety properties always be satisfied:

- ***Reliable delivery***
>No messages are lost: if a message is delivered to one node, it is delivered to all nodes.

- ***Totally ordered delivery***
> Messages are delivered to every node in the same order.

Consensus services such as [[ZooKeeper]] and [[etcd]] actually implement total order broadcast. This fact is a hint that there is a strong connection between ***total order broadcast*** and [[Consensus]]

***Total Order Broadcast*** is very useful in:
- [[Replication]] - if each replica receives messages (writes) in the same order, they will remain consistent with each other. This principle is known as [[State Machine Replication]]
- [[Serializable|Serializable transactions]] - if every message represents a deterministic transaction to be executed as a stored procedure, and if every node processes those messages in the same order, then the [[Partitioning|partitions]] and [[Replica|replicas]] of the database are kept consistent with each other
- [[Fencing Token]] - every request to acquire the lock is appended as a message to the log, and all messages are sequentially numbered in the order they appear in the log. The sequence number can then serve as a fencing token, because it is monotonically increasing. In ZooKeeper, this sequence number is called `zxid`.

# Connection with [[Linearizability]]
***Total order broadcast*** is [[Asynchronous]]: messages are guaranteed to be delivered reliably in a fixed order, but there is ***no guarantee*** about when a message will be delivered (so one recipient may lag behind the others).

By contrast, ***linearizability*** is a recency guarantee: a read is guaranteed to see the latest value written.

However, if you have total order broadcast, you can build linearizable storage on top of it

# Solution to the Problem
Imagine that for every possible username, you can have a linearizable register with an atomic [[Compare And Set]] operation. Every register initially has the value `null` (indicating that the username is not taken). 

When a user wants to create a username, you execute a `compare-and-set` operation on the register for that username, setting it to the user `account ID`, under the condition that the previous register value is `null`. If multiple users try to concurrently grab the same username, only one of the `compare-and-set` operations will succeed, because the others will see a value other than `null` (due to linearizability).

You can implement such a linearizable `compare-and-set` operation as follows by using ***total order broadcast*** as an append-only log:
1. Append a message to the log, tentatively indicating the username you want to claim.
2. Read the log, and wait for the message you appended to be delivered back to you.
3. Check for any messages claiming the username that you want. If the first message for your desired username is your own message, then you are successful: you can commit the username claim (perhaps by appending another message to the log) and acknowledge it to the client. If the first message for your desired username is from another user, you abort the operation.

While this procedure ensures ***linearizable writes***, it doesn’t guarantee ***linearizable reads*** - if you read from a store that is asynchronously updated from the log, it may be stale.

To make reads linearizable:
- You can sequence reads through the log by appending a message, reading the log, and performing the actual read when the message is delivered back to you. The message’s position in the log thus defines the point in time at which the read happens.
- If the log allows you to fetch the position of the latest log message in a linearizable way, you can query that position, wait for all entries up to that position to be delivered to you, and then perform the read. (This is the idea behind [[ZooKeeper|ZooKeeper's]] sync() operation.)
- You can make your read from a replica that is synchronously updated on writes, and is thus sure to be up to date. (This technique is used in [[Chain Replication]])

# Interesting
You can also implement ***total order broadcast*** using ***linearizable storage***.

Just have a linearizable counter which you can atomically ***increment-and-get***.

Every message you want to send through *total order broadcast* you *increment-and-get* the counter and attach the value as a sequence number to the message

❗It is hard to make a linearizable integer with an atomic increment-and-get
>It can be proved that a ***linearizable compare-and-set register*** and ***total order broadcast*** are both ***equivalent to [[Consensus|consensus]]***. That means that if you solve one problem, you can transform it into solution for the others.