# Atomic Data: Concepts

The base URL for following concepts will be `https://atomicdata.dev/core/`.

## Atom

The smallest possible piece of _meaningful_ data / information.
The model of an Atom is comparable with an RDF Triple / Statement ([although there are imporant differences](../interoperability/rdf.md)).
An Atom consists of three values:

* [`subject`](#Subject) - the Thing that the atom is providing information about. (must be a URI to an Atomic Thing)
* [`predicate`](#Predicate) - the property of the Thing that the atom is about. (must be a URI to an Atomic Property)
* [`object`](#Object) - the new piece of information about the Atom (can be any datatype, as long as its defined by the predicate)

Let's turn this sentence into Atoms:

`Arnold, who's born on the 20th of Januari 1991, has a best friend named Britta.`

```atomic-ndjson
["https://example.com/arnold" "https://example.com/properties/bornAt" "1991-01-20"]
["https://example.com/arnold" "https://example.com/properties/firstName" "Arnold"]
["https://example.com/arnold" "https://example.com/properties/bestFriend" "https://example.com/britta"]
["https://example.com/britta" "https://example.com/properties/firstName" "Britta"]
```

## Resource

A Resource is a set of Atoms that share the same Subject URI.
Every thing is Resource, such as the person "Michael Jackson", or the abstract class "Person".
All the concepts on this page are Resources.
More specifically, they are Classes, which is a subclass of Resources.

## Subject

The Resource that the Atom is providing information about.
MUST be a URI to a Resource, which SHOULD resolve and return the Resource.

## Predicate

The predicate is a link that points to an Atomic Property. For example `https://example.com/createdAt` or `https://example.com/firstName`.
The predicate MUST be a URI, and that URI MUST resolve to an Atomic Property.

When Atomic Properties correctly resolve, that's when most of the benefits of Atomic Data become real: the static types and the

## Object

A set of Atoms that describe how an object should be updated.
