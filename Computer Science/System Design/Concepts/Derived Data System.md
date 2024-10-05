---
tags:
  - concept
---
***Derived data system*** is a system that stores data that is the result of taking some existing data from another system and transforming or processing it in some way

If you lose derived data, you can recreate it from the original source.

A classic examples are [[Cache|caches]], denormalized values, [[Index|indexes]] and [[Materialized View|materialized views]]

>Technically speaking, derived data is ***redundant***

The workflow of ***derived dataset*** consists of 2 parts:
- ***Write Path*** - whenever some piece of information is written to the system, it may go through multiple stages of [[Batch Processing|batch]] and [[Stream Processing|stream]] processing, and eventually every derived dataset is updated to incorporate the data that was written
- ***Read Path*** - when serving a user request you read from the derived dataset, perhaps perform some processing on the results, and construct the response to the user
![[Pasted image 20240610184826.png]]
Taken together the *write path* and *read path* encompass the whole journey of the data.

## Important Take Away
The *derived dataset* is the place where the *write path* and the *read path* meet. It represents a ***trade-off*** between the amount of work that needs to be done at write time and the amount that needs to be done at read time