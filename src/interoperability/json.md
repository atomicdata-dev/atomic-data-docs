# How does Atomic Data relate to JSON?

Because JSON is so popular, Atomic Data is designed to be easily serializable to JSON.

Atomic Data is a strict subset of RDF, and the most popular serialization of RDF for JSON data is [JSON-LD](https://json-ld.org/).
All JSON-LD is perfectly valid JSON, but with a couple of handy features.

## From JSON to Atomic Data

Atomic Data requires a bit more information about pieces of data than JSON tends to contain. Let's take a look at a regular JSON example:

```json
{
  "name": "John",
  "birthDate": "1991-01-20"
}
```

We need more information to convert this JSON into Atomic Data.
The following things are missing:

* What is the Subject URL of the resource being described?
* What is the Predicate URL of the keys being used? (`name` and `birthDate`), and consequentially, how should the values be parsed? What are their DataTypes?

We can add this data by adding some _@context_:

```json
{
  "@context": {
    "name": "https://example.com/properties/name",
    "birthDate": "https://example.com/properties/birthDate",
    "@id": "https://example.com/people/john"
  },
  "name": "John",
  "birthDate": "1991-01-20"
}
```

The JSON above is called JSON-LD.
It is still perfectly valid JSON, but it contains more information, and in turn can be converted into RDF formats.

## From Atomic Data to JSON-LD

Since Atomic Schema requires the presence of a `key` slug in Properties, converting Atomic Data to JSON results in dev-friendly objects with nice shorthands.

```ndjson
["https://example.com/john","https://example.com/properties/lastname","Houdini"]
["https://example.com/john","https://example.com/properties/bestFriend","https://example.com/sarah"]
```

Can be automatically converted to:

```json
{
  "@context": {
    "name": "https://example.com/properties/lastname",
    "bestFriend": "https://example.com/properties/bestFriend",
  },
  "name": "John",
  "bestFriend": {
    "@id": "https://example.com/sarah"
  },
}
```

The `@context` object provides a _mapping_ to the original URLs.
The `@id` key shows that the value should be interpreted as a link (a URI).

## JSON-LD Requirements

- Make sure the URLs used in the `@context` resolve to Atomic Properties.
<!-- Not sure about this.. maybe use RDF collections or some other model? -->
- Convert JSON-LD arrays into ResourceArrays
- Creating nested JSON objects is possible (by resolving the identifiers from `@id` relations), but it is up to the serializer to decide how deep this object nesting should happen.

## Considerations

- Whilst JSON-LD is great for traditional JSON usage (dot.syntax ORM style navigation of objects), it is not great for linked data usage.
