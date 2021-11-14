# Authentication in Atomic Data

Atomic Data uses [Hierarchies](hierarchy.md) to describe who gets to access some resource, and who can edit it.
When an Agent wants to _edit_ a resource, they have to send a signed [Commit](commits/intro.md).
But how do we deal with _reading_ data, how do we know who is trying to get access?

Authentication is done by signing individual (HTTP) requests with the Agent's private key.

## Sending a request

Here's an example (js) client side implementation with comments:

```ts
// The Private Key of the agent is used for signing
// https://atomicdata.dev/properties/publicKey
const privateKey = "someBase64Key";
// The current time as milliseconds since unix epoch
const timestamp = Math.round(new Date().getTime());;
// This is what you will need to sign.
// The timestmap is to limit the harm of a man-in-the-middle attack.
// The `subject` is the full HTTP url that is to be fetched.
const message = `${subject} ${timestamp}`;
// Sign using Ed25519
const signed = await signToBase64(message, privateKey);
// Set all of these headers
headers.set('x-atomic-public-key', await agent.getPublicKey());
headers.set('x-atomic-signature', signed);
headers.set('x-atomic-timestamp', timestamp.toString());
headers.set('x-atomic-agent', agent?.subject);
```

## Handling a request

- If none of the `x-atomic` HTTP headers are present, the server assigns the [PublicAgent](https://atomicdata.dev/agents/publicAgent) to the request. This Agent represents any guest who is not signed in.
- If some (but not all) of the `x-atomic` headers are present, the server will return with a `500`.
- The server must check the timestamp (max 10 seconds difference).
- The server must check whether the public key matches the one from the Agent.
- The server must check if the signature is valid.
- The server must check if the request resource can be shared

## Authentication for [websockets](websockets.md)

- Since there's only a single HTTP request, we don't have a subject to fetch. Use `ws` as a subject, so sign a string like `ws 12940791247`.
