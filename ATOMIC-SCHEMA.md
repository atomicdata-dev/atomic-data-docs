# Atomic Schema

Atomic Schema is the standard for specifying classes, properties and shapes in Atomic Data.

## Concepts

### Class

A Class is an abstract type of resource, such as `Person`.

Consists of:

- ``

### Property

A Property is an abstract type of

- `key` - the shortname for the property, used in dot syntax.
- `datatype` - a URI to an Atomic Datatype

### Datatype

A Datatype specifies how the the property should be interpreted.

- ``

## Base Datatypes

The Base Datatype Schema consists of some of the most used datatypes.
These can be extended.

### URI

A Uniform Resource Identifier, preferably a URL.
Could be HTTPS, or any other type of schema.

### String

UTF-8 String, no max character count.

### Integer

Signed Integer, max 64 bit.

### Boolean

True or false.

### Array

Sequential, ordered list of Resources.
