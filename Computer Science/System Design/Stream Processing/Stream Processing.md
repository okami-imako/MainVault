---
tags:
  - stream-processing
relates to:
  - "[[stream]]"
---
***Stream processing*** is a type of processing where the data is ***unbounded*** - it is incrementally made available over type.

The idea of ***stream processing*** is opposite to the idea of ***bounded*** [[Batch Processing]]

The concept of *stream processing* is used all over the place:
- `stdin` and `stdout` in [[Unix]]
- filesystem APIs
- [[Transmission Control Protocol|TCP]]

A piece of data in ***stream processing*** system is called [[Event]]. An ***event*** is generated once by a [[Producer]], and then potentially processed by multiple [[Consumer]]

Related ***events*** are usually grouped together into [[Topic|topics]]

# Uses of Stream Processing
---
- ***Complex event processing*** - ***CEP*** allows you to specify rules to search for certain patterns of events in a stream, similar to [[Regular Expression|regexp]]
- ***Stream analytics*** - Kinda like ***CEP***, but is more oriented toward aggregation and statistical metrics over a large number of events
- Maintaining [[Materialized View]]
- Search on streams - looking for an event that matches some criteria
- [[Message-Passing Dataflow]]