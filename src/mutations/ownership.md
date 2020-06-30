# Atomic Ownership

When data changes, we need a way of thinking about _who is able to change data_.
Of course, anybody can copy some piece of data and make changes to is, but for P2P data sharing to work, we also need to be able to _verify_ that the changes are _authentic_.
That's why Atomic Data has the _Ownership_ concept.

## Owner

The Owner of a Resource is the _authority_ of the content of the resource and its mutations.
It can be either a person or some more abstract entity, such as an organization or some hardware running somewhere.
You can think of an Owner as the one accepting Pull Requests in a Git repository.

The Owner identifies itself using a generated key-pair.
It signs authored Mutations with his private key, so others can verify the authenticity of the Mutations using the corresponding public key.

An owner SHOULD be explicitly referred to from every single Resource using the `owner` Property:

- `owner` (required, AtomicURL, Owner) - the Owner of the resource

## Using HTTP(S)

Any Atomic Resource has a Subject, and that Subject will be a URL.
Resolving that URL will link to the resource itself and show you the latest state.
HTTP URLs already show you who's in control, because the domain name points you there.

## Using IPFS

Since IPFS uses content-based addressing, the URL will always change when the content changes.
This means that we need some other system of showing where the

## Using DID

The DID (decentralized identifiers) paves the way for a more decentralized web.

TODO! Something with DID controllers https://w3c.github.io/did-core/#dfn-did-controllers

## Using Hypercore (DAT)

TODO!
