# Atomic Data

_status: early draft, far from usable_

A standard for data exchange that enables decentralized, typed graphs.
Inspired by linked data, but more constrained (and easier to use) than RDF.

It consists of three parts:

- [Atomic Data](readme.md): typed, linked data
- [Atomic Schema](atomic-schema.md): defining and sharing models / shapes of data
- [Atomic Mutations](atomic-mutations.md): sharing state changes

## Design goals

* **Typed**. All Atomic data has an unambiguous, static datatype. Models expressed in Atomic Data can be mapped to programming langauge models, such as `structs` or `interfaces` in Typescript / Rust / Go.
* **Semantic**. Every data Atom and relation has a clear semantic meaning.
* **Browseable**. Data should explicitly link to other pieces of data, and these links should be followable.
* **ORM-friendly**. Navigate a _decentralized_ graph by using dot.syntax, similar to how you navigate a JSON object in javascript.
* **Open**. Free to use, open source, no strings attached.
* **Interoperable**. Can easily and consitently be converted to other data formats (e.g. JSON, XML, and all RDF formats).
* **Clear Ownership**. The URI of the data shows who is in control of the data
* **Extensible**. Anyone can define their own data types and create Atoms with it.
* **Mergeable**. Any two sets of Atoms can be merged into a sinlge graph without any merge conflicts / name collissions.

## Motivation

Linked data (RDF / the semantic web) enables us to use the web as a large, decentralized graph database.
However, it's been almost 20 years since the introduction of linked data, and its adoption has been slow.
We believe this lack of growth has to do with [some problems that lie in the RDF data model](rdf.md#Why-these-changes).
Atomic Data aims to take the best parts from RDF, and learn from the past to make a more developer-friendly, performant and reliable data model to achieve a truly linked web.

## Concepts

The base URL for following concepts will be `https://atomicdata.dev/core/`.

### Atom

The smallest possible piece of meaningful data / information.
The model of an Atom is comparable with an RDF Triple / Statement ([although there are imporant differences](rdf.md)).
An Atom consists of a:

* `subject` - the Thing that the atom is providing information about. (must be a URI to an Atomic Thing)
* `predicate` - the property of the Thing that the atom is about. (must be a URI to an Atomic Property)
* `object` - the new piece of information about the Atom (can be any datatype, as long as its defined by the predicate)

```n-triples
<https://example.com/arnold> <https://example.com/properties/bornAt> "1991-01-20".
<https://example.com/arnold> <https://example.com/properties/firstName> "Arnold".
<https://example.com/arnold> <https://example.com/properties/bestFriend> <https://example.com/britta>.
```

### Resource

A Resource is a set of Atoms where the subject has the same value.
It's a thing, such as a Person or an Issue.

### Subject

The Resource that the Atom is providing information about.
MUST be a URI to a Resource, which SHOULD resolve and return the Resource.

### Predicate

The predicate is a link that points to an Atomic Property. For example `https://example.com/createdAt` or `https://example.com/firstName`.
The predicate MUST be a URI, and that URI MUST resolve to an Atomic Property.

When Atomic Properties correctly resolve, that's when most of the benefits of Atomic Data become real: the static types and the

### Object

A set of Atoms that describe how an object should be updated.

### Serialization

For the time being, existing RDF serialization formats can be used, such as N-Triples, Turtle, HexTuples or JSON-LD.
In the future, new (more constrained and optimized) serialization formats will be introduced.

### Compatibility with other data formats

Atomic data is designed to be highly interoperable. It is possible to convert Atomic to many types of serialization formats.

* [RDF](rdf.md): some RDF can be automatically converted into valid Atomic data.
* [JSON](json.md): JSON requires a mapping to Atomic Properties, and explicit
