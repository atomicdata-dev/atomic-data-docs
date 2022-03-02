# 5 Levels of data usability

Not all data are created equal.
There are notable differences in how much you can do with data, how flexible it is.
The more usable data is, the easier it will be to re-use it for developer, researcher or other type of data user.

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
A human needs to make


- Requires human interpretation
- No semantic definitions of what properties represent
- Can be readed by machines if mapped correctly
- Often requires handling invalid data

```json
{
  "name": "Joep",
  "birthYear": ""
}
```

## Level 3: type-safe data

_Examples: SQL + DB SCHEMA, JSON + JSON schema, XSD + XML, RDF + SHACL_

Type-safe data means that every value of the data has an explicit datatype, and that these datatypes can be constrained.
This means that someone re-using this data can know for certain that it conforms to a certain specification, a set of rules.
The shape of the data is predictable.


```json
{
  "https://atomicdata.dev/properties/name": "Joep",
  "https://atomicdata.dev/properties/birthYear": 1991
}
```

## Level 4: browsable data

_Examples: Atomic Data_

If your data is _connected_ to other pieces of machine-readable dat, is becomes browsable, similar to how websites link to each other.
This effectively creates a _web of data_, and allows for a whole new way to think about the internet.
This is what allows decentralized applications, true data ownership, and a new set of applications.

- Is connected to other pieces of machine verifiable data
