# Atomic Mutations: Concepts

## Mutation

The smallest possible piece of a state change.
A mutation describes how an Resource should be updated.
Mutations are very similar to Atoms, but they contain more information.
An Atomic Mutation consists of a:

- `subject` - the Thing that the atom is providing information about. (must be a URI to an Atomic Thing)
- `property` - the property of the Thing that the atom is about. (must be a URI to an Atomic Property)
- `value` - the new piece of information about the Atom (can be any datatype, as long as its defined by the property)
- `method` - How the resource needs to be updated using the Atom. If empty, just replace the current state.
- `hash` - The [IPFS URL](versioning.md#Hashing) of the updated version of the resource. If this does not match with your resource, the Mutation is faulty. The hash can be empty if it is sent in
- `date` - A timestamp of when the mutation was created.
- `actor` - A timestamp of when the mutation was created.

## Ledger

A Ledger is an (append-only) log of Mutations.

- `mutations` (required, ResourceArray) - A list of all the mutations, from old to new.

## Commit

A Commit is a set of Mutations, made by some Actor

TODO!

## Serialization with AtomicMutations-ndjson

Although Mutations can be communicated with

Work in progress, see [linked-delta](https://github.com/ontola/linked-delta).

```ndjson
["https://example.com/john", "https://example.com/properties/lastName", "Mc'Lovin", "https://purl.org/linked-delta/add", "AEF1245612F3"]
```

## Streaming (pub/sub)

We're using HexTuples-NDJSON, since that allows for streaming parsing of mutations.

TODO! Something about endpoints / protocol for pub/sub.

## Base Methods

See [linked-delta](http://purl.org/linked-delta)
