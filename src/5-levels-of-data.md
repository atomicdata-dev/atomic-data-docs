# 5 Levels of data reusability

Not all data are created equal.
There are notable differences in how much you can do with data, how flexible it is.
The more reusable data is, the easier it will be to use it as a developer, researcher or other type of data user.

_This list is inspired by Tim Berners-Lee's [5-star open data](https://5stardata.info/en/)_.

## Level 1: unstructured data

_Examples: images, videos, plain text_

Unstructured data is the least usable.
Humans can read it, and AI / Machine Learning systems can draw more conclusions from it then ever,
but it's hard to build an actual application or graphic from only unstructured data.

```
Hi! I'm Joep, I'm born in 1991.
```

## Level 2: structured data

_Examples: CSV, XML, JSON, TOML, EXCEL_

Structured data can be read by machines, and this allows us to do all sorts of useful things.
We can _query_, _sort_ and _filter_.
But still, this type of data often requires human input when it needs to be processed.
And we don't have guarantees about which fields will be filled, or what their datatypes are.
One time, a `birthYear` can be a string, and the next time it can be a number.
Data can be _structured_, but still _unpredictable_.

```json
{
  "name": "Joep",
  "birthYear": 1991
}
```

If we want predictability, we need to make it _type-safe_.

## Level 3: type-safe data

_Examples: SQL + DB SCHEMA, JSON + JSON schema, XSD + XML, RDF + SHACL, In-memory data in type-safe programming langauges_

Type-safe data means that every value of the data has an explicit datatype.
It is _strongly typed_ and has a clear _schema_ that describes which properties you can expect in a Resource.
This means that someone re-using type-safe data can know for certain that it conforms to a specification, a set of rules.
The shape of the data is _predictable_.
This predictability means that developers can safely re-use it in their system without worrying about missing fields or datatype errors.

Lots of software has _internal_ type safety, especially if you use type-safe programming langauges like Typescript, Kotlin or Rust.
However, when the data _leaves the system_, a lot of type related data is lost.
Even if this schema related information is described, the schema itself is often not machine-readable.
The best way to have type-safe data, is to describe the schema in a machine-readable format.

In Atomic Data, the Properties themselves (the links in the keys in JSON-AD) describe the datatypes, which helps developers when re-using data.

```json
{
  "https://atomicdata.dev/properties/name": "Joep",
  "https://atomicdata.dev/properties/birthYear": 1991,
  "https://atomicdata.dev/properties/worksOn": "Atomic Data",
}
```

## Level 4: browsable data

_Examples: Atomic Data_

If your data is _connected_ to other pieces of machine-readable dat, is becomes browsable, similar to how websites link to each other.
This effectively creates a _web of data_, and allows for a whole new way to think about the internet.
This is what allows decentralized applications, true data ownership, and a new set of applications.

```json
{
  "https://atomicdata.dev/properties/name": "Joep",
  "https://atomicdata.dev/properties/birthYear": 1991,
  "https://atomicdata.dev/properties/worksOn": "https://atomicdata.dev",
}
```

## Level 5: verifiable data

_Examples: Atomic Data + Atomic Commits_

When your data is _verifiable_, other people can verify who created it and modified it.
They can use cryptography to validate signatures, which proves that one person or machine created a piece of data.

```json
{
  "https://atomicdata.dev/properties/name": "Joep",
  "https://atomicdata.dev/properties/birthYear": 1991,
  "https://atomicdata.dev/properties/worksOn": "https://atomicdata.dev",
  "https://atomicdata.dev/properties/previousCommit": "https://atomicdata.dev/commits/EF18751AE781",
}
```
