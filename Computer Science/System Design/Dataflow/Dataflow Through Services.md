---
tags:
  - dataflow/services
---
The *servers* expose an API over the network, and the *clients* can connect to the servers to make requests to that API. The API exposed by the server is known as a *service*.

# REST
There are two popular approaches to web services: [[REST]] and [[SOAP]]. They are almost diametrically opposed in terms of philosophy, and often the subject of heated debate among their respective proponents.

# RPC
The *remote procedure call* or *RPC* model tries to make a request to a remote network service look the same as calling a function or method in your programming language, within the same process (this abstraction is called *location transparency*). Although RPC seems convenient at first, the approach is fundamentally flawed. A network request is very different from a local function call:

RPC isn't going away though. Today RPC frameworks do not hide that they are a remote call and bring a lot of useful features to the table. For example [[gRPC]] supports [[stream]] communication

REST is more generalized and has to use something like JSON for encoding, which is not optimal. But it is easier to test, all languages support it and there is a ton of tools like caches, proxies, load balancers, etc. The main focus for RPC frameworks today is requests between services within one organization.

## Data encoding and evolution for RPC

it is reasonable to assume that all the servers will be updated first, and all the clients second. Thus, you only need backward compatibility on requests, and forward compatibility on responses.