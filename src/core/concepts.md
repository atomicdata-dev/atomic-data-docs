# Atomic Data Core: Concepts

Understanding the Core concepts of Atomic Data are fundamental for reading the rest of the documentation.

## Atomic Data

Atomic Data is a data format for representing information on the web.
It is a directed, labeled graph, similar to RDF.
It can be used to express any type of information, inlcuding personal data, vocabularies, metadata, documents, files and more.
Contrary to some other (labeled) graph data models, a relationship between two items (Resources) does not have attributes.

## Atom (or Atomic Triple)

The smallest possible piece of _meaningful_ data / information.
The model of an Atom is comparable with an RDF Triple / Statement ([although there are imporant differences](../interoperability/rdf.md)).
An Atom consists of three values:

* **[Subject](#Subject)**: the Thing that the atom is providing information about.
* **[Property](#Property)**: the property of the Thing that the atom is about (will always be a URL to a [Property](../schema/concepts.md#Property)).
* **[Object](#Object)**: the new piece of information about the Atom.

Let's turn this sentence into Atoms:

`Arnold, who's born on the 20th of Januari 1991, has a best friend named Britta.`

```ad3
["https://example.com/arnold","https://example.com/properties/bornAt","1991-01-20"]
["https://example.com/arnold","https://example.com/properties/firstName","Arnold"]
["https://example.com/arnold","https://example.com/properties/bestFriend","https://example.com/britta"]
["https://example.com/britta","https://example.com/properties/firstName","Britta"]
```

In the Atomic Data above, we have:

- four different Atoms (every line is an Atom)
- two different Subjects: `https://example.com/arnold` and `https://example.com/britta`.
- three different Propertys (`https://example.com/properties/bornAt`, `https://example.com/properties/firstName`, and `https://example.com/properties/bestFriend`)
- four different Objects (`1991-0-20`, `Arnold`, `https://example.com/britta` and `Britta`)

## Subject

The Subject field is the first part of an Atom.
It is the identifier that the rest of the Atom is providing information about.
It's a URL that points to the Resource.
The creator of the Subject MUST make sure that it resolves.
In other words: following / downloading the Subject link will provide you with all the Atoms about the Subject (see [Atomic Querying](querying.md).

## Property

The Property field is the second part of an Atom.
It is a URL that points to an Atomic [Property](../schema/classes.md#Property).
For example `https://example.com/createdAt` or `https://example.com/firstName`.
<!-- Making this a requirement is what makes Atomic Data typed and semantic -->
The Property MUST be a URL, and that URL MUST resolve to an Atomic Property.

## Value

The Value field is the third part of an Atom.
Contrary to the Subject and Property values, the Object can be of any datatype.
This includes URLs, strings, integers, dates and more.

## Graph

A Graph is a set of Atoms.
A Graph can describe various subjects, and may or may not be related.
Graphs can have several characteristics (Schema Complete, Valid, Closed)

## Resource

A Resource is a set of Atoms (a Graph) that share the same Subject URL.
Every thing is Resource, such as the person "Michael Jackson", or the abstract class "Person".
All the concepts on this page are Resources.
A

Properties:

- `a` - (optional, AtomicURL) the [Class]() of the Resource.
