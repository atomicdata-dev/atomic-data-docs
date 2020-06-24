# Atomic Schema

Atomic Schema is the proposed standard for specifying classes, properties and datatypes in Atomic Data.
You can compare it to what XSD is for XML.
Atomic Schema deals with the

This section will define various Classes, Properties and Datatypes (discussed in [Atomic Core: Concepts](../core/concepts.md)).

## Design Goals

- **Typed**: Every Atom of data has a clear datatype.
- **IDE-friendly**: You should not have to type full URLs - the schema sets shornames.
- **Self-documenting**: When seeing a piece of data, simply following links will explain you how the model is to be understood. This removes the need for (most of) existing API documentation.
- **Performant**: Datatypes can have a binary represenatation for optimal storage, communication, serialization and parsing efficiency.
- **Extensible**: Anybody can create their own Datatypes, Properties and Classes.
- **Accessible**: Support for languages, easily translateable. Useful for humans and machines.
- **Atomic**: All the design goals of Atomic Data itself also apply here.
- **Self-describing**: Atomic Schema is to be described as Atomic Data using Atomic Schema.

## In short

In short, Atomic Schema works like this:

The **Property** _field_ in an Atom links to a Property _Resource_. It is important that the URL to the Property Resource resolves.
This Property does three things:

1. it tells something about its semantic meaning, and links to a Datatype.
1. it links to a Datatype or Class, which indicates which Value is acceptable.
1. it provides a Shortname, which is used for ORM.

**DataTypes** define the shape of the Value, e.g. a Number (`124`) or Boolean (`true`).

**Classes** are a special kind of Resource that describe an abstract class of things (such as "Person" or "Blog").
Classes can _recommend_ or _require_ a set of Properties.
They behave as Models, similar to `struts` in C or `interfaces` in Typescript.
A Resource _could_ have one or more classes, which _could_ provide information about which Properties are expected or required.
