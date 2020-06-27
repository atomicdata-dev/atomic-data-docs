# Atomic Data Overview

_Status: early draft, far from usable. [Feedback welcome](get-involved.md)._

Atomic Data is a proposed standard for modeling and exchanging data.
It uses links to connect pieces of data, and therefore makes it easier to connect datasets to each other - even when these datasets exist on separate machines.
Atomic Data is heavily inspired by [Linked Data](https://ontola.io/what-is-linked-data/), and can be thought of as a more strict subset of RDF.
Atomic Data is typed (you know if something is a `string`, `number`, `URL`, etc.) and extensible through [Atomic Schema](schema/intro.md), which means that you can define your own Classes, Properties and Datatypes.
Atomic Data has a standard for synchronizing data by communicating state changes, called [Atomic Mutations](mutations/intro.md).
You can use parts of Atomic Data separately, but the standard is designed as a full data management package that makes it easier to create, share and use structured data on the web.

- [Atomic Data Core](core/intro.md): the core model for typed, Linked Data
- [Atomic Schema](schema/intro.md): defining properties, datatypes and classes
- [Atomic Mutations](mutations/intro.md): sharing state changes, verifying changes and collaboration

## Motivation

Linked data (RDF / the semantic web) enables us to use the web as a large, decentralized graph database.
Using links everywhere in data has amazing merits: links remove ambiguity, they enable exploration, they enable connected datasets.
Linked Data could help to democratize the web by decentralizing information storage, and giving people more control.

At [Ontola](ontola.io/), we've been working with linked data quite intensely for the last couple of years.
We went all-in, and challenged ourselves to create software that communicates exclusively using RDF.
That has been an inspiring, but also sometimes a frustrating journey.
While building various production grade apps (e.g. our e-democracy platform [Argu.co](https://argu.co/), which is used by various governments), we had to solve many problems.
Some related to modeling, serializing, and rendering RDF.
Most of these problems we've tackled by having a tight grip on the data that we create, and another part is creating new standards and various libraries.

It's been almost 20 years since the introduction of linked data, and its adoption has been slow.
We know that some of its merits are undeniable, and we truly want the semantic web to succeed.
We believe the lack of growth partially has to do with a lack of tooling, but also with [some problems that lie in the RDF data model](../interoperability/rdf.md#why-these-changes).

Atomic Data aims to take the best parts from RDF, and learn from the past to make a more developer-friendly, performant and reliable data model to achieve a truly linked web.
