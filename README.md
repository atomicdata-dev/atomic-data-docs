# Atomic data

A standard for data exchange. It works nicely with [Atomic-Schema](atomic-schema.md) \(for defining and sharing models / shapes of data\) and [Atomic-Mutations](atomic-mutations.md) \(for sharing state changes\).

_status: draft_

Names:

* Atomic data \(related to Atomicity and data atoms\), call the conversion process "atomize"

## Motivation

Linked data \(RDF / the semantic web\) enables us to use the web as a large, decentralized graph database. However, it's been almost 20 years since the introduction of linked data, and its adoption has been slow. We believe this lack of growth has to do with [some problems that lie in the RDF data model](rdf.md). Atomic Data aims to take the best parts from RDF, and learn from the past to make a more developer-friendly, performant and reliable data model to achieve a truly linked web.

## Design goals

* **Typed**. Every Atom has a clear datatype. It can be mapped to programming langauge models, such as `structs` in Typescript / Rust / Go.
* **Browseable**. Data should explicitly link to other pieces of data, and these links should be followable.
* **ORM-friendly**. Navigate a _decentralized_ graph by using dot.syntax, similar to how you navigate a JSON object in javascript.
* **Open**. Free to use, open source, no strings attached.
* **Interoperable**. Can easily \(and consitently\) be converted to other data formats \(e.g. JSON, XML, and all RDF formats\).
* **Extendible**. Anyone can defined their own data types and create Atoms with it.

## Concepts

### Atom

The smallest possible piece of meaningful data. Comparable with an RDF Triple / Statement \([read more about relation to RDF here](rdf.md)\). An Atom consists of a:

* `subject` - the Thing that the atom is providing information about. \(must be a URI to an Atomic Thing\)
* `predicate` - the property of the Thing that the atom is about. \(must be a URI to an Atomic Property\)
* `object` - the new piece of information about the Atom \(can be any datatype, as long as its defined by the predicate\)

```text
<https://example.com/arnold> <https://example.com/properties/bornAt> <https://example.com/properties/bornAt>
```

### Resource

A resource is a set of Atoms where the subject has the same value. It's a thing, such as a Person or an Issue.

### Subject

The Resource that the atom is providing information about.

* SHOULD be a URI to an Atomic Thing.

### Predicate

The predicate is a link that points to an Atomic Property. For example `https://example.com/createdAt` or `https://example.com/firstName`. The predicate MUST be a URI, and that URI SHOULD resolve to an Atomic Property.

When Atomic Properties correctly resolve, that's when most of the benefits of Atomic Data become real: the static types and the

### Object

A set of Atoms that describe how an object should be updated.

### Serialization

For the time being, existing RDF serialization formats can be used, such as N-Triples, Turtle or JSON-LD. In the future, new \(more constrained and optimized\) serialization formats will be introduced.

### Compatibility with other data formats

Atomic data is designed to be highly interoperable. It is possible to convert Atomic to many types of serialization formats.

* [RDF](rdf.md): some RDF can be automatically converted into valid Atomic data.
* [JSON](json.md): JSON requires a mapping to Atomic Properties, and explicit

