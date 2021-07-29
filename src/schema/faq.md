# Atomic Schema FAQ

## How do I create a Property that supports multiple Datatypes?

A property only has one single Datatype.
However, feel free to create a new kind of Datatype that, in turn, refers to other Datatypes.
Perhaps Generics, or Option like types should be part of the Atomic Base Datatypes.

## How should a client deal with Shortname collisions?

Atomic Data guarantees Subject-Property uniqueness, which means that Valid Resources are guaranteed to have only one of each Property.
Properties offer Shortnames, which are short strings.
These strings SHOULD be unique inside Classes, but these are not guaranteed to be unique inside all Resources.
Note that Resources can have multiple Classes, and through that, they can have colliding Shortnames.
Resources are also free to include Properties from other Classes, and their Shortnames, too, might collide.

For example:

```json
{
  "@id": "https://example.com/people/123",
  "https://example.com/name": "John",
  "https://another.example.com/someOtherName": "Martin"
}
```

Let's assume that `https://example.com/name` and `https://another.example.com/someOtherName` are Properties that have the Shortname: `name`.

What if a client tries something such as `people123.name`?
To consistently return a single value, we need some type of _precedence_:

1. The earlier Class mentioned in the [`isA`](https://atomicdata.dev/properties/isA) Property of the resource. Resources can have multiple classes, but they appear in an ordered ResourceArray. Classes, internally SHOULD have no key collisions in required and recommended properties, which means that they might have. If these exist internally, sort the properties by how they are ordered in the `isA` array - first item is preferred.
1. When the Properties are not part of any of the mentioned Classes, use Alphabetical sorting of the Property URL.

When shortname collisions are possible, it's recommended to not use the shortname, but use the URL of the Property:

```
people123."https://example.com/name"
```

It is likely that using the URL for keys is also the most _performant_, since it probably more closely mimics the internal data model.

## Atomic Data uses a lot of links. How do you deal with links that don't work?

Many features in Atomic Data apps depend on the availability of Resources on their subject URL.
If that server is offline, or the URL has changed, the existing links will break.
This is a fundamental problem to HTTP, and not unique to Atomic Data.
Like with websites, hosts should make sure that their server stays available, and that URLs remain static.

One possible solution to this problem, is using Content Addressing, such as the [IPFS](../interoperability/ipfs.md) protocol enables, which is why we're planning for using that in the near future.

Another approach, is using [foreign keys (see issue)](https://github.com/ontola/atomic-data-docs/issues/43).

## How does Atomic Schema relate to RDF / SHACL / SheX / OWL / RDFS?

Atomic Schema is _the_ schema language for atomic data, whereas RDF has a couple of competing ones, which all vary greatly.
In short, OWL is not designed for schema validation, but SHACL and SheX can maybe be compared to Atomic Schema.
An important difference is that SHACL and SheX have to deal with all the complexities of RDF, whereas Atomic Data is more constrained.

For more information, see [RDF interoperability](../interoperability/rdf.md).
