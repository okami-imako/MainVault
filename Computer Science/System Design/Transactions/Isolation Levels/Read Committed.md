---
tags:
  - transactions/isolation
relates to:
  - "[[ACID - Isolation]]"
---
# Forbidden Anomalies
---
- [[Dirty Write]]
- [[Dirty Read]]
# Description
---
The most basic level of transaction isolation is ***read committed***.

It makes two guarantees:
1. When reading from the database, you will only see the data that has been committed (***no [[Dirty Read|dirty reads]]***).
2. When writing to the the database, you will only overwrite the data that has been committed (***no [[Dirty Write|dirty writes]]***).