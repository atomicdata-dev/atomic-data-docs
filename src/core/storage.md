# Storing Atomic Data

## Schema Completeness

When a Graph has a set of Atoms, it might not posess all the information that is required to determine the datatype of each Atom.
When that is the case, we say the Graph is _Schema Complete_.

Imagine some application (perhaps an app running inside a webbrowser) that has only the following data:

```ndjson
["https://example.com/john","https://example.com/birthDate","1991-01-20"]
```

Now, by looking at this single Atom, we might assume that the Object is an ISO date,
but this type information is not known yet to the application.
This type information should be specified in the `example:birthDate` Property.
It is the responsibility of the application to make sure it posesses the required Schema data.

We say a Graph is _Schema Complete_ when it contains _at least_ all the Properties that are used in predicates.

So let's add the missing Property: `https://example.com/birthDate`

```ndjson
["https://example.com/john","https://example.com/birthDate","1991-01-20"]
["https://example.com/birthDate","https://atomicdata.dev/datatypes/Datatype","https://atomicdata.dev/datatypes/dateTime"]
```

Now, since we've introduced yet another Property, we need to include that one as well:

```ndjson
["https://example.com/john","https://example.com/birthDate","1991-01-20"]
["https://example.com/birthDate","https://atomicdata.dev/datatypes/Datatype","https://atomicdata.dev/datatypes/dateTime"]
["https://atomicdata.dev/datatypes/Datatype","https://atomicdata.dev/datatypes/Datatype","https://atomicdata.dev/datatypes/atomicURI"]
```

Since all valid Atomic Data requires predicates to resolve to Atomic Properties, which are required to have an associated DataType...
We can safely say that the last atom in the example above (the one describing `https://atomicdata.dev/datatypes/Datatype`) will have to be present in all Schema Complete Atomic Graphs.
