---
tags:
  - stream-processing/join
relates to:
  - "[[Stream Joins]]"
---
Say you want to join 2 streams of data on some ***ID*** field. Some events in one stream may not have corresponding event in the second stream and even if it does, the time between 2 events is highly variable (from a couple of seconds to days or event weeks).

To handle such joins ***stream processor*** needs to maintain ***state***

## Example
---
All the events that occurred in the last hour are indexed by ***ID***. Whenever new event occurs, it is added to the appropriate [[Index|index]], and the stream processor also checks the other index to see if another event for the same ***ID*** has already arrived. If there is a matching event, you emit a merged event. If an event expires without seeing a matching event from another stream, you emit an event saying, that there was no match