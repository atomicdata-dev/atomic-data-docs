# Atomic Schema: Concepts

## Class

_uri: `https://atomicdata.dev/classes/Class`_

A Class is an abstract type of Resource, such as `Person`.
It is convention to use an Uppercase in its URI.
A Resource can have zero to many Classes, so this might be different from most data works.

Properties:

- `key` - (required, Slug)
- `description` - (required, langstring) human readable explanation of what the Class represents.
- `requiredProperties` - (optional, ResourceArray) a list of Properties that are required. If absent, none are required.
- `disallowedProperties` - (optional, ResourceArray) a list of Properties that are not allowed.  If absent, all are allowed.
- `allowedProperties` - (optional, ResourceArray) a list of Properties that are allowed. If absent, none are required.

Example:

```ndjson
["https://example.com/classes/Person","https://atomicdata.dev/properties/isA","Class"]
["https://example.com/classes/Person","https://atomicdata.dev/properties/datatype","https://atomicdata.dev/datatypes/datetime"]
```

## Property

_uri: `https://atomicdata.dev/classes/Class`_

A Property is an abstract type of Resource that describes the relation between a subject and an object.

Properties:

- `key` - (required, Slug) the shortname for the property, used in dot syntax. String with a-Z characters only. Case sensitive.
- `datatype` - (required, Datatype) a URI to an Atomic Datatype
- `description` - (required) the semantic meaning of the (langstring).

```turtle
<https://example.com/properties/createdAt> <https://atomicdata.dev/property/key> "createdAt".
<https://example.com/properties/createdAt> <https://atomicdata.dev/property/datatype> <https://atomicdata.dev/datatype/datetime>.
```

## Datatype

_uri: `https://atomicdata.dev/classes/Datatype`_

A Datatype specifies how the the property should be interpreted.

- `description` - (required, langstring) how the datatype functions.
- `stringSerialization` - (required, langstring) how the datatype should be parsed / serialized as an UTF-8 string
- `stringExample` - (required, string) an example stringSerialization example value that should be parsed correclty
- `binarySerialization` - (optional) how the datatype should be parsed / serialized as a byte array.
- `binaryExample` - (optional) an example stringSerialization that should be parsed correclty. Should have the same contents as the stringExample. Required if binarySerialization is present on the DataType.
