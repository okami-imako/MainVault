---
tags:
  - stream-processing
relates to:
  - "[[Messaging System]]"
---
***Message Broker*** is kind of database that is optimized for handling message streams.

It runs as a server, which [[Producer|producers]] and [[Consumer|consumers]] connect to as clients. ***Producers*** write messages to the ***broker***, and ***consumers*** receive them by reading them from the ***broker***

# Benefits
- Clients may come and go
- [[Durability]] if the broker writes to the disk
- Allow ***unbounded*** queueing
- [[Asynchronous]] producing and consuming

# Notes
## Multiple Consumers
2 strategies:
- ***Load Balancing*** - each message is delivered to one of the consumers, so the consumers can share the work of processing the messages in the topic
- ***Fan Out*** - each message is delivered to all consumers
> These 2 approaches can be combined