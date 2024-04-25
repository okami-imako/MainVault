---
tags:
  - transactions/isolation/anomaly
relates to:
  - "[[ACID - Isolation]]"
---
***Write Skew*** is an anomaly when one transaction reads something, makes a decision based on the data it has just read, and writes the decision to the database. However by the time the write is made, the initial premise is no longer true.

Let's suppose you have a hospital where there should be at least 1 doctor on-call.
In the event there are 2 doctors on-call, and both of them feel sick and try to go off-call this can happen:
![[WriteSkew.png]]

This anomaly is called ***write skew***. It is neither [[Dirty Write|dirty write]] nor [[Lost Update|lost update]], because two transactions are updating two different objects.

***Write Skew*** is a more generalized *dirty write*.

>Two transactions read the same objects and then update some of those objects (different transactions may update different objects). In the special case when two transactions update the same object, you get a ***dirty write*** or ***lost update*** anomaly (depending on the timing)

***Write Skew*** is a tricky anomaly to detect and requires [[Serializable|Serializable Isolation Level]] 

# Write Skew Pattern
1. A `SELECT` query checks whether some requirement is satisfied by searching for rows that match some search condition (there are at least two doctors on call, there are no existing bookings for that room at that time, the position on the board doesn’t already have another figure on it, the username isn’t already taken, there is still money in the account).
2. Depending on the result of the first query, the application code decides how to continue (perhaps to go ahead with the operation, or perhaps to report an error to the user and abort).
3. If the application decides to go ahead, it makes a write (`INSERT`, `UPDATE`, or `DELETE`) to the database and commits the transaction. The effect of this write changes the precondition of the decision of step 2. In other words, if you were to repeat the `SELECT` query from step 1 after commiting the write, you would get a different result, because the write changed the set of rows matching the search condition (there is now one fewer doctor on call, the meeting room is now booked for that time, the position on the board is now taken by the figure that was moved, the username is now taken, there is now less money in the account).

# Tricky Part
The doctor example can be fixed with a `SELECT FOR UPDATE`
But what if in the first step we check for the ***absence*** of rows matching some condition?
We can't lock rows, that don't exist

## Example
___
`booking` table, where you insert reservations for a room for a specific time slot. The reservation transaction may look like this
```sql
BEGIN TRANSACTION;
-- Check for any existing bookings that overlap with the period of noon-1pm
SELECT COUNT(*) FROM bookings
WHERE room_id = 123 AND
end_time > '2015-01-01 12:00' AND start_time < '2015-01-01 13:00';
-- If the previous query returned zero:
INSERT INTO bookings
(room_id, start_time, end_time, user_id)
VALUES (123, '2015-01-01 12:00', '2015-01-01 13:00', 666);
COMMIT;
```

In order to avoid the problem of [[Phantom Read|phantoms]] we can artificially introduce locks to the database

We can create a separate table where each row corresponds to a particular room for a particular time period (say, 15 minutes).

Now in the beginning of transaction we lock the rows, corresponding to the time period for which we want to book the room and only after that check the amount of overlapping reservations. 

This approach is called ***materializing conflicts***