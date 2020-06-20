# Serialization of Atomic Data

Atomic Data is not necessarily bound to a single serialization format.
It's fundamentally a data model, and that's an important distinction to make.
We recommend you use `Atomic-NDJSON`, which is specifically designed to be a simple, performant format for Atomic Data.

## Atomic-NDJSON

Since the data model of Atomic Data is a bit simpler than RDF, serialization and parsing can be simpler as well.
In fact, a single Atom can be represented by an array of three strings, respectively representing the Subject, Predicate and Object.

It looks like this:

```ndjson
["https://example.com/subject","https://example.com/predicate","some object"]
["https://example.com/subject","https://example.com/otherProperty","https://example.com/somethingelse"]
```

NDJSON has some important benefits:

- It visually represents the underlying datamodel (the Atom)
- It can be streaming parsed, i.e. before the entire document is loaded. That is not possible with regular JSON.
- NDJSON parsers are everywhere
- Modern browers have highly performant (ND)JSON parsing, which means that it's _fast_ in one of the most imporant contexts: the browser.

Mime type (not registered yet!): `application/atomic+x-ndjson; charset=utf-8`

File name extention:

Disclaimer: note that Atomic-NDJSON is useful for communicating _current state_, but not for _state changes_.

## RDF serializatinon formats

Because of the similarties with RDF, RDF serialization formats can be used to communicate and store Atomic Data, such as N-Triples, Turtle, HexTuples or JSON-LD.
_However_, keep in mind that RDF users will expect other things from their data.
Read more about the various existing formats and their respective merits [here](https://ontola.io/blog/rdf-serialization-formats/).

## Future formats

In the future, new serialization formats will be introduced.
For example, a fully optimized binary serialization format would make sense.
