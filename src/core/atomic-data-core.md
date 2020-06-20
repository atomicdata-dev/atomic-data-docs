# Atomic Data Core: design goals and motivation

The Atomic Data Core describes the fundamental data model of Atomic Data.
Before we dive into its concepts, we'll talk about why this standard is made in the first place.

## Design goals

* **Typed**: All Atomic data has an unambiguous, static datatype. Models expressed in Atomic Data can be mapped to programming langauge models, such as `structs` or `interfaces` in Typescript / Rust / Go.
* **Semantic**: Every data Atom and relation has a clear semantic meaning.
* **Browseable**: Data should explicitly link to other pieces of data, and these links should be followable.
* **ORM-friendly**: Navigate a _decentralized_ graph by using dot.syntax, similar to how you navigate a JSON object in javascript.
* **Open**: Free to use, open source, no strings attached.
* **Interoperable**: Can easily and consitently be converted to other data formats (e.g. JSON, XML, and all RDF formats).
* **Clear Ownership**: The URL of the data shows who is in control of the data
* **Extensible**: Anyone can define their own data types and create Atoms with it.
* **Mergeable**: Any two sets of Atoms can be merged into a sinlge graph without any merge conflicts / name collissions.

## Motivation

Linked data (RDF / the semantic web) enables us to use the web as a large, decentralized graph database.
Using links everywhere in data has amazing merits: links remove ambiguity, they enable exploration, they enable connected datasets.
However, it's been almost 20 years since the introduction of linked data, and its adoption has been slow.
We believe this lack of growth has to do with [some problems that lie in the RDF data model](../interoperability/rdf.md#why-these-changes).
Atomic Data aims to take the best parts from RDF, and learn from the past to make a more developer-friendly, performant and reliable data model to achieve a truly linked web.
