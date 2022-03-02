# How to create and publish a JSON-AD file

[JSON-AD](core/json-ad.md) is the default serialization format of Atomic Data.
It's just JSON, but with some extra requirements.

Most notably, all keys are links to [Atomic Properties](https://atomicdata.dev/classes/Property).
These Properties must be actually hosted somewhere on the web, so other people can visit them to read more about them.

Ideally, in JSON-AD, each Resource has its own `@id`.
This is the URL of the resource.
This means that if someone visits that `@id`, they should get the resource they are requesting.
That's great for people re-using your data, but as a data provider, implementing this can be a bit of a hassle.
That's why there is a different way that allows you to create Atomic Data _without manually hosting every resource_.

## Creating JSON-AD without hosting individual resources yourself

In this section, we'll create a single JSON-AD file containing various resources.
This file can then be published, shared and stored like any other.

The goal of this preparation, is to ultimately import it somewhere else.
We'll be importing it to Atomic-Server.
Atomic-Server will create URLs for every single resource upon importing it.
This way, we only deal with the JSON-AD and the data structure, and we let Atomic-Server take care of hosting the data.

Let's create a BlogPost.
We know the fields that we need: a `name` and some `body`.
But we can't use these keys in Atomic Data, we should use URLs that point to Properties.
We can either create new Properties (see the Atomic-Server tutorial), or we can use existing ones, for example by searching on [AtomicData.dev/properties](https://atomicdata.dev/properties).

## Using Ontologies, Classes and Ontologies

Ontologies are groups of concepts that describe some domain.
For example, we could have an Ontology for BlogPosts or .

At this moment, there are few models created in Atomic Data.

## Setting the first values

```json
{
  "https://atomicdata.dev/properties/name": "Writing my first blogpost",
  "https://atomicdata.dev/properties/description": "Hi! I'm a blogpost. I'm also machine readable!",
}
```

## Multiple items

If we want to have _multiple_ items, we can simply use a JSON Array at the root, like so:

```json
[{
  "https://atomicdata.dev/properties/name": "Writing my first blogpost",
  "https://atomicdata.dev/properties/description": "Hi! I'm a blogpost. I'm also machine readable!",
},{
  "https://atomicdata.dev/properties/name": "Another blogpost",
  "https://atomicdata.dev/properties/description": "I'm writing so much my hands hurt.",
}]
```

## Preventing deduplication with `localId`

When we want to _publish_ Atomic Data, we also want someone else to be able to _import_ it.
An important thing to prevent, is _data duplication_.
If you're importing a list of Blog posts, for example, you'd want to only import every article _once_.

The way to prevent this, is by adding a `localId`.
This `localId` is used by the importer to find out if it has already imported it before.
So we, as data producers, need to make sure that our `localId` is _unique_ and _does not change_!
We can use any type of string that we like, as long as it conforms to these requirements.
Let's use a unique _slug_, a short name that is often used in URLs.

```json
{
  "https://atomicdata.dev/properties/name": "Writing my first blogpost",
  "https://atomicdata.dev/properties/description": "Hi! I'm a blogpost. I'm also machine readable!",
  "https://atomicdata.dev/properties/localId": "my-first-blogpost"
}
```

## Describing relationships between resources using `localId`

Let's say we also want to describe the `author` of the BlogPost, and give them an e-mail, a profile picture and some biography.
This means we need to create a new Resource for each Author, and again have to think about the properties relevant for Author.
We'll also need to create a link from BlogPost to Author, and perhaps the other way around, too.

Normally, when we link things in Atomic Data, we can only use full URLs.
But, since we don't have URLs yet for our Resources, we'll need a different solution.
Again, this is where we can use `localId`!
We can simply refer to the `localId`, instead of some URL that does not exist yet.

```json
[{
  "https://atomicdata.dev/properties/name": "Writing my first blogpost",
  "https://atomicdata.dev/properties/description": "Hi! I'm a blogpost. I'm also machine readable!",
},{
  "https://atomicdata.dev/properties/name": "Another blogpost",
  "https://atomicdata.dev/properties/description": "I'm writing so much my hands hurt.",
},{
  "https://atomicdata.dev/properties/firstName": "Johny Author",
  "https://atomicdata.dev/properties/description": "I'm writing so much my hands hurt.",
}]
```
