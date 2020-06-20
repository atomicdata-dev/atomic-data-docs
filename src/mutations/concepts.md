
# Atomic Mutations: Concepts

## Mutation

The smallest possible piece of a state change.
Comparable with an RDF Triple / Statement.
An Atom consists of a:

- `subject` - the Thing that the atom is providing information about. (must be a URI to an Atomic Thing)
- `predicate` - the property of the Thing that the atom is about. (must be a URI to an Atomic Property)
- `object` - the new piece of information about the Atom (can be any datatype, as long as its defined by the predicate)
- `method` - How the resource needs to be updated using the Atom. If empty, just replace the current state.
- `hash` - The hash of the updated state of the resource. If this does not match with your resource, the Mutation is faulty. The hash can be empty if it is sent in
- `date` - A timestamp of when the mutation was created.

## Ledger

A Ledger is an (append-only) log of Mutations.

TODO!

## Commit

A Commit is a set of Mutations, made by some Actor

TODO!

## Serialization / Parsing

Work in progress, see [HexTuples](https://github.com/ontola/hextuples) and [linked-delta](https://github.com/ontola/linked-delta).

## Streaming (pub/sub)

We're using HexTuples-NDJSON, since that allows for streaming parsing of mutations.

TODO! Something about endpoints / protocol for pub/sub.

## Base Methods

See [linked-delta](http://purl.org/linked-delta)
