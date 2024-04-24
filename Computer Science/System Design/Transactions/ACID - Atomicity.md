---
tags:
  - transactions/acid
relates to:
  - "[[ACID Properies]]"
---
[[Atomicity]] is a general computer science term.

In the scope of transactions *atomicity* describes what happens if a client wants to make several writes, but a [[Fault|fault]] occurres after some of the writes have been processed.

If the writes are grouped together into an ***atomic*** transaction, and the transaction cannot be completed ([[Commit|commited]]), then the whole transaction is aborted ([[Rollback|rollbacked]]) and none of the writes take effect.