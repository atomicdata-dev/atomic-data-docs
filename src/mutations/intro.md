# Atomic Mutations

_Disclaimer: This part of the draft spec is highly WIP._

Atomic Mutations is a proposed standard for communicating state changes of [Atomic Data](../core/intro.md).
It is the part of Atomic Data that is concerned with writing, editing and updating.
You can think of it as Git for structured data.

## Design goals

- **Event sourced**: Store and standardize _changes_, as well as the _current_ state. This enables versioning, history playback, undo, audit logs, and more.
- **Traceable origin**: Every change should be traceable to an actor and a point in time.
- **Verifiable**: Have cryptographic proof for every change. Know _when_, and _what_ was changed by _whom_.
- **Identifiable**: A single mutation has an identifier - it is a resource.
- **Decentralized**: Can be used in P2P networks to send mutations from device to device.
- **Extensible**: The methods inside a mutation are not fixed, and can be added by anyone.
- **Streamable**: The mutations could be used in streaming context, e.g. a client app that reads data that changes every second.
- **Pub/Sub**: Easy to subscribe to changes and get notified on changes.
- **ACID-compliant**: An Atomic Mutation will only occur if it results in a valid state.
- **Atomic**: All the Atomic Data design goals also apply here.

## Motivation

Although it's a good idea to keep data at the source as much as possible, we'll often need to synchronize two systems.
For example when data has to be queried or indexed differently than its source can support.
Doing this synchronization can be very difficult, since most of our software is designed to only maintain and share the _current state_ of a system.

I noticed this mainly when working on OpenBesluitvorming.nl - an open data project where we aimed to fetch and standardize meeting data (votes, meeting minutes, documents) from 150+ local governments in the Netherlands.
We wrote software that fetched data from various systems (who all had different models, serialization formats and APIs), transformed this data to a single standard and share it through an API and a fulltext search endpoint.
One of the hard parts was keeping our data in sync with the sources.
How could we now if something was changed upstream?
We queried all these systems every night for _all meetings from the next and previous month_, and made deep comparisons to our own data.

This approach has a couple of issues:

- It costs a lot of resources, both for us and for the data suppliers.
- It's not real-time - we can only run this once every 24 ours (because of how costly it is).
- It's very prone to errors. We've had issues during all phases of Extraction, Transformation and Loading (ETL) processing.
- It causes privacy issues. When some data at the source is removed (because it contained faulty or privacy sensitive data), how do we learn about that?

Keeping track of where data comes from is essential to knowing whether you can trust it - whether you consider it to be true.
When you want to persist data, that quickly becomes bothersome.
Atomic Data and Atomic Mutations aim to make this easier by using cryptography for ensuring data comes from some particular source, and is therefore trustworthy.

## FAQ

### Is Atomic Mutations a Conflict-free Replicated Data Type (CRDT)?

Since Atomic Data always has a clear _owner_, all changes are coming from a single source or truth.
This prevents a lot of the issues that CRDT aims to solve, such as two people working on the same word at the same time in some text editor.

## In short

- [Atomic Mutations](concepts.md) describe how a Resource _was changed_.
- [Atomic Suggestions](concepts.md) suggest how a Resource _should be changed_.
