{{#title Atomic Data Extended specification}}
# Atomic Data Extended

Atomic Data is a _modular_ specification, which means that you can choose to implement parts of it.
All parts of Extended are _optional_ to implement.
The _Core_ of the specification (described in the previous chapter) is required for all of the Extended spec to work, but not the other way around.

However, many of the parts of Extended do rely on _eachother_.

- [Commits](commits/intro.md) communicate state changes. These Commits are signed using cryptographic keys, which ensures that every change can be audited. Commits are also used to construct a history of versions.
- [Agents](agents.md) are Users that enable [authentication](authentication.md).
- [Collections](schema/collections.md) add query options, filetering, sorting and pagination.
- [Paths](core/paths.md) allow you to traverse graphs.
- [Hierarchies](hierarchy.md) are used for authorization and keeping data organized.
- [Invites](invitations.md) can be used to easily create new users and provide them with rights.
- [WebSockets](websockets.md) allow for real-time updates.
- [Endpoints](endpoints.md) provide machine-readable descriptions of web services.
