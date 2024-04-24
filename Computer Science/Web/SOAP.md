---
tags:
  - web
  - soap
---
By contrast, SOAP is an XML-based protocol for making network API requests. Although it is most commonly used over HTTP, it aims to be independent from HTTP and avoids using most HTTP features. Instead, it comes with a sprawling and complex multitude of related standards that add various features.

The API of a SOAP web service is described using an XML-based language called the *Web Services Description Language*, or *WSDL*. WSDL enables code generation so that a client can access a remote service using local classes and method calls (which are encoded to XML messages and decoded again by the framework).

- WSDL is not human-readable
- SOAP messages are too complex to construct manually
- users of SOAP heavily rely on tools, code generation and IDEs