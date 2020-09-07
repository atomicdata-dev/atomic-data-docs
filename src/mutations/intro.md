# Atomic Mutations

Atomic Mutations is a proposed standard for communicating state changes of [Atomic Data](../core/intro.md).
It is the part of Atomic Data that is concerned with writing, editing and updating.

_Disclaimer: This part of the draft spec is highly WIP._

## Design goals

- **Event sourced**: Store State changes, as well as the current state. This enables versioning, history playback, undo, audit controls, and more.
- **Traceable origin**: Every state change should be traceable to an actor and a point in time.
- **Verifiable**: Have cryptographic proof for every state change.
- **Decentralized**: Can be used in P2P networks to send mutations from device to device. See [CRDT](https://en.wikipedia.org/wiki/Conflict-free_replicated_data_type).
- **Extensible**: The methods are not fixed, and can be added by anyone.
- **Streamable**: The state changes could be used in streaming context, e.g. a client app that reads data that changes every second.
- **Pub/Sub**: Easy to subscribe to changes and get notified on changes.
- **Atomic**: All the Atomic Data design goals also apply here.

## Motivation

So many problems that confine data exchange are the result of thinking in current-state exchange.
State synchronization is often an afterthought, and ... TODO!

Keeping track of where data comes from is essential to knowing whether you can trust it - whether you consider it to be true.
When you want to persist data, that quickly becomes bothersome.
Atomic Data and Atomic Mutations aim to make this easier by using cryptography for ensuring data comes from some particular source, and is therefore trustworthy.

## In short

- [Atomic Mutations](concepts.md) describe how a Resource _was changed_.
- [Atomic Suggestions](concepts.md) suggest how a Resource _should be changed_.
