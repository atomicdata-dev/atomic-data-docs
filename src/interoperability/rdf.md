# How does Atomic Data relate to RDF?

RDF (the [Resource Description Framework](https://www.w3.org/TR/rdf-primer/)) is a W3C specification from 1999 that describes the original data model for linked data.
It is the forerunner of Atomic Data, and is therefore highly similar in its model.
Both heavily rely on using URLs, and both have a fundamentally simple and uniform model for data statements.
Both view the web as a single, connected graph database.
Because of that, Atomic Data is also highly compatible with RDF - **all Atomic Data can be converted into valid RDF**.
Atomic Data can be thought of as a **more constrained, type safe version of RDF**.
However, it does differ in some fundamental ways.

- Atomic calls the three parts of a Triple `subject`, `property` and `value`, instead of `subject`, `predicate`, `object`.
- Atomic does not support having multiple statements with the same `<subject> <predicate>`, every combination should be unique.
- Atomic has no difference between `literal`, `named node` and `blank node` objects - these are all `values`, but with different datatypes.
- Atomic does not support `blank nodes`.
- Atomic requires URL (not URI) values in its `subjects` and `predicates` (properties), which means that they should be resolvable.
- Atomic only allows those who control a resource's `subject` URL endpoint to edit the data. This means that you can't add triples about something that you don't control.
- Atomic has no separate `datatype` field, but it requires that `Properties` (the resources that are shown when you follow a `predicate` value) specify a datatype
- Atomic has no separate `language` field, but it does support [Translation Resources](../schema/translations.md).
- Atomic has a native Event (state changes) model ([Atomic Mutations](../mutations/intro.md)), which enables communication of state changes
- Atomic has a native Schema model ([Atomic Schema](../schema/intro.md)), which helps developers to know what data types they can expect (string, integer, link, array)

## Why these changes?

I love RDF, and have been working with it for quite some time now.
Using URIs (and more-so URLs, which are URIs that can be fetched) for everything is a great idea, since it helps with interoperability and enables truly decentralized knowledge graphs.
However, some of the characteristics of RDF might have contributed to its relative lack of adoption.

### Difficulty in selecting values

One of the main reasons for having more strict requirements, has to do with how hard it is to identify a specific value (`object`) in RDF.
For example, let's say I want to render someone's birthday:

```ttl
<example:joep> <schema:birthDate> "1991-01-20"^^xsd:date
```

Rendering this item might be as simple as fetching the subject, taking the predicate, parse it as a date.
However, this is also valid RDF:

```ttl
<example:joep> <schema:birthDate> "1991-01-20"^^xsd:date <example:someNamedGraph>
<example:joep> <schema:birthDate> <example:birthDateObject> <example:someNamedGraph>
<example:joep> <schema:birthDate> "20th of januari 1991"@en <example:someNamedGraph>
<example:joep> <schema:birthDate> "20 januari 1991"@nl <example:someNamedGraph>
<example:joep> <schema:birthDate> "2000-02-30"^^xsd:date <example:someNamedGraph>
```

Now things get more complicated if you just want to render the birthdate:

```
1. **Select the named graph**. The triple containing that birthday may exist in some named graph, which means I first need to identify and fetch that graph.
1. **Select the subject**.
1. **Select the predicate**.
1. **Select the datatype**. You probably need a specific datatype (in this case, a Date), so you need to select all the triples that match that datatype.
1. **Select the language**. Same could be true for language, too, but that is not neessary in this birthdate example.
1. **Select the triple**. Even after all our previous selectors, we _still_ might have multiple values. How do I know which is the triple I'm supposed to use?
```

To be fair, with lots of RDF data, only steps 2 and 3 are needed.
But if you're building a system that uses RDF, that system also needs to deal with steps 1,4,5 and 6.
As a developer who uses RDF data, I want to be able to do something like this:

```js
// Fetches the resource
const joep = get("https://example.com/person/joep")

// Returns the value of the birthDate atom
console.log(joep.birthDate()) // => Date(1991-01-20)
// Fetches the employer relation at possibly some other domain, checks that resource for a property with the 'name' shortkey
console.log(joep.employer().name()) // => "Ontola.io"
```

Basically, I'd like to use all knowledge of the world as if it were a big JSON object.
You can't do that with RDF, as long as you add some constraints:

- Traverse data on various domains (which is already possible with RDF)
- Have [unique `subject-predicate` combinations](#subject-predicate-uniqueness)
- Map properties URLs to keys (which often requires local mapping with RDF)
- Link properties to datatypes

### Less focus on semantics, more on usability

One of the core ideas of the semantic web, is that anyone should be able to say anything about anything, using triples.
This is one of the reasons why it can be so hard to select a specific value in RDF.
When you want to make all graphs mergeable (which is a great idea), but also want to allow anyone to create any triples about any subject, you get `subject-predicate` non-uniqueness.
Atomic Data chooses a more constrained approach, which makes it easier to use the data, but at the cost of some expressiveness.

### Changing the names

RDF's `subject`, `predicate` and `object` terminology can be confusing to newcomers, so Atomic Data uses `subject`, `property`, `value`.
This more closely resembles common CS terminology. ([discussion](https://github.com/ontola/atomic-data/issues/3))

### Subject + Predicate uniqueness

In RDF, it's very much possible for a graph to contain multiple statements that share both a `subject` and a `predicate`.
One of the reasons this is possible, is because RDF graphs should always be mergeable.
However, this introduces some extra complexity for data users.
Whereas most languages and datatypes have `key-value` uniqueness that allow for unambiguous value selection, RDF clients have to deal with the possibility that multiple triples with the same `subject-predicate` combination might exist.

Atomic Data requires `subject-property` uniqueness, which means that this is no longer an issue for clients.
However, in order to guarantee this, and still retain _graph merge-ability_ we also need to limit who creates statements about a subject.

### Limiting subject usage

RDF allows that `anne.com` creates and hosts statements about the subject `john.com`.
In other words, domain A creates statements about domain B.
This means that someone using RDF data about domain B cannot know that domain B is actually the source of the data.
Knowing _where data comes from_ is one of the great things about URIs, but RDF does not require that you can think of subjects as the source of data. Many subjects in RDF don't actually resolve to all the known triples of the statement.
It would make the conceptual model way simpler if statements about a subject could only be made from the source of the domain owner of the subject.

### No more literals / named nodes

In RDF, an `object` can either be a `named node`, `blank node` or `literal`. A `literal` has a `value`, a `datatype` and an optional `language` (if the `literal` is a string).
Although RDF statements are often called `triples`, a single statement can consist of five fields: `subject`, `predicate`, `object`, `language`, `datatype`.
Having five fields is way more than most information systems. Usually we have just `key` and `value`.
This difference leads to compatibility issues when using RDF in applications.
In practice, clients have to run a lot of checks before they can use the data - which makes RDF in most contexts harder to use than something such as JSON.

Atomic Data drops the `named node` / `literal` distinction.
We just have `values`, and they are interpreted by looking at the `datatype`, which is defined in the `property`.
When a value is a URL, we don't call it a named node, but we simply use a URL datatype.

### Requiring URLs

RDF allows any type of URIs for `subject` and `predicate` value, which means they can be URLs, but don't have to be. This means they don't always resolve, or even function as locators. The links don't work, and that restricts how useful the links are. Atomic Data takes a different approach: these links MUST Resolve. Requiring Properties to resolve is part of what enables the type system of Atomic Schema - they provide the `shortname` and `datatype`.

Requiring URLs makes things easier for data users, at the cost of the data producer.
With Atomic Data, the data producer MUST offer the triples at the URL of the subject.
This is a challenge - especially with the current (lack of) tooling.

However - making sure that links _actually work_ offer tremendous benefits for data consumers, and that advantage is often worth the extra trouble.

### No more blank nodes

RDF allows `blank nodes` (resources with identifiers that exist only locally), Atomic Data does not.
They make things easier for content providers, but make things [harder for content consumers](http://richard.cyganiak.de/blog/2011/03/blank-nodes-considered-harmful/).
They severely limit how client systems can store data, as name collisions with blank nodes are possible and cache invalidation is hard (or impossible) with blank nodes.

Blank nodes make a lot of sense in hand-written RDF (e.g. Turtle) files.
However, that argument doesn't hold for systems that create the identifiers for you.
Although data creators _should_ have means to specify URLs for certain resources, they _should not_ have to specify every single one.
Ideally, the interface that you use as a data producer will create (persistent, resolvable) identifiers when you create the resources.

### Combining datatype and predicate

Having both a `datatype` and a `predicate` value can lead to confusing situations.
For example, the [`schema:dateCreated`](https://schema.org/dateCreated) Property requires an ISO DateTime string (according to the schema.org definition), but using a value `true` with an `xsd:boolean` datatype results in perfectly valid RDF.
This means that client software using triples with a `schema:dateCreated` predicate cannot safely assume that its value will be a DateTime.
So if the client wants to use `schema:dateCreated` values, the client must also specify which type of data it expects, check the datatype field of every Atom and provide logic for when these don't match.
Also important combining `datatype` and `predicate` fits the model of most programmers and languages better - just look at how every single struct / model / class / shape is defined in programming languages: `key: datatype`.
This is why Atomic Data requires that a `predicate` links to a Property which must have a `Datatype`.

### Adding shortnames (slugs / keys) in Properties

Using full URI strings as keys (in RDF `predicates`) results in a relatively clunky Developer Experience.
Consider the short strings that developers are used to in pretty much all languages and data formats (`object.attribute`).
Adding a _required_ / tightly integrated key mapping (from long URLs to short, simple strings) in Atomic Properties solves this issue, and provides developers a way to write code like this: `someAtomicPerson.bestFriend.name => "Britta"`.
Although the RDF ecosystem does have some solutions for this (@context objects in JSON-LD, @prefix mappings, the @ontologies library), these prefixes are not defined in Properties themselves and therefore are often defined locally or separate from the ontology, which means that developers have to manually map them most of the time.
This is why Atomic Data introduces a `shortname` field in Properties, which forces modelers to choose a 'key' that can be used in ORM contexts.

### Adding native arrays

RDF lacks a clear solution for dealing with [ordered data](https://ontola.io/blog/ordered-data-in-rdf/), resulting in confusion when developers have to create lists of content.
Adding an Array data type as a base data type helps solve this. ([discussion](https://github.com/ontola/atomic-data/issues/4))

### Adding a native mutation standard

There is no integrated standard for communicating state changes.
Although [linked-delta](https://github.com/ontola/linked-delta) and [rdf-delta](https://afs.github.io/rdf-delta/) do exist, they aren't referred to by the RDF spec.
I think developers need guidance when learning a new system such as RDF, and that's why [Atomic Mutations](../mutations/intro.md) is included in this book.

### Adding a schema language

Validating RDF graphs is hard. Validating both the _shape_ (whether required fields are present) of RDF data, as well as its _authenticity_ (whether we can trust the individual Statements) is complex. Shape validations are possible using both [SHACL](https://www.w3.org/TR/shacl/) and [SHEX](https://shex.io/), and they are both very powerful and well designed.

### A new name, with new docs

Besides the technical reasons described above, I think that there are social reasons to start with a new concept and give it a new name:

- The RDF vocabulary is intimidating. When trying to understand RDF, you're likely to traverse many pages with new concepts: `literal`, `named node`, `graph`, `predicate`, `named graph`, `blank node`... The core specification provides a formal description of these concepts, but fails to do this in a way that results in quick understanding and workable intuitions. Even experienced RDF developers tend to be confused about the nuances of the core model.
- There is a lack of learning resources that provide a clear, complete answer to the lifecycle of RDF data: modeling data, making data, hosting it, fetching it, updating it. Atomic Data aims to provide an opinionated answer to all of these steps. It feels more like a one-stop-shop for questions that developers are likely to encounter, whilst keeping the extendability.
- All Core / Schema URLs should resolve to simple, clear explanations with both examples and machine readable definitions. Especially the Property and Class concepts.
- The Semantic Web community has had a lot of academic attention from formal logic departments, resulting in a highly developed standard for knowledge modeling: the Web Ontology Language (OWL). While this is mostly great, its open-world philosophy and focus on reasoning abilities can confuse developers who are simply looking for a simple way to share models in RDF.

## Convert RDF to Atomic Data

- **All the `subject` URLs MUST actually resolve, and return all triples about that subject**. All `blank nodes` should be converted into URLs. Atomic Data tools might help to achieve this, for example by hosting the data.
- **All `predicates` SHOULD resolve to Atomic Properties, and these SHOULD have a `datatype`**. You will probably need to change predicate URLs to Atomic Property URLs, or update the things that the predicate points to to include the required Atomic Property items (e.g. having a Datatype and a Shortname). This also means that the `datatype` in the original RDF statement can be dropped.
- Literals with a `language` tag are converted to TranslationBox resources, which also means their identifiers must be created. Keep in mind that Atomic Data does not allow for blank nodes, so the TranslationBox identifiers must be URLs.

Step by step, it entails:

1. Set up some server to make sure the URLs will resolve.
1. Create (or find and refer to) Atomic Properties for all the `predicates`. Make sure they have a DataType and a Shortname.
1. If you have triples about a subject that you don't control, change the URL to some that you _can_ control, and refer to that external resource.

Atomic Data will need [tooling](../tooling.md) to facilitate in this process.
This tooling should help to create URLs, Properties, and host everything on an easy to use server.

## Convert Atomic data to RDF

Since all Atomic Data is also valid RDF, it's trivial to convert / serialize Atoms to RDF.
However, contrary to Atomic Data, RDF has optional Language and Datatype elements in every statement.
It is good practice to use these RDF concepts when serializing Atomic Data into Turtle / RDF/XML, or other [RDF serialization formats](https://ontola.io/blog/rdf-serialization-formats/).

- Convert Atoms with linked `TranslationBox` Resources to Literals with an `xsd:string` datatype and the corresponding language in the tag.
- Dereference the Property and Datatype from Atomic Properties, and add the URLs in `datatypes` in RDF statements.
