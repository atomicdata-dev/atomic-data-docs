# How does Atomic Data relate to RDF?

RDF is the original data model behind linked data.
It is also the forerunner of Atomic Data, and is therefore highly similar in its philosophy and model.
Both heavily rely on using URLs, and both have a fundamentally simple and uniform model for data statements.
Both view the web as a single, connected graph database.
Because of that, Atomic Data is also highly compatible with RDF - **all Atomic Data can be converted into valid RDF**.
Atomic Data can be thought of as a **more constrained, type safe version of RDF**.
However, it does differ in some fundamental ways.

- Atomic has no seperate `datatype` field, but it requires that `Properties` (the resources that are shown when you folllow a `predicate` value) specify a datatype
- Atomic has no seperate `language` field, but it enables that string-type `predicates` specify a datatype
- Atomic has a native Event (state changes) model ([Atomic Mutations](/ATOMIC-MUTATIONS.md)), which enables communication of state changes
- Atomic has a native Schema model ([Atomic Schema](/ATOMIC-SCHEMA.md)), which helps developers to know what data types they can expect (string, integer, link, array)
- Atomic does not support `graph` fields in statments.
- Atomic does not support `blank nodes`.
- Atomic does not support having multiple statements with the same `<subject> <predicate>`, every one should be unique.
- Atomic only allows those who control a resource's `subject` URI endpoint to edit the data.

## Why these changes?

I love RDF, and have been working with it for quite some time now.
Using URIs for everything is a great idea, since it helps with interoperability and enables truly decentralized knowledge graphs.
However, some of the characteristics of RDF might have contributed to its relative lack of adoption.

- Using URLs as keys (in predicates) results in clunky Developer Experience, compared to the short strings that developers are used to in pretty much all languages and data formats. Using URIs as keys also limits interoperability. Adding a required / tightly integrated key mapping (from long URIs to short, simple strings) in Atomic Properties solves this issue.
- RDF lacks a clear solution for dealing with [ordered data](https://ontola.io/blog/ordered-data-in-rdf/), resulting in confusion when developers have to create lists of content. Adding an Array data type as a base data type helps solve this.
- Having both a `datatype` and a `predicate` value can lead to confusing situations. For example, the `schema:createdAt` Property requires an ISO DateTime string, but having a `xsd:boolean` datatype results in perfectly valid RDF.
- There is no integrated standard for communicating state changes (although [linked-delta](https://github.com/ontola/linked-delta) and [rdf-delta](https://afs.github.io/rdf-delta/) do exist)
- RDF allows that domain A creates statements about domain B. This means that someone using RDF data about domain B cannot know that domain B is actually the source of the data. Knowing _where data comes from_ is one of the great things about URIs, but RDF does not require that you can think of subjects as the source of data. Many subjects in RDF don't actually resolve to all the known triples of the statement. It would make the conceptual model way simpler if statements about a subject could only be made from the source of the domain owner of the subject.
- The documentation feels dated and verbose. All URLs should resolve to simple, clear explanations and machine readable definitions.

## Convert Atomic data to RDF

## Convert RDF to Atomic Data

- All `predicates` SHOULD resolve to Atomic Properties, and these SHOULD have a `datatype`. This means that the `datatype` in the original RDF statement can be dropped.
- What to do with `language`? TODO!
