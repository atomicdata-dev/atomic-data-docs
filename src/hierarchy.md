# Hierarchy, rights and authorization

It's hard to think about data without thinking of hierarchy.
Most websites use breadcrumbs to show users where they are.
Your computer probably has a bunch of _drives_ and deeply nested _folders_ that contain _files_.
We generally use these hierarchical elements to keep data organized, and to keep a tighter grip on rights management.
We might want to share this specific folder with a team, but a different folder could be private.

Although you are free to use Atomic Data with your own custom authorization system, we have a standardized model that is currently being used by some of the tools that we've built.

## Usecases

- Hierarchical navigation (browsing folders, displaying breadcrumbs)
- Rights management / authorization
- Disk space management

## Atomic Hierarchy Model

- Every Resource SHOULD have a `parent`.
- Any Resource can be a `parent` of some other Resource, as long as both Resources exists on the same Atomic Server.
- Inversely, every Resource could have `children`.
- Only `Drive`s (Resources with the class `Drive`) are allowed to be a top-level parent.
- Any Resource might have `read` and `write` Atoms. These both contain a list of Agents. These Agents will be granted the rights to edit (using Commits) or read / use the Resources.
- Rights are _additive_, which means that the rights add up. If a Resource itself has no `write` Atom containing your Agent, but it's `parent` _does_ have one, you will still get the `write` right.
- Rights cannot be removed by children or parents - they can only be added.
