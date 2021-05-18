# Atomic Data Core

The Atomic Data Core describes the fundamental data model of Atomic Data.

## Design goals

* **Browsable**: Data should explicitly link to other pieces of data, and these links should be followable.
* **Semantic**: Every data Atom and relation has a clear semantic meaning.
* **Interoperable**: Plays nice with other data formats (e.g. JSON, XML, and all RDF formats).
* **Open**: Free to use, open source, no strings attached.
* **Clear Ownership**: The data shows who is in control of the data, so new versions of the data can easily be retrieved.
* **Mergeable**: Any two sets of Atoms can be merged into a single graph without any merge conflicts / name collisions.
* **Extensible**: Anyone can define their own data types and create Atoms with it.
* **ORM-friendly**: Navigate a _decentralized_ graph by using dot.syntax, similar to how you navigate a JSON object in javascript.
* **Typed**: All valid Atomic data has an unambiguous, static datatype. Models expressed in Atomic Data can be mapped to programming language models, such as `structs` or `interfaces` in Typescript / Rust / Go.
