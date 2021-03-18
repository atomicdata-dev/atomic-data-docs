# JSON-AD: The Atomic Data serialization format

`JSON-AD` is the _default_ serialization format for Atomic Data.
It is what the current [Rust](https://github.com/joepio/atomic) and [Typescript / React](https://github.com/joepio/atomic-data-browser) implementation use to communicate.
It is a [JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/) with a lot of links in it and the following rules:

- Every Object is a Resource.
- Every Key is a Property URL.
- The `@id` field is special: it defines the Subject of the Resource.
- JSON arrays are mapped to [Resource Arrays](https://atomicdata.dev/datatypes/resourceArray)
- Numbers can be [Integers](https://atomicdata.dev/datatypes/integer), [Timestamps](https://atomicdata.dev/datatypes/timestamp) or [Floats](https://atomicdata.dev/datatypes/float).
- JSON booleans map to Atomic Booleans.
- Strings can be many datatypes, including [String](https://atomicdata.dev/datatypes/string), [Markdown](https://atomicdata.dev/datatypes/markdown), [Date](https://atomicdata.dev/datatypes/date) or other.
- Nested Objects are Nested Resources. A Nested Resource can either be an Anonymous Resource (without an `@id` field) or a regular Resource.
- When you want to describe multiple Resources in one JSON-AD document, use an array as the root item.

Let's look at an example JSON-AD Resource:

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

## Canonicalized JSON-AD

When you need deterministic serialization of Atomic Data (e.g. when calculating a cryptographic hash or signature, used in Atomic Commits), you can use the following procedure:

1. Serialize your Resource to JSON-AD
1. Do not include empty objects, empty arrays or null values.
1. All keys are sorted alphabetically (lexicographically) - both in the root object, as in any nested objects.
1. The JSON-AD is minified: no newlines, no spaces.

The last two steps of this process is more formally defined by the JSON Canonicalization Scheme (JCS, [rfc8785](https://tools.ietf.org/html/rfc8785)).
