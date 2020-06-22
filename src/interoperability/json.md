# How does Atomic Data relate to JSON?

## From Atomic Data to JSON



## From JSON to Atomic Data

Atomic Data requires a bit more information about pieces of data than JSON tends to contain. Let's take a look at an example:

```json
{
  "name": "John",
  "birthDate": "1991-01-20"
}
```

The following things are missing:

* What is the URL of the resource being described?
* What is the URL of the keys being used? \(`name` and `birthDate`\), and consequentially, how should the values be parsed?

We can add this data by adding _context_:

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

The JSON above is called JSON-LD. It is still perfectly valid JSON, but it contains more information, and in turn can be converted into RDF formats.
TODO!

## JSON-LD Requirements

- Make sure the URLs used in the `@context` resolve to Atomic Properties.
