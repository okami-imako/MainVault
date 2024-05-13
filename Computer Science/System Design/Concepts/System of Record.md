---
tags:
  - concept
---
A ***System of Record***, also known as ***source of truth***, is a system that stores the data and holds the authoritative version of the data.

When new data comes, it is first written here

Each fact is represented exactly once (the representation is [[Normal Forms|normalized]])

If there is any diff between another system and the ***system of record*** then the value in the *system of record* is by definition the correct one