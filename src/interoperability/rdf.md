# How does Atomic Data relate to RDF?

RDF is the original data model behind linked data.
It is also the forerunner of Atomic Data, and is therefore highly similar in its philosophy and model.
Both heavily rely on using URLs, and both have a fundamentally simple and uniform model for data statements.
Both view the web as a single, connected graph database.
Because of that, Atomic Data is also highly compatible with RDF - **all Atomic Data can be converted into valid RDF**.
Atomic Data can be thought of as a **more constrained, type safe version of RDF**.
However, it does differ in some fundamental ways.

- Atomic calls the three parts of a Triple `subject`, `property` and `value`, instead of `subject`, `predicate`, `object`.
- Atomic requires URL (not URI) values in its `subjects` and `predicates` (properties), which means that they should be resolvable.
- Atomic only allows those who control a resource's `subject` URL endpoint to edit the data. This means that you can't add triples about something that you don't control.
- Atomic has no separate `datatype` field, but it requires that `Properties` (the resources that are shown when you follow a `predicate` value) specify a datatype
- Atomic has no separate `language` field, but it does support language strings as a Datatype in Properties.
- Atomic has a native Event (state changes) model ([Atomic Mutations](../mutations/intro.md)), which enables communication of state changes
- Atomic has a native Schema model ([Atomic Schema](../schema/intro.md)), which helps developers to know what data types they can expect (string, integer, link, array)
- Atomic does not support `graph` fields in statements.
- Atomic does not support `blank nodes`.

- Atomic does not support having multiple statements with the same `<subject> <predicate>`, every combination should be unique.

## Why these changes?

I love RDF, and have been working with it for quite some time now.
Using URIs (and more-so URLs, which are URIs that can be fetched) for everything is a great idea, since it helps with interoperability and enables truly decentralized knowledge graphs.
However, some of the characteristics of RDF might have contributed to its relative lack of adoption.

