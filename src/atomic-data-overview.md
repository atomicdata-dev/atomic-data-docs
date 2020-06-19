# Atomic Data Overview

_Status: early draft, far from usable. [Feedback welcome](get-involved.md)._

Atomic Data is a standard for modelling and exchanging data.
It uses links to connect pieces of data, and therefore makes it easier to connect datasets to each other.
It is heavily inspired by linked data, but Atomic Data has some stricter requirements that aim to make it easier to use for developers.
It is typed and extendible through [Atomic Schema](schema/atomic-schema.md), which means that you can define your own Classes and Datatypes.
Atomic Data also has a standard for synchronizing data by communicating state changes, called [Atomic Mutations](mutations/atomic-mutations.md).
You can use parts of Atomic Data seperately, but the standard is designed as a full data management package that makes it easier to create, share and use structured data on the web.

- [Atomic Data Core](core/atomic-data-core.md): the core model for typed, linked data
- [Atomic Schema](schema/atomic-schema.md): defining properties, datatypes and classes
- [Atomic Mutations](mutations/atomic-mutations.md): sharing state changes
