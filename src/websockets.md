{{#title Atomic Data Websockets - live synchronization}}
# WebSockets in Atomic Data

WebSockets are a very fast and efficient way to have a client and server communicate in an asynchronous fashion.
They are used in Atomic Data to allow real-time updates, which makes it possible to create things like collaborative applications and multiplayer games.
These have been implemented in `atomic-server` and `atomic-data-browser` (powered by `@tomic/lib`).

## Initializing a WebSocket connection

Send an HTTP `GET` request to the `/ws` endpoint of an `atomic-server`. The Server should update that request to a secure WebSocket (`wss`) connection.
Use `x-atomic` [authentication headers (read more here)](./authentication.md) and use `ws` as a subject when signing.

## Client to server messages

- `SUBSCRIBE ${subject}` tells the Server that you'd like to receive Commits about this Subject.
- `UNSUBSCRIBE ${subject}` tells the Server that you'd like to stop receiving Commits about this Subject.
- `GET ${subject}` fetch an individual resource.

## Server to client messages

- `COMMIT ${CommitBody}` an entire Commit for a resource that you're subscribed to
- `RESOURCE ${CommitBody}` a resource as a response to a GET request.

## Example implementations

- [Example client implementation in Typescript (@tomic/lib).](https://github.com/atomicdata-dev/atomic-data-browser/blob/main/lib/src/websockets.ts)
- [Example server implementation in Rust using Actix-Web](https://github.com/joepio/atomic-data-rust/blob/master/server/src/handlers/web_sockets.rs)
