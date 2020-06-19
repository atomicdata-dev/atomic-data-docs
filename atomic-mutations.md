# Atomic Mutations

Atomic Mutations is a standard for communicating state changes of [Atomic Data](/README.md).

## Design goals

- **Event sourced**: State changes are standardized just as the current state. This enables versioning, history playback, undo, audit controls...
- **Traceable origin**: Every state change should be traceable to an actor and a point in time.
- **Verifiable**: Have cryptographic proof for every state change.
- **Decentralized**: Can be used in P2P networks to send mutations from device to device.
- **Extendible**: The methods are not fixed, and can be added by anyone.
- **Streamable**: The state changes could be used in streaming context, e.g. a client app that reads data that changes every second.
- **Atomic**: All the Atomic Data design goals also apply here.

## Motivation

So many problems that confine data exchange are the result of thinking in current-state exchange.
State synchronization is often an afterthought, and that

## Concepts

### Mutation

The smallest possible piece of a state change.
Comparable with an RDF Triple / Statement.
An Atom consists of a:

- `subject` - the Thing that the atom is providing information about. (must be a URI to an Atomic Thing)
- `predicate` - the property of the Thing that the atom is about. (must be a URI to an Atomic Property)
- `object` - the new piece of information about the Atom (can be any datatype, as long as its defined by the predicate)
- `method` - How the resource needs to be updated using the Atom. If empty, just replace the current state.
- `hash` - The hash of the updated state of the resource. If this does not match with your resource, the Mutation is faulty. The hash can be empty if it is sent in
- `date` - A timestamp of when the mutation was created.

### Serialization

Work in progress, see [HexTuples](https://github.com/ontola/hextuples) and [linked-delta](https://github.com/ontola/linked-delta)

### Base Methods

See [linked-delta](http://purl.org/linked-delta)
