{{#title Atomic Data Hierarchy, rights and authorization }}
# Hierarchy, rights and authorization

Hierarchies help make information easier to find and understand.
For example, most websites use breadcrumbs to show you where you are.
Your computer probably has a bunch of _drives_ and deeply nested _folders_ that contain _files_.
We generally use these hierarchical elements to keep data organized, and to keep a tighter grip on rights management.
For example, sharing a specific folder with a team, but a different folder could be private.

Although you are free to use Atomic Data with your own custom authorization system, we have a standardized model that is currently being used by some of the tools that we've built.

## Design goals

- **Fast**. Authorization can sometimes be costly, but in this model we'll be considering performance.
- **Simple**. Easy to understand, easy to implement.
- **Handles most basic use-cases**. Should deal with basic read / write access control, calculating the size of a folder, rendering things in a tree.

## Atomic Hierarchy Model

- Every Resource SHOULD have a [`parent`](https://atomicdata.dev/properties/parent).
- Any Resource can be a `parent` of some other Resource, as long as both Resources exists on the same Atomic Server.
- Inversely, every Resource could have `children`.
- Only [`Drive`](https://atomicdata.dev/classes/Drive)s (Resources with the class `Drive`) are allowed to be a top-level parent.
- Any Resource might have `read` and `write` Atoms. These both contain a list of Agents. These Agents will be granted the rights to edit (using Commits) or read / use the Resources.
- Rights are _additive_, which means that the rights add up. If a Resource itself has no `write` Atom containing your Agent, but it's `parent` _does_ have one, you will still get the `write` right.
- Rights cannot be removed by children or parents - they can only be added.

## Authentication

See [authentication](./authentication.md).

## Current limitations of the current Authorization model

The specification is growing (and please contribute in the [docs repo](https://github.com/ontola/atomic-data-docs/issues)), but the current specification lacks some features:

- Rights can only be added, but not removed in a higher item of a hierarchy. This means that you cannot have a secret folder inside a public folder.
- No model for representing groups of Agents, or other runtime checks for authorization.
- No way to limit delete access seperately from write rights
- No way to request a set of rights for a Resource
