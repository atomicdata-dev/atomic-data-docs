# Atomic Schema: Datatypes

The Atomic Datatypes consist of some of the most commonly used [Datatypes](classes.md#Datatype).

## Slug

_URL: `https://atomicdata.dev/datatypes/slug`_

A string with a limited set of allowed characters, used in IDE / Text editor context.
Similar to [`xsd:token`](http://books.xmlschemata.org/relaxng/ch19-77319.html)

## Atomic URL

_URL: `https://atomicdata.dev/datatypes/atomicURL`_

A URL that should resolve to an [Atomic Resource](../core/concepts.md#Resource).

## URI

_URL: `https://atomicdata.dev/datatypes/URI`_

A Uniform Resource Identifier, preferably a URL (i.e. an URI that can be fetched).
Could be HTTP, HTTPS, or any other type of schema.

## String

_URL: `https://atomicdata.dev/datatypes/string`_

UTF-8 String, no max character count.
Newlines use backslash escaped `\n` characters.
Should not contain language specific data, use a [TranslationBox](translations.md) instead.

e.g. `String time! \n Second line!`

## Integer

_URL: `https://atomicdata.dev/datatypes/integer`_

Signed Integer, max 64 bit.
Max value: [`9223372036854775807`](https://en.wikipedia.org/wiki/9,223,372,036,854,775,807)

e.g. `-420`

## Boolean

_URL: `https://atomicdata.dev/datatypes/boolean`_

True or false, one or zero.

**String serialization**

`true` or `false`.

**Binary serialization**

Use a single bit one boolean.

1 for `true`, or 0 for `false`.

##  DateTime

_URL: `https://atomicdata.dev/datatypes/dateTime`_

ISO 8601 encoded string.

e.g. `2020-06-11`

## ResourceArray

_URL: `https://atomicdata.dev/datatypes/resourceArray`_

Sequential, ordered list of Atomic URIs.
Serialized as a JSON array with strings.
Note that other types of arrays are not included in this spec, but can be perfectly valid.
([discussion]())

- e.g. `["https://example.com/1", "https://example.com/1"]`
