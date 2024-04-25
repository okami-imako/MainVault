---
tags:
  - transactions/acid
relates to:
  - "[[ACID Properies]]"
---
***Isolation*** in the sense of [[ACID Properies|ACID]] means that concurrently executed transactions are ***isolated*** from each other: the cannot step on each other's toes.

The classic database textbook formalize isolation of ***serializability*** - each transaction can pretend that it is the only transaction running on the entire database.

The database ensures that when the transactions are [[Commit|committed]], the result is the same as if the transactions have run one after another in some order.