---
tags:
  - replication/anomaly
---
2 users are collaboratively working on a wiki page.
- First user changes the title of the document from A to B
- Second user changes the title of the document from A to C
- Both changes are flushed to the local working copies of the users
- When changes are asynchronously replicated - a ***conflict*** is detected

![[WriteConflictResolution.png]]

The best strategy is to ***avoid*** conflicts. If you can ensure that all writes dedicated to a specific record go through the same leader, the conflicts cannot occur.

In a [[Multi-Leader Replication]] setup there is no 'correct' order of writes.
If first user changes title to B and then to C, while the other changes it to C and then to B, what should be the final state of the title? Neither of variants is more correct then the other. But replicas can't just accept writes in the order they see them and just settle. All of the replicas ***must*** ***eventually*** contain the same information. There are multiple approaches to this:
- Assign an ID to each write and make the one with the highest ID *winner* and all of the other *losers*. If timestamps are used, then this is called [[Last Write Wins]]. This approach leads to ***data loss***.
- Give each replica a unique ID and make the replica with the highest ID win. This approach also leads to ***data loss***.
- Somehow merge the values together. In the example above it will result in something like "B/C"
- Store all conflicting values in a some kind of data structure and move the conflict resolution logic to the application layer (perhaps ask the user later to resolve the conflict by hand)

Most multi-leader replication let you write the custom conflict resolution logic. The code can be executed:
- On writes. In that case the code can't prompt the user and has to handle the conflict quickly as it probably may be running in a background process
- On reads. In that case when conflict is detected, all the conflict writes are stored. Later, when the data is being read, the application is supplied with multiple versions of it and the app may prompt the user.

A lot of research went into ***Automatic Conflict Resolution***:
- [[Conflict-Free Replicated Datatypes]]
- Mergeable persistent [[Data Structures|data structures]] track history explicitly, similarly to the [[Git]] [[Version Control System|version control system]], and use a three-way merge function (whereas CRDTs use two-way merges).
- Operational transformation is the conflict resolution algorithm behind collaborative editing applications such as Etherpad and Google Docs. It was designed particularly for concurrent editing of an ordered list of items, such as the list of characters that constitute a text document.