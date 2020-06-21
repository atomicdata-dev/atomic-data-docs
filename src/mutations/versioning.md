# Versioning

When Atomic Mutations are applied to some Resource, the resource will change.
However, its identifier (the Subject) will often remain the same.

- Versioned representations should provide a link to the authority that might update it, and a link to where the latest version can be found.
- The latest version should have a link to its permanent verison.
- Should [IPFS](../interoperability/ipfs.md) content-hash URLs be used for Versioned resources?

## Hashing

- Serialize all Atoms of the Subject (the entire Resource) as Atomic-NDJSON
- Sort all lines (every atom) alphabetically
