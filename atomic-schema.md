# Atomic Schema

Atomic Schema is the standard for specifying classes, properties and datatypes in Atomic Data.
You can compare it to what XSD is for XML.
The most imporant concept in the Atomic Schema is the Property, which

## Design Goals

- **Typed**: Every Atom of data has a clear datatype.
- **IDE-friendly**: Every property has a simple short key representation (useful in text-based context) that maps to a URL that contains more information.
- **Human readable**: All datatypes should have a human-readable represenatation.
- **Performant**: Datatypes can have a binary represenatation for optimal storage, communication, serialization and parsing efficiency.
- **Extensible**: Anybody can create their own Datatypes, Properties and Classes.
- **Accessible**: Support for languages, easily translateable.
- **Atomic**: All the design goals of Atomic Data itself also apply here.

## Concepts

Whenever you see a key like `somevalue`, read: `https://atomicdata.dev/somevalue`.

### Class

A Class is an abstract type of resource, such as `Person`.

Consists of:

- `key` - (required)
- `description` - (required, langstring) human readable explanation of
- `requiredProperties` - (optional, ResourceArray) a list of Properties that are required. If absent, none are required.

### Property

A Property is an abstract type of relation between a subject and an object.
It specifies

- `key` - (required) the shortname for the property, used in dot syntax. String with no weird chars.
- `datatype` - (required) a URI to an Atomic Datatype
- `description` - (required) the semantic meaning of the (langstring).

```n-triples
<https://example.com/properties/createdAt> <https://atomicdata.dev/property/key> "createdAt"
<https://example.com/properties/createdAt> <https://atomicdata.dev/property/datatype> <https://atomicdata.dev/datatype/datetime>
```

### Datatype

_uri: `https://atomicdata.dev/Datatype`_

A Datatype specifies how the the property should be interpreted.

- `description` - (required, langstring) how the datatype functions.
- `stringSerialization` - (required, langstring) how the datatype should be parsed / serialized as an UTF-8 string
- `stringExample` - (required, string) an example stringSerialization example value that should be parsed correclty
- `binarySerialization` - (optional) how the datatype should be parsed / serialized as a byte array.
- `binaryExample` - (optional) an example stringSerialization that should be parsed correclty. Should have the same contents as the stringExample. Required if binarySerialization is present on the DataType.

## Base Datatypes

The Base Datatype Schema consists of some of the most used datatypes.
These can be extended by you, as everyone can create and link to their own Datatypes.
Note that systems that parse your data might support only a subset of Datatypes.

### Atomic URI

A URI that should resolve to an Atomic resource.

### URI

A Uniform Resource Identifier, preferably a URL.
Could be HTTPS, or any other type of schema.

### String

_uri: `https://atomicdata.dev/datatypes/string`_

UTF-8 String, no max character count.
Newlines use backslash escaped `\n` characters.
Should not contain language specific data, use a `langstring` instead.

e.g. `String time! \n Second line!`

### Multilingual String (langstring)

_uri: `https://atomicdata.dev/datatypes/langstring`_

<!--
So this is something I'm having serious doubts on.
It seems so verbose and hard to parse.
However, the underlying problem is kind of tough: we want <subject> <predicate> combination uniqueness...
... but we also want to have multilingual strings that can be added later.
-->

Array of special UTF-8 Strings.
Each element of the Array starts with a language string code, followed by a newline.

e.g. `["en-US\nHi there"],["nl-NL\nHallo daar"]`

### Integer

Signed Integer, max 64 bit.
Max value: [`9223372036854775807`](https://en.wikipedia.org/wiki/9,223,372,036,854,775,807)

e.g. `-420`

### Boolean

True or false, one or zero.

**String serialization**

`true` or `false`.

**Binary serialization**

Use a single bit one boolean.

1 for `true`, or 0 for `false`.

###  Datetime

ISO 8601 encoded string.

e.g. `2020-06-11`

### MIMEFile

Any type of file, starting with its [mime type](https://www.iana.org/assignments/media-types/media-types.xhtml)
Although MIME types [often don't exist in your OS](https://stackoverflow.com/a/29019569/2502163), specifying them seems like a good idea.

**String serialization**

Start with the mimetype string, do a newline `\n` and continue with the UTF-8 stringified data.

- e.g. `application/text\nOh hi mark`
- e.g. `text/html\n<html><p>oh, hi mark</p></html>`

**Binary serialization**


### ResourceArray

Sequential, ordered list of Atomic URIs.
Serialized as an
Note that other types of arrays are not included in this spec, but can be perfectly valid.

## FAQ

### How do I create a Property that supports multiple Datatypes?

A property only has one single Datatype.
However, feel free to create a new kind of Datatype that, in turn, refers to other Datatypes.
Perhaps this should be part of the Atomic Base Datatypes.
