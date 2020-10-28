# Atomic Translations

Dealing with translations can be hard.
([See discussion on this subject here.](https://github.com/ontola/atomic-data/issues/6))

## TranslationBox

_URL: `https://atomicdata.dev/classes/TranslationBox`_

A TranslationBox is a collection of translated strings, uses to provide multiple translations.
It has a long list of optional properties, each corresponding to some language.
Each possible language Property uses the following URL template: `https://atomicdata.dev/languages/{langguageTag}`.
Use a [BCP 47](http://www.rfc-editor.org/rfc/bcp/bcp47.txt) language tag, e.g. `nl` or `en-US`.

For example:

```ndjson
["https://example.com/john","https://example.com/lifestory","https://example.com/johns/lifestory"]
["https://example.com/johns/lifestory","https://atomicdata.dev/langs/en-US","Well, John was born and later he died."]
["https://example.com/johns/lifestory","https://atomicdata.dev/langs/nl","Tsja, John werd geboren en stierf later."]
```

Every single property used for Translation strings are instances of the Translation class.

A translation string uses the [MDString](https://atomicdata.dev/datatypes/markdown) datatype, which means it allows Markdown syntax.
