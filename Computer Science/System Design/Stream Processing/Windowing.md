---
tags:
  - stream-processing
relates to:
  - "[[Stream Processing]]"
---
One way to process a unbound stream of data is using ***windowing***

There are 2 main timestamps:
- ***event timestamp*** - point in time at which event was generated
- ***processing timestamp*** - point in time at which event was processed by the consumer

In most cases it makes more sense to window over the ***event timestamp***

Example:
![[Pasted image 20240528210719.png]]

# Reasoning About Time
---
The main challenge is to ***know when you are ready*** to close current window and start processing the next one. Events can be shuffled and you can still receive events belonging to previous windows while processing new one. Such events are called ***straggler*** events

There are 2 options on how to deal with ***straggler*** events:
- Ignore. You can track the number of dropped events to raise alarm in case when you start loosing too much data
- Publish a ***correction***, an updated value for the window with stragglers included

## Buffering
In case of a mobile app that reports events for usage metrics to a server, it can go offline and events will be buffered locally. Then, when device will go online, they will be sent all at once, and any consumer of the stream will see a lot of extremely delayed ***stragglers***

In this context, the timestamp of the event should be the time at which the user interaction occurred, but we can't trust the clock on user's device as it may be set to the wrong time.

We can adjust for incorrect device clocks using 3 timestamps:
- The time at which the event occurred, according to the device clock
- The time at which the event was sent, according to the device clock
- The time at which the event was received by the server, according to the server clock
We can assume that the diff between the second and the third timestamps is very small, we can calculate the offset between the device's and server's clock. Then we can apply that offset to the first timestamp

# Types Of Windows
---
## Tumbling Window
Has a fixed length and every event belongs to exactly one window
![[Pasted image 20240528215948.png]]
## Hopping Window
Has a fixed length, but windows may overlap - 3-minute window with a hop size of 1 minute
![[Pasted image 20240528215919.png]]

## Sliding Window
Has a fixed length, contains all events that occur within some interval of each other
![[Pasted image 20240528220022.png]]
## Session Window
Has no fixed length. Defined by grouping together all events for the same user that occur closely together in time, and the window ends when the user has been inactive for some time