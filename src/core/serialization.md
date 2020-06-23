# Serialization of Atomic Data

Atomic Data is not necessarily bound to a single serialization format.
It's fundamentally a data model, and that's an important distinction to make.
We recommend you use `AtomicTriples`, which is specifically designed to be a simple, performant format for Atomic Data.

## AtomicTriples-ndjson (.ad3)

Since the data model of Atomic Data is a bit simpler than RDF, serialization and parsing can be simpler as well.
In fact, a single Atom can be represented by an array of three strings, respectively representing the Subject, Property and Value.

It looks like this:

```ndjson
["https://example.com/subject","https://example.com/property","some object"]
["https://example.com/subject","https://example.com/otherProperty","https://example.com/somethingelse"]
```

We use Newline Delimited JSON ([NDJSON](http://ndjson.org/)), which is just a large JSONG string with newlines between each object.

NDJSON has some important benefits:

- It visually represents the underlying datamodel (the Atom)
- It can be streaming parsed, i.e. before the entire document is loaded. That is not possible with regular JSON.
- NDJSON parsers are everywhere
- Modern browers have highly performant JSON parsing, which means that it's _fast_ in one of the most imporant contexts: the browser.

_Mime type (not registered yet!): `application/ad3-ndjson`_

_File name extention: `.ad3`_

Disclaimer: note that Atomic-NDJSON is useful for communicating _current state_, but not for _state changes_.

## AtomicDoubles-ndjson (.ad2)

AtomicDoubles is similar to AtomicTriples, with one exception: the Subject is left out.
For many usecases, omitting the Subject is a _bad idea_.

However, it can be useful in (at least) two scenarios:

- The **Subject is not yet known** (for example, because it still has to be determined by some server or hash function).
- The **Subject is already known by the client**, and leaving it out saves bandwith. This happens for example during Subject Fetching, where the request itself contains the Subject, because the fetched URL itself is the Subject of all returned triples. Note that in this scenario, the server is unable to include

```ndjson
["https://example.com/property","some object"]
["https://example.com/otherProperty","https://example.com/somethingelse"]
```

This format is **not suitable for persistent storage** or peer to peer sharing - it is only useful when

- _Mime type (not registered yet!): `application/ad2-ndjson`_
- _File name extention: `.ad2`_

## RDF serializatinon formats

Because of the similarties with RDF, RDF serialization formats can be used to communicate and store Atomic Data, such as N-Triples, Turtle, HexTuples or JSON-LD.
_However_, keep in mind that RDF users will expect other things from their data.
Read more about the various existing formats and their respective merits [here](https://ontola.io/blog/rdf-serialization-formats/).

## Future formats

In the future, new serialization formats will be introduced.
For example, a fully optimized binary serialization format would make sense.
