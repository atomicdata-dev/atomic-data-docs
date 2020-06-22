# How does Atomic Data relate to RDF?

RDF is the original data model behind linked data.
It is also the forerunner of Atomic Data, and is therefore highly similar in its philosophy and model.
Both heavily rely on using URLs, and both have a fundamentally simple and uniform model for data statements.
Both view the web as a single, connected graph database.
Because of that, Atomic Data is also highly compatible with RDF - **all Atomic Data can be converted into valid RDF**.
Atomic Data can be thought of as a **more constrained, type safe version of RDF**.
However, it does differ in some fundamental ways.

- Atomic only allows those who control a resource's `subject` URL endpoint to edit the data. This means that you can't add triples about something that you don't control.
- Atomic requires URL values in its `subjects` and `predicates`, which means that they should be resolveable.
- Atomic has no seperate `datatype` field, but it requires that `Properties` (the resources that are shown when you folllow a `predicate` value) specify a datatype
- Atomic has no seperate `language` field, but it does support language strings as a Datatype in Properties.
- Atomic has a native Event (state changes) model ([Atomic Mutations](../mutations/intro.md)), which enables communication of state changes
- Atomic has a native Schema model ([Atomic Schema](../schema/intro.md)), which helps developers to know what data types they can expect (string, integer, link, array)
- Atomic does not support `graph` fields in statments.
- Atomic does not support `blank nodes`.
- Atomic does not support having multiple statements with the same `<subject> <predicate>`, every combination should be unique.

## Why these changes?

I love RDF, and have been working with it for quite some time now.
Using URIs (and moreso URLs, which are URIs that can be fetched) for everything is a great idea, since it helps with interoperability and enables truly decentralized knowledge graphs.
However, some of the characteristics of RDF might have contributed to its relative lack of adoption.

- Having both a `datatype` and a `predicate` value can lead to confusing situations. For example, the [`schema:dateCreated`](https://schema.org/dateCreated) Property requires an ISO DateTime string (according to the schema.org definition), but using a value `true` with an `xsd:boolean` datatype results in perfectly valid RDF. This means that client software using triples with a `schema:dateCreated` predicate cannot safely assume that its value will be a DateTime. So if the client wants to use `schema:dateCreated` values, the client must also specify which type of data it expects, check the datetype field of every Atom and provide logic for when these don't match.
- Using full URI strings as keys (in predicates) results in clunky Developer Experience, compared to the short strings that developers are used to in pretty much all languages and data formats. Adding a required / tightly integrated key mapping (from long URLs to short, simple strings) in Atomic Properties solves this issue, and provides developers a way to write code like this: `someAtomicPerson.bestFriend.name => "Britta"`. Although the RDF ecosystem does have some solutions for this (@context objects in JSON-LD, @prefix mappings, the @ontologies library), these prefixes are not defined in Properties themselves and therefore are defined locally only, which means that developers have to manually map them most of the time.
- RDF lacks a clear solution for dealing with [ordered data](https://ontola.io/blog/ordered-data-in-rdf/), resulting in confusion when developers have to create lists of content. Adding an Array data type as a base data type helps solve this.
- There is no integrated standard for communicating state changes (although [linked-delta](https://github.com/ontola/linked-delta) and [rdf-delta](https://afs.github.io/rdf-delta/) do exist)
- RDF allows that domain A creates statements about domain B. This means that someone using RDF data about domain B cannot know that domain B is actually the source of the data. Knowing _where data comes from_ is one of the great things about URIs, but RDF does not require that you can think of subjects as the source of data. Many subjects in RDF don't actually resolve to all the known triples of the statement. It would make the conceptual model way simpler if statements about a subject could only be made from the source of the domain owner of the subject.
- RDF allows any type of URIs for `subject` and `predicate` value, which means they can be URLs, but don't have to be. This means they don't always resolve, or even function as locators. The links don't work, and that restricts how useful the links are. Atomic Data takes a different approach: these links MUST Resolve. Requiring that is part of what enables the type system of Atomic Schema.

Besides these technical reasons about the RDF model, I think that there are more reasons to start with a new concept and give it a new name:

- The RDF documentation is intimidating for beginners. When trying to understand RDF, you're likely to traverse. All Core / Schema URLs should resolve to simple, clear explanations with both examples and machine readable definitions.
- There is a lack of learning resources that provide a clear, complete answer to the lifecycle of RDF data: modelling data, making data, hosting it, fetching it, updating it. Atomic Data aims to provide an opinionated answer to all of these steps.
- The Semantic Web community has had a lot of academic attention from formal logic departments, resulting in a highly developed standard for knowledge modelling: the Web Ontology Language (OWL). While this is mostly great, its open-world philosophy and focus on reasoning abilities can confuse developers who are simply looking for a simple way to share models in RDF.
<!-- - Re-using predicate URIs in new contexts can be result in unclear descriptions, since the meaning of predicates can be very class-dependent. For examle, a `name` for a Person means something else than a `name` for a  -->

## Convert Atomic data to RDF

Since all Atomic Data is also valid RDF, it's trivial to convert / serialize Atoms to RDF.

- In conversion to RDF, convert `langstring` objects to Literals with an `xsd:string` datatype

## Convert RDF to Atomic Data

- All `predicates` SHOULD resolve to Atomic Properties, and these SHOULD have a `datatype`. This means that the `datatype` in the original RDF statement can be dropped.
- Literals with a `language` tag are converted to the `atomic:langstring` type. TODO! How to fis
