---
tags:
  - stream-processing
relates to:
  - "[[Stream Processing]]"
---
Conventional design: *writes* to the store go through an *event log*, while *reads* go directly to the nodes that store the data being queried

Another interesting approach is to treat both *writes* and *reads* as [[Event|events]]

In that case they are routed to the same ***stream operator*** in order to be handled. In fact it performs a [[Stream-Table Join]] between the stream of read queries and the database.

Recording a log of *read events* has benefits

It allows tracking [[Causal Dependency|causal dependencies]]. It would allow you to reconstruct what the user saw before they made a particular decision.

Though this approach has additional I/O costs, but if you already log read requests, it is not such a great change