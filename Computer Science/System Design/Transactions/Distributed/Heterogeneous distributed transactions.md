---
tags:
  - transactions
  - distributed-systems
relates to:
  - "[[Distributed Transactions]]"
---
The participants are two or more different technologies: for example, two databases from different vendors, or even non-database systems such as message brokers. A distributed transaction across these systems ***must ensure atomic commit***, even though the systems may be entirely different under the hood. This type is challenging