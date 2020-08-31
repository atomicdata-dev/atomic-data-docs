# Serialization of Atomic Data

Atomic Data is not necessarily bound to a single serialization format.
It's fundamentally a data model, and that's an important distinction to make.
However, it's recommended to use `AtomicTriples`, which is specifically designed to be a simple, performant format for Atomic Data.

## AtomicTriples (.ad3)

A single Atom can be represented by an array of three strings, respectively representing the Subject, Property and Value.

It looks like this:

```ad3
["https://example.com/subject","https://example.com/property","some object"]
["https://example.com/subject","https://example.com/otherProperty","https://example.com/somethingelse"]
```

It uses Newline Delimited JSON ([NDJSON](http://ndjson.org/)) for serialization, which is just a large string with newlines between each JSON object.

NDJSON has some important benefits:

- **Streaming parsing**: An NDJSON document can be parsed before it's fully loaded / transmitted. That is not possible with regular JSON.
- **High compatibility**: NDJSON parsers can use JSON parsers, and are therefore everywhere.
- **Performance**: Modern browsers have highly performant JSON parsing, which means that it's _fast_ in one of the most important contexts: the browser.

_Mime type (not registered yet!): `application/ad3-ndjson`_

_File name extension: `.ad3`_

Disclaimer: note that Atomic-NDJSON is useful for communicating _current state_, but not for _state changes_.

Atomic Triples is heavily inspired by [NDJSON HexTuples](https://github.com/ontola/hextuples).

## AtomicDoubles (.ad2)

AtomicDoubles is similar to AtomicTriples, with one exception: the Subject is left out.
For many use-cases, omitting the Subject is a _bad idea_.
It means that you can't describe multiple resources in a single document, and that is useful in many contexts.

However, omitting the subject can be useful in (at least) three scenarios:

- The **Subject is not yet known when creating the data** (for example, because it still has to be determined by some server or hash function).
- The **Subject is already known by the client**, and leaving it out saves bandwidth. This happens for example during Subject Fetching, where the request itself contains the Subject, because the fetched URL itself is the Subject of all returned triples. Note that in this scenario, the server is unable to include
- The **Atoms are only valid coming from a specific source**. Since

```ndjson
["https://example.com/property","some object"]
["https://example.com/otherProperty","https://example.com/somethingelse"]
```

Keep in mind that this approach also has some downsides:

- It becomes impossible to include other resources in a single serialized document / response.

- _Mime type (not registered yet!): `application/ad2-ndjson`_
- _File name extension: `.ad2`_

## RDF serialization formats

Because of the similarities with RDF, RDF serialization formats can be used to communicate and store Atomic Data, such as N-Triples, Turtle, HexTuples or JSON-LD.
_However_, keep in mind that RDF users will expect other things from their data.
Read more about the various existing formats and their respective merits [here](https://ontola.io/blog/rdf-serialization-formats/).
Read more about serializing Atomic Data to RDF in the [RDF interoperability section](../interoperability/rdf.md).

## Future serialization formats

In the future, new serialization formats will be introduced.
Here's some (vague) ideas that might inspire you to design one:

### AtomicData-FS

Possible extension: `.adf`

FS stands for FileSystem.
It should be designed as a format that's easy to manipulate Atomic Data by hand, using plaintext editors and IDE software.
It fits nicely in our line-based paradigm, where we us IDEs and Github to manage our information.
It should use Shortnames wherever possible to make life easier for those who modify instances.
It might use hierarchical path structures to shape URLs.
It might use hierarchical path structures to shape data, and set constraints (e.g. all items directly in the `./person` directory should be Person instances).
Folder structure should reflect the structure inside URLs.

Note that this format is _not_ useful for sending arbitrary Atomic Data to some client.
It is useful for managing Atomic Data from a filesystem.

An example AtomicData-FS dir can be [found in the repo](https://github.com/ontola/atomic-data/tree/master/examples/atomic-fs/people).

```
# in ./projectDir/people/john.adf
# serialization uses YAML syntax
firstName: John
lastName: McLovin
# If a Property is not available in the Class, you can the URL of the property
https://schema.org/birthDate: 1991-01-20
# Perhaps support relative paths to other local resources
bestFriend: ./mary
```

Perhaps YAML isn't the right pick for this, because it's kind of hard to parse.

### AtomicData-Binary

Possible extension: `.adb`

A binary serialization format, designed to be performant and highly compressed.
Perhaps it works like this:

- An `adb` file consists of a large sequence of Maps and Statements
- A _Map_ is a combination of an internal identifiers (the _ID_, some short binary object) and a URL strings. These make sure that URLs can be used again cheaply, if they are used multiple times.
- A _Statement_ is a set of two IDs and a value, which can be a String, a URL or some binary format.
- Perhaps some extra compression is possible, because many URLs will have a common domain.
