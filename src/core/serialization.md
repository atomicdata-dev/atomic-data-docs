# Serialization of Atomic Data

Atomic Data is not necessarily bound to a single serialization format.
It's fundamentally a data model, and that's an important distinction to make.

## JSON-AD

However, it's recommended to use [`JSON-AD`](json-ad.md) (more about that on the next page), which is specifically designed to be a simple, complete and performant format for Atomic Data.

## JSON (simple)

Atomic Data is designed to be serializable to clean, simple [JSON](../interoperability/json.md), for usage in (client) apps that don't need to know the full URLs of properties.

## RDF serialization formats

Since Atomic Data is a strict subset of RDF, RDF serialization formats can be used to communicate and store Atomic Data, such as N-Triples, Turtle, HexTuples, JSON-LD and [other RDF serialization formats](https://ontola.io/blog/rdf-serialization-formats/).
However, not all valid RDF is valid Atomic Data.
Atomic Data is more strict.
Read more about serializing Atomic Data to RDF in the [RDF interoperability section](../interoperability/rdf.md).

## Experimental serialization formats

Some experimental ideas for Atomic Data serialization are [written here](https://github.com/ontola/atomic-data/blob/master/src/experimental-serialization.md).
