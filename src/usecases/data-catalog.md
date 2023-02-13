{{#title Atomic Server as a Data Catalog}}
# Using Atomic-Server as a Data Catalog

A data catalog is a system that collects metadata - data about data.
They are inventories of datasets.

They are often used to:

- **Increase data-reuse of (open) datasets**. By making descriptions of datasets, you increase their discoverability.
- **Manage data quality**. The more datasets you have, the more you'll want to make sure they are usable. This could mean settings serialization requirements or schema compliance.
- **Manage compliance with privacy laws**. If you have datasets that contain GDPR-relevant data (personal data), you're legally required to maintain a list of where that data is stored, what you need it for and what you're doing with it.

## Why Atomic Server could be great for Data Catalogs

- Free & **open source**. MIT licensed!
- Many built-in **features**, like full-text search, versioning, live synchronization, rights management,
- Great **performance**. Requests take nanoseconds to milliseconds.
- Very **easy to setup**. One single binary, no weird runtime dependencies.
- Everything is linked data. Not just datasets (which you might), but also everything around them (users, comments, implementations)
- [Atomic Schema](../schema/intro.md) can be used to describe the shape of your datasets: the properties you use, which fields are required - things like that. Because Atomic Schema uses URLs, we can easily re-use properties and class definitions. This helps to make your datasets highly interoperable.

## Atomic Server compared to CKAN

- Atomic-Server is MIT licensed - which is more permissive than CKAN's AGPL license.
- Whereas CKAN needs an external database, a python runtime, solrd and a HTTPS server, Atomic-Server has all of these built-in!
- CKAN uses plain RDF, which has some [very important drawbacks](../interoperability/rdf.md).
- But... Atomic-Server still misses a few essentials:

## What we should add to Atomic-Server before it's actually good

- Add a model for datasets. This is absolutely essential. It could be based on (and link to) DCAT, but needs to be described using Atomic Schema. This step means we can generate forms for Datasets and we can validate their fields.
- Add views for datasets. Atomic-Server already renders decent views for unknown resources, but a specific view should be created for Datasets.
