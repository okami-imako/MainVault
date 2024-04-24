---
tags:
  - encoding
---
[[XML]] is often being criticized for being to verbose and unnecessarily complicated.

[[JSON]]'s popularity is mainly due to its built-in support in web browsers (by virtue of being a subset of JavaScript) and simplicity relative to XML

[[CSV]] is another popular language-independent format, albeit less powerful

Good thing is all of them are textual, thus somewhat human-readable formats.

Though they also have subtle problems:
- Ambiguity. XML and CSV don't distinguish numbers and strings that happen to contain numbers. JSON doesn't distinguish integers and floats
- Lack of support for binary strings. Workarounds such as Base64 encoding have to be used in order to pass binary data, which increases the size of payload by ~33%
- Complicated schema formats
- CSV doesn't have any schema and is generally very vague format. What if value contains comma or a newline character? Escaping rules are formally defined, but not all parsers implement them correctly.

Despite these flaws, JSON, XML, and CSV are good enough for many purposes. It’s
likely that they will remain popular, especially as data interchange formats