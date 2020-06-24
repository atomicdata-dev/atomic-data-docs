# Atomic Schema

Atomic Schema is the proposed standard for specifying classes, properties and datatypes in Atomic Data.
You can compare it to what XSD is for XML.
Atomic Schema deals with the

This section will define various Classes, Properties and Datatypes (discussed in [Atomic Core: Concepts](../core/concepts.md)).

## Design Goals

- **Typed**: Every Atom of data has a clear datatype.
- **IDE-friendly**: Every property has a simple short key representation (useful in text-based context) that maps to a URL that contains more information.
- **Self-documenting**: When seeing a piece of data, simply following links will explain you how the model is to be understood. This removes the need for (most of) existing API documentation.
- **Performant**: Datatypes can have a binary represenatation for optimal storage, communication, serialization and parsing efficiency.
- **Extensible**: Anybody can create their own Datatypes, Properties and Classes.
- **Accessible**: Support for languages, easily translateable. Useful for humans and machines.
- **Atomic**: All the design goals of Atomic Data itself also apply here.
- **Self-describing**: Atomic Schema is to be described as Atomic Data using Atomic Schema.
