---
tags:
  - transactions/isolation/anomaly
relates to:
  - "[[ACID - Isolation]]"
---
***Lost Update*** is a situation in which an update of transaction is lost (shocker)

>Two transactions read the counter value, first one increments it and commits, then the second one increments the previously read value and commits - an update made by the first transaction is lost.

***Lost Updates*** can be prevented by a number of techniques such as:
___
[[Atomicity|Atomic]] write operations which remove the need to implement error-prone *read-modify-write* cycle
```sql
UPDATE counter SET value = value + 1 WHERE key = 'foo';
```
___
Explicit [[Lock|locking]] - if db doesn't support atomic writes, or the logic is too complex for an atomic operation - just lock the row
```sql
BEGIN TRANSACTION;
SELECT * FROM figures WHERE name = 'robot' AND game_id = 222 FOR UPDATE;
-- Check whether move is valid, then update the position
-- of the piece that was returned by the previous SELECT.
UPDATE figures SET position = 'c4' WHERE id = 1234;
COMMIT;
```
___
Allow executing updates in parallel, but if you detect a lost update, abort the transaction and force it to retry its *read-modify-write* cycle. [[Write Conflict Resolution]]
___
[[Compare And Set]]
```sql
-- This may or may not be safe, depending on the database implementation
UPDATE wiki_pages SET content = 'new content'
WHERE id = 1234 AND content = 'old content';
```
🔴Warning: if the database allows the `WHERE` clause to read from an old snapshot, this statement won't prevent lost updates
___
In case of [[Multi-Leader Replication]] or [[Leaderless Replication]] writes happen [[Concurrency|concurrently]] and are being replicated [[Asynchronous|asynchronously]], so there is no single up-to-date copy of the data. Thus, techniques based on locks or compare-and-set do not apply.
Instead such techniques are used: [[Write Conflict Resolution]]