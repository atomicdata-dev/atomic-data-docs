# Atomic Commits: Concepts

## Commit

A Commit describes how a Resource must be updated.
The **required fields** are:

- `subject` - The thing being changed. A Resource Subject URL that the Commit is providing information about.
- `author` - Who's making the change. The Atomic URL of the Author's profile - which in turn must contain a `publicKey`.
- `signature` - Cryptographic proof of the change. A hash of the JSON-serialized Commit (without the `signature` field), signed by the `actor`'s `privateKey`. This proves that the author is indeed the one who created this exact commit. The signature of the Commit is also used as the identifier of the commit.
- `createdAt` - When the change was made. A UNIX timestamp number of when the commit was created.

The **optional method fields** describe how the data must be changed:

- `destroy` - If true, the existing Resource will be removed.
- `remove` - an array of Properties that need to be removed (including their values).
- `set` - a Nested Resource which contains all the new or edited fields.

These commands are executed in the order above.
This means that you can set `destroy` to `true` and include `set`, which empties the existing resource and sets new values.

### Posting commits using HTTP

Since Commits contains cryptographic proof of authorship, they can be accepted at a public endpoint.
There is no need for authentication.

A commit should be sent (using an HTTPS POST request) to a `/commmit` endpoint of an Atomic Server.
The server then checks the signature and the author rights, and responds with a `2xx` status code if it succeeded, or an `5xx` error if something went wrong.
The error will be a JSON object.

### Serialization with JSON

Let's look at an example Commit:

```json
{
  "subject": "http://examle.com/someResource",
  "createdAt": 1601239744,
  "author": "https://example.com/profile",
  "set": {
    "https://atomicdata.dev/properties/description": "my new resource description"
  },
  "remove": ["https://atomicdata.dev/properties/shortname"],
  "signature": "24c7d4b3c1b6b5f924243d67dbfc33fb680b5d3e2a77614cebe03c4a2840d29a"
}
```

This Commit can be sent to any Atomic Server.
This server, in turn, should verify the signature and the author's rights before the server applies the Commit.

### Calculating the signature

The signature is a base64 encoded Ed25519 signature of the deterministically serialized Commit.
Calculating the signature is a delicate process that should be followed to the letter - even a single character in the wrong place will result in an incorrect signature, which makes the Commit invalid.

The first step is **serializing the commit deterministically**.
This means that the process will always end in the exact same string.

- Serialize the Commit as JSON.
- Do not serialize the signature field.
- Do not include empty objects or arrays.
- If `destroy` is false, do not include it.
- All keys are sorted alphabetically - both in the root object, as in any nested objects.
- The JSON is minified: no newlines, no spaces.

[Here's an example implementation of this process written in Rust](https://github.com/joepio/atomic/blob/ceb88c1ae58811f2a9e6bacb7eaa39a2a7aa1513/lib/src/commit.rs#L81).

This will result in a string.
The next step is to sign this string using the Ed25519 private key.
This signature is a byte array, which should be encoded in base64.
Make sure that the Author's URL resolves to a Resource that contains the linked public key.

Congratulations, you've just created a valid Commit!

## Author

An Author is a person, organization, computer or other type of agent that can create and sign Commits.
The most important property of the Author is the
