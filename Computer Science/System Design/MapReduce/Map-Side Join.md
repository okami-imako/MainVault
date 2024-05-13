---
tags:
  - map-reduce
relates to:
  - "[[MapReduce]]"
---
This approach to the data joining uses a ***cut-down*** MapReduce job in which there are no reducers and no sorting.

Instead, each mapper simply reads one input file block from the distributed filesystem and writes one output file to the filesystem.

# Broadcast hash joins
This algo is applicable when a large dataset is being joined with a small dataset (so small that it can fit in memory)

1) Mapper starts up and reads the small dataset into an in-memory [[Hash Table]]
2) Mapper scans over the large dataset and simply looks up the hash table

***Broadcast*** - each mapper for a partition of the large input reads the entirety of the small input
***Hash*** - hash table is being used

Alternatively instead of loading the small dataset into memory, a read-only [[Index]] can be used on the local disk.

# Partitioned hash joins
If both datasets that are being joined are [[Partitioning|partitioned]] in the same way, then it is sufficient for each mapper to only read one partition from each of the input datasets

This has the advantage that each mapper can load a smaller amount of data into its *hash table*

# Map-Side Merge joins
If the input datasets are both ***partitioned*** in the same way and ***sorted*** based on the same key, it does not matter whether the inputs are small enough to fit in memory, because a ***mapper*** can perform the same merging operation that would normally be done by a reducer: reading both input files incrementally, in order of ascending key, and matching records with the same key.

If a ***map-side merge join*** is possible, it probably means that prior MapReduce jobs brought the input datasets into this partitioned and sorted form in the first place. In principle, this join could have been performed in the ***reduce stage of the prior job***.

However, it may still be appropriate to perform the ***merge join*** in a ***separate*** map-
only job, for example if the partitioned and sorted datasets are also needed for other purposes besides this particular join.