---
tags:
  - consistency-guarantee/consensus
relates to:
  - "[[Two-Phase Commit]]"
  - "[[Heterogeneous distributed transactions]]"
---
***X/Open XA*** (short for ***eXtended Architecture***) is a standard for implementing [[Two-Phase Commit|two-phase commit]] across [[Heterogeneous distributed transactions|heterogeneous]] technologies

It is a C API for interfacing with a transaction coordinator

***XA*** assumes that your application uses a network driver of client library to communicate with the *participant* databases or messaging services. If the driver supports XA, that means it calls the XA API to find out whether an operation should be a part of a [[Distributed Transactions]] - and if so it sends the necessary information to the database server. The driver also exposes callbacks through which the coordinator can ask the participant to ***prepare***, ***commit***, or ***abort***

The transaction coordinator implements the XA API