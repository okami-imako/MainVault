---
tags:
  - transactions/acid
relates to:
  - "[[ACID Properies]]"
---
Generally you have some certain statements about your data (*invariants*) that must always be true.

>For example: transfer from one bank account to another shouldn't change the overall balance across accounts.

Database allows creating [[Integrity Constraints|integrity constraints]] (NOT NULL, UNIQUE). If the data complies with integrity constraints, than it is integrant.

However some of the *invariants* are to complex to define on the database level.

***Consistency*** is a more strict term then ***integrity***

[[ACID - Atomicity|Atomicity]], [[ACID - Isolation|isolation]] and [[ACID - Durability|durability]] are the properties of the database, while ***consistency*** is the property of the application.

The application can rely on the database's ***atomicity*** and ***isolation*** principles in order to achieve ***consistency***

Thus, the letter *C* doesn't really belong in ***[[ACID Properies|ACID]]***