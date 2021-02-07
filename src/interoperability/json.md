# How does Atomic Data relate to JSON?

Because JSON is so popular, Atomic Data is designed with JSON in mind.

- You can always serialize Atomic Data to simple, clean JSON. The JSON keys are then derived from the `shortnames` of properties.
- You can also serialize Atomic Data to JSON-LD, which is compatible with RDF. This contains more information about the datatypes and the URLs of properties.
- The default serialization is JSON-AD, which is also JSON based. It uses URLs as keys, which means we can look up more information about properties, but this might be less convenient to use for developers who expect

## From JSON to JSON-AD

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
  "@id": "https://example.com/people/john",
  "https://example.com/properties/name": "John",
  "https://example.com/properties/birthDate": "1991-01-20"
}
```

## From Atomic Data to JSON-LD

Atomic Data is a strict subset of RDF, and the most popular serialization of RDF for JSON data is [JSON-LD](https://json-ld.org/).
All JSON-LD is perfectly valid JSON, but with a couple of handy features.

Since Atomic Schema requires the presence of a `key` slug in Properties, converting Atomic Data to JSON results in dev-friendly objects with nice shorthands.

```json
{
  "@id": "https://example.com/people/John",
  "https://example.com/properties/lastname": "John",
  "https://example.com/properties/bestFriend": "https://example.com/sarah",
}
```

Can be automatically converted to:

```json
{
  "@context": {
    "@id": "https://example.com/people/John",
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


## JSON-LD Requirements

- Make sure the URLs used in the `@context` resolve to Atomic Properties.
<!-- Not sure about this.. maybe use RDF collections or some other model? -->
- Convert JSON-LD arrays into ResourceArrays
- Creating nested JSON objects is possible (by resolving the identifiers from `@id` relations), but it is up to the serializer to decide how deep this object nesting should happen.

## Considerations

- Whilst JSON-LD is great for traditional JSON usage (dot.syntax ORM style navigation of objects), it is not great for linked data usage.
