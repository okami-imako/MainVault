---
tags:
  - replication
  - concept
---
Replication Log is a log maintained by the leader that the followers use to receive updates

# Statement-based replication

In the simplest case, the leader logs every write request (statement) that it executes and sends that statement log to its followers.

Problems:
- Non-deterministic function calls such as `rand()`
- Should be executed in strict order, because of things like autoincrements
- Statements with side-effects (triggers, stored procedures, etc.) may result in different behavior on different replicas unless they are absolutely deterministic

# Write-ahead log shipping

Usually all writes are appended to a log ([[Write-Ahead Log]])

The log is an append-only sequence of bytes containing all writes to the database. We can use the exact same log to build a replica on another node: besides writing the log to disk, the leader also sends it across the network to its followers. When the follower processes this log, it builds a copy of the exact same data structures as found on the leader.

WAL contains details of which bytes were changed in which disk blocks. This makes replication closely coupled to the storage engine. If the database changes its storage format from one version to another, it is typically not possible to run different versions of the database software on the leader and the followers.

# Logical (row-based) log replication

An alternative is to use different log formats for replication and for the storage engine, which allows the replication log to be decoupled from the storage engine internals. This kind of replication log is called a logical log, to distinguish it from the storage engine’s (physical) data representation.

A logical log for a relational database is usually a sequence of records describing writes to database tables at the granularity of a row:
- For an inserted row, the log contains the new values of all columns.
- For a deleted row, the log contains enough information to uniquely identify the row that was deleted. Typically this would be the primary key, but if there is no primary key on the table, the old values of all columns need to be logged.
- For an updated row, the log contains enough information to uniquely identify the updated row, and the new values of all columns (or at least the new values of all columns that changed).

Useful for [[Change Data Capture|change data capture]]

# Trigger-based replication

Handling replication on application level. Might be useful in cases when:
- Only want to replicate a subset of data
- Want to replicate between different kinds of databases
- Conflict resolution logic is needed

Might prove helpful: [[Triggers|triggers]] and [[Stored Procedures|stored procedures]].

Trigger-based replication typically has greater overheads than other replication methods, and is more prone to bugs and limitations than the database’s built-in replication. However, it can nevertheless be useful due to its flexibility.

# Related Topics
- [[Replication]]