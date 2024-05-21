---
tags:
  - batch-processing/map-reduce
---
***MapReduce*** is a programming [[Framework]] used to write code to process large datasets in a distributed filesystem - [[Batch Processing]]

The pattern of data processing looks like this:
1) Call the ***mapper*** function to extract a ***key*** and ***value*** from each input ***record***
2) Sort all of the ***key-value*** pairs by ***key*** (this step is *implicit*)
3) Call the ***reducer*** function on each subset of ***key-value*** pairs with the same ***key***

To create a MapReduce job, you need to implement two callback functions - ***mapper*** and ***reducer***

Due to the fact that *mapper* and *reducer* only operate on one record at a time, the ***MapReduce*** job can be easily [[Parallel Execution|parallelized]] without having to explicitly handle the parallelism.

# Mapper
___
The mapper is called once for every input record, and its job is to extract the key and value from the input record. For each input, it may generate ***any number*** of key-value pairs (including none). It does not keep any state from one input record to the next, so each record is handled independently.

# Sorting
___
The key-value pairs must be sorted, but the dataset is likely too large to be sorted with a conventional sorting algorithm on a single machine. Instead, the sorting is performed in stages.
1) First, each map task partitions its output by ***reducer***, based on the hash of the key. Each of these partitions is written to a sorted file on the ***mapper’s*** local disk ([[SSTables]] and [[LSM-Trees]])
2) Whenever a ***mapper*** finishes reading its input file and writing its sorted output files, the *MapReduce scheduler* notifies the ***reducers*** that they can start fetching the output files from that mapper. The ***reducers*** connect to each of the ***mappers*** and download the files of sorted key-value pairs for their partition. The process of partitioning by reducer, sorting, and copying data partitions from mappers to reducers is known as the ***shuffle***
# Reducer
___
The MapReduce framework takes the key-value pairs produced by the mappers, collects all the values belonging to the same key, and calls the reducer with an iterator over that collection of values. The reducer can produce output records (such as the number of occurrences of the same URL).
# Example
___
Here is an example MapReduce workflow from Hadoop
![[HadoopMapReduceJob.png]]

# Big Ideas
___
- MapReduce programming model has separated the physical network communication aspect from the application logic. It shields the application code from having to worry about partial [[Failure|failures]], such as the crash of another node.
- The MapReduce job is a [[Pure Function]], meaning that it doesn't modify input, has no side-effects like writing to the external db
- Input of the batch job is often just a distributed file system. With that approach you can just dump the data without thinking ahead about a perfect data model. Later it becomes more clear how to interpret the data to gain meaningful insights via running batch job against it. Moreover the same raw data can be interpreted differently by different batch jobs 