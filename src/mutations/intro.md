# Atomic Mutations

Atomic Mutations is a standard for communicating state changes of [Atomic Data](../core/intro.md).
It is the part of Atomic Data that is concerned with writing, editing and updating.

_Disclaimer: This part of the draft spec lacks even more clarity than the others, and is constantly moving._

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
State synchronization is often an afterthought, and ... TODO!

Keeping track of where data comes from is essential to knowing whether you can trust it - whether you consider it to be true.
When you want to persist data, that quickly becomes bothersome.
Atomic Data and Atomic Mutations aim to make this easier by using cryptography for ensuring data comes from some particular source, and is therefore trustworthy.

## In short

- [Atomic Mutations](concepts.md) are small pieces of information that descibe how a Resource was changed. Think of these as Commits which are
- [Atomic Suggestions](concepts.md) are small pieces of information that suggest how a Resource should be changed.
