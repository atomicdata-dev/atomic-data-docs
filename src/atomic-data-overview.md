# Atomic Data Overview

_Status: early draft, far from usable. [Feedback welcome](get-involved.md)._

Atomic Data is a propsed standard for modelling and exchanging data.
It uses links to connect pieces of data, and therefore makes it easier to connect datasets to each other - even when these datasets exist on seperate machines.
Atomic Data is heavily inspired by [Linked Data](https://ontola.io/what-is-linked-data/), and can be thought of as a more strict subset of RDF.
Atomic Data is typed (you know if something is a `string`, `number`, `URL`, etc.) and extensible through [Atomic Schema](schema/intro.md), which means that you can define your own Classes, Properties and Datatypes.
Atomic Data has a standard for synchronizing data by communicating state changes, called [Atomic Mutations](mutations/intro.md).
You can use parts of Atomic Data separately, but the standard is designed as a full data management package that makes it easier to create, share and use structured data on the web.

- [Atomic Data Core](core/intro.md): the core model for typed, Linked Data
- [Atomic Schema](schema/intro.md): defining properties, datatypes and classes
- [Atomic Mutations](mutations/intro.md): sharing state changes, verifying changes and collaboration
