---
tags:
  - transactions/isolation
relates to:
  - "[[Predicate Locks]]"
---
The idea is to ***broaden*** the lock condition in order to reduce overhead at the cost of locking more objects then necessary.

In the room booking example you would probable have a [[Secondary Indexes|index]] on `room_id`, `start_time` and `end_time`. Now:
- If the database uses the index on `room_id` to find bookings for the room 123, it can simply attach a shared lock to this index entry, indicating that a transaction has searched for bookings of room 123
- If the database uses a time-based index to find existing bookings, it can attach a lock to the index value, indicating that the a transaction has searched for bookings that overlap with the specific time period

Now, if another transaction wants to insert, update or delete a booking for the same room, and/or an overlapping time period, it will have to update the same parts of the index. In the process of doing so, it will encounter the shared [[Lock|lock]], and will be forced to wait until the lock is released.
___
This approach is locking more rows, that strictly speaking [[Predicate Locks]] require, but since they have much lower overheads, they are a good compromise.
___
If there are no suitable indexes, the database can lock the entire table