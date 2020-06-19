# Atomic Schema

Atomic Schema is the standard for specifying classes, properties and shapes in Atomic Data.

## Concepts

### Class

A Class is an abstract type of resource, such as `Person`.

Consists of:

* \`\`

### Property

A Property is an abstract type of

- `key` - the shortname for the property, used in dot syntax. String with no weird chars.
- `datatype` - a URI to an Atomic Datatype
- `description` - Long language string.

```n-triples
<https://example.com/properties/createdAt> <https://atomicdata.dev/property/key> "createdAt"
<https://example.com/properties/createdAt> <https://atomicdata.dev/property/datatype> <https://atomicdata.dev/datatype/sting>
```

### Datatype

A Datatype specifies how the the property should be interpreted.

- `description` - explains

## Base Datatypes

The Base Datatype Schema consists of some of the most used datatypes. These can be extended.

### Atomic URI

A URI that should resolve to an Atomic resource.

### URI

A Uniform Resource Identifier, preferably a URL. Could be HTTPS, or any other type of schema.

### String

UTF-8 String, no max character count.
Newlines use forward slash escaped `/n` characters.

e.g. `String time! /n Second line!`

### Language String

URF-8 String, that starts with a language code,followed by a colon

e.g. `en-US: Hi there`

### Integer

Signed Integer, max 64 bit.

e.g. `-420`

### Boolean

True or false.

e.g. `1`

### Array

Sequential, ordered list of Resources.
