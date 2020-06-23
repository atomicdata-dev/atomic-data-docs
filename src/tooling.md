# Tooling for Atomic Data

At this moment, no real tooling for Atomic Data exists.
Great tooling is required to make this a succes.
The following list is a set of ideas that we're likely to be working on.

## Atomic Validator

Takes some Graph as an input, and validates its contents.
Could be useful for many purposes, and should be one of the first things to become available.
Not only should this parse Atomic-NDJSON, it should also make sure the URLs resolve and the DataTypes resolve.
Perhaps it should also return if non-standard Datatypes are being used, and if so, which ones.

## Atomic creator (CLI)

A CLI tool for generating Atomic Data.
Should produce Atomic Mutations.

```sh
# Create an atom
# atomic <method> <subject> <property> <value>
atomic add john birthdate 1991-01-20
# It's possible to use these keys instead of full URLs, as long as they are known locally,
# either in a local Atomic store a local prefixes file (e.g. ~/.ldget/prefixes)
# If the property is not used before, the CLI will ask for the required attributes (datatype, description) and create the Property
# The value will be parsed accordingly. If it does not meet the requirements, it wll not create the Atom.
# If everything is well, an Atomic Mutation will be sent to the Atomic Server
```

## Atomic server

- Makes a graph available at some endpoint.
- Responds to requests for created Atomic Resources (including Properties / DataTypes)
- Offer useful query options (e.g. Triple Pattern Fragments)
- Offers pub/sub functionality to clients that will want to listen to changes (Mutation Feed?)

## Atomizer (data importer and conversion kit)

- Import data from some data source (CSV / SQL / JSON / RDF), fill in the gaps (mapping / IRI creation / datatypes) an create new Atoms
- Perhaps a CLI, library, GUI or a combination of all of these

## Libraries

The most important tooling for Atomic Data, are libraries.
Tools that developers use to fetch, manipulate and share Atomic Data inside their applications.
In this section, I'll create some rough API designs.

### Atomic-js (Javascript / Typescript)

A JS compatible library, accessible as an NPM package is the most popular and developer friendly way to start.

Here's some pseudocode that indicates how it might be used:

```js
import {createStore} from '@atomicdata';

const config = {
  // A URL to a TPF compatible endpoint where the data can be fetched
  tpfEndpoint: "https://example.com/tpf",
  // A UTL to an Atomic Mutations endpoint where the client can subscribe to changes
  mutationsEndpoint: "https://example.com/mutations",
  // A UTL to an Atomic Suggestions endpoint where the client can send suggested state changes
  sugestionsEndpoint: "https://example.com/suggestions",
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

console.log(person.subject) //=> Should return a newly created identifier

// Checks the store for the subject, and returns it.
// If it does not exists locally, it will fetch it first using the `tpfEndpoint`.
const alice = await store.get("https://example.com/alice")

// Because of the keys in Atomic Properties, we can use this dot syntax to traverse the graph and get a value
console.log(alice.bestFriend.firstName); // => "Bob"
```

I think a Developer Experience similar to the one above is essential for getting people to create linked data.
It should be incredibly easy, and this is what enables that.
However, realizing a library + IDE support as shown above is hard at the least, perhaps even impossible.
Theoretically, the information is accessible - but I'm not sure whether the IDE and the JS context (e.g. the Typescript compiler) can successfully see which shape is being returned by the `classInitializer` function.

### Atomic-rs

Rust's compiler has strict type checking.
It also features a very flexible macro language, which could enable intuitive API designs for Atomic Data.
It could fetch the Properties and Classes at compile time, and convert these to

```rust
use atomic::{init_store}

fn main() {
  let mut graph = init_store();
  // TODO! Design a macro solution

}
```

## Atomic Browsser

A web-browser application that enables viewing, browsing, navigating Atomic Data.
