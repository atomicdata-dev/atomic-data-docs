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

```ndjson
["https://example.com/people/123", "https://example.com/name", "John"]
["https://example.com/people/123", "https://somepage.example.com/name", "John"]
```

Let's assume that `https://somepage.example.com/name` and `https://example.com/name` are Properties that have the Shortname: `name`.

What if a client tries something such as `people123.name`?
To consistently return a single value, we need some form or precedence, and it goes like this:

1. The earlier Class mentioned in the `class` Property of the resource. Resources can have multiple classes, but they appear in an ordered ResourceArray. Classes, internally SHOULD have no key collisions in required and recommended properties, which means that they might have. If these exist internally, sort the properties from A-Z.
<!-- This  -->
1. When the Properties are not part of any of the mentioned Classes, use Alphabetical sorting of the Property URL.

When shortname collisions are possible, it's recommended to not use the shortname, but use the URL of the Property:

```
people123."https://example.com/name"
```

## Atomic Data uses a lot of links. How do you deal with links that don't work?

1. Use URIs schemes that use content dressing, such as IPFS URIs.

## What's a URI, and what's a URL?

URI stands for Unique Resource Identifier
