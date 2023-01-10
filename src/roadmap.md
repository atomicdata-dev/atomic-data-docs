# Strategy, history and roadmap for Atomic Data

We have the ambition to make the internet more interoperable.
We want Atomic Data to be a commonly used specification, enabling a vast amount of applications to work together and share information.
This means we need a lot of people to understand and contribute to Atomic Data.
In this document, discuss the strategic principles we use, the steps we took, and the path forward.
This should help you understand how and where you may be able to contribute.

## Strategy for adoption

- **Work on both specification and implementations (both client and server side) simultaneously** to make sure all ideas are both easily explainable and properly implementable. Don't design a spec with a large committee over many months, only to learn that it has implementation issues later on.
- **Create libraries whenever possible.** Enable other developers to re-use the technology in their own stacks. Keep the code as modular as possible.
- **Document everything**. Not just your APIs - also your ideas, considerations and decisions.
- **Do everything public**. All code is open source, all issues are publicly visible. Allow outsiders to learn everything and start contributing.
- **Make an all-in-one workspace app that stand on its own**. Atomic Data may be an abstract, technical story, but we still need end-user friendly applications that solve actual problems if we want to get as much adoption as possible.
- **Let realistic use cases guide API design**. Don't fall victim to spending too much time for extremely rare edge-cases, while ignoring more common issues and wishes.
- **Familiarity first**. Make tools and specs that feel familiar, build libraries for popular frameworks, and stick to conventions whenever possible.

## History

- **First draft of specification** (2020-06). Atomic Data started as an unnamed bundle of ideas and best practices to improve how we work with linked data, but quickly turned into a single (draft) specification. The idea was to start with a cohesive and easy to understand documentation, and use that as a stepping stone for writing the first code. After this, the code and specification should both be worked on simultaneously to make sure ideas are both easily explainable and properly implementable. Many of the earliest ideas were changed to make implementation easier.
- **[atomic-cli](https://crates.io/crates/atomic-cli) + [atomic-lib](https://docs.rs/atomic_lib/0.32.1/atomic_lib/)** (2020-07). The CLI functioned as the first platform to explore some of the most core ideas of Atomic Data, such as Properties and fetching. `atomic_lib` is the place where most logic resides. Written in Rust.
- **[Atomic-Server](https://github.com/atomicdata-dev/atomic-data-rust/)** (2020-08). The server (using the same `atomic_lib` as the CLI) should be a fast, lightweight server that must be easy to set-up. Functions as a graph database with no dependencies.
- **[Collections](schema/collections.md)** (2020-10). Allows users to perform basic queries, filtering, sorting and pagination.
- **[Commits](commits/intro.md)** (2020-11). Allow keeping track of an event-sourced log of all activities that mutate resources, which in turn allows for versioning and adding new types of indexes later on.
- **[JSON-AD](core/json-ad.md)** (2021-02). Instead of the earlier proposed serialization format `.ad3`, we moved to the more familiar `json-ad`.
- **[Atomic-Data-Browser](https://github.com/atomicdata-dev/atomic-data-browser)** (2021-02). We wanted typescript and react libraries, as well as a nice interactive GUI that works in the browser. It should implement all relevant parts of the specification.
- **[Endpoints](endpoints.md)** (2021-03). Machine readable API endpoints (think Swagger / OpenAPI spec) for things like versioning, path traversal and more.
- **Classes and Properties editable from the browser** (2021-04). The data-browser is now powerful enough to use for managing the core ontological data of the project.
- **[Hierarchies](hierarchy.md) & [Invitations](invitations.md)** (2021-06). Users can set rights, structure Resources and invite new people to collaborate.
- **[Websockets](websockets.md)** (2021-08). Live synchronization between client and server.
- **Use case: Document Editor** (2021-09). Notion-like editor with real-time synchronization.
- **Full-text search** (2021-11). Powered by Tantivy.
- **Authentication for read access** (2021-11). Allows for private data.
- **Desktop support** (2021-12). Run Atomic-Server on the desktop, powered by Tauri. Easier install UX, system tray icon.
- **File management** (2021-12). Upload, download and view Files.
- **Indexed queries** (2022-01). Huge performance increase for queries. Allows for far bigger datasets.
- **Use case: ChatRoom** (2022-04). Group chat application. To make this possible, we had to extend the Commit model with a `push` action, and allow Plugins to create new Commits.
- **[JSON-AD Publishing and Importing](create-json-ad.md)** (2022-08). Creating and consuming Atomic Data becomes a whole lot easier.

## Where we're at

Most of the specification seems to become pretty stable.
The implementations are working better every day, although 1.0 releases are still quite a bit far away.
At this point, the most important thing is to get developers to try out Atomic Data and provide feedback.
That means not only make it easy to install the tools, but also allow people to make Atomic Data _without_ using any of our own tools.
That's why we're now working on the JSON-AD and Atomizer projects (see below).

## Roadmap

- **[Atomizer](https://github.com/atomicdata-dev/atomic-data-rust/issues/434)** (2022-Q4). Import files and automatically turn these into Atomic Data.
- **Improved modelling tools** (2022-Q4). Makes it even easier to create Classes and define Properties.
- **Video(s) about Atomic Data** (2022-Q4). Explain what Atomic Data is, why we're doing this, and how to get started.
- **[Atomic-server plugins](https://github.com/atomicdata-dev/atomic-data-rust/issues/73)** (2023). Let developers design new features without having to make PRs in Atomic-Server, and let users install apps without re-compiling (or even restarting) anything.
- **Use case: headless CMS** (2023). Use Atomic-Server to host and edit data that is being read by a front-end JAMSTACK type of tool, such as NextJS or SvelteKit.
- **Atomic-browser plugins** (2023). Create new views for Classes.
- **1.0 release** (2024). Mark the specification, the server [(tracking issue)](https://github.com/atomicdata-dev/atomic-data-rust/milestone/5) and the browser as _stable_. It is possible that the Spec will become 1.0 before any implementation is stable.
- **Model Marketplace** (2024). A place where user can easily find, compare and use Classes, Properties and Ontologies.
