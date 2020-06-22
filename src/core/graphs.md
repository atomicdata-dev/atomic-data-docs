# Types of Atomic Graphs

An Graph is a set of Atoms.
Since Atomic Data is desgigned to facilitate decentralized data storage, Graphs will often lack information or contain invalid data.
In this section, we define some of these aspects of Graphs.

- A **Valid Graph** contains no mismatches between Datatypes from Properties and their usage in Atoms
- A **Closed Graph** contains no unfetched outgoing links
- A **Verified Graph** contains only Atoms from a verified Author
- A **Schema Complete Graph** contains all used linked Properties

These concepts are important when creating an implementation of a Store.

## Valid Graphs

We refer to a Graph as Valid, if the following constraints are met:

- **The Datatypes are correctly used**. The Graph does not contain Atoms where the Datatype of the Object does not match the Datatype of the Property of the Atom.
- **The links work**. All URLs used in the Graph (Subject, Predicate, Object) resolve correctly to the required Datatype.
- **The Class Restrictions are met**. If a Class sets required properties, these must be present in Resources that are instances of that Class.

Making sure Graphs are Valid is of great imporance to anyone creating, sharing or using Atomic Data.
Services should specify whether they check the validity of graphs.

## Closed Graph

A Graph is Closed, when the Resources of all URLs are present in the Graph.
In other words, if you were to fetch and download every single URL in a Graph, you would not have any more Atoms than before.
Closed Graphs are _rarely_ required, it's often perfectly fine to have outgoing links that do not have been fetched.

## Schema Complete Graphs

When a Graph has a set of Atoms, it might not posess all the information that is required to determine the datatype of each Atom.
When that is the case, we say the Graph is _Schema Complete_.

Having a Schema Complete Graph is essential for determining what the Datatype is of an Object.
Most implementations of Atomic Data will need Schema Completenss to create fitting views, or apply functinoal business logic.

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
