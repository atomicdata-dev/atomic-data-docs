# How does Atomic Data relate to JSON?

Atomic Data requires a bit more information about pieces of data than JSON tends to contain. Let's take a look at an example:

```javascript
{
  name: "John",
  birthDate: "1991-01-20"
}
```

The following things are missing:

* What is the URI of the resource being described?
* What is the URI of the keys being used? \(`name` and `birthDate`\), and consequentially, how should the values be parsed?

We can add this data by adding _context_:

```javascript
{
  @context: {
    name: "https://example.com/properties/name",
    birthDate: "https://example.com/properties/birthDate",
    @id: "https://example.com/people/john"
  },
  name: "John",
  birthDate: "1991-01-20"
}
```

The JSON above is called JSON-LD. It is still perfectly valid JSON, but it contains more information, and in turn can be converted into other

