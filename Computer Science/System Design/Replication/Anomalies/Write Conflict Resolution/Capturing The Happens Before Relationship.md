---
tags:
  - replication/anomaly
---
# Description
Some of the [[Write Conflict Resolution|write conflicts]] can be handled by capturing the [[Happens Before]] relationship between the events. That way if the system knows that event *A* ***happens before*** event *B*, then *B* can safely ***overwrite*** *A*.

# Example
2 users are writing to the same shopping cart via overriding it's content with some value.
![[HappensBeforeCapture1.png]]
[[Capturing The Happens Before Relationship#Example Breakdown|breakdown]]
Here server at the given moment stores 2 values for the shopping cart.

Here is a full dataflow
![[HappensBeforeCapture2.png]]

Arrows indicate that given operation ***knows about*** or ***depends on*** some other operation, in other words capturing the [[Happens Before]] relationship.

Old versions are getting overwritten eventually and ***no data is lost***
# Example Breakdown
1) Client 1 adds `milk` to the cart. This is the first write to that key, so the server successfully stores it and assigns it version 1. The server also echoes the value back to the client, along with the version number.
2) Client 2 adds `eggs` to the cart, not knowing that client 1 concurrently added `milk` (client 2 thought that its `eggs` were the only item in the cart). The server assigns version 2 to this write, and stores `eggs` and `milk` as two separate values. It then returns both values to the client, along with the version number of 2.
3) Client 1, oblivious to client 2’s write, wants to add `flour` to the cart, so it thinks the current cart contents should be `[milk, flour]`. It sends this value to the server, along with the version number 1 that the server gave client 1 previously. The server can tell from the version number that the write of `[milk, flour]` supersedes the prior value of `[milk]` but that it is concurrent with `[eggs]`. Thus, the server assigns version 3 to `[milk, flour]`, overwrites the version 1 value `[milk]`, but keeps the version 2 value `[eggs]` and returns both remaining values to the client.
4) Meanwhile, client 2 wants to add `ham` to the cart, unaware that client 1 just added `flour`. Client 2 received the two values `[milk]` and `[eggs]` from the server in the last response, so the client now merges those values and adds `ham` to form a new value, `[eggs, milk, ham]` . It sends that value to the server, along with the previous version number 2. The server detects that version 2 overwrites `[eggs]` but is concurrent with `[milk, flour]`, so the two remaining values are `[milk, flour]` with version 3, and `[eggs, milk, ham]` with version 4.
5) Finally, client 1 wants to add `bacon`. It previously received `[milk, flour]` and `[eggs]` from the server at version 3, so it merges those, adds `bacon`, and sends the final value `[milk, flour, eggs, bacon]` to the server, along with the version number 3. This overwrites `[milk, flour]` (note that `[eggs]` was already overwritten in the last step) but is concurrent with `[eggs, milk, ham]`, so the server keeps those two concurrent values.

# Algorithm
- The ***server*** stores ***multiple*** versions of each key at the same time
- When ***client*** ***reads*** the key, server responds with ***all*** versions of the key, that have not been overwritten yet along with the ***latest*** version number. A client ***must*** read the key before writing
- When ***client*** wants to ***write*** the key, he must ***merge*** all the versions he has received and provide a version number he ***received*** in the last read
- When ***server*** receives a ***write***, he can safely ***overwrite*** all the versions which are ***less or equal*** to the version number provided (they have been merged into the new value), but he must keep all the values with the version number ***higher*** than provided (because those values are [[Concurrency|concurrent]] with the incoming write)

When a write includes a version number from the prior read, that tells us which previous state this write is based on. If write doesn't include the version, than it is concurrent with ***all other writes*** and won't overwrite anything, but will be returned as one of the values on subsequent reads.

Clients have to clean up after concurrent operations (***siblings***). This problem is similar to [[Write Conflict Resolution]]. You can use [[Last Write Wins]] strategy, or merge the values together like in the example. In that case key deletions should be treated cautiously (via using [[Tombstone|tombstones]] for example)

As merging siblings on application level is hard to get right, some datastores use [[Conflict-Free Replicated Datatypes|CFRD]] - special data structures that automatically merge siblings.

In case of [[Leaderless Replication]] we have to track the version per key per replica, that brings as to ***version vector***. Like the ***version number*** version vector is returned by the database on reads and should be provided on writes, so that the db can distinguish between values that can be overwritten and *siblings*.