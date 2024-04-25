---
tags:
  - transactions/isolation
relates to:
  - "[[Two-Phase Locking]]"
  - "[[Lock]]"
---
Conceptually ***predicate lock*** works the same as shared/exclusive lock, but rather then belonging to a single object, it belongs to all objects that match some search condition, such as:
```sql
SELECT * FROM bookings 
WHERE room_id = 123
	AND end_time > '2018-01-01 12:00'
	AND start_time < '2018-01-01 13:00';
```

___
The ***predicate locking*** mechanism would work as follows:
- When transaction A wants to read objects, matching some condition, it must acquire a ***shared lock*** on that condition. If another transaction B has an ***exclusive lock*** on that condition, transaction A must wait until B releases the exclusive lock.
- If transaction A wants to write (insert, update, delete) an object, than it must check what conditions does it's old/new value match, and take exclusive locks on those conditions.

___
The key idea is that a predicate lock applies even to objects, that do not exist yet - [[Phantom Read|phantoms]]. If a [[Two-Phase Locking|2PL]] mechanism includes predicate locks, the database prevents all forms of [[Write Skew]] and other [[Race Condition|race conditions]], so the isolation becomes [[Serializable]]

Unfortunately, ***predicate locks*** do not perform well because of the overhead, that they bring. For that reason most databases with 2PL actually implement [[Index-Range Locking]]