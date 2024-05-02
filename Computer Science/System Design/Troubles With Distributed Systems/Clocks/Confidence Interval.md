---
tags:
  - clock
relates to:
  - "[[Time-Of-Day Clocks]]"
---
Google's ***TrueTime*** API in *Spanner* reports the ***confidence interval of the local clock***

When you ask it for the current time, you get back `[earliest, latest]`, which are the ***earliest possible*** and the ***latest possible*** timestamp.

You can then confidently compare two timestamps:
- $A = [A_{earliest}, A_{latest}]$
- $B = [B_{earliest}, B_{latest}]$
If $A_{earliest} < A_{latest} < B_{earliest} < B_{latest}$ - then B definitely happened ***after*** A