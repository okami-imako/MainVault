---
tags:
  - transactions/isolation/anomaly
relates to:
  - "[[ACID - Isolation]]"
---
***Read Skew*** (also known as ***Non-Repeatable Read***) is an anomaly when a transaction sees different parts of the database at different points in time.

For example:
1) transaction A reads a row
2) transaction B updates that row and commits
3) transaction A reads the row again
If the 2 reads return different data - you have a ***Non-Repeatable Read*** anomaly.