- RDF's `subject`, `predicate` and `object` terminology can be confusing to newcomers, so Atomic Data uses `subject`, `property`, `value`. This more closely resembles known CS terminology. ([discussion](https://github.com/ontola/atomic-data/issues/3))
- Having both a `datatype` and a `predicate` value can lead to confusing situations. For example, the [`schema:dateCreated`](https://schema.org/dateCreated) Property requires an ISO DateTime string (according to the schema.org definition), but using a value `true` with an `xsd:boolean` datatype results in perfectly valid RDF. This means that client software using triples with a `schema:dateCreated` predicate cannot safely assume that its value will be a DateTime. So if the client wants to use `schema:dateCreated` values, the client must also specify which type of data it expects, check the datatype field of every Atom and provide logic for when these don't match. Also important: developers tend to combine these two concepts into one - just look at how every single struct / model / class / shape is defined in programming languages: `key: datatype`. This is why Atomic Data requires that a `predicate` links to a Property which must have a `Datatype`.
- Using full URI strings as keys (in RDF `predicates`) results in a relatively clunky Developer Experience. Consider the short strings that developers are used to in pretty much all languages and data formats (`object.attribute`). Adding a _required_ / tightly integrated key mapping (from long URLs to short, simple strings) in Atomic Properties solves this issue, and provides developers a way to write code like this: `someAtomicPerson.bestFriend.name => "Britta"`. Although the RDF ecosystem does have some solutions for this (@context objects in JSON-LD, @prefix mappings, the @ontologies library), these prefixes are not defined in Properties themselves and therefore are defined locally only, which means that developers have to manually map them most of the time. This is why Atomic Data introduces a `shortname` field in Properties, which forces modellers to choose a 'key' that can be used in ORM contexts.
- RDF lacks a clear solution for dealing with [ordered data](https://ontola.io/blog/ordered-data-in-rdf/), resulting in confusion when developers have to create lists of content. Adding an Array data type as a base data type helps solve this. ([discussion](https://github.com/ontola/atomic-data/issues/4))
- There is no integrated standard for communicating state changes. Although [linked-delta](https://github.com/ontola/linked-delta) and [rdf-delta](https://afs.github.io/rdf-delta/) do exist, they aren't referred to by the RDF spec. I think developers need guidance when learning a new system such as RDF, and that's why [Atomic Mutations](../mutations/intro.md) is included in this book.
- RDF allows that `anne` creates statements about the subject `john`. The reasoning behind this, was that it was possible to say things about thingsIn other words, domain A creates statements about domain B. This means that someone using RDF data about domain B cannot know that domain B is actually the source of the data. Knowing _where data comes from_ is one of the great things about URIs, but RDF does not require that you can think of subjects as the source of data. Many subjects in RDF don't actually resolve to all the known triples of the statement. It would make the conceptual model way simpler if statements about a subject could only be made from the source of the domain owner of the subject.
- RDF allows blank nodes, Atomic Data does not. They make things easier for content providers, but make things [harder for content consumers](http://richard.cyganiak.de/blog/2011/03/blank-nodes-considered-harmful/). They severely limit how client systems can store the data, as name collisions with blank nodes are very possible. They make sense in hand-written Turtle files, but that argument doesn't hold for systems that create the data (and the identifiers) for you. It's very much possible to design systems that create reliable URLs without any overhead for the data creator.
- RDF allows any type of URIs for `subject` and `predicate` value, which means they can be URLs, but don't have to be. This means they don't always resolve, or even function as locators. The links don't work, and that restricts how useful the links are. Atomic Data takes a different approach: these links MUST Resolve. Requiring that is part of what enables the type system of Atomic Schema
- Validating RDF graphs is hard. Validating both the _shape_ (whether required fields are present) of RDF data, as well as its _authenticity_ (whether we can trust the individual Statements) is complex. Shape validations are possible using both [SHACL](https://www.w3.org/TR/shacl/) and [SHEX](https://shex.io/), and they are both very powerful and well designed.

Besides these technical reasons about the RDF model, I think that there are more reasons to start with a new concept and give it a new name:

- The RDF documentation is intimidating for beginners. When trying to understand RDF, you're likely to traverse. All Core / Schema URLs should resolve to simple, clear explanations with both examples and machine readable definitions.
- There is a lack of learning resources that provide a clear, complete answer to the lifecycle of RDF data: modeling data, making data, hosting it, fetching it, updating it. Atomic Data aims to provide an opinionated answer to all of these steps.
- The Semantic Web community has had a lot of academic attention from formal logic departments, resulting in a highly developed standard for knowledge modeling: the Web Ontology Language (OWL). While this is mostly great, its open-world philosophy and focus on reasoning abilities can confuse developers who are simply looking for a simple way to share models in RDF.
<!-- - Re-using predicate URIs in new contexts can be result in unclear descriptions, since the meaning of predicates can be very class-dependent. For example, a `name` for a Person means something else than a `name` for a  -->

## Convert Atomic data to RDF

Since all Atomic Data is also valid RDF, it's trivial to convert / serialize Atoms to RDF.

- Convert Atoms with linked `LangString` Resources to Literals with an `xsd:string` datatype and the corresponding language in the tag.

## Convert RDF to Atomic Data

- You need to make sure that all the subject URLs will actually resolve. Atomic Data tools might help to achieve this, for example by hosting the data.
- All `predicates` SHOULD resolve to Atomic Properties, and these SHOULD have a `datatype`. You will probably need to change predicate URLs to Atomic Property URLs, or update the things that the predicate points to to include the required Atomic Property items (e.g. having a Datatype and a Shortname). This also means that the `datatype` in the original RDF statement can be dropped.
- Literals with a `language` tag are converted to LangString resources, which also means their identifiers must be created. Keep in mind that Atomic Data does not allow for blank nodes, so the LangString identifiers must be URLs.
