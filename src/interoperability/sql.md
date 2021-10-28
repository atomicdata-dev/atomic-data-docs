{{#title How does Atomic Data relate to SQL?}}
# Atomic Data and SQL

Atomic Data has some characteristics that make it similar and different from SQL.

- Atomic Data has a _dynamic_ schema. Any Resource could have different properties. However, the properties themselves are validated (contrary to most NOSQL solutions)
- Atomic Data separates _reading_ and _writing_, whereas SQL has one language for both.
- Atomic Data has a standardized way of storing changes ([Commits](../commits/intro.md))

## Tables and Rows vs. Classes and Properties

At its core, SQL is a query language based around _tables_ and _rows_.
The _tables_ in SQL are similar to `Classes` in Atomic Data: they both define a set of `properties` which an item could have.
Every single item in a table is called a _row_ in SQL, and a `Resource` in Atomic Data.

## Identifiers: numbers vs. URLs

In SQL, rows have numbers as identifiers, whereas in Atomic Data, every resource has a resolvable HTTP URL as an identifier.
This allows Atomic Data records to be easily re-used by other systems, as there is a guarantee that identifiers will be globally unique.

## Dynamic vs static schema

In SQL, the schema of the database defines which shape the data can have, which properties are required, what datatypes they have.
In Atomic Data, the schema exists as a Resource on the web, which means that they can be retrieved using HTTP.
An Atomic Database (such as [Atomic-Server](https://crates.io/crates/atomic-server)) uses a _dynamic schema_,
which means that any Resource can have different properties, and the properties themselves can be validated, even when the server is not aware of these properties beforehand.
In SQL, you'd have to manually adjust the schema of your database to add a new property.
Atomic Data is a decentralized, open system, which can read new schema data from other sources.
SQL is a centralized, closed system, which relies on the DB manager to define the schema.

## Querying

The SQL query language is for both _reading_ and _writing_ data.
In Atomic Data a distinction is made between Query and Command - getting and setting (Command Query Responsibility Segregation, [CQRS](https://martinfowler.com/bliki/CQRS.html)).
The [Query side](../core/querying.md) is handled using Subject Fetching (sending a GET request to a URL, to get a single resource) and [Collections](../schema/collections.md) (filtering and sorting data).
The Command side is typically done using [Atomic Commits](../commits/intro.md), although you're free not to use it.

SQL is way more powerful, as a query language.
In SQL, the one creating the query basically defines the shape of a table that is requested, and the database returns that shape.
Atomic Data does not offer such functionality.
So if you need to create custom tables at runtime, you might be better off using SQL, or move your Atomic Data to a query system.

## FAQ

### Is Atomic Data NOSQL or SQL?

Generally, Atomic Data apps do not use SQL - so they are NOSQL.
Atomic-server, for example, internally uses a key-value store (sled) for persistence.

Like most NOSQL systems, Atomic Data does not limit data entries to a specific table shape, so you can add any property that you like to a resource.
However, unlike most NOSQL systems, Atomic Data _does_ perform validations on each value.
So in a way, Atomic Data tries to combine best of both worlds: the extendibility and flexibility of NOSQL, with the type safety of SQL.

### Is Atomic Data transactional / ACID?

Yes, if you use Atomic-Server, then you can only write to the server by using Atomic Commits, which are in fact transactions.
This means that if part of the transaction fails, it is reverted - transactions are only applied when they are 100% OK.
This prevents inconsistent DB states.

### Can I use a SQL database with Atomic Data?

Yes, if you want to make your existing project serve Atomic Data, you can keep your existing SQL database, see [the upgrade guide](upgrade.md).
When you want to _import arbitrary Atomic Data_, it might be easier to use `atomic-server`.
If you want to store arbitrary Atomic Data in a SQL database, you might be best off by creating a `Resources` table with a `subject` and a `propertyValues` column, or create both a `properties` table and a `resources` one.
