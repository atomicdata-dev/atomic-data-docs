# Atomic Data and Graph Databases

Atomic Data fundamentally is a _graph data model_.
We can think of Atomic Resources as _nodes_, and links to other resources through _properties_ as _edges_.

In this section, we'll explore how Atomic Data relates to some graph technologies.

## Comparing Atomic Data to Neo4j

Neo4j is a popular graph database that supports multiple query languages.
The first difference is that Atomic Data is not a single piece of software but a _specification_.
However, we can compare Neo4j as a _product_ with the open source [Atomic-Server](https://crates.io/crates/atomic-server).
Atomic-Server is fully open source and free (MIT licensed), whereas Neo4j is partially open source and GPL licensed.

### Labeled Property Graph

The data model of Neo4j features a _labeled property graph_, which means that edges (relationships between nodes) can have their own properties.
This can be useful when adding data to relationship between nodes.
For example: in the `john - (knows) -> mary` relationship, you might want to specify _for how long_ they have known each other.
In Neo4j, we can add this data to the labeled property graph.

In Atomic Data, we'd have to make a new resource to describe the relation between the two, if we wanted to add information about the relationship itself.
This is called _reification_.
This process can be time consuming, especially in Atomic Data, as this means that you'll have to specify the Class of this relationship and its properties.
However, one benefit of this approach, is that the relationship itself becomes clearly defined and re-usable.
Another benefit is that the simpler model of Atomic Data maps perfectly to datamodels like JSON, which makes things very convenient and familiar for developers.

### Query language vs REST

Neo4j supports multiple query languages, but its mainly known for _Cypher_.
It is used for doing practically everything: reading, writing, modelling, and more.

Atomic Data on the other hand does not have a query language.
It uses a RESTful HTTP + JSON-AD approach for everything.
Atomic Data uses [Endpoints](../endpoints.md) for specific goals that you'd do in a query language:

 - [Collections](../schema/collections.md) (which can filter by Property or Value, and sort by any Property) to generate lists of resources
 - [Paths](../core/paths.md) for traversing graphs by property

And finally, data is written using [Commits](../commits/intro.md).
Commits are very strict, as each one describes modifications to individual resources, and every Commits has to be signed.
This means that with Atomic Data, we get _versioning + audit trails_ for all data, but at the cost of more storage requirements and a bit more expensive write process.

### Schema language and type safety

In Neo4j, constraints can be added to the database by
Atomic Data uses Atomic Schema for validating datatypes and required properties in resources.

### Other differences

- Atomic Data has an [Authentication model](../agents.md) and [Hierarchy model](../hierarchy.md) for authorization. Neo4j uses [roles](https://neo4j.com/docs/operations-manual/current/authentication-authorization/built-in-roles/#auth-built-in-roles).
- Neo4j is actually used in production by many big organizations
