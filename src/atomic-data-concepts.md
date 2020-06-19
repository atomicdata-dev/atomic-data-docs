# Atomic Data: Concepts

The base URL for following concepts will be `https://atomicdata.dev/core/`.

## Atom

The smallest possible piece of meaningful data / information.
The model of an Atom is comparable with an RDF Triple / Statement ([although there are imporant differences](rdf.md)).
An Atom consists of a:

* `subject` - the Thing that the atom is providing information about. (must be a URI to an Atomic Thing)
* `predicate` - the property of the Thing that the atom is about. (must be a URI to an Atomic Property)
* `object` - the new piece of information about the Atom (can be any datatype, as long as its defined by the predicate)

```n-triples
<https://example.com/arnold> <https://example.com/properties/bornAt> "1991-01-20".
<https://example.com/arnold> <https://example.com/properties/firstName> "Arnold".
<https://example.com/arnold> <https://example.com/properties/bestFriend> <https://example.com/britta>.
```

## Resource

A Resource is a set of Atoms where the subject has the same value.
It's a thing, such as a Person or an Issue.

## Subject

The Resource that the Atom is providing information about.
MUST be a URI to a Resource, which SHOULD resolve and return the Resource.

## Predicate

The predicate is a link that points to an Atomic Property. For example `https://example.com/createdAt` or `https://example.com/firstName`.
The predicate MUST be a URI, and that URI MUST resolve to an Atomic Property.

When Atomic Properties correctly resolve, that's when most of the benefits of Atomic Data become real: the static types and the

## Object

A set of Atoms that describe how an object should be updated.
