---
tags:
  - stream-processing
relates to:
  - "[[Stream Processing]]"
  - "[[Message-Passing Dataflow]]"
---
A common approach for notifying consumers about new events is to use a ***messaging system***: a [[Producer]] sends a message containing the [[Event]], which is then pushed to [[Consumer|consumers]]

Messaging systems differ in a wide range if things:
1) What happens if the producers send messages faster than the consumers can process them?
	- Drop the message
	- Buffer message in a queue
	- Apply [[Backpressure]]
2) What happens if nodes crash or temporarily go offline?
	- [[Replication]]

There are 2 main approaches to delivering the messages:
- Direct communication channel between producer and consumer
- [[Message Broker]]