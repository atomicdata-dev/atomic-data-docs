# Atomic Data: Concepts

The base URL for following concepts will be `https://atomicdata.dev/core/`.

## Atom

The smallest possible piece of _meaningful_ data / information.
The model of an Atom is comparable with an RDF Triple / Statement ([although there are imporant differences](../interoperability/rdf.md)).
An Atom consists of three values:

* **[Subject](#Subject)**: the Thing that the atom is providing information about.
* **[Predicate](#Predicate)**: the property of the Thing that the atom is about.
* **[Object](#Object)**: the new piece of information about the Atom.

Let's turn this sentence into Atoms:

`Arnold, who's born on the 20th of Januari 1991, has a best friend named Britta.`

```atomic-ndjson
["https://example.com/arnold" "https://example.com/properties/bornAt" "1991-01-20"]
["https://example.com/arnold" "https://example.com/properties/firstName" "Arnold"]
["https://example.com/arnold" "https://example.com/properties/bestFriend" "https://example.com/britta"]
["https://example.com/britta" "https://example.com/properties/firstName" "Britta"]
```

In the Atomic Data above, we have:

- four different Atoms (every line is an Atom)
- two different Subjects: `https://example.com/arnold` and `https://example.com/britta`.
- three different Predicates (`https://example.com/properties/bornAt`, `https://example.com/properties/firstName`, and `https://example.com/properties/bestFriend`)
- four different Objects (`1991-0-20`, `Arnold`, `https://example.com/britta` and `Britta`)

## Subject

The Subject is the first part of an Atom.
It is the identifier that the rest of the Atom is providing information about.
It's a URL that points to the Resource.
In other words: following / downloading the Subject link will provide you with all the Atoms about the Subject.

## Predicate

The Predicate is the second part of an Atom.
It is a URL that points to an Atomic Property.
For example `https://example.com/createdAt` or `https://example.com/firstName`.
The Predicate MUST be a URL, and that URL MUST resolve to an Atomic Property.

When Atomic Properties correctly resolve, that's when most of the benefits of Atomic Data become real: the static types and the

## Object

The Object is the third part of an Atom.
It contains

## Resource

A Resource is a set of Atoms that share the same Subject URL.
Every thing is Resource, such as the person "Michael Jackson", or the abstract class "Person".
All the concepts on this page are Resources.
More specifically, they are Classes, which is a subclass of Resources.
