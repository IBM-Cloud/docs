---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# JSON

The majority of requests and responses to and from Cloudant
use the [JavaScript Object Notation (JSON) ![External link icon](../images/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/JSON){:new_window}
for formatting the content and structure of the data and responses.
{:shortdesc}

In Cloudant databases,
the JSON object is used to represent a variety of structures,
including all documents in a database.

Parsing JSON into a JavaScript object is supported through the `JSON.parse()` function in JavaScript,
or through various [libraries](../libraries/index.html)
that perform the parsing of the content into a JavaScript object for you.
[Libraries](../libraries/index.html) for parsing and generating JSON
are available for many major programming languages.

JSON is used because it is the simplest and easiest solution for working with data using a web browser.
This is because JSON structures can be evaluated and used as JavaScript objects within the web browser environment.
JSON also integrates with the server-side JavaScript used within Cloudant.
JSON documents are always UTF-8 encoded.

>   **Note**: Care should be taken to ensure that:

-   Your JSON structures are valid.
    Invalid structures cause Cloudant to return an HTTP status code of [400 (bad request)](../api/http.html#400).
-   You normalize strings in JSON documents retrieved from Cloudant,
    before you compare them.
    This is because Unicode normalization might have been applied,
    so that a string stored and then retrieved is not identical on a binary level.

JSON supports the same basic types as supported by JavaScript:

-   [Numbers](#numbers)
-   [Strings](#strings)
-   [Booleans](#booleans)
-   [Arrays](#arrays)
-   [Objects](#objects)

## Numbers

Numbers can be integer or floating point values.

_Example of a number in JSON format:_

```json
123
```
{:codeblock}

## Strings

String should be enclosed by double-quotes. Strings support Unicode characters and backslash escaping.

_Example of a string in JSON format:_

```json
"A String"
```
{:codeblock}

## Booleans

A `true` or `false` value.

_Example of a boolean in JSON format:_

```json
{
  "value": true
}
```
{:codeblock}

## Arrays

A list of values enclosed in brackets. The values enclosed can be any valid JSON.

_Example of an array in JSON format:_

```json
[
    "one",
    2,
    "three",
    [],
    true,
    {
        "foo":
        "bar"
    }
]
```
{:codeblock}

_Example of an array in JSON format (linear):_

```json
[ "one", 2, "three", [], true, { "foo": "bar" } ]
```
{:codeblock}

## Objects

A set of key/value pairs,
such as an associative array,
or a hash.
The key must be a string,
but the value can be any of the supported JSON values.

_Example of a JSON object:_

```json
{
    "servings" : 4,
    "subtitle" : "Easy to make in advance, and then cook when ready",
    "cooktime" : 60,
    "title" : "Chicken Coriander"
}
```
{:codeblock}
