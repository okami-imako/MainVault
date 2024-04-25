---
tags:
  - transactions/isolation/anomaly
relates to:
  - "[[ACID - Isolation]]"
---
***Dirty Write*** is a situation when a transaction can overwrite the uncommitted write of another transaction

Most databases prevent ***dirty writes*** by using row-level [[Lock|locks]]

![[DirtyWrite.png]]