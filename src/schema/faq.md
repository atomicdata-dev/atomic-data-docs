# Atomic Schema FAQ

## How do I create a Property that supports multiple Datatypes?

A property only has one single Datatype.
However, feel free to create a new kind of Datatype that, in turn, refers to other Datatypes.
Perhaps this should be part of the Atomic Base Datatypes.

Solutions:

- Generic datatype?

## How should a client deal with dot syntax key collisions?

Atomic Data guarantees `<subject> <property>` uniqueness, but when you're working on Atomic Data in an IDE / text editor, you're likely to use the `key` of the `Property`.

For example:

```ndjson
["https://example.com/people/123", "https://example.com/name", "John"]
["https://example.com/people/123", "https://somepage.example.com/name", "John"]
```

Let's assume that `https://somepage.example.com/name` and `https://example.com/name` are Properties that have a `key` with the object `name`.

```ndjson
["https://somepage.example.com/name"]
```

This

## Atomic Data uses a lot of links. How do you deal with links that don't work?

1. Use URIs schemes that use content adressing, such as IPFS URIs.

## What's a URI, and what's a URL?

URI stands for Unique Resource Identifier
