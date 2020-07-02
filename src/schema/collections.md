# Atomic Collections

Sooner or later, developers will have to deal with long lists of items.
For example, a set of blog posts, activities or users.
Collections often need to be paginated, sorted, and filtered.
For dealing with these problems, we have Atomic Collections.

Note that Collections are designed to be _dynamic resources_, often generated at runtime.

## Collection

An Atomic Collection is a Resource that links to a set of resources.
We call these links _Members_.
Members can be of the same type (Class), but don't have to be.

Properties:

- `pages`: (required, ResourceArray) - a set of
- `iriTemplate`: () - `https://argu.co/argu/discussions{?display,filter%5B%5D*,sort%5B%5D*,page,page_size,type,before%5B%5D*}{#fragment}`
- `sortOptions`:
- `totalItems`:
- `totalItems`:

## Page

## Sorting

- `sortKey`
