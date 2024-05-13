---
tags:
  - concept
---
# Service (online systems)
___
A service waits for a request or instruction from a client to arrive. When one is received, the service tries to handle it as quickly as possible and sends a response back. Response time is usually the primary measure of performance of a service, and availability is often very important.

# Batch processing systems (offline systems)
___
A batch processing system takes a large amount of input data, runs a job to process it, and produces some output data. Jobs often take a while (from a few minutes to several days), so there normally isn’t a user waiting for the job to finish. Instead, batch jobs are often scheduled to run periodically (for example, once a day). The primary performance measure of a batch job is usually [[Throughput]] (the time it takes to crunch through an input dataset of a certain size).

# Stream processing systems (near-real-time systems)
___
Stream processing is somewhere between online and offline/batch processing (so it is sometimes called ***near-real-time*** or ***nearline*** processing). Like a batch processing system, a stream processor consumes inputs and produces outputs (rather than responding to requests). However, a stream job operates on events shortly after they happen, whereas a batch job operates on a fixed set of input data. This difference allows stream processing systems to have lower latency than the equivalent batch systems.