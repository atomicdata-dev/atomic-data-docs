# Tooling for Atomic Data

At this moment, no real tooling for Atomic Data exists.
However, basic tooling is required to make this a succes.
The following list is a set of ideas that we're working on.

## Atomic creator (CLI)

A CLI tool for generating Atomic Data.
Should produce Atomic Mutations.

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

- Respond to requests for created Atomic Resources (including Properties / DataTypes)
- Offer useful query options (e.g. Triple Pattern Fragments)
- Offers pub/sub functionality to clients that will want to re-use data (Mutation Feed?)

## Atomizer (data importer and conversion kit)

- Import data from some data source (CSV / SQL / JSON / RDF), fill in the gaps (mapping / IRI creation / datatypes) an create new Atoms
- Perhaps a CLI, library, GUI or a combination of all of these

## Language support

## IDE tooling & libraries

I want to be able to do this:

```js
import atomicfetch from '@atomic/fetch';

const resource = "https://example.com/person/mickey";
const class = "https://example.com/classes/Person";

const fetchedperson = atomicfetch(resource, class)

// IDE tooling is aware that the "example:Person" class requires a "bestFriend" property, which is another "Person", which has a "firstName".
const bestFriendsName = fetchedperson.bestFriend.firstName // => "Pluto"
```

## Libraries

### Javascript / Typescript

We need a library for fetching, storing and converting Atomic Data.

Here's some pseudocode that indicates how it might function

```js
import {createStore} from '@atomic';

const config = {
  // A URL to a TPF compatible endpoint where the data can be fetched
  tpfEndpoint: "https://example.com/tpf",
  // A UTL to an Atomic Mutations endpoint where the client can subscribe to changes
  mutationsEndpoint: "https://example.com/mutations",
  // A UTL to an Atomic Suggestions endpoint where the client can send suggested state changes
  sugestionsEndpoint: "https://example.com/suggestions",
};

const store = createStore(config); // Initializes the store
store.fetch("https://example.com/john") // Fetches the required data, in this case using the tpf endpoint

const john = store.get("https://example.com/john") // Checks the store for the subject,

const newPerson = store.makeA("https://example.com/classes/Person", {
  firstName: "Joep",
  name: "Meinderstsma",
})

```
