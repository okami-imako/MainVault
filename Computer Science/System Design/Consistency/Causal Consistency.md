---
tags:
  - consistency-guarantee
---
Two operations are [[Concurrency|concurrent]] if neither [[Happens Before|happened before]] the other.

Put another way, two events are ***ordered*** if they are ***causally related*** (one happened before the other), but they are ***incomparable*** if they are ***concurrent***.

This means that ***causality*** defines a ***[[Partial Order]]***, not a ***[[Total Order]]***: some operations are ordered with respect to each other, but some are *incomparable*

[[Linearizability]] implies ***causal consistency***, but linearizability is a much ***stronger*** guarantee

# Examples
- [[Consistent Prefix Reads]] - ***causal dependency*** between the question and the answer
- Insert comes before update
- [[Happens Before]] is an expression of causality