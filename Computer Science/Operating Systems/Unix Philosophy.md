---
tags:
  - operating-system
  - unix
relates to:
  - "[[Unix]]"
---
1. Make each program do one thing well. To do a new job, build afresh rather than complicate old programs by adding new “features”.
2. Expect the output of every program to become the input to another, as yet unknown, program. Don’t clutter output with extraneous information. Avoid stringently columnar or binary input formats. Don’t insist on interactive input.
3. Design and build software, even operating systems, to be tried early, ideally within weeks. Don’t hesitate to throw away the clumsy parts and rebuild them.
4. Use tools in preference to unskilled help to lighten a programming task, even if you have to detour to build the tools and expect to throw some of them out after you’ve finished using them.

This approach - automation, rapid prototyping, incremental iteration, being friendly to experimentation, and breaking down large projects into manageable chunks - sounds remarkably like the [[Agile]] and [[DevOps]] movements of today. Surprisingly little has changed in four decades.

## Big Idea
You want to be able to connect ***any*** program's output to ***any*** program's input, that means that ***all*** programs must use the same input/output interface.