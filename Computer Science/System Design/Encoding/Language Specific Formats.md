---
tags:
  - encoding
---
There are language specific encoding formats such as *java.io.Serializable*

They have a number of deep problems:
- The encoding is tied to a specific language, which you are committing yourself to.
- Attacker can send an arbitrary byte sequence, which you will decode into an arbitrary object, exposing yourself to a potential attack.
- In most such tools versioning is not supported. Good luck with Forward and Backward compatibility
- Efficiency is often an afterthought. Java's Serializable is known for horrible performance and bloated encoding