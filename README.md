# Atomic data

A standard for data exchange.
It works nicely with Atomic-Schema (for defining and sharing models / shapes of data) and Atomic-Mutations (for sharing state changes).

_status: draft_

Names:

- Atomic data (related to Atomicity and data atoms), call the conversion process "atomize"

## Motivation

Linked data (RDF / the semantic web) enables us to use the web as a large, decentralized graph database.
However, it's been almost 20 years since the introduction of linked data, and its adoption has been slow.
We believe this lack of growth has to do with some problems that lie in the RDF data model.
STLD aims to take the best parts from RDF, and learn from the past to make a more developer-friendly, performant and reliable data model to achieve a truly linked web.

## Design goals

- **Browseable**. Every Atom of data should have a clear origin, so a single atom can be verified
- **ORM-friendly**. Navigate a decentralized graph by using dot.syntax, similar
- **Open**. Free to use, open source, no strings attached.
- **Interoperable**. Can easily be converted to other data formats (e.g. JSON, XML, and all RDF formats).
- **Typed**. Every atom has a clear datatype. It can be mapped to programming langauge models, such as `structs` in Typescript / Rust / Go.
- **Extendible**. Anyone can defined their own data types and create Atoms with it.

## Concepts

### Atom

The smallest possible piece of meaningful data.
Comparable with an RDF Triple / Statement ([read more about relation to RDF here](/RDF.md)).
An Atom consists of a:

- `subject` - the Thing that the atom is providing information about. (must be a URI to an Atomic Thing)
- `predicate` - the property of the Thing that the atom is about. (must be a URI to an Atomic Property)
- `object` - the new piece of information about the Atom (can be any datatype, as long as its defined by the predicate)

```n-triples
<https://example.com/arnold> <https://example.com/properties/bornAt> <https://>
```

### Resource

A resource is a set of Atoms where the subject has the same value.
It's a thing, such as a Person or an Issue.

### Subject

The Resource that the atom is providing information about.

- SHOULD be a URI to an Atomic Thing.

### Predicate

The predicate refers to some abstract Property.
For example `createdAt` or `firstName`.
The predicate MUST be a URI, and that URI SHOULD resolve to an Atomic Property.

### Object

A set of Atoms that describe how an object should be updated.

### Serialization

Atomic data currently has a single serialization format: `atomic-ndjson`.
This is likely to expand in the future, especially

### Compatibility with other data formats

Atomic data is designed to be highly interoperable.
It is possible to convert Atomic to many types of serialization formats.

- [RDF](/RDF.md)
- [JSON](/JSON.md)
