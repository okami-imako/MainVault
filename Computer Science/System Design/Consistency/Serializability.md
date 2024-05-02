---
tags:
  - concept
  - transactions
---
***Serializability*** is an isolation property of [[Transaction|transactions]], where every transaction may read and write multiple objects (rows, documents, records).

It guarantees that transactions behave the same as if they had executed in ***some serial order*** (each transaction running to completion before the next transaction starts). It is okay for that serial order to be different from the order in which transactions were actually run.