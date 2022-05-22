# Authentication in Atomic Data

Authentication means knowing _who_ is doing something, either getting access or creating some new data.
When an Agent wants to _edit_ a resource, they have to send a signed [Commit](commits/intro.md), and the signatures are checked in order to authorize a Commit.

But how do we deal with _reading_ data, how do we know who is trying to get access?
That's what this page will explain.
The short answer is: **By signing the HTTP request**.

## Design goals

- **Secure**: Because, what's the point of authentication if it's not?
- **Easy to use**: Setting up an identity should not require _any_ effort, and proving identity should be minimal effort.
- **Anonimity allowed**: Users should be able to have multiple identities, some of which are fully anonymous.
- **Self-sovereign**: No dependency on servers that user's don't control. Or at least, minimise this.
- **Dummy-proof**: We need a mechanism for dealing with forgetting passwords / client devices losing data.
- **Compatible with Commits**: Atomic Commits require clients to sign things. Ideally, this functionality / strategy would also fit with the new model.
- **Fast**: Of course, authentication will always slow things down. But let's keep that to a minimum.

Authentication is done by signing individual (HTTP) requests with the Agent's private key.

## HTTP Headers

All of the following headers are required, if you need authentication.

- `x-atomic-public-key`: The base64 public key (Ed25519) of the Agent sending the request
- `x-atomic-signature`: A base64 signature of the following string: `{subject} {timestamp}`
- `x-atomic-timestamp`: The current time (when sending the request) as milliseconds since unix epoch
- `x-atomic-agent`: The subject URL of the Agent sending the request.

## Sending a request

Here's an example (js) client side implementation with comments:

```ts
// The Private Key of the agent is used for signing
// https://atomicdata.dev/properties/privateKey
const privateKey = "someBase64Key";
const timestamp = Math.round(new Date().getTime());;
// This is what you will need to sign.
// The timestmap is to limit the harm of a man-in-the-middle attack.
// The `subject` is the full HTTP url that is to be fetched.
const message = `${subject} ${timestamp}`;
// Sign using Ed25519, see example implementation here: https://github.com/atomicdata-dev/atomic-data-browser/blob/30b2f8af59d25084de966301cb6bd1ed90c0eb78/lib/src/commit.ts#L176
const signed = await signToBase64(message, privateKey);
// Set all of these headers
const headers = new Headers;
headers.set('x-atomic-public-key', await agent.getPublicKey());
headers.set('x-atomic-signature', signed);
headers.set('x-atomic-timestamp', timestamp.toString());
headers.set('x-atomic-agent', agent?.subject);
const response = await fetch(subject, {headers});
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

## Hierarchies for authorization

Atomic Data uses [Hierarchies](hierarchy.md) to describe who gets to access some resource, and who can edit it.

## Limitations / considerations

- Since we need the Private Key to sign Commits and requests, the client should have this available. This means the client software as well as the user should deal with key management, and that can be a security risk in some contexts (such as a web browser). [See issue #49](https://github.com/ontola/atomic-data-docs/issues/49).
- When using the Agent's subject to authenticate somwehere, the authorizer must be able to check what the public key of the agent is. This means the agent must be publicly resolvable. This is one of the reasons we should work towards a server-independent identifier, probably as base64 string that contains the public key (and, optionally, also the https identifier). See [issue #59 on DIDs](https://github.com/ontola/atomic-data-docs/issues/59).
- Signing every single request takes a bit of time. We picked a fast algorithm (Ed25519) to minimize this cost.
- We'll probably introduce some form of token-based-authentication in the future. [See #87](https://github.com/ontola/atomic-data-docs/issues/87)
