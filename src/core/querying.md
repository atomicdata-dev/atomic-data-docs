# Querying Atomic Data

There are multiple ways of getting Atomic Data into some system:

- [**Atomic Paths**](paths.md) is a simple way to traverse Atomic Graphs and target specific values
- [**Subject Fetching**](#subject-fetching-http) requests a single subject right from its source
- [**Triple Pattern Fragments**](#triple-pattern-fragments) allows querying for specific (combinations of) Subject, Property and Value.
- [**SRARQL**](#SPARQL) is a powerful Query language for traversing graphs

## Atomic Paths

An Atomic Path is a string that consist of one or more URLs, which when traversed point to an item.
For more information, see [Atomic Paths](paths.md).

## Subject fetching (HTTP)

The simplest way of getting Atomic Data when the Subject is an HTTP URL, is by sending a GET request to the subject URL.
Set the `Content-Type` header to an Atomic Data compatible mime type, such as `application/ad3-ndjson`.

```HTTP
GET https://example.com/myResource HTTP/1.1
Content-Type: application/ad3-ndjson
```

The server SHOULD respond with all the Atoms of which the requested URL is the subject:

```HTTP
HTTP/1.1 200 OK
Content-Type: application/ad3-ndjson
Connection: Closed

["https://example.com/myResource","https://example.com/properties/name","My awesome resource!"]
```

The server MAY also include other resources, if they are deemed relevant.

## Subject Fetching (IPFS)

IPFS is a new protocol for sharing data using content-addressing.

## Triple Pattern Fragments

[Triple Pattern Fragments](https://linkeddatafragments.org/specification/triple-pattern-fragments/) (TPF) is an interface for querying RDF.
It works great for Atomic Data as well.

An HTTP implementation of a TPF endpoint might accept a GET request to a URL such as this:

`http://example.org/tpf?subject={subject}&property={property}&value={value}`

Make sure to URL encode the `subject`, `property`, `value` strings.

For example, let's search for all Atoms where the value is `test`.

```HTTP
GET https://example.com/tpf?value="test" HTTP/1.1
Content-Type: application/ad3-ndjson
```

This is the HTTP response:

```HTTP
HTTP/1.1 200 OK
Content-Type: application/ad3-ndjson
Connection: Closed

["https://example.com/myResource","https://example.com/properties/name","test"]
```
<!--
## Bulk API

Bulk-API is an (currently still closed) in-development specification for asking for multiple Subjects in one request.
This is especially useful in browser clients that traverse the graph iteratively, and HTTP/2 is not an option. -->

## SPARQL

[SPARQL](https://www.w3.org/TR/rdf-sparql-query/) is a powerful RDF query language.
Since all Atomic Data is also valid RDF, it should be possible to query Atomic Data using SPARQL.
