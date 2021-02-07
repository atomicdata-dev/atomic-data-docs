# Serialization of Atomic Data

Atomic Data is not necessarily bound to a single serialization format.
It's fundamentally a data model, and that's an important distinction to make.
However, it's recommended to use `JSON-AD`, which is specifically designed to be a simple and performant format for Atomic Data.

Atomic Data is designed to be serializable to clean, simple [JSON](../interoperability/json.md).
It's also serializable to RDF, which includes Turtle, N-triples, RDF/XML and [other serialization formats](https://ontola.io/blog/rdf-serialization-formats/).

## JSON-AD

`JSON-AD` is the _default_ serialization format for Atomic Data.
It is what the current [Rust](https://github.com/joepio/atomic) and [Typescript / React](https://github.com/joepio/atomic-react) implementation use to communicate.
It is just JSON with a lot of links in it.

- The `@id` field is special: it defines the Subject of the Resource.
- JSON arrays are mapped to [Resource Arrays](https://atomicdata.dev/datatypes/resourceArray)
- Numbers can be [Integers](https://atomicdata.dev/datatypes/integer), [Timestamps](https://atomicdata.dev/datatypes/timestamp) or [Floats](https://atomicdata.dev/datatypes/float).
- JSON booleans map to Atomic Booleans.
- Strings can be many datatypes, including [String](https://atomicdata.dev/datatypes/string), [Markdown](https://atomicdata.dev/datatypes/markdown), [Date](https://atomicdata.dev/datatypes/date) or other.
- Nested Objects are Nested Resources. A Nested Resource can either be an Anonymous Resource (without an `@id` field) or a regular Resource.

Let's look at an example:

```json
{
  "@id": "https://atomicdata.dev/properties/description",
  "https://atomicdata.dev/properties/datatype": "https://atomicdata.dev/datatypes/markdown",
  "https://atomicdata.dev/properties/description": "A textual description of something. When making a description, make sure that the first few words tell the most important part. Give examples. Since the text supports markdown, you're free to use links and more.",
  "https://atomicdata.dev/properties/isA": [
    "https://atomicdata.dev/classes/Property"
  ],
  "https://atomicdata.dev/properties/shortname": "description"
}
```

## RDF serialization formats

Because of the similarities with RDF, RDF serialization formats can be used to communicate and store Atomic Data, such as N-Triples, Turtle, HexTuples or JSON-LD.
_However_, keep in mind that RDF users will expect other things from their data.
Read more about the various existing formats and their respective merits [here](https://ontola.io/blog/rdf-serialization-formats/).
Read more about serializing Atomic Data to RDF in the [RDF interoperability section](../interoperability/rdf.md).

## Experimental serialization formats

Some experimental ideas for Atomic Data serialization are [written here](../experimental-serialization.md).
