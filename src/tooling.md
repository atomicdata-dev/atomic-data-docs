# Tooling for Atomic Data

- Server: [atomic-server](https://github.com/joepio/atomic)
- Front-end browser + typescript client library: [atomic-data-browser](https://github.com/joepio/atomic-data-browser)
- CLI (atomic-cli): [atomic-cli](https://github.com/joepio/atomic)
- Rust library: [atomic-lib](https://github.com/joepio/atomic)

## `atomic-server`

Server for hosting Atomic Data. Uses `atomic-lib`.

- Responds to requests for created Atomic Resources, makes atomic data available at their URL.
- Manages data on disk.
- Useful query options (e.g. Triple Pattern Fragments)
- Browser-friendly HTML presentation, JSON serialization, AD3 serialization.

One liner: `$ docker run -p 80:80 -p 443:443 -v atomic-storage:/atomic-storage joepmeneer/atomic-server`

[demo](https://atomicdata.dev/)

[MIT licensed repository + issue tracker](https://github.com/joepio/atomic).

## `atomic-data-browser`

Data browser + react typescript / javascript front-end library.

- View & edit atomic data, using dynamic forms
- Collections with pagination and sorting
- Client-side full-text search

[demo](https://atomicdata.dev/) (same as `atomic-server`)

[MIT licensed repository + issue tracker](https://github.com/joepio/atomic-data-browser).

## `atomic-cli`

A tool for generating / querying Atomic Data from the command line. Install with `cargo install atomic-cli`.

```
atomic 0.20.0
Joep Meindertsma <joep@ontola.io>
Create, share, fetch and model linked atomic data!

USAGE:
    atomic-cli [SUBCOMMAND]

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information

SUBCOMMANDS:
    destroy    Permanently removes a Resource. Uses Commits.
    edit       Edit a single Atom from a Resource using your text editor. Uses Commits.
    get        Traverses a Path and prints the resulting Resource or Value.
    help       Prints this message or the help of the given subcommand(s)
    list       List all bookmarks
    new        Create a Resource
    remove     Remove a single Atom from a Resource. Uses Commits.
    set        Update an Atom's value. Uses Commits.
    tpf        Finds Atoms using Triple Pattern Fragments.

Visit https://github.com/joepio/atomic for more info
```

[MIT licensed repository + issue tracker](https://github.com/joepio/atomic).

## `atomic-lib` (Rust)

Library that powers `atomic-server` and `atomic-cli`. Features:

- An in-memory store
- Parsing (JSON-AD, AD3) / Serialization (JSON-AD, AD3, JSON-LD, TTL, N-Triples)
- Commit validation and processing
- TPF queries
- Constructing Collections
- Path traversal
- Basic validation

[MIT licensed repository + issue tracker](https://github.com/joepio/atomic).

## Want to add to this list? Some ideas for tooling

This document contains a set of ideas that would help achieve that success.

## Atomizer (data importer and conversion kit)

- Import data from some data source (CSV / SQL / JSON / RDF), fill in the gaps (mapping / IRI creation / datatypes) an create new Atoms
- Perhaps a CLI, library, GUI or a combination of all of these

## Atomic Preview

- A simple (JS) widget that can be embedded anywhere, which converts an Atomic Graph into an HTML view.
- Would be useful for documentation, and as a default view for Atomic Data.

## Atomic-Dart + Flutter

Library + front-end app for browsing / manipulating Atomic Data on mobile devices.
