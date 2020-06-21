# Querying Atomic Data

There are multiple ways of getting Atomic Data into some system:

- Subject Fetching requests a single subject right from its source
- Triple Pattern Fragments allows querying for specific (combinations of) Subject, Predicate and Object values.
- SRARQL is a powerful Query language for traversing graphs

## Subject fetching (HTTP)

The simplest way of getting Atomic Data, is by sending an HTTP GET request to the subject URL.
Set the `Content-Type` header to an Atomic Data compatible mime type, such as `application/atomic+x-ndjson`.

```HTTP
GET https://example.com/myResource HTTP/1.1
Content-Type: application/atomic+x-ndjson
```

The server should respond with all the Atoms of which the requested URL is the subject:

```HTTP
HTTP/1.1 200 OK
Content-Type: application/atomic+x-ndjson
Connection: Closed

["https://example.com/myResource","https://example.com/properties/name","My awesome resource!"]
```

## Triple Pattern Fragments

[Triple Pattern Fragments](https://linkeddatafragments.org/specification/triple-pattern-fragments/) is an interface for querying RDF.
It works great for Atomic Data as well.

An HTTP implementation of a TPF endpoint might accept a GET request to a URL such as this:

`http://example.org/tpf?subject={subject}&predicate={predicate}&object={object}`

Make sure to URL encode the `subject`, `predicate`, `object` strings.

For example, let's search for all Atoms where the object is `test`.

```HTTP
GET https://example.com/tpf?object="test" HTTP/1.1
Content-Type: application/atomic+x-ndjson
```

```HTTP
HTTP/1.1 200 OK
Content-Type: application/atomic+x-ndjson
Connection: Closed

["https://example.com/myResource","https://example.com/properties/name","test"]
```

## Bulk API

[Bulk-API](https://github.com/ontola/bulk-api) is an (currently still closed) in-development specification for asking for multiple Subjects in one request.
This is especially useful in browser clients that traverse the graph iteratively, and HTTP/2 is not an option.

## SPAQRL

[SPARQL](https://www.w3.org/TR/rdf-sparql-query/) is a powerful RDF query language.
Since all Atomic Data is also valid RDF, it is possible to query Atomic Data using SPARQL.
