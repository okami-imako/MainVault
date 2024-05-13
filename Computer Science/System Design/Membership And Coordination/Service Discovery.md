---
tags:
  - architecture
---
***Service Discovery*** is a technology used to find out which [[Internet Protocol|IP address]] you need to connect to in order to reach a particular service. 

In cloud datacenter environments, where it is common for nodes to come and go, you often don't know the IP address of you services ahead of time.

Instead, you can configure your services such that when they start up they register themselves in a ***service registry***, where they can then be found by other services.

### Does Service Discovery need [[Consensus]]?
[[Domain Name System|DNS]] is the traditional way of looking up the IP address for a service name, and it uses multiple layers of caching to achieve good performance and availability. 

Reads from DNS are absolutely not [[Linearizability|linearizable]], and it is usually not considered problematic if the results from a DNS query are a little stale. It is more important that DNS is reliably available and robust to network interruptions.