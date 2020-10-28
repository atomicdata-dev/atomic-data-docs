# Tooling for Atomic Data

Because Atomic Data is very young, **little tooling for Atomic Data exists**.
Great tooling is required to make this a success.

## Existing tooling

### `atomic-cli`

A tool for generating / querying Atomic Data from the command line.

```sh
# Add a mapping, and store the Atomic Class locally
atomic map person https://example.com/person
# Create a new instance with that Class
atomic new person
name (required): John McLovin
age: 31
Created at: ipfs:Qwhp2fh3o8hfo8w7fhwo77w38ohw3o78fhw3ho78w3o837ho8fwh8o7fh37ho
# link to an Atomic Server where you can upload your stuff
# If you don't, your data exists locally and gets published to IPFS
atomic setup
# install ontologies and add their shortnames to bookmarks
atomic install https://atomicdata.dev/ontologies/meetings
# when no URL is given, use the Ontola repo's ontologies
atomic install meetings
```

MIT licensed [repo here](https://github.com/joepio/atomic).

### `atomic-lib` (Rust)

Library that contains:

- An in-memory store
- Parsing (AD3) / Serialization (AD3, JSON, more to come)
- Path traversal
- Basic validation

MIT licensed [repo here](https://github.com/joepio/atomic).


### `atomic-server`

Server for hosting Atomic Data. Uses `atomic-lib`.

- Responds to requests for created Atomic Resources, makes atomic data available at their URL.
- Manages data on disk.
- Useful query options (e.g. Triple Pattern Fragments)
- Browser-friendly HTML presentation, JSON serialization, AD3 serialization.

MIT licensed [repo here](https://github.com/joepio/atomic).

## Some ideas for tooling

This document contains a set of ideas that would help achieve that success.

## ATOML / VSCode Extension

Extending the TOML format to map it to Atomic Classes.
This will make editing .TOML files awesome by providing on-screen validation, autocompletion and documentation for fields.

## Atomizer (data importer and conversion kit)

- Import data from some data source (CSV / SQL / JSON / RDF), fill in the gaps (mapping / IRI creation / datatypes) an create new Atoms
- Perhaps a CLI, library, GUI or a combination of all of these

## Atomic Preview

- A simple (JS) widget that can be embedded anywhere, which converts an Atomic Graph into an HTML view.
- Would be useful for documentation, and as a default view for Atomic Data.

## Atomic-js (Javascript / Typescript)

A JS compatible library, accessible as an NPM package is the most popular and developer friendly way to start.

Here's some pseudocode that indicates how it might be used:

```js
import {createStore} from '@atomicdata';

const config = {
  // A URL to a TPF compatible endpoint where the data can be fetched
  tpfEndpoint: "https://example.com/tpf",
  // A URL to an Atomic Commits endpoint where the client can subscribe to changes
  commitssEndpoint: "https://example.com/commits",
};

const store = createStore(config); // Initializes the store

// The `classInitializer` function takes an Atomic Class URI as its argument
// fetches the Class, its Properties and the DataTypes
// and returns a function that let's you create instances of that class
const personBuilder = await store.classInitializer("https://example.com/classes/Person");

// Create an instance of the Person Class
// An Atomic Suggestion is sent to the
const alice = await personBuilder({
  // The Subject field is optional, but recommended if you want to control its URL.
  // Otherwise, the Server will pick something
  subject: "https://example.com/alice",
  // The IDE is aware of the existing keys and their acceptable values,
  // because a conversion from Atomic Classes and Properties
  // to typescript interfaces can be made automatically
  firstName: "Alice",
  lastName: "Anderson",
  bestFriend: "https://example.com/Bob",
  birthDate: new Date("1991-01-20"),
  // Since the URL in the key below can be fetched, and has a Property + Datatype, the IDE + the compiler can determine that 'true' is an acceptable type.
  "https://example.com/someOtherProperty": true,
})

console.log(person.subject) //=> Should return a newly created identifier, https://example.com/alice

// Checks the store for the subject, and returns it.
// If the subject does not exists locally, it will fetch it first using the `tpfEndpoint`.
const alice = await store.get("https://example.com/alice")

// Because of the keys in Atomic Properties, we can use this dot syntax to traverse the graph and get a value
console.log(await alice.path("bestFriend.firstName")).value(); // => "Bob"
// What should happen here?
console.log(await alice.bestFriend); // => {...}

// It's also possible to convert a resource to a native JS object.
// By specifying the depth, nested resources will be fetched as well.
const aliceJS = await store.get("https://example.com/alice").toJS(depth: 2)

console.log(aliceJS.bestFriend) // => { name: Bob, birthdate: Date(1991-01-20)}

```

I think a Developer Experience similar to the one above is essential for getting people to create linked data.
It should be incredibly easy, and this is what enables that.
However, realizing a library + IDE support as shown above is hard at the least, perhaps even impossible.
Theoretically, the information is accessible - but I'm not sure whether the IDE and the JS context (e.g. the Typescript compiler) can successfully see which shape is being returned by the `classInitializer` function.

## Atomic Browser

A web-browser application that enables viewing, browsing, navigating Atomic Data.
