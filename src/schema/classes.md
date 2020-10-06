# Atomic Schema: Classes

## How to read classes

Example:

- `description` - (required, AtomicURL, TranslationBox) human readable explanation of what the Class represents.

Means:

This class has a _required_ property with shortname `description`.
This Property has a Datatype of `AtomicURL`, and these should point to `TranslationBox` instances.

_Note: the URLs for properties are missing and will be added at a later time._

## Property

_URL: [`https://atomicdata.dev/classes/Property`](https://atomicdata.dev/classes/Property)_

The Property class.
The thing that the Property field should link to.
A Property is an abstract type of Resource that describes the relation between a Subject and a Value.
A Property provides some semantic information about the relationship (in its `description`), it provides a shorthand (the `shortname`) and it links to a Datatype.
Here's a [list of useful Properties](properties.md).
You can constrain properties further by using [SHACL Properties](https://www.w3.org/TR/shacl/#property-shapes).

Properties of a Property instance:

- [`shortname`](https://atomicdata.dev/properties/shortname) - (required, Slug) the shortname for the property, used in ORM-style dot syntax (`thing.property.anotherproperty`).
- [`description`](https://atomicdata.dev/properties/description) - (optional, AtomicURL, TranslationBox) the semantic meaning of the.
- [`datatype`](https://atomicdata.dev/properties/datatype) - (required, AtomicURL, Datatype) a URL to an Atomic Datatype, which defines what the datatype should be of the Value in an Atom where the Property is the
- [`classtype`](https://atomicdata.dev/properties/classtype) - (optional, AtomicURL, Class) if the `datatype` is an Atomic URL, the `classtype` defines which class(es?) is (are?) acceptable.

```ndjson
["https://example.com/properties/createdAt","https://atomicdata.dev/property/shortname","createdAt"]
["https://example.com/properties/createdAt","https://atomicdata.dev/property/datatype","https://atomicdata.dev/datatype/datetime"]
```

## Datatype

_URL: `https://atomicdata.dev/classes/Datatype`_

A Datatype specifies how a `Value` value should be interpreted.
Datatypes are concepts such as `boolean`, `string`, `integer`.
Since DataTypes can be linked to, you dan define your own.
However, using non-standard datatypes limits how many applications will know what to do with the data.

Properties:

- `description` - (required, AtomicURL, TranslationBox) how the datatype functions.
- `stringSerialization` - (required, AtomicURL, TranslationBox) how the datatype should be parsed / serialized as an UTF-8 string
- `stringExample` - (required, string) an example `stringSerialization` that should be parsed correctly
- `binarySerialization` - (optional, AtomicURL, TranslationBox) how the datatype should be parsed / serialized as a byte array.
- `binaryExample` - (optional, string) an example `binarySerialization` that should be parsed correctly. Should have the same contents as the stringExample. Required if binarySerialization is present on the DataType.

## Class

_URL: `https://atomicdata.dev/classes/Class`_

A Class is an abstract type of Resource, such as `Person`.
It is convention to use an Uppercase in its URI.
Note that in Atomic Data, a Resource can have several Classes - not just a single one.
If you need to set more complex constraints to your Classes (e.g. maximum string length, Properties that depend on each other), check out [SHACL](https://www.w3.org/TR/shacl/).

Properties:

- `shortname` - (required, Slug) a short string shorthand.
- `description` - (required, AtomicURL, TranslationBox) human readable explanation of what the Class represents.
- `requires` - (optional, ResourceArray, Property) a list of Properties that are required. If absent, none are required. These SHOULD have unique shortnames.
- `recommends` - (optional, ResourceArray, Property) a list of Properties that are recommended. These SHOULD have unique shortnames.
- `deprecatedProperties` - (optional, ResourceArray, Property) - a list of Properties that should no longer be used.
<!-- Maybe remove this next one? -->
<!-- - `disallowedProperties` - (optional, ResourceArray) a list of Properties that are not allowed.  If absent, all are allowed. -->
<!-- What are the consequences of this? How to deal with this field if there are more classes in aSSubject? -->
<!-- - `allowedProperties` - (optional, ResourceArray) a list of Properties that are allowed. If absent, none are required. -->

A resource indicates it is an _instance_ of that class by adding a `https://atomicdata.dev/properties/isA` Atom.

Example:

```ad3
["https://example.com/classes/Person","https://atomicdata.dev/properties/isA","https://atomicdata.dev/classes/Class"]
["https://example.com/classes/Person","https://atomicdata.dev/properties/recommends","https://example.com/classes/Person/recommends"]
["https://example.com/classes/Person/recommends","https://atomicdata.dev/properties/isA","https://atomicdata.dev/dataTypes/ResourceArray"]
```
