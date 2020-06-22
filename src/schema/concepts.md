# Atomic Schema: Concepts

In short, Atomic Schema works like this:

- The Predicate value in an Atom links to a Property. It is important that these resolve.
- This Property tells something about its semantic meaning, and links to a Datatype.
- The Datatype tells
- A Resource _could_ have one or more classes, which _could_ provide information about which Properties are expected or required.

## Property

_URL: `https://atomicdata.dev/classes/Class`_

A Property is an abstract type of Resource that describes the relation between a subject and an object.
A Property provides some semantic information about the relationship (in its `description`), it provides a shorthand (the `key`) and it links to a Datatype.

Properties:

- `key` - (required, Slug) the shortname for the property, used in dot syntax. String with a-Z characters only. Case sensitive.
- `description` - (optional, [Langstring](base.md#Langstring)) the semantic meaning of the.
- `datatype` - (required, Datatype) a URI to an Atomic Datatype, which defines what the datatype should be of the Object in an Atom where the Predicate is the
- `classtype` - (optional, Class) if the `datatype` is an Atomic URI, the `classtype` defines which class(es?) is (are?) acceptable.

```turtle
<https://example.com/properties/createdAt> <https://atomicdata.dev/property/key> "createdAt".
<https://example.com/properties/createdAt> <https://atomicdata.dev/property/datatype> <https://atomicdata.dev/datatype/datetime>.
```

## Datatype

_URL: `https://atomicdata.dev/classes/Datatype`_

A Datatype specifies how an `Object` value should be interpreted.

- `description` - (required, langstring) how the datatype functions.
- `stringSerialization` - (required, langstring) how the datatype should be parsed / serialized as an UTF-8 string
- `stringExample` - (required, string) an example stringSerialization example value that should be parsed correclty
- `binarySerialization` - (optional) how the datatype should be parsed / serialized as a byte array.
- `binaryExample` - (optional) an example stringSerialization that should be parsed correclty. Should have the same contents as the stringExample. Required if binarySerialization is present on the DataType.

## Class

_URL: `https://atomicdata.dev/classes/Class`_

A Class is an abstract type of Resource, such as `Person`.
It is convention to use an Uppercase in its URI.
A Resource can have zero to many Classes, so this might be different from most data works.

Properties:

- `key` - (required, Slug) a short string shorthand.
- `description` - (required, langstring) human readable explanation of what the Class represents.
- `requires` - (optional, ResourceArray) a list of Properties that are required. If absent, none are required.
- `recommends` - (optional, ResourceArray) a list of Properties that are recommended.
<!-- Maybe remove this next one? -->
<!-- - `disallowedProperties` - (optional, ResourceArray) a list of Properties that are not allowed.  If absent, all are allowed. -->
<!-- What are the consequences of this? How to deal with this field if there are more classes in a Subject? -->
<!-- - `allowedProperties` - (optional, ResourceArray) a list of Properties that are allowed. If absent, none are required. -->

Example:

```ndjson
["https://example.com/classes/Person","https://atomicdata.dev/properties/isA","Class"]
["https://example.com/classes/Person","https://atomicdata.dev/properties/datatype","https://atomicdata.dev/datatypes/datetime"]
```

Incoming Properties:

- `hasClass` - A property that any resource
