# Atomic Schema

Atomic Schema is the proposed standard for specifying classes, properties and datatypes in Atomic Data.
You can compare it to what XSD is for XML.

This section will define various Classes, Properties and Datatypes (discussed in [Atomic Core: Concepts](../core/concepts.md)).
<!-- Making this a requirement is what makes Atomic Data typed and semantic -->
Some of these Classes, Properties and Datatypes are _optional_ to use, but

## Design Goals

- **Typed**: Every Atom of data has a clear datatype.
- **IDE-friendly**: Every property has a simple short key representation (useful in text-based context) that maps to a URL that contains more information.
- **Human readable**: All Datatypes should have a human-readable represenatation.
- **Performant**: Datatypes can have a binary represenatation for optimal storage, communication, serialization and parsing efficiency.
- **Extensible**: Anybody can create their own Datatypes, Properties and Classes.
- **Accessible**: Support for languages, easily translateable.
- **Atomic**: All the design goals of Atomic Data itself also apply here.
- **Self-describing**: Atomic Schema is to be described as Atomic Data using Atomic Schema.
