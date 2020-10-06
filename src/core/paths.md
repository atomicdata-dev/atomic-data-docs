# Atomic Paths

An Atomic Path is a string that consists of at least one URL, followed by one or more URLs or Shortnames.
Every single value in an Atomic Resource can be targeted through such a Path.
They can be used as identifiers for specific Values.

The simplest path, is the URL of a resource, which represents the entire Resource with all its properties.
If you want to target a specific atom, you can use an Atomic Path with a second URL.
This second URL can be replaced by a Shortname, if the Resource is an instance of a class which has properties with that shortname (sounds more complicated than it is).

## Example

Let's start with this simple graph:

```ad3
["https://example.com/john", "https://example.com/lastName", "McLovin"]
```

Then the following Path targets the `McLovin` value:

`https://example.com/john https://example.com/lastname` => `McLovin`

If the resource is an instance of a Class (an `atomic:isA` property), you can use the Shortnames of the Properties that are referred to by that class.
Since John is an instance of a Person, he might have a `lastname` which maps to `https://example.com/latname`.

`https://example.com/john lastname` => `McLovin`

We can also traverse relationships:

```ad3
["https://example.com/john", "https://atomicdata.dev/properties/isA", "https://example.com/Person"]
["https://example.com/john", "https://example.com/lastName", "McLovin"]
["https://example.com/john", "https://example.com/employer", "https://example.com/XCorp"]
["https://example.com/XCorp", "https://example.com/description", "The greatest company!"]
```

`https://example.com/john employer description` => `The greatest company!`

In the example above, the XCorp subject exists and is the source of the `The greatest company!` value.
However, using paths, it's also possible to created nested resources _without creating new URLs for all children_.

## Nested Resources

All Atomic Data Resources that we've discussed so far have a URL as a subject.
Unfortunately, creating unique and resolvable URLs can be a bother, and sometimes not necessary.
If you've worked with RDF, this is what Blank Nodes are used for.
In Atomic Data, we have something similar: _Nested Resources_.

Let's use a Nested Resource in the example from the previous section:

```ad3
["https://example.com/john", "https://example.com/lastName", "McLovin"]
["https://example.com/john https://example.com/employer", "https://example.com/description", "The greatest company!"]
```

By combining two Subject URLs into a single string, we've created a nested resource.
The Subjet of the nested resource is `https://example.com/john https://example.com/employer`, including the spacebar.

Note that the path from before still resolves:

`https://example.com/john employer description` => `The greatest company!`

Serialization formats are free to use nesting to denote paths - which means that it is not necessary to include these path strings explicitly in most serialization formats.

For example:

```json
{
  "@id": "https://example.com/john",
  "@context": "https://example.com/person",
  "hasShoes": [
    {
      "name": "Mr. Boot",
    },
    {
      "name": "Sunny Sandals",
    }
  ]
}
```

The Path of `Mr. Boot` is:

```
https://example.com/john hasShoes 1 name
```

This Path is useful for storing the value in other serialization formats, such as `.ad3`:

```ad3
["https://example.com/john https://example.com/hasShoes 0", "https://example.com/name", "Mr. Boot"]
["https://example.com/john https://example.com/hasShoes 1", "https://example.com/name", "Sunny Sandals"]
```

You can target an item in an array by using a number to indicate its position, starting with 0.

Notice how the Resource with the `name: Mr. Boot` does not have an explicit `@id`, but it _does_ have a Path.
