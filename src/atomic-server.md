# Creating Atomic Data using Atomic-Server

[`Atomic-Server`](https://github.com/joepio/atomic-data-rust/blob/master/server/README.md) is the _reference implementation_ of the Atomic Data Core + Extended specification.
It was developed parallel to this specification, and it served as a testing ground for various ideas (some of which didn't work, and some of which ended up in the spec).
It's a graph database server for storing and sharing typed linked data.
It's free, open source (MIT license), and has a ton of features:

- ⚛️  **Dynamic schema validation** / type checking using [Atomic Schema](https://docs.atomicdata.dev/schema/intro.html). Combines safety of structured data with the
- 🚀  **Fast** (1ms responses on my laptop)
- 🪶  **Lightweight** (15MB binary, no runtime dependencies)
- 💻  **Runs everywhere** (linux, windows, mac, arm)
- 🌐  **Embedded server** with support for HTTP / HTTPS / HTTP2.0 and Built-in LetsEncrypt handshake.
- 🎛️  **Browser GUI included** powered by [atomic-data-browser](https://github.com/joepio/atomic-data-browser). Features dynamic forms, tables, authentication, theming and more.
- 💾  **Event-sourced versioning** / history powered by [Atomic Commits](https://docs.atomicdata.dev/commits/intro.html)
- 🔄  **Synchronization using websockets**: communicates state changes with a client. Send a `wss` request to `/ws` to open a webscocket.
- 🧰  **Many serialization options**: to JSON, [JSON-AD](https://docs.atomicdata.dev/core/json-ad.html), and various Linked Data / RDF formats (RDF/XML, N-Triples / Turtle / JSON-LD).
- 🔎  **Full-text search** with fuzzy search and various operators, often <3ms responses.
- 📖  **Pagination, sorting and filtering** using [Atomic Collections](https://docs.atomicdata.dev/schema/collections.html)
- 🔐  **Authorization** (read / write permissions) and Hierarchical structures powered by [Atomic Hierarchy](https://docs.atomicdata.dev/hierarchy.html)
- 📲  **Invite and sharing system** with [Atomic Invites](https://docs.atomicdata.dev/invitations.html)
- 📂  **File management**: Upload, download and preview attachments.
- 🖥️  **Desktop app**: Easy desktop installation, with status bar icon, powered by [tauri](https://github.com/tauri-apps/tauri/).

## Running Atomic-Server locally (optional)

In this guide, we'll can simply use `atomicdata.dev` in our browser without installing anything.
So you can skip this step and go to _Creating your first Atomic Data_.
But if you want to, you can run Atomic-Server on your machine in a couple of ways:

- **Using a desktop installer**: download a desktop release from the [`releases`](https://github.com/joepio/atomic-data-rust/releases) page and install it using your desktop GUI.
- **Using a binary**: download a binary release from the [`releases`](https://github.com/joepio/atomic-data-rust/releases) page and open it using a terminal.
- **Using Docker** is probably the quickest: `docker run -p 80:80 -p 443:443 -v atomic-storage:/atomic-storage joepmeneer/atomic-server`.
- **Using Cargo**: `cargo install atomic-server` and then run `atomic-server` to start.

_[Atomic-Server's README](https://github.com/joepio/atomic-data-rust/blob/master/server/README.md) contains more (and up-to-date) information about how to use it!_

Open your server in your browser.
By default, that's [`http://localhost:9883`](http://localhost:9883).
Fun fact: `&#9883;` is HTML entity code for the Atom icon: ⚛.

The first screen should show you your [_Drive_](https://atomicdata.dev/classes/Drive).
You can think of this as your root folder.
It is the resource hosted at the root URL, effectively being the home page of your server.

There's an instruction on the screen about the `/setup` page.
Click this, and you'll get a screen showing an [_Invite_](https://atomicdata.dev/classes/Invite).
Normally, you could `Accept as new user`, but since you're running on `localhost`, you won't be able to use the newly created Agent on non-local Atomic-Servers.
Therefore, it may be best to create an Agent on some _other_ running server, such as the [demo Invite on AtomicData.dev](https://atomicdata.dev/invites/1).
And after that, copy the Secret from the `User settings` panel from AtomicData.dev, go back to your `localhost` version, and press `sign in`.
Paste the Secret, and voila! You're signed in.

Now, again go to `/setup`. This time, you can `Accept as {user}`.
After clicking, your Agent has gotten `write` rights for the Drive!
You can verify this by hovering over the description field, clicking the edit icon, and making a few changes.
You can also press the menu button (three dots, top left) and press `Data view` to see your agent after the `write` field.
Note that you can now edit every field.
You can also fetch your data now as various formats.

Try checking out the other features in the menu bar, and check out the `collections`.

Again, check out the [README](https://github.com/joepio/atomic-data-rust/blob/master/server/README.md) for more information and guides!

Now, let's create some data.

## Creating your first Atomic Data

Let's create a _Class_!
A Class represents an abstract concept, such as a `BlogPost` (which we'll do here).
We can do this in a couple of ways:

- Press the `new resource` button on the left menu, and selecting Class
- Opening [Class](https://atomicdata.dev/classes/Class) and pressing `new class`
- Going to the [Classes Collection])(https://atomicdata.dev/classes/) and pressing the plus icon

The result is the same: we end up with a form in which we can fill in some details.


Let's add a shortname, and then a description.

After that, we'll add the `required` properties.
This form you're looking at is constructed by using the `required` and `recommended` Properties defined in `Class`.
We can use these same fields to generate our BlogPost resource!
Which fields would be required in a `BlogPost`?
A `name`, and a `description`, probably.

So let's search for these Properties, and add them.

Now, we can skip the `recommended` properties, and get right to saving our resource.
