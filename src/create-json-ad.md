# How to create and publish a JSON-AD file

[JSON-AD](core/json-ad.md) is the default serialization format of Atomic Data.
It's just JSON, but with some extra requirements:

- All keys are links to [Atomic Properties](https://atomicdata.dev/classes/Property)
- Resources that are hosted somewhere must have `@id`s, called _Subjects_

In this section, we'll create a JSON-AD file and import it into Atomic-Server.
