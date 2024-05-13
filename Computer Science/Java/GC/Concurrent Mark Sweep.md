---
tags:
  - java
  - gc
---
# Heap Structure

![[Pasted image 20240509154835.png]]

# Young GC

![[Pasted image 20240509154944.png]]

Live objects are copied from the Eden space and survivor space to the other survivor space. Any older objects that have reached their aging threshold are promoted to old generation.

![[Pasted image 20240509155140.png]]

After a young GC, the Eden space is cleared and one of the survivor spaces is cleared.

![[Pasted image 20240509155100.png]]

# Old GC
Two [[Stop The World]] events take place: initial mark and remark. When the old generation reaches a certain occupancy rate, the CMS is kicked off.

![[Pasted image 20240509155236.png]]

(1) Initial mark is a short pause phase where live (reachable) objects are marked. (2) Concurrent marking finds live objects while the application continues to execute. Finally, in the (3) remark phase, objects are found that were missed during (2) concurrent marking in the previous phase.

> **Note:** Unmarked objects == Dead Objects

After the (4) Sweeping phase, you can see that a lot of memory has been freed up. You will also notice that no compaction has been done.

![[Pasted image 20240509155337.png]]

Finally, the CMS collector will move through the (5) resetting phase and wait for the next time the GC threshold is reached.