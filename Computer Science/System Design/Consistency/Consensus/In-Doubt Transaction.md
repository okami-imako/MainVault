---
tags:
  - consistency-guarantee/consensus
relates to:
  - "[[Distributed Transactions]]"
  - "[[Two-Phase Commit]]"
---
When the participant was asked to ***prepare***, replied with `yes` and coordinator crashed - it has to wait to hear from it again

This state of the transaction is called ***In Doubt*** or ***Uncertain***