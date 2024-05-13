---
tags:
  - map-reduce
relates to:
  - "[[MapReduce]]"
---
Consider the following data relation
![[Pasted image 20240512163620.png]]

The workflow in which there is a need to perform a join:
![[Pasted image 20240512163546.png]]

The MapReduce job can arrange the records to be sorted such that the ***reducer*** always sees the record from the user database first, followed by the activity events - this technique is known as a ***secondary sort***

***Advantages***
- The [[Reduce-Side Join]] approach has the advantage that you do not need to make any assumptions about the input data. 

***Disadvantages***
-  All that sorting, copying to reducers, and merging of reducer inputs can be quite expensive