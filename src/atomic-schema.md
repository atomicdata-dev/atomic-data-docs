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
- **Self-describing**: Atomic Schema is to be described with Atomic Schema.

## FAQ

### How do I create a Property that supports multiple Datatypes?

A property only has one single Datatype.
However, feel free to create a new kind of Datatype that, in turn, refers to other Datatypes.
Perhaps this should be part of the Atomic Base Datatypes.

### How should a client deal with dot syntax key collisions.

TODO!

###
