# What is Atomic Data?

## Atomic Data Core

Atomic Data is a modular specification for sharing information on the web.
Since Atomic Data is a _modular_ specification, you can mostly take what you want to use, and ignore the rest.
The _Core_ part, however, is the _only required_ part of the specification, as all others depend on it.

Atomic Data Core can be used to express any type of information, including personal data, vocabularies, metadata, documents, files and more.
It's designed to be easily serializable to both JSON and linked data formats.
It is _typed_ data model, which means that every value should be validated and predictable.

It is a directed, labeled graph, similar to RDF, so contrary to some other (labeled) graph data models (e.g. NEO4j), a relationship between two items (Resources) does not have attributes.

## Design goals

* **Browsable**: Data should explicitly link to other pieces of data, and these links should be followable.
* **Semantic**: Every data Atom and relation has a clear semantic meaning.
* **Interoperable**: Plays nice with other data formats (e.g. JSON, XML, and all RDF formats).
* **Open**: Free to use, open source, no strings attached.
* **Clear Ownership**: The data shows who (or which domain) is in control of the data, so new versions of the data can easily be retrieved.
* **Mergeable**: Any two sets of Atoms can be merged into a single graph without any merge conflicts / name collisions.
* **Extensible**: Anyone can define their own data types and create Atoms with it.
* **ORM-friendly**: Navigate a _decentralized_ graph by using `dot.syntax`, similar to how you navigate a JSON object in javascript.
* **Type-safe**: All valid Atomic data has an unambiguous, static datatype.

## Resource

A _Resource_ is a bunch of information about a thing, referenced by a single link (the Subject).
Formally, it is a set of Atoms (i.e. a Graph) that share a Subject URL.
You can think of a Resource as a single row in a spreadsheet or database.
In practice, Resources can be anything - a Person, a Blogpost, a Todo item.
A Resource consists of at least one Atom, so it always has some Property and some Value.
A Property can only occur once in every Resource.

## Atom (or Atomic Triple)

Every Resource is composed of _Atoms_.
The Atom is the smallest possible piece of _meaningful_ data / information (hence the name).
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

The table above shows human readable strings, but in Atomic Data, we use links (URLs) wherever we can.
That's because links are awesome.
Links **remove ambiguity** (we know exactly which person or property we mean), they are **resolvable** (we can click on them), and they are **machine readable** (machines can fetch links to do useful things with them).
So the table from above, will more closely resemble this one:

Subject | Property | Value
--- | --- | ---
https://example.com/arnold | https://example.com/properties/lastname | Peters
https://example.com/arnold | https://example.com/properties/birthDate | 1991-01-20
https://example.com/arnold | https://example.com/properties/bestFriend | https://example.com/britta
https://example.com/britta | https://example.com/properties/lastname | Smalls

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

The `@id` field denotes the Subject of each Resource, which is also the URL that should point to where the resource can be found.

In the JSON-AD example above, we have:

- two **Resources**, describing two different **Subjects**: `https://example.com/arnold` and `https://example.com/britta`.
- three different **Properties** (`https://example.com/properties/bornAt`, `https://example.com/properties/firstName`, and `https://example.com/properties/bestFriend`)
- four **Values** (`1991-01-20`, `Arnold`, `https://example.com/britta` and `Britta`)
- four **Atoms** - every row is one Atom.

All Subjects and Properties are Atomic URLs: they are links that point to more Atomic Data.
One of the Values is a URL, too, but we also have values like `Arnold` and `1991-01-20`.
Values can have different _Datatypes_
In most other data formats, the datatypes are limited and are visually distinct.
JSON, for example, has `array`, `object`, `string`, `number` and `boolean`.
In Atomic Data, however, datatypes are defined somewhere else, and are extendible.
To find the Datatype of an Atom, you fetch the Property, and that Property will have a Datatype.
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
In JSON-AD, the Subject is denoted by `@id`.

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

A Graph is a collection of Atoms.
A Graph can describe various subjects, and may or may not be related.
Graphs can have several characteristics (Schema Complete, Valid, Closed)

## Nested Resource

A Nested Resource only exists inside of another resource.
It does not have its own subject.

In the following JSON-AD example, the `address` is a nested resource:

```json
{
  "@id": "https://example.com/arnold",
  "https://example.com/properties/address": {
    "https://example.com/properties/firstLine": "Longstreet 22",
    "https://example.com/properties/city": "Watertown",
    "https://example.com/properties/country": "the Netherlands",
  }
}
```

Nested Resources can be _named_ or _anonymous_. An _Anonymous Nested Resource_ does not have it's own `@id` field.
It _does_ have its own unique [path](./paths.md), which can be used as its identifier.

In the next chapter, we'll explore how Atomic Data is serialized.
