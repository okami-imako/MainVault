---
tags:
  - encoding/binary
---

Apache Avro is another binary encoding format that is interestingly different from Protocol Buffers and Thrift. It was started in 2009 as a subproject of Hadoop, as a result of Thrift not being a good fit for Hadoop’s use cases .

Avro also uses a schema to specify the structure of the data being encoded. It has two schema languages: one (Avro IDL) intended for human editing, and one (based on JSON) that is more easily machine-readable.

```avro
record Person {
	string               userName;
	union { null, long } favoriteNumber = null;
	array<string>        interests;
}
```

The equivalent JSON representation of that schema is as follows:

```json
{
	"type": "record",
	"name": "Person",
	"fields": [
		{"name": "userName", "type": "string"},
		{
			"name": "favoriteNumber",
			"type": ["null", "long"],
			"default": null
		},
		{
			"name": "interests",
			"type": {"type": "array", "items": "string"}
		}
	]
}
```

# Example

```json
{
	"userName": "Martin",
	"favoriteNumber": 1337,
	"interests": ["daydreaming", "hacking"]
}
```

Here is the result of encoding the above json:

![[AvroExample.png]]

Key Points:
- There is nothing to identify the fields or their datatypes - no tags, no names
- To parse the data you go through it with and look at the schema

# Evolvability

Writer writes using the *writer's schema*
Reader reads the data using the *reader's schema*

The key idea with Avro is that the writer’s schema and the reader’s schema don’t have to be the same - they only need to be compatible.

Avro library resolves the differences by looking at the writer’s schema and the reader’s schema side by side and translating the data from the writer’s schema into the reader’s schema.

![[AvroTranslation.png]]

With Avro, forward compatibility means that you can have a new version of the schema as writer and an old version of the schema as reader. Conversely, backward compatibility means that you can have a new version of the schema as reader and an old version as writer.

To maintain compatibility, you may only add or remove a field that has a default value. If you were to add a field that has no default value, new readers wouldn’t be able to read data written by old writers, so you would break backward compatibility. If you were to remove a field that has no default value, old readers wouldn’t be able to read data written by new writers, so you would break forward compatibility.

If you want to allow a field to be null, you have to use a union type. For example, `union { null, long, string } field;` indicates that field can be a number, or a string, or null.

Changing the datatype of a field is possible, provided that Avro can convert the type. Changing the name of a field is possible but a little tricky: the reader’s schema can contain aliases for field names, so it can match an old writer’s schema field names against the aliases. This means that changing a field name is backward compatible but not forward compatible. Similarly, adding a branch to a union type is backward compatible but not forward compatible.

