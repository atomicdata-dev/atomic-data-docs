# Atomic Data Overview

_Status: early draft, far from usable. [Feedback welcome](get-involved.md)._

Atomic Data is a standard for modelling and exchanging data.
It uses links to connect pieces of data, and therefore makes it easier to connect datasets to each other.
It is heavily inspired by linked data, but Atomic Data has some stricter requirements that aim to make it easier to use for developers.
It is typed and extendible through [Atomic Schema](schema/intro.md), which means that you can define your own Classes and Datatypes.
Atomic Data also has a standard for synchronizing data by communicating state changes, called [Atomic Mutations](mutations/intro.md).
You can use parts of Atomic Data seperately, but the standard is designed as a full data management package that makes it easier to create, share and use structured data on the web.

- [Atomic Data Core](core/intro.md): the core model for typed, linked data
- [Atomic Schema](schema/intro.md): defining properties, datatypes and classes
- [Atomic Mutations](mutations/intro.md): sharing state changes, verifying changes and collaboration
