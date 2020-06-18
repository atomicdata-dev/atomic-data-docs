# Atomic Data Tooling

At this moment, no real tooling for Atomic Data exists.
However, tooling is required to make this a succes.
The following list is a set of ideas

## Atomic creator (CLI)

A CLI tool for generating Atomic Data.

```sh
# Create an atom
# atomic <method> <subject> <predicate> <object>
atomic add john birthdate 1991-01-20
# It's possible to use these prefixes instead of full URLs, as long as they are defined in a local file (e.g. ~/.ldget/prefixes)
# If the predcate is not used before, the CLI will ask for the required attributes (datatype, description)
# The object will be parsed accordingly. If it does not meet the requirements, it wll not create the Atom.
```

## Atomic server

## Atomizer (dat importer and conversion kit)

## Atomic Modeller
