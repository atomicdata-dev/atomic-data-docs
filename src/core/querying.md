# Querying Atomic Data

There are multiple ways of getting Atomic Data into some system:

- Subject Fetching requests a single subject right from its source
- Triple Pattern Fragments allows querying for specific (combinations of) Subject, Predicate and Object values.
- SRARQL is a powerful Query language for traversing graphs

## Subject fetching (HTTP)

The simplest way of getting Atomic Data, is by sending an HTTP GET request to the subject URL.
Set the correct `Content-Type` header to make sure you

```HTTP
GET https://example.com/myResource HTTP/1.1
Content-Type: application/atomic+x-ndjson
```

The server should respond with a set of Atoms:

```HTTP
HTTP/1.1 200 OK
Content-Type: application/atomic+x-ndjson
Connection: Closed

["https://example.com/myResource","https://example.com/properties/name","My awesome resource!"]
```

The example above sets the `Content-Type` field to the Atomic NDJSON mime type.

## Triple Pattern Fragments

## SPAQRL
