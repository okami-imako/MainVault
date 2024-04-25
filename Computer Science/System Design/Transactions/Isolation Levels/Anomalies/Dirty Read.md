---
tags:
  - transactions/isolation/anomaly
relates to:
  - "[[ACID - Isolation]]"
---
***Dirty Read*** is a situation when a transaction can see uncommitted writes of the other transactions

***Dirty Reads***  can be prevented by storing both committed and dirty values, and returning committed value to all reads.