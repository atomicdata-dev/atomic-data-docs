# Atomic Schema: Classes

In short, Atomic Schema works like this:

- The Property field in an Atom links to a Property Class. It is important that these resolve.
- This Property tells something about its semantic meaning, and links to a Datatype.
- The Datatype tells
- A Resource _could_ have one or more classes, which _could_ provide information about which Properties are expected or required.

## Property

_URL: `https://atomicdata.dev/classes/Class`_

The Property class.
The thing that the Property field should link to.
A Property is an abstract type of Resource that describes the relation between a Subject and a Value.
A Property provides some semantic information about the relationship (in its `description`), it provides a shorthand (the `shortname`) and it links to a Datatype.
Here's a [list of useful Properties](properties.md).

Properties of a Property instance:

- `shortname` - (required, Slug) the shortname for the property, used in ORM-style dot syntax (`thing.property.anotherproperty`).
- `description` - (optional, [Langstring](datatypes.md#Langstring)) the semantic meaning of the.
- `datatype` - (required, Datatype) a URI to an Atomic Datatype, which defines what the datatype should be of the Value in an Atom where the Property is the
- `classtype` - (optional, Class) if the `datatype` is an Atomic URI, the `classtype` defines which class(es?) is (are?) acceptable.

```ndjson
["https://example.com/properties/createdAt","https://atomicdata.dev/property/shortname","createdAt"]
["https://example.com/properties/createdAt","https://atomicdata.dev/property/datatype","https://atomicdata.dev/datatype/datetime"]
```

## Datatype

_URL: `https://atomicdata.dev/classes/Datatype`_

A Datatype specifies how a `Value` value should be interpreted.
Datatypes are concepts such as `boolean`, `string`, `integer`.
Since DatatTypes can be linked to, you dan define your own.
However, using non-standard datatypes limits how many applications will know what to do with the data.

Properties:

- `description` - (required, langstring) how the datatype functions.
- `stringSerialization` - (required, langstring) how the datatype should be parsed / serialized as an UTF-8 string
- `stringExample` - (required, string) an example stringSerialization example value that should be parsed correclty
- `binarySerialization` - (optional, langstring) how the datatype should be parsed / serialized as a byte array.
- `binaryExample` - (optional, string) an example stringSerialization that should be parsed correclty. Should have the same contents as the stringExample. Required if binarySerialization is present on the DataType.

## Class

_URL: `https://atomicdata.dev/classes/Class`_

A Class is an abstract type of Resource, such as `Person`.
It is convention to use an Uppercase in its URI.
Note that in Atomic Data, a Resource can have several Classes - not just a single one.

Properties:

- `shortname` - (required, Slug) a short string shorthand.
- `description` - (required, langstring) human readable explanation of what the Class represents.
- `requires` - (optional, ResourceArray) a list of Properties that are required. If absent, none are required. These SHOULD have unique shortnames.
- `recommends` - (optional, ResourceArray) a list of Properties that are recommended. These SHOULD have unique shortnames.
<!-- Maybe remove this next one? -->
<!-- - `disallowedProperties` - (optional, ResourceArray) a list of Properties that are not allowed.  If absent, all are allowed. -->
<!-- What are the consequences of this? How to deal with this field if there are more classes in aSSubject? -->
<!-- - `allowedProperties` - (optional, ResourceArray) a list of Properties that are allowed. If absent, none are required. -->

Example:

```ndjson
["https://example.com/classes/Person","https://atomicdata.dev/properties/isA","Class"]
["https://example.com/classes/Person","https://atomicdata.dev/properties/datatype","https://atomicdata.dev/datatypes/datetime"]
```

Incoming Properties:

- `class` - The Class of the Resource
