# Atomic Data Core: Concepts

## Atomic Data

Atomic Data is a data model for sharing information on the web.
It can be used to express any type of information, including personal data, vocabularies, metadata, documents, files and more.
It's designed to be easily serializable to both JSON and linked data formats.
It is _typed_ data model, which means that every value should be validated and predictable.

It is a directed, labeled graph, similar to RDF, so contrary to some other (labeled) graph data models (e.g. NEO4j), a relationship between two items (Resources) does not have attributes.

## Resource

A Resource is a bunch of information about a single things.
Formally, it is a set of Atoms (a Graph) that share the same Subject URL.
You can think of a Resource as a single row in a spreadsheet or database.
In practice, Resources can be anything - a Person, a Blogpost, a Todo item.
A Resource consists of at least one Atom, so it always has some Property and some Value.
The most important Property of a Resource is the [`is-a`](https://atomicdata.dev/properties/isA) Property, which refers to which _Class_ it belongs (e.g. Person or Blogpost).
A Class can specify [`required`](https://atomicdata.dev/properties/requires) and [`recommended`](https://atomicdata.dev/properties/recommends) properties.
More on that in the Atomic Schema chapter!

## Atom (or Atomic Triple)

Every Resource is composed of Atoms.
The Atom is the smallest possible piece of _meaningful_ data / information.
You can think of an Atom as a single cell in a spreadsheet or database.
An Atom consists of three fields:

* **[Subject](#subject-field)**: the Thing that the atom is providing information about.
* **[Property](#property-field)**: the property of the Thing that the atom is about (will always be a URL to a [Property](../schema/classes.md#property)).
* **[Value](#value-field)**: the new piece of information about the Atom.

If you're familiar with RDF, you'll notice similarities.
An Atom is comparable with an RDF Triple / Statement ([although there are important differences](../interoperability/rdf.md)).

Let's turn this sentence into Atoms:

`Arnold Peters, who's born on the 20th of Januari 1991, has a best friend named Britta Smalls.`

Subject | Property | Value
--- | --- | ---
Arnold | last name | Peters
Arnold | birthdate | 1991-01-20
Arnold | best friend | Britta
Britta | last name | Smalls

The table above shows easily readable strings, but in reality, Atomic Data will almost exclusively consist of links (URLs).
The standard serialization format for Atomic Data is JSON-AD, which looks like this:

```json
[{
  "@id": "https://example.com/arnold",
  "https://example.com/properties/lastname": "Peters",
  "https://example.com/properties/birthDate": "1991-01-20",
  "https://example.com/properties/bestFriend": "https://example.com/britta",
},{
  "@id": "https://example.com/britta",
  "https://example.com/properties/lastname": "Smalls",
}]
```

The `@id` field denotes the Subject of each Resource, which is also the URL that should point to where the resource can be downloaded.

In the Atomic Data above, we have:

- two different **Resources**, describing two different **Subjects**: `https://example.com/arnold` and `https://example.com/britta`.
- three different **Properties** (`https://example.com/properties/bornAt`, `https://example.com/properties/firstName`, and `https://example.com/properties/bestFriend`)
- four different **Values** (`1991-01-20`, `Arnold`, `https://example.com/britta` and `Britta`)

All Subjects and Properties are Atomic URLs: they are links that point to more Atomic Data.
One of the Values is a URL, too, but we also have values like `Arnold` and `1991-01-20`.
These Values have different _Datatypes_
In most other data formats, the datatypes are limited and are visually distinct.
JSON, for example, has `array`, `object`, `string`, `number` and `boolean`.
In Atomic Data, however, datatypes are defined somewhere else, and are extendible.
To find the Datatype of an Atom, you fetch the Property, and that one has a Datatype.
For example, the `https://example.com/properties/bornAt` Property requires an ISO Date string, and the `https://example.com/properties/firstName` Property requires a regular string.
This might seem a little tedious and weird at first, but is has some nice advantages!
Their Datatypes are defined in the Properties.

## Subject field

The Subject field is the first part of an Atom.
It is the identifier that the rest of the Atom is providing information about.
The Subject field is a URL that points to the Resource.
The creator of the Subject MUST make sure that it resolves.
In other words: following / downloading the Subject link will provide you with all the Atoms about the Subject (see [Querying Atomic Data](querying.md).
This also means that the creator of a Resource must make sure that it is available at its URL - probably by hosting the data, or by using some service that hosts it.

## Property field

The Property field is the second part of an Atom.
It is a URL that points to an Atomic [Property](../schema/classes.md#Property).
For example `https://example.com/createdAt` or `https://example.com/firstName`.
<!-- Making this a requirement is what makes Atomic Data typed and semantic -->
The Property field MUST be a URL, and that URL MUST resolve to an Atomic Property, which contains information about the Datatype.

## Value field

The Value field is the third part of an Atom.
In RDF, this is called an `object`.
Contrary to the Subject and Property values, the Value can be of any datatype.
This includes URLs, strings, integers, dates and more.

## Graph

A Graph is a set of Atoms.
A Graph can describe various subjects, and may or may not be related.
Graphs can have several characteristics (Schema Complete, Valid, Closed)

## Atomic Web

The Atomic Web refers to all Atomic Graphs on the web.

In the next chapter, we'll explore how Atomic Data is serialized.
