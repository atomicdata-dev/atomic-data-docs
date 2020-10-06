# Interoperability: Relation to other technology

Atomic data is designed to be highly interoperable.
It's also serializable to RDF, which includes Turtle, N-triples, RDF/XML and [other serialization formats](https://ontola.io/blog/rdf-serialization-formats/).

## Data formats

* [JSON](json.md): Atomic Data is designed to be easily serializable to clean, idiomatic JSON. However, if you want to turn JSON into Atomic Data, you'll have to make sure that all keys in the JSON object are URLs that link to Atomic Properties, and the data itself also has to be available at its Subject URL.
* [RDF](rdf.md): Atomic Data is a strict subset of RDF, and can therefore be trivially serialized to all RDF formats (Turtle, N-triples, RDF/XML, JSON-LD, and others). The other way around is more difficult. Turning RDF into Atomic Data requires that all predicates are Atomic Properties, the values must match its properties datatype, the atoms must be available at the subject URL, and the subject-predicate combinations must be unique.

## Protocols

* [IPFS](ipfs.md): Content-based addressing to prevent 404s and centralization
