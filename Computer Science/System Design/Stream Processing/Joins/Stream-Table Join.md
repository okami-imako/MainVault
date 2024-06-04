---
tags:
  - "#stream-processing/join"
relates to:
  - "[[Stream Joins]]"
---
***Stream-Table Join*** (or ***stream enrichment***) has to be performed when you want to join a stream of data with some db table

For example if you want to ***enrich*** user events with user's details

The approach is very similar to [[Map-Side Join]] in [[Batch Processing|batch processing job]]. That is, stream processor can keep a local copy of the user profile db either in-memory if it is small, or just have a local db instance.

The problem is that as opposed to the ***Batch Processing Job*** which runs on some point-in-time snapshot of the db, ***Stream Processing Job*** is a long-running process, and the contents of db are likely to change.

The solution is to subscribe to the changelog of the user profile db