# Atomic Data Overview

_Status: early draft, far from usable. [Feedback welcome](https://github.com/ontola/atomic-data)._

Atomic Data is a standard for exchanging data.
It uses links to connect pieces of data, and therefore makes it easier to connect datasets to each other.
It is heavily inspired by linked data, but more constrained than RDF triple.
It is typed and extendible through Atomic Schema, which means that you can use it to define your own Classes and Datatypes.
Atomic Data also has a standard for synchronizing data by communicating state changes, called [Atomic Mutations]().

Atomic Data is accompanies by a Schema and Mutations standard, which respectively deal with a modelling / type system, and communicating state changes.

- [Atomic Data Core](core/atomic-data-core.md): the core model for typed, linked data
- [Atomic Schema](schema/atomic-schema.md): defining properties, datatypes and classes
- [Atomic Mutations](mutations/atomic-mutations.md): sharing state changes
