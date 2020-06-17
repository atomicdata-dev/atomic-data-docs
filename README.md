# Atomic data

A standard for data exchange.

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
- **Traceable origin**. Every state change should be traceable to an actor and a point in time.
- **Verifiable**. Have cryptographic proof for every state change.
- **Event sourced**. State changes are standardized just as the current state. This enables versioning, history playback, undo, audit controls...
- **Decentralized**. Can be used in P2P networks.
- **Open**. Free to use, open source, no strings attached.
- **Interoperable**. Can easily be converted to other formats (e.g. JSON, XML, all RDF formats).
- **Typed**. Every atom has a clear datatype. It can be mapped to programming langauge models, such as `structs` in Typescript / Rust / Go.
- **Extendible**. Atomic Data

## Concepts

### Atom

The smallest possible piece of meaningful data.
An Atom consists of a:

- `subject` - the Thing that the atom is providing information about. (must be a URI to an Atomic Thing)
- `predicate` - the property of the Thing that the atom is about. (must be a URI to an Atomic Property)
- `object` - the new piece of information about the Atom (can be any datatype, as long as its defined by the predicate)
- `method` - How the resource needs to be updated using the Atom. If empty, just replace the current state.
- `previous` - The hash of the previous state of the resource. If this does not match with your resource, the Mutation if faulty.
- `signature` - The hash of

### Mutation

A set of Atoms that describe how an object should be updated.

### Class

### Property

- `key`

### Serialization

Atomic data currently has a single serialization format: `atomic-ndjson`.
This is likely to expand in the future, especially

### Compatibility with...

#### JSON-LD
