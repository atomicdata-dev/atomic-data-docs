# Atomic Schema: Base Datatypes

The Atomic Base Datatypes consist of some of the most commonly used [Datatypes](concepts.md#Datatype).

## Slug

_URL: `https://atomicdata.dev/datatypes/slug`_

A string with a limited set of allowed characters, used in IDE / Text editor context.

## Atomic URI

_URL: `https://atomicdata.dev/datatypes/atomicURI`_

A URL that should resolve to an [Atomic Resource](../core/concepts.md#Resource).

## URI

_URL: `https://atomicdata.dev/datatypes/URI`_

A Uniform Resource Identifier, preferably a URL (i.e. an URI that can be fetched).
Could be HTTP, HTTPS, or any other type of schema.

## String

_URL: `https://atomicdata.dev/datatypes/string`_

UTF-8 String, no max character count.
Newlines use backslash escaped `\n` characters.
Should not contain language specific data, use a `langstring` instead.

e.g. `String time! \n Second line!`

## Langstring

_URL: `https://atomicdata.dev/datatypes/langstring`_

<!--
So this is something I'm having serious doubts on.
It seems so verbose and hard to parse.
However, the underlying problem is kind of tough: we want <subject> <predicate> combination uniqueness...
... but we also want to have multilingual strings that can be added later.
-->

Array of special UTF-8 Strings.
Each element of the Array starts with a language string code, followed by a newline.

e.g. `["en-US\nHi there"],["nl-NL\nHallo daar"]`

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

##  Datetime

_URL: `https://atomicdata.dev/datatypes/dateTime`_

ISO 8601 encoded string.

e.g. `2020-06-11`

## MIMEFile

_URL: `https://atomicdata.dev/datatypes/mimeFile`_

Any type of file, starting with its [mime type](https://www.iana.org/assignments/media-types/media-types.xhtml)
Although MIME types [often don't exist in your OS](https://stackoverflow.com/a/29019569/2502163), specifying them seems like a good idea.

**String serialization**

Start with the mimetype string, do a newline `\n` and continue with the UTF-8 stringified data.

- e.g. `application/text\nOh hi mark`
- e.g. `text/html\n<html><p>oh, hi mark</p></html>`

**Binary serialization**

## ResourceArray

_URL: `https://atomicdata.dev/datatypes/resourceArray`_

Sequential, ordered list of Atomic URIs.
Serialized as a JSON array with strings.
Note that other types of arrays are not included in this spec, but can be perfectly valid.

- e.g. `["https://example.com/1", "https://example.com/1"]`

##
