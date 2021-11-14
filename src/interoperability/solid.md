{{#title How does Atomic Data relate to Solid?}}
# Atomic Data and Solid

The [Solid project](https://solidproject.org/) is an initiative by the inventor of linked data and the world wide web: sir Tim Berners-Lee.
In many ways, it has **similar goals** to Atomic Data:

- Decentralize the web
- Make things more interoperable
- Give people more control over their data

Technically, both are also similar:

- Usage of personal servers, or PODs (Personal Online Datastores). Both Atomic Data and Solid aim to provide users with a highly personal server where all sorts of data can be stored.
- Usage of **linked data**. All Atomic Data is valid RDF, which means that **all Atomic Data is compatible with Solid**. However, the other way around is more difficult. In other words, if you choose to use Atomic Data, you can always put it in your Solid Pod.

But there are some important **differences**, too, which will be explained in more detail below.

- Atomic Data uses a strict built-in schema to ensure type safety.
- Atomic Data standardizes state changes (which also provides version control / history, audit trails)
- Atomic Data is more easily serializable to other formats (like JSON)
- Atomic Data has a different model for Authorzation and Hierarchies
- Atomic Data is less mature, and currently lacks things like authentication for read Access

_Disclaimer: I've been quite involved in the development of Solid, and have a lot of respect for all the people who are working on it.
The following is not meant as a critique on Solid, let alone the individuals working on it._

## Atomic Data is type-safe, because of its built-in schema

Atomic Data is more strict than Solid - which means that it only accepts data that conforms to a specific shape.
In a Solid Pod, you're free to add any shape of data that you like - it is not _validated_ by some schema.
Yes, there are some efforts of using SHACL or SHEX to _constrain_ data before putting it in, but as of now it is not part of the spec or any implementation that I know of.
A lack of schema strictness can be helpful during prototyping and rapid development, especially if you write data by hand, but it also limits how easy it is to build reliable apps with that data.
Atomic Data aims to be very friendly for developers that re-use data, and that's why we take a different approach: all data _must be_ validated by Atomic Schema before it's stored on a server.
This means that all Atomic Properties will have to exist on a publicly accessible URL, before the property can be used somewhere.

You can think of Atomic Data more like a (dynamic) SQL database that offers guarantees about its content type, and a Solid Pod more like a document store that takes in all kinds of content.
Most of the differences have to do with how Atomic Schema aims to make linked data easier to work with, but that is covered in the previous [RDF chapter](./rdf.md).

## Atomic Data standardizes state changes (event sourcing)

With Solid, you change a Resource by sending a POST request to the URL that you want to change.
With Atomic, you change a Resource by sending a signed Commit that contains the requested changes to a Server.

Event sourcing means that all changes are stored (persisted) and used to calculate the current state of things.
In practice, this means that users get a couple of nice features for free:

- **Versioning for all items by default**. Storing events means that these events can be _replayed_, which means you get to traverse time / undo / redo.
- **Edit / audit log for everything**. Events contain information about who made which change at which point in time. Can be useful for finding out why things are the way they are.
- **Easier to add query options / indexes**. Any system can play-back the events, which means that the events can be used as an API to add new query options / fill new indexes. This is especially useful if you want to add things like full-text search, or some geolocation index.

It also means that, compared to Solid, there is a relatively simple and strict API for changing data.
Atomic Data has a **uniform write API**.
All changes to data are done by posting Commits to the `/commits` endpoint of a Server.
This removes the need to think about differences between all sorts of HTTP methods like POST / PUT / PATCH, and how servers should reply to that.

## Atomic Data is more easily serializable to other formats (like JSON)

Atomic Data is designed with the modern developer in mind.
One of the things that developers expect, is to be able to traverse (JSON) objects easily.
Doing this with RDF is not easily possible, because doing this requires _subject-predicate uniqueness_.
Atomic Data does not have this problem (properties _must_ be unique), which means that traversing objects becomes easy.

Another problem that Atomic Data solves, is dealing with long URLs as property keys.
Atomic Data uses `shortnames` to map properties to short, human-readable strings.

For more information about these differences, see the previous [RDF chapter](./rdf.md).

## Hierarchy model, authorization, authentication

Atomic Data identities (Agents) are a combination of HTTP based, and cryptography (public / private key) based.
In Atomic, all actions (from GET requests to Commits) are signed using the private key of the Agent.
This makes Atomic Data a bit more unconventional, but also makes its auth mechanism very decentralized and lightweight.

Solid uses HTTP based WebID identifiers combined with an OIDC flow.

Atomic Data uses `parent-child` [hierarchies](../hierarchy.md) to model data and performan authorization checks.
This closely resembles how filesystems work, and is therefore familiar to most users.

## Solid is more mature

Atomic Data has significant gaps at this moment - not just in the implementations, but also in the spec.
This makes it not yet usable for most applications.
Here's a list of things missing in Atomic Data, with links to their open issues and links to their existing Solid counterpart.

- No inbox or [notifications](https://www.w3.org/TR/ldn/) ([issue](https://github.com/ontola/atomic-data/issues/28))
- No support from a big community, a well-funded business or the inventor of the world wide web.
