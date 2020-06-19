# Base Datatypes

The Atomic Base Datatypes consist of some of the most commonly used datatypes.

## Slug

A string with a limited set of allowed characters, used in IDE / Text editor context.

## Atomic URI

A URI that should resolve to an Atomic Resource.

## URI

A Uniform Resource Identifier, preferably a URL.
Could be HTTPS, or any other type of schema.

## String

_uri: `https://atomicdata.dev/datatypes/string`_

UTF-8 String, no max character count.
Newlines use backslash escaped `\n` characters.
Should not contain language specific data, use a `langstring` instead.

e.g. `String time! \n Second line!`

## Multilingual String (langstring)

_uri: `https://atomicdata.dev/datatypes/langstring`_

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

Signed Integer, max 64 bit.
Max value: [`9223372036854775807`](https://en.wikipedia.org/wiki/9,223,372,036,854,775,807)

e.g. `-420`

## Boolean

True or false, one or zero.

**String serialization**

`true` or `false`.

**Binary serialization**

Use a single bit one boolean.

1 for `true`, or 0 for `false`.

##  Datetime

ISO 8601 encoded string.

e.g. `2020-06-11`

## MIMEFile

Any type of file, starting with its [mime type](https://www.iana.org/assignments/media-types/media-types.xhtml)
Although MIME types [often don't exist in your OS](https://stackoverflow.com/a/29019569/2502163), specifying them seems like a good idea.

**String serialization**

Start with the mimetype string, do a newline `\n` and continue with the UTF-8 stringified data.

- e.g. `application/text\nOh hi mark`
- e.g. `text/html\n<html><p>oh, hi mark</p></html>`

**Binary serialization**

## ResourceArray

Sequential, ordered list of Atomic URIs.
Serialized as a JSON array with strings.
Note that other types of arrays are not included in this spec, but can be perfectly valid.

- e.g. `["https://example.com/1", "https://example.com/1"]`
