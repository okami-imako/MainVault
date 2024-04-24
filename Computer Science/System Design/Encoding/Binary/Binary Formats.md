---
tags:
  - encoding
---

Once the data gets big enough it might be worth to switch to binary format

There are binary counterparts to JSON ([[MessagePack]], BSON, BJSON, UBJSON, BISON, and Smile, to name a few) and for XML (WBXML and Fast Infoset, for example)

There are problems with those though. As they don't have a schema, the binary representation has to contain stuff like field names. So the json
```json
{
	"userName": "Martin",
	"favoriteNumber": 1337,
	"interests": ["daydreaming", "hacking"]
}
```
will need to include the strings *userName*, *favoriteNumber*, and *interests* somewhere

Widely adopted binary formats include:
- [[Thrift and Protocol Buffers]]
- [[Avro]]

Key points about the Binary Formats:
- They can be much more compact than the various “binary JSON” variants, since they can omit field names from the encoded data.
- The schema is a valuable form of documentation, and because the schema is required for decoding, you can be sure that it is up to date (whereas manually maintained documentation may easily diverge from reality).
-  Keeping a database of schemas allows you to check forward and backward compatibility of schema changes, before anything is deployed.
- For users of statically typed programming languages, the ability to generate code from the schema is useful, since it enables type checking at compile time.