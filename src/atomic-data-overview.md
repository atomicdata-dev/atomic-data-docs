# Atomic Data Docs - Overview

_Status: early draft, [feedback welcome](get-involved.md). Early Rust implementation accessible [here](https://github.com/joepio/atomic)._

Atomic Data is a proposed standard for modeling and exchanging data.
It uses links to connect pieces of data, and therefore makes it easier to connect datasets to each other - even when these datasets exist on separate machines.

Atomic Data is especially suitable for knowledge graphs, distributed datasets, semantic data, p2p applications, decentralized apps, and data that is meant to be highly reusable.
It is designed to be highly extensible, easy to use, and to make the process of domain specific standardization as simple as possible.

Atomic Data is [Linked Data](https://ontola.io/what-is-linked-data/), as it is a more strict subset of RDF.
It is typed (you know if something is a `string`, `number`, `URL`, etc.) and extensible through [Atomic Schema](schema/intro.md), which means that you can define your own Classes, Properties and Datatypes.
Atomic Data has a standard for synchronizing data by communicating state changes, called [Atomic Commits](commits/intro.md).
You can use parts of Atomic Data separately, but the standard is designed as a full, integrated data management package that makes it easier to create, share and use structured data on the web.

- [Atomic Data Core](core/intro.md): the core model for typed, Linked Data
- [Atomic Schema](schema/intro.md): defining properties, datatypes and classes
- [Atomic Commits](commits/intro.md): sharing state changes, verifying changes and collaboration

## Motivation

Linked data (RDF / the semantic web) enables us to use the web as a large, decentralized graph database.
Using links everywhere in data has amazing merits: links remove ambiguity, they enable exploration, they enable connected datasets.
Linked Data could help to democratize the web by decentralizing information storage, and giving people more control.
The Solid Project by Tim Berners-Lee is a great example of why linked data can help to create a more decentralized web.

At [Ontola](https://ontola.io/), we've been working with linked data quite intensely for the last couple of years.
We went all-in on RDF, and challenged ourselves to create software that communicates exclusively using it.
That has been an inspiring, but also sometimes a frustrating journey.
While building various production grade apps (e.g. our e-democracy platform [Argu.co](https://argu.co/), which is used by various governments), we had to [solve many problems](https://ontola.io/blog/full-stack-linked-data/).
How to properly model data in RDF? How to deal with sequences? How to communicate state changes? Converting RDF to HTML? Typing? CORS?
We tackled some of these problems by having a tight grip on the data that we create (e.g. we know the type of data, because we control the resources), and another part is creating new protocols, formats, tools, and libraries.
But it took a long time, and it was hard.
It's been almost 15 years since the [introduction of linked data](https://www.w3.org/DesignIssues/LinkedData.html), and its adoption has been slow.
We know that some of its merits are undeniable, and we truly want the semantic web to succeed.
We believe the lack of growth partially has to do with a lack of tooling, but also with [some problems that lie in the RDF data model](interoperability/rdf.md#why-these-changes).

Atomic Data aims to take the best parts from RDF, and learn from the past to make a more developer-friendly, performant and reliable data model to achieve a truly linked web.
