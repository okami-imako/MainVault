Last Write Wins is a [[Write Conflict Resolution]] technique that implies assigning a timestamp to each write and making the nodes discard the older writes. That way the nodes will [[Eventual Consistency|eventually]] contain the same value.

LWW implies discarding writes, so you will have a ***data loss***