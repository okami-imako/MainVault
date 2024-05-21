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