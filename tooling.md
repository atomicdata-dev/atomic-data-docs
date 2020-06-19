# Atomic Data Tooling

At this moment, no real tooling for Atomic Data exists.
However, basic tooling is required to make this a succes.
The following list is a set of ideas that we're working on.

## Atomic creator (CLI)

A CLI tool for generating Atomic Data.

```sh
# Create an atom
# atomic <method> <subject> <predicate> <object>
atomic add john birthdate 1991-01-20
# It's possible to use these prefixes instead of full URLs, as long as they are defined in a local file (e.g. ~/.ldget/prefixes)
# If the predicate is not used before, the CLI will ask for the required attributes (datatype, description) and create the Property
# The object will be parsed accordingly. If it does not meet the requirements, it wll not create the Atom.
# If everything is well, an Atomic Mutation will be sent to the Atomic Server
```

## Atomic server

- Makes sure the created Atomic Resources / Properties / etc. actually resolve
- Might offer useful query options (e.g. Triple Pattern Fragments)
- Offers pub/sub functionality to clients that will want to re-use data

## Atomizer (data importer and conversion kit)

- Perhaps a CLI, library or GUI that helps with converting existing formats to

## Language support

## IDE tooling

I want to be able to do this:

```js
import atomicfetch from '@atomic/fetch';

const resource = "https://example.com/person/mickey";
const class = "https://example.com/classes/Person";

// IDE could know that the "example:Person" class requires a "bestFriend" property.
const fetchedperson = atomicfetch(resource, class)

const bestFriendsName = fetchedperson.bestFriend.firstName // => "Pluto"

```

## Libraries
