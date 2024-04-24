---
tags:
  - encoding/binary
---
Apache Thrift and Protocol Buffers (protobuf) are binary encoding libraries
that are based on the same principle. Protocol Buffers was originally developed at
Google, Thrift was originally developed at Facebook, and both were made open
source in 2007–08.

# Examples

Both Thrift and Protocol Buffers require a schema for any data that is encoded

```Thrift
struct Person {
	1: required string       userName,
	2: optional i64          favoriteNumber,
	3: optional list<string> interests
}
```

The equivalent schema definition for Protocol Buffers looks very similar:

```protobuf
message Person {
	required string user_name = 1;
	optional int64  favorite_number = 2;
	repeated string interests = 3;
}
```

Thrift and Protocol Buffers each come with a code generation tool that takes a schema definition like the ones shown here, and produces classes that implement the schema in various programming languages.

## Thrift

Thrift has two different binary encoding formats, called BinaryProtocol and CompactProtocol, respectively. Let’s look at BinaryProtocol first.

### BinaryProtocol

```json
{
	"userName": "Martin",
	"favoriteNumber": 1337,
	"interests": ["daydreaming", "hacking"]
}
```
Here is a result of encoding the above json using BinaryProtocol. The end result takes up **59 bytes**

![[ThriftBinaryProtocolExample.png]]

Key points:
- No field names - only field tags (1, 2, 3)

### CompactProtocol

The Thrift CompactProtocol encoding is semantically equivalent to BinaryProtocol,
but it packs the same information into only **34 bytes**

![[ThriftCompactProtocolExample.png]]

Key points:
- Packing field type and tag into a single byte
- Variable-length integers

## ProtocolBuffers 

Very similar to CompactProtocol. Fits the data into **33 bytes**

![[ProtocolBuffersExample.png]]

# Evolvability

Each field is identified by it's tag number and annotated with its datatype. Field's name isn't encoded so it doesn't matter and can be changed. Tag of the field is what really matters and has to be kept.

You can add new fields to the schema. Old code won't recognize new field and ignore it. This maintains *Forward Compatibility* - old code can read records written by new code

As long as each field has unique tag number, new code will be able to read the data written by old code. The only detail is that you cannot make it required - records written by the old code won't contain new field and that check would fail. Therefore, to maintain backward compatibility, every field you add after the initial deployment of the schema must be optional or have a default value.

Removing a field is just like adding a field, with backward and forward compatibility concerns reversed. That means you can only remove a field that is optional (a required field can never be removed), and you can never use the same tag number again (because you may still have data written somewhere that includes the old tag number, and that field must be ignored by new code).

## Datatypes

Datatypes can be changed, but there is a risk of lost of precision. 
If you change int32 to int64, new code will be able to read records produced by old code and pad them with zeroes. In the meantime the old code will have to truncate values produced by the new code.

In ProtoBuffers there is no list or array datatype. There is *repeated*, which brings a nice effect that it’s okay to change an *optional* (single-valued) field into a *repeated* (multi-valued) field. New code reading old data sees a list with zero or one elements (depending on whether the field was present); old code reading new data sees only the last element of the list.

Thrift has a dedicated list datatype, which is parameterized with the datatype of the
list elements. This does not allow the same evolution from single-valued to multi-
valued as Protocol Buffers does, but it has the advantage of supporting nested lists.