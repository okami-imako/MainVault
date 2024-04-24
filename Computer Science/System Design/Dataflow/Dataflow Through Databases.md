---
tags:
  - dataflow/database
---
Storing something in the [[Database|database]] is *sending a message to your future self*.
Backward compatibility is clearly necessary here; otherwise your future self won’t be able to decode what you previously wrote.

Alternatively if there are multiple instances of a single application, and you perform a rolling update, new code can be writing to the database values while the older code is still running

You may add a column to the db, new code will fill it in, old code will read the row, deserialize it into an object, update it and write back to the db - value of the new column that old code isn't aware of may be lost in the process

