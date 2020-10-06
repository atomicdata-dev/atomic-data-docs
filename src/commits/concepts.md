# Atomic Commits: Concepts

## Commit

The smallest possible piece of a state change.
A Commit describes how an Resource should be updated.
The **required fields** are:

- `subject` - the Resource that the Commit is providing information about. (must be a URI to an Atomic Resource)
- `author` - The Atomic URL of the Actor's profile - which in turn should contain a `publicKey`.
- `signature` - A SHA-256 hash of the JSON-serialized Commit (without the `signature` field), signed by the `actor`'s `privateKey`. This proves that the author is indeed the one who created this exact commit. The signature of the Commit is also used as the identifier of the commit.
- `created_at` - A UNIX timestamp of when the commit was created.

The **optional method fields** describe how the data should be changed:

- `set` - a Nested Resource which contains all the new or edited fields.
- `remove` - an array of Properties that need to be removed (including their values).
- `destroy` - whether the Resource needs to be removed

### Serialization with JSON

Let's look at an example Commit:

```json
{
  "subject": "http://examle.com/someResource",
  "created_at": 1601239744,
  "author": "https://example.com/profile",
  "set": {
    "https://atomicdata.dev/properties/description": "my new resource description"
  },
  "remove": ["https://atomicdata.dev/properties/shortname"],
  "destroy": false,
  "signature": "24c7d4b3c1b6b5f924243d67dbfc33fb680b5d3e2a77614cebe03c4a2840d29a"
}
```

This Commit can be sent to any Atomic Server.
This server, in turn, should verify the signature and the author's rights before the server applies the Commit.

## Applying a commit

An example implementation can be viewed in [Atomic-Lib (WIP)](https://github.com/joepio/atomic/blob/e43cdd065dc813a1aecf409023fa40d66ab386f9/lib/src/storelike.rs#L74).

## Ledger

A Ledger is an (append-only) log of Commits.

- `Commits` (required, ResourceArray) - A list of all the Commits, from old to new.
