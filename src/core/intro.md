# Atomic Data Core

The Atomic Data Core describes the fundamental data model of Atomic Data.
Before we dive into its concepts, we'll talk about why this standard is made in the first place.

## Design goals

* **Browsable**: Data should explicitly link to other pieces of data, and these links should be followable.
* **Semantic**: Every data Atom and relation has a clear semantic meaning.
* **Open**: Free to use, open source, no strings attached.
* **Clear Ownership**: The data shows who is in control of the data, so new versions of the data can easily be retrieved.
* **Mergeable**: Any two sets of Atoms can be merged into a single graph without any merge conflicts / name collisions.
* **Interoperable**: Can easily and constantly be converted to other data formats (e.g. JSON, XML, and all RDF formats).
* **Extensible**: Anyone can define their own data types and create Atoms with it.
* **ORM-friendly**: Navigate a _decentralized_ graph by using dot.syntax, similar to how you navigate a JSON object in javascript.
* **Typed**: All valid Atomic data has an unambiguous, static datatype. Models expressed in Atomic Data can be mapped to programming language models, such as `structs` or `interfaces` in Typescript / Rust / Go.

Note that for these last four goals, [Atomic Schema](../schema/intro.md) is required.

## When should you use Atomic Data

- **Flexible schemas**. When dealing with structured wikis or semantic data, various instances of things will have different attributes. Atomic Data allows _any_ kind of property on _any_ resource.
- **High-value open data**. Atomic Data is a bit harder to create, but it is easier to re-use and understand. It's use of URLs for properties makes data self-documenting.
- **Standardization is important**. When multiple groups of people have to use the same schema, Atomic Data provides easy ways to constrain and validate the data.
- **Multi-class / multi-model**. Contrary to (SQL) tables, Atomic Data allows a single thing to have multiple classes, each with their own properties.
- **Connected / decentralized data**. With Atomic Data, you use URLs to point to things on other computers. This makes it possible to connect datasets very explicitly, without creating copies.
- **Interactive data**. When users need to make changes
- **RDF as Output**. Atomic Data serializes to idiomatic, clean RDF (Turtle / JSON-LD / n-triples / RDF/XML).

## When not to use Atomic Data

- **Internal use only**. If you're not sharing structured data, Atomic Data will probably only make things harder for you.
- **Big Data**. If you're dealing with TeraBytes of data, you probably don't want to use Atomic Data.
