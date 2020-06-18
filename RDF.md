# How does Atomic Data relate to RDF?

RDF is the original data model behind linked data.
It is also the forerunner of Atomic Data, and is therefore highly similar in its philosophy and model.
Both heavily rely on using URLs, and both have a fundamental "stament" model.
Both view the web as one, connected graph database.
Because of that, Atomic Data is also highly compatible with RDF - **all Atomic Data can be converted into valid RDF**.
However, it does differ in some fundamental ways.

- Atomic has a native Event (state changes) model ([Atomic Mutations](/ATOMIC-MUTATIONS.md)), which enables communication of state changes
- Atomic has a native Schema model (Atomic Schema), which helps developers to know what data types they can expect (string, integer, link)
- Atomic has no seperate `datatype` field, but it requires that `predicates` specify a datatype
- Atomic has no seperate `language` field, but it enables that string-type `predicates` specify a datatype
- Atomic does not support `graph` fields in statments.
- Atomic does not support `blank nodes`

## Why these changes?

## Convert Atomic data to RDF

## Convert RDF to Atomic Data
