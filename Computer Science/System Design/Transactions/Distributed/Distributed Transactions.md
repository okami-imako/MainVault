---
tags:
  - transactions
  - distributed-systems
---
There are 2 main types of ***Distributed Transactions***:
___
![[Database-Internal Distributed Transactions]]
___
![[Heterogeneous distributed transactions]] 
___

# Problems
- Bad Performance
- Operational Cost
- In case of [[Two-Phase Commit]] coordinator itself acts as a database and if not replicated is a single point of failure. Also if coordinator is a part of the application server, then the servers becomes [[Stateful]]
- [[In-Doubt Transaction]] can hold on to [[Lock|locks]]
- In case of [[eXtended Architecture|XA]] there is no [[Deadlock]] detection and no [[Serializable Snapshot Isolation]]