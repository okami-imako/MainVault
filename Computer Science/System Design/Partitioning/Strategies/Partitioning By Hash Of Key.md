---
tags:
  - partitioning/strategy
---
# Description
In contrast to [[Partitioning By Key Range]] in order to evenly distribute [[Skewed Partitioning|skewed data]] you can assign partitions based on the [[Hash|hash]] of the key.

The hashing function doesn't have to be cryptographically strong.

Once you have a hashing function, you can assign a range of hashes to each partition.
![[PartitioningByHashOfKey.png]]

The partition boundaries could be evenly spaced or they can by chosen [[Consistent Hashing|pseudorandomly]].

# Interesting Facts
## Range Queries
The problem with the *hash partitioning* is that you can't perform effective range queries.

#Cassandra achieves a compromise between the [[Partitioning By Key Range]] and [[Partitioning By Hash Of Key]] strategies. A table in Cassandra may be declared with a ***compound primary key*** consisting of several columns. Only the first part of that key is used to determine the partition and other ones are used as a concatenated index for sorting the data. That way the query can't search for a range of values within the first column, but if the value of the first column is fixed, than it can perform an efficient range scan.

## Bad Hash Function
#Java/gotcha Java's `Object.hashCode()` isn't suitable for this use case. The same value can have different hash values in different processes [click](https://martin.kleppmann.com/2012/06/18/java-hashcode-unsafe-for-distributed-systems.html) 

## Relieving The Hot-Spot
To relieve the hot-spot in case of [[Skewed Partitioning|skew data]] it may make sense to append some gibberish to the beginning or the end of the key - just 2 random digits could evenly spread the data across 100 nodes 🤯

Good example is social media application with a celebrity with millions of followers. 

But in return you now have to collect the data on reads from multiple nodes - yikes.

# Related Topics
- [[Computer Science/System Design/Partitioning/Partitioning]]