---
tags:
  - stream-processing/fault-tolerance
relates to:
  - "[[Stream Processing Fault Tolerance]]"
---
***Microbatching*** is an approach when you break the [[stream]] into small blocks, and treat each block like a miniature [[Batch Processing|batch process]]

***Microbatching*** implicitly provides a [[Windowing#Tumbling Window]] equal to the batch size (windowed by processing time, not event timestamp)