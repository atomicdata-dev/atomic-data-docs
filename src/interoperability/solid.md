# Atomic Data and Solid

The Solid project is an initiative by the inventor of linked data and the world wide web: sir Tim Berners-Lee.
In many ways, it has similar goals to Atomic Data:

- Decentralize the web
- Make things more interoperable
- Give people more control over their data

Technically, both are also similar:

- Usage of linked data
- Usage of person-scoped servers (PODs: Personal Online Datastores)

One of the design goals of Atomic Data is to be serializable to RDF, which means that all the data that you define in Atomic Data can easily be put on your Solid Pod.
The other way around is more difficult, as Atomic Data has a far stricter built-in schema.

## Atomic Data has a built-in schema

Atomic Data is more strict than Solid - which means that it only accepts data that conforms to a specific shape.
In a Solid Pod, you're free to add any shape of data that you like - it is not _validated_ by some schema.
Yes, there are some efforts of using SHACL or SHEX to _constrain_ data before putting it in, but as of now it is not part of the spec or any implementation that I know of.
A lack of schema strictness can useful and quick, especially if you write data by hand, but it also limits how easy it is to build reliable apps with that data.
Atomic Data aims to be very friendly for developers that re-use data, and that's why we take a different approach: all data _must be_ validated by Atomic Schema before it's stored on a server.

You can think of Atomic Data more like a (dynamic) SQL database that offers guarantees about its content type, and a Solid Pod more like a document store that takes in all kinds of content.

## Atomic data uses event sourcing

Event sourcing means that all changes are stored (persisted) and used to calculate the current state of things.
In practice, this means that users get a couple of nice features for free:

- **Versioning for all items by default**. Storing events means that these events can be _replayed_, which means you get to traverse time / undo / redo.
- **Edit / audit log for everything**. Events contain information about who made which change at which point in time. Can be useful for finding out why things are the way they are.
- **Easier to add query options**. Any system can play-back the events, which means that it can be used as an API to add new query options / fill new indexes. This is especially useful if you want to add things like full-text search, or some geolocation index.

It also means that, compared to Solid, there is a relatively simple and strict API for changing data.
Atomic Data has a **uniform write API**.
All changes to data are done by posting Commits to the `/commits` endpoint of a Server.
This removes the need to think about differences between all sorts of HTTP methods like POST / PUT / PATCH, and how servers should reply to that.

## Solid is more mature

Atomic Data has significant gaps at this moment - not just in the implementations, but also in the spec.
This makes it not yet usable for most applications.
Here's a list of things missing in Atomic Data, with links to their open issues and links to their existing Solid counterpart.

- No way to restrict access to reading content. Only for writing content with Commits. [WAC](https://github.com/solid/web-access-control-spec) in Solid.
- [No hierarchy model](https://github.com/ontola/atomic-data/issues/18). [ShapeTrees in Solid](https://shapetrees.org/TR/specification/index.html#ecosystem)
- No way to discover content from user ID.
- No [inbox]() or [notifications](https://www.w3.org/TR/ldn/)
- No support from a big community, a well-funded business or the inventor of the world wide web.
