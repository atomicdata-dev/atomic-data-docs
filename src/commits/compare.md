# Atomic Commits compared to other (RDF) delta models

Let's compare the Atomic Commit approach with some existing protocols for communicating state changes / patches / mutations / deltas in linked data or JSON.
First, I'll briefly discuss the existing examples ([open a PR / issue](https://github.com/ontola/atomic-data/issues) if we're missing something!).
After that, we'll discuss how Atomic Data differs from the existing ones.

## RDF-Delta

https://afs.github.io/rdf-delta/

Describes changes (RDF Patches) in a specialized turtle-like serialization format.

```
TX .
PA "rdf" "http://www.w3.org/1999/02/22-rdf-syntax-ns#" .
PA "owl" "http://www.w3.org/2002/07/owl#" .
PA "rdfs" "http://www.w3.org/2000/01/rdf-schema#" .
A <http://example/SubClass> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.w3.org/2002/07/owl#Class> .
A <http://example/SubClass> <http://www.w3.org/2000/01/rdf-schema#subClassOf> <http://example/SUPER_CLASS> .
A <http://example/SubClass> <http://www.w3.org/2000/01/rdf-schema#label> "SubClass" .
TC .
```

Similar to Atomic Commits, these Delta's should have identifiers (URLs), which are denoted in a header.

## Delta-LD

http://www.tara.tcd.ie/handle/2262/91407

## PatchR

https://www.igi-global.com/article/patchr/135561

## LD-Patch

https://www.w3.org/TR/ldpatch/

```
PATCH /timbl HTTP/1.1
Host: example.org
Content-Length: 478
Content-Type: text/ldpatch
If-Match: "abc123"

@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix schema: <http://schema.org/> .
@prefix profile: <http://ogp.me/ns/profile#> .
@prefix ex: <http://example.org/vocab#> .

Delete { <#> profile:first_name "Tim" } .
Add {
  <#> profile:first_name "Timothy" ;
    profile:image <https://example.org/timbl.jpg> .
} .

Bind ?workLocation <#> / schema:workLocation .
Cut ?workLocation .

UpdateList <#> ex:preferredLanguages 1..2 ( "fr-CH" ) .

Bind ?event <#> / schema:performerIn [ / schema:url = <https://www.w3.org/2012/ldp/wiki/F2F5> ]  .
Add { ?event rdf:type schema:Event } .

Bind ?ted <http://conferences.ted.com/TED2009/> / ^schema:url ! .
Delete { ?ted schema:startDate "2009-02-04" } .
Add {
  ?ted schema:location [
    schema:name "Long Beach, California" ;
    schema:geo [
      schema:latitude "33.7817" ;
      schema:longitude "-118.2054"
    ]
  ]
} .
```

## Linked-Delta

https://github.com/ontola/linked-delta

An N-Quads serialized delta format.
Methods are URLs, which means they are extensible.
Does not specify how to bundle lines.
Used in production of a web app that we're working on.
Designed with simplicity (no new serialization format, simple to parse) and performance in mind.

```
Initial state:

<http://example.org/resource> <http://example.org/predicate> "Old value 🙈" .

Linked-Delta:

<http://example.org/resource> <http://example.org/predicate> "New value 🐵" <http://purl.org/linked-delta/replace> .

New state:

<http://example.org/resource> <http://example.org/predicate> "New value 🐵" .
```

## JSON-PATCH

http://jsonpatch.com/

A simple way to edit JSON objects:

```
The original document

{
  "baz": "qux",
  "foo": "bar"
}

The patch

[
  { "op": "replace", "path": "/baz", "value": "boo" },
  { "op": "add", "path": "/hello", "value": ["world"] },
  { "op": "remove", "path": "/foo" }
]

The result

{
  "baz": "boo",
  "hello": ["world"]
}
```

It uses the [JSON-Pointer spec](http://tools.ietf.org/html/rfc6901) for denoting `path`s.
It has quite a bunch of implementations, in various languages.

## JSON-LD-PATCH

https://github.com/digibib/ls.ext/wiki/JSON-LD-PATCH

A JSON denoted patch notation for RDF.
Seems similar to the [RDF/JSON](https://www.w3.org/TR/rdf-json/) serialization format.
Uses string literals as operators / methods.
Conceptually perhaps most similar to linked-delta.

```
[
  {
    "op": "add",
    "s": "http://example.org/my/resource",
    "p": "http://example.org/ontology#title",
    "o": {
      "value": "New Title",
      "type": "http://www.w3.org/2001/XMLSchema#string"
    }
  }
]
```

## SPARQL UPDATE

https://www.w3.org/TR/sparql11-update/

SPARQL queries that change data.

```sparql
PREFIX dc: <http://purl.org/dc/elements/1.1/>
INSERT DATA
{
  <http://example/book1> dc:title "A new book" ;
                         dc:creator "A.N.Other" .
}
```

Allows for very powerful queries, combined with updates.
E.g. rename all persons named `Bill` to `William`:

```
PREFIX foaf:  <http://xmlns.com/foaf/0.1/>

WITH <http://example/addresses>
DELETE { ?person foaf:givenName 'Bill' }
INSERT { ?person foaf:givenName 'William' }
WHERE
  { ?person foaf:givenName 'Bill'
  }
```

SPARQL Update is the most powerful of the formats, but also perhaps the most difficult to implement and understand.

## Atomic Commits

Let's talk about the differences between the concepts above and Atomic Commits.

For starters, Atomic Commits can only work with a _specific subset_ of RDF, namely Atomic Data.
RDF allows for blank nodes, does not have subject-predicate uniqueness and offers named graphs - which all make it hard to unambiguously select a single value.
Most of the alternative patch / delta models described above had to support these concepts.
Atomic Data is more strict and constrained than RDF.
It does not support named graphs and blank nodes.
This enables a simpler approach to describing state changes, but it also means that Atomic Commits will not work with most existing RDF data.

Secondly, individual Atomic Commits are tightly coupled to specific Resources.
A single Commit cannot change multiple resources - and most of the models discussed above to enable this.
This is a big constraint, and it does not allow for things like compact migrations in a database.
However, this resource-bound constraint opens up some interesting possibilities:

- it becomes easier to combine it with _authorization_ (i.e. check if the person has the correct rights to edit some resource): simply check if the Author has the rights to edit the Subject.
- it makes it easier to find all Commits for a Resource, which is useful when constructing a history / audit log / previous version.

Thirdly, Atomic Commits don't introduce a new serialization format.
It's just JSON.
This means that it will feel familiar for most developers, and will be supported by many existing environments.

Finally, Atomic Commits use cryptography (hashing) to determine authenticity of commits.
This concept is borrowed from git commits, which also uses signatures to prove authorship.
As is the case with git, this also allows for verfiable P2P sharing of changes.
