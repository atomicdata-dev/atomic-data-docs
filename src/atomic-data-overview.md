# Atomic Data Docs - Overview

Atomic Data is a specification for sharing, modifying and modeling data.

It uses links to connect pieces of data, and therefore makes it easier to connect datasets to each other - even when these datasets exist on separate machines.

Atomic Data is especially suitable for knowledge graphs, distributed datasets, semantic data, p2p applications, decentralized apps and linked open data.
It is designed to be highly extensible, easy to use, and to make the process of domain specific standardization as simple as possible.

Atomic Data is [Linked Data](https://ontola.io/what-is-linked-data/), as it is a more strict subset of RDF.
It is typed (you know if something is a `string`, `number`, `date`, `URL`, etc.) and extensible through [Atomic Schema](schema/intro.md), which means that you can define your own Classes, Properties and Datatypes.
Atomic Data has a standard for synchronizing data by communicating state changes, called [Atomic Commits](commits/intro.md).
You can use parts of Atomic Data separately, but the standard is designed as a full, integrated data management package that makes it easier to create, share and use structured data on the web.

- [Atomic Data Core](core/intro.md): the core model for typed, Linked Data
- [Atomic Schema](schema/intro.md): defining properties, datatypes and classes
- [Atomic Commits](commits/intro.md): sharing state changes, verifying changes and collaboration

## Get Started

If you want to read more about how Atomic Data works - read on.
If you'd rather play and discover for yourself, play with the existing [tooling](tooling.md):

- Server: [atomic-server](https://github.com/joepio/atomic) (powers [atomicdata.dev](https://atomicdata.dev), run with `docker run -p 80:80 -p 443:443 -v atomic-storage:/atomic-storage joepmeneer/atomic-server`)
- Browser app [atomic-data-browser](https://github.com/joepio/atomic-data-browser) ([demo](https://joepio.github.io/atomic-data-browser/))
- CLI (atomic-cli): [atomic-cli](https://github.com/joepio/atomic) (`cargo install atomic-cli`)
- Rust library: [atomic-lib](https://github.com/joepio/atomic)

Make sure to [join our Discord](https://discord.gg/a72Rv2P) if you'd like to discuss Atomic Data with others.

## Reading these docs

This is written mostly as a book, so reading it in the order of the Table of Contents will probably give you the best experience.
That being said, feel free to jump around - links are often used to refer to earlier discussed concepts.
If you encounter any issues while reading, please leave an [issue on Github](https://github.com/ontola/atomic-data/issues).
Use the arrows on the side / bottom to go to the next page.
