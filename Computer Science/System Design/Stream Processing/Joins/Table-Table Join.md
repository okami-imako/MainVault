---
tags:
  - stream-processing/join
relates to:
  - "[[Stream Processing]]"
---
Say we want to implement a timeline cache for twitter: a kind of per-user "inbox" to which tweets are written as they are sent, so that reading the timeline is a single lookup:
- When user A sends a new tweet, it is added to the timeline of every user who us following A
- When a user deletes a tweet, it is removed from all users' timelines
- When user A starts following user B, recent tweets by B are added to A's timeline
- When user A unfollows user B, tweets by B are removed from A's timeline

To implement this [[Cache]] maintenance in a stream processor, you need streams of events for ***tweets*** (sending and deleting) and for ***follow relationship*** (following and unfollowing). Te stream process needs to maintain a database containing the set of followers for each user so that it knows which timelines need to be updated when a new tweet arrives

Another way of looking at this stream process is that it maintains a [[Materialized View]] for a query that joins two tables (tweets and follows)

Thus, the join of streams corresponds directly to the join of the tables. The timelines are effectively a cache of the join-query, updated every time the underlying tables change