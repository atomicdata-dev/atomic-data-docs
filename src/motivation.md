# Motivation: Why Atomic Data?

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
