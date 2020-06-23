# Atomic Suggestions

Atomic Suggestions is a proposed standard that enables decentralized collaboration on resources.
It's basically Git for linked data.
<!-- It describes how proposals for data changes -->

## Design goals

- **Asynchronous collaboration**: Various users can work on the same thing at the same time.
- **Branching & merging**: Issues that result from async changes (merge conflicts) can be resolved.

## Concepts

### Suggestion

<!-- Perhaps suggestions are too similar to Mutations, and should be merged into a single concept? -->

A Suggestion is a (set of?) Mutation(s?) that is proposed to be appended to some Ledger.
The important difference between a Suggestion and a Mutation, is that a Mutation has been verified, signed and approved by the Controller.

### Controller

The actor (person / organization) that is in control of a specific Resource and its mutations.

### Inbox

An Inbox represents an endpoint that accepts incoming Suggestions.
It's similar to an e-mail inbox.
