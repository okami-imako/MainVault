---
tags:
  - architecture
  - distributed-system
relates to:
  - "[[Fault]]"
---
Many systems need to automatically detect faulty nodes:
- A [[Load Balancer]] needs to stop sending requests to the dead node
- If in [[Leader-Based Replication]] leader dies, [[Failover]] must happen

Unfortunately, detecting node failures isn't easy

Generally you need to query the application itself if it is alive. Even then if you don't get a response it is ***impossible*** to know why. It could be
- Application Crash
- Network Failure
- Queuing 
- Overloaded network, or application

# Timeouts
Generally you want to wait for a response for some time (*timeout*) and if there is no response during that, time - consider the node dead.

How long the timeout should be? Unclear
- Too long - long wait until a node is declared dead
- Too short - you may consider node dead even if it's not - for example it was overloaded and was slow to answer - ***premature timeout***

# Network Congestion
If several nodes at the same time try to send packets to the same destination - [[Network Switch]] has to queue them up and feed into the destination link one by one. If the switch's queue get's filled up - packets are dropped
![[NetworkCongestion.png]]