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

# Design Documents

Instead of storing data in a document,
you might also have special documents that store other content,
such as functions.
The special documents are called "design documents".
{:shortdesc}

Design documents are [documents](document.html) that have an `_id` beginning with `_design/`.
They can be read and updated in the same way as any other document in the database.
Cloudant reads specific fields and values of design documents as functions.
Design documents are used to [build indexes](#indexes), [validate updates](#update-validators), and [format query results](#list-functions).

## Creating or updating a design document

-	**Method**: `PUT /$DATABASE/_design/design-doc`
-	**Request**: JSON of the design document information
-	**Response**: JSON status
-	**Roles permitted**: `_admin`

To create a design document, upload it to the specified database.

In these examples,
`$VARIABLES` might refer to standard or design documents.
To distinguish between them,
standard documents have an `_id` indicated by `$DOCUMENT_ID`,
while design documents have an `_id` indicated by `$DESIGN_ID`.

>	**Note**: If a design document is updated,
Cloudant deletes the indexes from the previous version,
and recreates the index from scratch.
If you need to make changes to a design document for a larger database,
have a look at the [Design Document Management Guide](../guides/design_document_management.html#managing-changes-to-a-design-document).

The structure of design document is as follows:

-	**`_id`**: Design Document ID
-	**`_rev`**: Design Document Revision
-	**views (optional)**: An object describing MapReduce views.
	-	**viewname** (one for each view): View Definition.
		-	**map**: Map Function for the view.
		-	**reduce (optional)**: Reduce Function for the view.
		-	**dbcopy (optional)**: Database name for storing view results.
-	**indexes (optional)**: An object describing search indexes.
	-	**index name** (one for each index): Index definition.
		-	**analyzer**: Object describing the analyzer to be used or an object with the following fields:
			-	**name**: Name of the analyzer. Valid values are `standard`, `email`, `keyword`, `simple`, `whitespace`, `classic`, and `perfield`.
			-	**stopwords (optional)**: An array of stop words.
				Stop words are words that should not be indexed.
				If this array is specified,
				it overrides the default list of stop words.
				The default list of stop words depends on the analyzer.
				The list of stop words for the standard analyzer is:
				`a`, `an`, `and`, `are`, `as`, `at`, `be`, `but`, `by`, `for`, `if`, `in`, `into`, `is`, `it`, `no`, `not`, `of`, `on`, `or`, `such`, `that`, `the`, `their`, `then`, `there`, `these`, `they`, `this`, `to`, `was`, `will`, and `with`.
			-	**default (for the per field analyzer)**: default language to use if there is no language specified for the field.
			-	**fields (for the per field analyzer)**: An object specifying which language to use to analyze each field of the index.
				Field names in the object correspond to field names in the index, that is, the first parameter of the index function.
				The values of the fields are the languages to be used, for example `english`.
		-	**index**: Function that handles the indexing.
-	**shows (optional)**: Show functions.
	-	**function name** (one for each function): Function definition.
-	**lists (optional)**: List functions.
	-	**function name** (one for each function): Function definition.

## Copying a Design Document

You can copy the latest version of a design document to a new document
by specifying the base document and target document.
The copy is requested using the `COPY` HTTP request.

>	**Note**:`COPY` is a non-standard HTTP command.

>	**Note**: Copying a design document does not automatically reconstruct the view indexes.
Like other views,
these are recreated the first time the new view is accessed.

The following example requests Cloudant to copy the design document `recipes` to the new design document `recipelist`,
and produces a response containing the ID and revision of the new document.

_Example command to copy a design document, using HTTP:_

```http
COPY /recipes/_design/recipes HTTP/1.1
Content-Type: application/json
Destination: /recipes/_design/recipelist
```
{:codeblock}

_Example command to copy a design document, using the command line:_

```sh
curl "https://$USERNAME:$PASSWORD@$ACCOUNT.cloudant.com/recipes/_design/recipes" \
	-X COPY \
	-H 'Content-Type: application/json' \
	-H 'Destination: /recipes/_design/recipelist'
```
{:codeblock}

_Example response to the copy request:_

```json
{
	"id": "recipes/_design/recipelist",
	"rev": "1-9c65296036141e575d32ba9c034dd3ee"
}
```
{:codeblock}

### The structure of the copy command

-	**Method**: `COPY /$DATABASE/_design/design-doc`
-	**Request**: None
-	**Response**: JSON describing the new document and revision.
-	**Roles permitted**: `_writer`
-	**Query Arguments**:
	-	**Argument**: `rev`
		-	**Description**:  Revision to copy from.
		-	**Optional**: yes
		-	**Type**: string
-	**HTTP Headers**
	-	**Header**: `Destination`
		-	**Description**: Destination document (and optional revision)
		-	**Optional**: no

The source design document is specified on the request line,
with the `Destination` HTTP Header of the request specifying the target document.

### Copying from a specific revision

To copy from a specific version,
add the `rev` argument to the query string.

The new design document is created using the specified revision of the source document.

_Example command to copy a specific revision of the design document, using HTTP:_

```http
COPY /recipes/_design/recipes?rev=1-e23b9e942c19e9fb10ff1fde2e50e0f5 HTTP/1.1
Content-Type: application/json
Destination: recipes/_design/recipelist
```
{:codeblock}

_Example command to copy a specific revision of the design document, using the command line:_

```sh
curl "https://$USERNAME:$PASSWORD@$ACCOUNT.cloudant.com/recipes/_design/recipes?rev=1-e23b9e942c19e9fb10ff1fde2e50e0f5" \
	-X COPY \
	-H 'Content-Type: application/json' \
	-H 'Destination: /recipes/_design/recipelist'
```
{:codeblock}

### Copying to an existing design document

To overwrite or copy to an existing document,
specify the current revision string for the target document,
using the `rev` parameter to the `Destination` HTTP Header string.

_Example command to overwrite an existing copy of the design document, using HTTP:_

```http
COPY /recipes/_design/recipes
Content-Type: application/json
Destination: recipes/_design/recipelist?rev=1-9c65296036141e575d32ba9c034dd3ee
```
{:codeblock}

_Example command to overwrite an existing copy of the design document, using the command line:_

```sh
curl "https://$USERNAME:$PASSWORD@$ACCOUNT.cloudant.com/recipes/_design/recipes" \
	-X COPY \
	-H 'Content-Type: application/json' \
	-H 'Destination: /recipes/_design/recipelist?rev=1-9c65296036141e575d32ba9c034dd3ee'
```
{:codeblock}

The return value is the ID and new revision of the copied document.

_Example response:_

```json
{
	"id" : "recipes/_design/recipes",
	"rev" : "2-55b6a1b251902a2c249b667dab1c6692"
}
```
{:codeblock}

## Deleting a design document

You can delete an existing design document.
Deleting a design document also deletes all of the associated view indexes,
and recovers the corresponding space on disk for the indexes in question.

To delete a design document successfully,
you must specify the current revision of the design document using the `rev` query argument.

_Example command to delete a design document, using HTTP:_

```http
DELETE /recipes/_design/recipes?rev=2-ac58d589b37d01c00f45a4418c5a15a8 HTTP/1.1
```
{:codeblock}

_Example command to delete a design document, using using the command line:_

```sh
curl "https://$USERNAME:$PASSWORD@$ACCOUNT.cloudant.com/recipes/_design/recipes?rev=2-ac58d589b37d01c00f45a4418c5a15a8" \
     -X DELETE
```
{:codeblock}

_Example response, containing the deleted document ID and revision:_

```json
{
	"id": "recipe/_design/recipes",
	"ok": true,
	"rev": "3-7a05370bff53186cb5d403f861aca154"
}
```
{:codeblock}

### The structure of the delete command

-	**Method**: `DELETE /db/_design/design-doc`
-	**Request**: None
-	**Response**: JSON of deleted design document.
-	**Roles permitted**: `_writer`
-	**Query Arguments**:
	-	**Argument**: `rev`
		-	**Description**: Current revision of the document for validation.
		-	**Optional**: yes
		-	**Type**: string
-	**HTTP Headers**
	-	**Header**: `If-Match`
		-	**Description**: Current revision of the document for validation.
		-	**Optional**: yes

## Views

An important use of design documents is for creating views.
These are discussed in more detail [here](creating_views.html).

## Rewrite rules

A design document can contain rules for URL rewriting, by using an array in the `rewrites` field.
Requests that match the rewrite rules must have a URL path that starts with `/$DATABASE/_design/doc/_rewrite`.

Each rule is a JSON object with 4 fields:

Field    | Description
---------|------------
`from`   | A path relative to `/$DATABASE/_design/doc/_rewrite`, used to match URLs to rewrite rules. Path elements that start with a `:` are treated as variables, and match any string that does not contain a `/`. A `*` can only appear at the end of the string, and matches any string - including slashes.
`method` | The HTTP method that should be matched on.
`query`  | The query part of the resulting URL. This is a JSON object containing the key/value pairs of the query.
`to`     | The path (relative to `/$DATABASE/_design/doc/` and not including the query part of the URL) that is the result of the rewriting step. Variables captured in `from` can be used in `to`. `*` can also be used and contains everything captured by the pattern in `from`.

_Example JSON describing some rewrite rules:_

```json
{
	"rewrites": [
		{
			"from": "/",
			"to": "index.html",
			"method": "GET",
			"query": {}
		},
		{
			"from": "/foo/:var",
			"to": "/foo",
			"method": "GET",
			"query": {"v": "var"}
		}
	]
}
```
{:codeblock}

### Example rewrite rules

The following table has some more examples of rewriting URL components:

Rule                                                           | URL                                       | Rewrite to                               | Tokens
---------------------------------------------------------------|-------------------------------------------|------------------------------------------|-------
`{"from": "/a/b", "to": "/some/"}`                             | `/$DATABASE/_design/doc/_rewrite/a/b?k=v` | `/$DATABASE/_design/doc/some?k=v`        | `k = v`
`{"from": "/a/b", "to": "/some/:var"}`                         | `/$DATABASE/_design/doc/_rewrite/a/b`     | `/$DATABASE/_design/doc/some/b?var=b`    | `var = b`
`{"from": "/a", "to": "/some/*"}`                              | `/$DATABASE/_design/doc/_rewrite/a`       | `/$DATABASE/_design/doc/some`            |
`{"from": "/a/*", "to": "/some/*}`                             | `/$DATABASE/_design/doc/_rewrite/a/b/c`   | `/$DATABASE/_design/doc/some/b/c`        |
`{"from": "/a", "to": "/some/*"}`                              | `/$DATABASE/_design/doc/_rewrite/a`       | `/$DATABASE/_design/doc/some`            |
`{"from": "/a/:foo/*","to": "/some/:foo/*"}`                   | `/$DATABASE/_design/doc/_rewrite/a/b/c`   | `/$DATABASE/_design/doc/some/b/c?foo=b`  | `foo = b`
`{"from": "/a/:foo", "to": "/some", "query": { "k": ":foo" }}` | `/$DATABASE/_design/doc/_rewrite/a/b`     | `/$DATABASE/_design/doc/some/?k=b&foo=b` | `foo =:= b`
`{"from": "/a", "to": "/some/:foo" }`                          | `/$DATABASE/_design/doc/_rewrite/a?foo=b` | `$DATABASE/_design/doc/some/b&foo=b`     | `foo = b`

## Indexes

All queries operate on pre-defined indexes defined in design documents.
These indexes are:

*	[Search](search.html)
*	[MapReduce](creating_views.html)

For example,
to create a design document used for searching,
you must ensure that two conditions are true:

1.	You have identified the document as a design document by having an `_id` starting with `_design/`.
2.	A [search index](search.html) has been created within the document
	by [updating](document.html#update) the document with the appropriate field
	or by [creating](document.html#create) a new document containing the search index.

As soon as the search index design document exists and the index has been built,
you can make queries using it.

For more information about search indexing,
refer to the [search](search.html) section of this documentation.

### General notes on functions in design documents

Functions in design documents are run on multiple nodes for each document,
and might be run several times.
To avoid inconsistencies,
they need to be [idempotent ![External link icon](../images/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/Idempotence#Computer_science_meaning){:new_window},
meaning they need to behave identically when run multiple times or on different nodes.
In particular,
you should avoid using functions that generate random numbers or return the current time.

## List Functions

Use list functions to customize the format of
[MapReduce](creating_views.html#using-views) query results.
A good example of their use is when you want to access Cloudant directly from a browser,
and need data to be returned in a different format,
such as HTML.

You can add any query parameters to the request that would normally be used for a view request.

Instead of using a MapReduce index, you can also use `_all_docs`.

>	**Note**: The result of a list function is not stored.
This means that the function is executed every time a request is made.
As a consequence,
using MapReduce functions might be more efficient.
For web and mobile applications,
consider whether any computations done in a list function would be better placed in the application tier.

When you define a list function,
you use it by sending a `GET` request to
`https://$USERNAME.cloudant.com/$DATABASE/$DESIGN_ID/_list/$LIST_FUNCTION/$MAPREDUCE_INDEX`.
In this request:

*	`$LIST_FUNCTION` is the name of list function you defined.
*	`$MAPREDUCE_INDEX` is the name of the index providing the query results you want to format.

List functions require two arguments:
[`head`](#head) and [`req`](#req).

The `head` argument identifies the documents to be processed by the list function.

The `req` argument contains additional information about the request.
It enables you to create list functions that are more dynamic,
because they are based on additional factors such as query parameters or the user context.

The values within the `req` argument are similar to the query parameters described
[here](cloudant_query.html#query-parameters).

_Example design document referencing a list function, expressed using JSON:_

```json
{
	"_id": "_design/list_example",
	"lists": {
		"FUNCTION_NAME": "function (head, req) { ... }"
	}
}
```
{:codeblock}

_Example of a list function, in pseudo-code:_

```javascript
function (head, req) {
	// specify our headers
	start({
		headers: {
			"Content-Type": 'text/html'
		}
	});

	// send the response, line by line
	send('<html><body><table>');
	send('<tr><th>ID</th><th>Key</th><th>Value</th></tr>')
	while(row = getRow()){
		send(''.concat(
			'<tr>',
			'<td>' + toJSON(row.id) + '</td>',
			'<td>' + toJSON(row.key) + '</td>',
			'<td>' + toJSON(row.value) + '</td>',
			'</tr>'
		));
	}
	send('</table></body></html>');
}
```
{:codeblock}

_Example invocation of a list function, using HTTP:_

```http
GET /$DATABASE/$DESIGN_ID/_list/$LIST_FUNCTION/$MAPREDUCE_INDEX HTTP/1.1
```
{:codeblock}

_Example invocation of a list function, using the command line:_

```sh
curl "https://$ACCOUNT.cloudant.com/$DATABASE/$DESIGN_ID/_list/$LIST_FUNCTION/$MAPREDUCE_INDEX" \
	-u "$USERNAME:$PASSWORD"
```
{:codeblock}

<!--

_Example invocation of a list function, using Javascript:_

```javascript
var nano = require('nano');
var account = nano("https://"+$USERNAME+":"+$PASSWORD+"@"+$USERNAME+".cloudant.com");
var db = account.use($DATABASE);

db.view_with_list($DESIGN_ID, $MAPREDUCE_INDEX, $LIST_FUNCTION, function (err, body, headers) {
	if (!err) {
		console.log(body);
	}
});
```
{:codeblock}

-->

### head

Field        | Description
-------------|-------------
`offset`     | Offset where the document list started
`total_rows` | Number of documents in the view

### req

Field            | Description
-----------------|-------------
`body`           | Request body data as string. If the request method is `GET`, this field contains the value `undefined`. If the method is `DELETE` or `HEAD`, the value is "" (the empty string).
`cookie`         | Cookies object.
`form`           | Form data object. Contains the decoded body as key-value pairs if the Content-Type header was `application/x-www-form-urlencoded`.
`headers`        | Request headers object.
`id`             | Requested document ID string if it was specified or null otherwise.
`info`           | Database information
`method`         | Request method as string or array. String value is one of the methods: `HEAD`, `GET`, `POST`, `PUT`, `DELETE`, `OPTIONS`, or `TRACE`. Alternatively, the method is represented as an array of character codes.
`path`           | List of requested path sections.
`peer`           | Request source IP address.
`query`          | URL query parameters object. Multiple keys are not supported, therefore the last duplicate key overrides the others.
`requested_path` | List of actual requested path section.
`raw_path`       | Raw requested path string.
`secObj`         | The database's [security object](authorization.html#viewing-permissions)
`userCtx`        | Context about the currently authenticated user, specifically their `name` and `roles` within the current database.
`uuid`           | A generated UUID.

## Show Functions

Show functions are similar to [list functions](#list-functions),
but are used to format individual documents.
They are used when you want to access Cloudant directly from a browser,
and need data to be returned in a different format,
such as HTML.

>	**Note**: The result of a show function is not stored.
This means that the function is executed every time a request is made.
As a consequence,
using [map functions](creating_views.html#a-simple-view) might be more efficient.
For web and mobile applications,
consider whether any computations done in a show function would be better placed in the application tier.

Show functions require two arguments: `doc`, and [req](#req).

`doc` is the document requested by the show function.

The [`req`](#req) argument contains additional information about the request.
It enables you to create show functions that are more dynamic,
because they are based on additional factors such as query parameters or the user context.

The [`req`](#req) argument corresponds to that used in a [list function](#list-functions).

When you have defined a show function,
you query it by sending a `GET` request to `https://$USERNAME.cloudant.com/$DATABASE/$DESIGN_ID/_show/$SHOW_FUNCTION/$DOCUMENT_ID`,
where `$SHOW_FUNCTION` is the name of the function that is included in the design document `$DESIGN_ID`.

_Example of a design document with a show function:_

```json
{
	"_id": "_design/show_example",
	"shows": {
		"FUNCTION_NAME": "function (doc, req) { ... }"
	}
}
```
{:codeblock}

_Example of a show function:_

```javascript
function (doc, req) {
	if (doc) {
		return "Hello from " + doc._id + "!";
	} else {
		return "Hello, world!";
	}
}
```
{:codeblock}

_Example of a show function query, using HTTP:_

```http
GET /$DATABASE/$DESIGN_ID/_show/$SHOW_FUNCTION/$DOCUMENT_ID HTTP/1.1
Host: $USERNAME.cloudant.com
```
{:codeblock}

_Example of a show function query, using the command line:_

```sh
curl https://$USERNAME.cloudant.com/$DATABASE/$DESIGN_ID/_show/$SHOW_FUNCTION/$DOCUMENT_ID \
     -u $USERNAME
```
{:codeblock}

<!--

_Example of a show function query, using Javascript:_

```javascript
var nano = require('nano');
var account = nano("https://"+$USERNAME+":"+$PASSWORD+"@"+$USERNAME+".cloudant.com");
var db = account.use($DATABASE);

db.show($DESIGN_ID, $SHOW_FUNCTION, $DOCUMENT_ID, function (err, body) {
	if (!err) {
		console.log(body);
	}
});
```
{:codeblock}

-->

## Update Handlers

Update handlers are custom functions that create or update a document.
They are used for tasks such as providing server-side modification timestamps,
and performing document updates to individual fields without the latest revision.

Update handlers require two arguments: `doc` and [req](#req).

If a document ID is provided in the request to the update handler,
then `doc` is the document corresponding to that ID.
If no ID is provided,
`doc` is `null`.

The [`req`](#req) argument contains additional information about the request.
It enables you to create update handlers that are more dynamic,
because they are based on additional factors such as query parameters or the user context.

The [`req`](#req) argument corresponds to that used in a [list function](#list-functions).

Update handler functions must return an array of two elements.
The first element is the document to save,
or `null` if you do not want to save the document.
The second element is the response body.

There are two methods for querying update handlers:

Method | URL
-------|------
`POST` | `https://$USERNAME.cloudant.com/$DATABASE/$DESIGN_ID/_update/$UPDATE_HANDLER`
`PUT`  | `https://$USERNAME.cloudant.com/$DATABASE/$DESIGN_ID/_update/$UPDATE_HANDLER/$DOCUMENT_ID`

In these methods:

Variable          | Purpose
------------------|--------
`$DESIGN_ID`      | The ID of the document defining the update handler.
`$DOCUMENT_ID`    | The ID of the document that the handler must work with.
`$UPDATE_HANDLER` | The name of the update handler.

_Example of a design document with an update handler:_

```json
{
	"_id": "_design/update_example",
	"updates": {
		"UPDATE_HANDLER_NAME": "function (doc, req) { ... }"
	}
}
```
{:codeblock}

_Example of an update handler:_

```javascript
function(doc, req){
	if (!doc){
		if ('id' in req && req.id){
			// create new document
			return [{_id: req.id}, 'New World']
		}
		// change nothing in database
		return [null, 'Empty World']
	}
	doc.world = 'hello';
	doc.edited_by = req.userCtx.name
	return [doc, 'Edited World!']
}
```
{:codeblock}

_Example of an update handler query, using HTTP:_

```http
POST /$DATABASE/$DESIGN_ID/_update/$UPDATE_HANDLER HTTP/1.1
Content-Type: application/json
```
{:codeblock}

_Example of an update handler query, using the command line:_

```sh
curl "https://$ACCOUNT.cloudant.com/$DATABASE/$DESIGN_ID/_update/$UPDATE_HANDLER" \
	-X POST \
	-H 'Content-Type: application/json' \
	-u "$USERNAME:$PASSWORD" \
	-d "$JSON"
```
{:codeblock}

<!--

_Example of an update handler query, using Javascript:_

```javascript
var nano = require('nano');
var account = nano("https://"+$USERNAME+":"+$PASSWORD+"@"+$USERNAME+".cloudant.com");
var db = account.use($DATABASE);

db.atomic($DESIGN_ID, $UPDATE_HANDLER, $DOCUMENT_ID, $JSON, function (err, body) {
	if (!err) {
		console.log(body);
	}
});
```
{:codeblock}

-->

## Filter Functions

Filter functions are design documents that enable you to filter
the [changes feed](database.html#get-changes).
They work by applying tests to each of the objects included in the changes feed.

If any of the function tests fail,
the object is 'removed' or 'filtered' from the feed.
If the function returns a `true` result when applied to a change,
the change remains in the feed.
This means that filter functions let you 'remove' or 'ignore' changes that you do not want to monitor.

>	**Note**: Filter functions can also be used to modify
a [replication task](advanced_replication.html#filtered-replication).

Filter functions require two arguments: `doc` and [`req`](#req).

The `doc` argument represents the document being tested for filtering.

The `req` argument contains additional information about the request.
It enables you to create filter functions that are more dynamic,
because they are based on additional factors such as query parameters or the user context.

For example,
you could control aspects of the filter function tests by using dynamic values provided as part of the HTTP request.
In many filter function use cases,
however,
only the `doc` parameter is used.

The [`req`](#req) argument corresponds to that used in a [list function](#list-functions).

_Example design document containing a filter function:_

```json
{
	"_id":"_design/FILTER_EXAMPLE",
	"filters": {
		"FILTER_EXAMPLE": "function (doc, req) { ... }"
	}
}
```
{:codeblock}

_Example of a filter function:_

```javascript
function(doc, req){
	// we need only `mail` documents
	if (doc.type != 'mail'){
		return false;
	}
	// we're interested only in `new` ones
	if (doc.status != 'new'){
		return false;
	}
	return true; // passed!
}
```
{:codeblock}

To apply a filter function to the changes feed,
include the `filter` parameter in the `_changes` query,
providing the name of the filter to use.

_Example of an filter function applied to a `_changes` query, using HTTP:_

```http
GET /$DATABASE/_changes?filter=$DESIGN_ID/$FILTER_FUNCTION HTTP/1.1
```
{:codeblock}

_Example of an filter function applied to a `_changes` query, using the command line:_

```sh
curl "https://$ACCOUNT.cloudant.com/$DATABASE/_changes?filter=$DESIGN_ID/$FILTER_FUNCTION" \
     -u "$USERNAME:$PASSWORD"
```
{:codeblock}

The `req` argument gives you access to aspects of the HTTP request using the `query` property.

_Example of supplying a `req` argument, using HTTP:

```http
GET /$DATABASE/_changes?filter=$DESIGN_ID/$FILTER_FUNCTION&status=new HTTP/1.1
```
{:codeblock}

_Example of supplying a `req` argument, using the command line:

```sh
curl "https://$ACCOUNT.cloudant.com/$DATABASE/_changes?filter=$DESIGN_ID/$FILTER_FUNCTION&status=new" \
	-u "$USERNAME:$PASSWORD"
```
{:codeblock}

_Example filter using a supplied `req` argument:_

```javascript
function(doc, req){
	// we need only `mail` documents
	if (doc.type != 'mail'){
		return false;
	}
	// we're interested only in `new` ones
	if (doc.status != req.query.status){
		return false;
	}
	return true; // passed!
}
```
{:codeblock}

### Predefined filter functions

A number of predefined filter functions are available:

*	[`_design`](#the-_design-filter): accepts only changes to design documents.
*	[`_doc_ids`](#the-_doc_ids-filter): accepts only changes for documents whose ID is specified in the `doc_ids` parameter or supplied JSON document.
*	[`_selector`](#the-_selector-filter): accepts only changes for documents which match a specified selector, defined using the same [selector syntax](cloudant_query.html#selector-syntax) used for [`_find`](cloudant_query.html#finding-documents-using-an-index).
*	[`_view`](#the-_view-filter): allows you to use an existing [map function](creating_views.html#a-simple-view) as the filter.

#### The `_design` filter

The `_design` filter accepts changes only for design documents within the requested database.

The filter does not require any arguments.

Changes are listed for _all_ the design documents within the database.

_Example application of the `_design` filter, using HTTP:_

```http
GET /$DATABASE/_changes?filter=_design HTTP/1.1
```
{:codeblock}

_Example application of the `_design` filter, using the command line:_

```sh
curl "https://$ACCOUNT.cloudant.com/$DATABASE/_changes?filter=_design" \
     -u "$USERNAME:$PASSWORD"
```
{:codeblock}

_Example response (abbreviated) after applying the `_design` filter:_

```json
{
    ...
    "results": [
        {
            "changes": [
                {
                    "rev": "10-304...4b2"
                }
            ],
            "id": "_design/ingredients",
            "seq": "8-g1A...gEo"
        },
        {
            "changes": [
                {
                  "rev": "123-6f7...817"
                }
            ],
            "deleted": true,
            "id": "_design/cookbook",
            "seq": "9-g1A...4BL"
        },
        ...
    ]
}
```
{:codeblock}

#### The `_doc_ids` filter

The `_doc-ids` filter accepts only changes for documents with specified IDs.
The IDs are specified in a `doc_ids` parameter,
or within a JSON document supplied as part of the original request.

_Example application of the `_doc_ids` filter, using HTTP:_

```http
POST /$DATABASE/_changes?filter=_doc_ids HTTP/1.1
```
{:codeblock}

_Example application of the `_doc_ids` filter, using the command line:_

```sh
curl "https://$ACCOUNT.cloudant.com/$DATABASE/_changes?filter=_doc_ids" \
     -u "$USERNAME:$PASSWORD"
```
{:codeblock}

_Example JSON document listing document IDs to match during filtering:_

```json
{
    "doc_ids": [
      "ExampleID"
    ]
}
```
{:codeblock}

_Example response (abbreviated) after filtering by `_docs_ids`:_

```json
{
    "last_seq": "5-g1A...o5i",
    "pending": 0,
    "results": [
        {
            "changes": [
                {
                  "rev": "13-bcb...29e"
                }
            ],
            "id": "ExampleID",
            "seq":  "5-g1A...HaA"
        }
    ]
}
```
{:codeblock}

#### The `_selector` filter

The `_selector` filter accepts only changes for documents which match a specified selector,
defined using the same [selector syntax](cloudant_query.html#selector-syntax) used
for [`_find`](cloudant_query.html#finding-documents-using-an-index).

For more examples showing use of this filter,
see the information on [selector syntax](cloudant_query.html#selector-syntax).

_Example application of the `_selector` filter, using HTTP:_

```http
POST /$DATABASE/_changes?filter=_selector HTTP/1.1
```
{:codeblock}

_Example application of the `_selector` filter, using the command line:_

```sh
curl "https://$ACCOUNT.cloudant.com/$DATABASE/_changes?filter=_selector" \
     -u "$USERNAME:$PASSWORD"
```
{:codeblock}

_Example JSON document containing the selector expression to use during filtering:_

```json
{
    "selector": {
        "_id": {
          "$regex": "^_design/"
        }
    }
}
```
{:codeblock}

_Example response (abbreviated) after filtering using a selector:_

```json
{
    "last_seq": "11-g1A...OaA",
    "pending": 0,
    "results": [
        {
            "changes": [
                {
                  "rev": "10-304...4b2"
                }
            ],
            "id": "_design/ingredients",
            "seq": "8-g1A...gEo"
        },
        {
            "changes": [
                {
                  "rev": "123-6f7...817"
                }
            ],
            "deleted": true,
            "id": "_design/cookbook",
            "seq": "9-g1A...4BL"
        },
        {
            "changes": [
                {
                  "rev": "6-5b8...8f3"
                }
            ],
            "deleted": true,
            "id": "_design/meta",
            "seq": "11-g1A...Hbg"
        }
    ]
}
```
{:codeblock}

#### The `_view` filter

The `_view` filter allows you to use an existing [map function](creating_views.html#a-simple-view) as the filter.

If the map function emits any output as a result of processing a given document,
then the filter considers the document to be allowed and so includes it in the list of documents that have changed.

_Example application of the `_view` filter, using HTTP:_

```http
GET /$DATABASE/_changes?filter=_view&view=$DESIGNDOC/$VIEWNAME HTTP/1.1
```
{:codeblock}

_Example application of the `_view` filter, using the command line:_

```sh
curl "https://$ACCOUNT.cloudant.com/$DATABASE/_changes?filter=_view&view=$DESIGNDOC/$VIEWNAME" \
     -u "$USERNAME:$PASSWORD"
```
{:codeblock}

_Example response (abbreviated) after filtering using a map function:_

```json
{
    "last_seq": "5-g1A...o5i",
    "results": [
        {
            "changes": [
                {
                  "rev": "13-bcb...29e"
                }
            ],
            "id": "ExampleID",
            "seq":  "5-g1A...HaA"
        }
    ]
}
```
{:codeblock}

## Update Validators

Update validators determine whether a document should be written to disk when insertions and updates are attempted.
They do not require a query because they implicitly run during this process.
If a change is rejected,
the update validator responds with a custom error.

Update validators require four arguments:

Argument  | Purpose
----------|--------
`newDoc`  | The version of the document passed in the request.
`oldDoc`  | The version of the document currently in the database, or `null` if there is none.
`secObj`  | The [security object](authorization.html#viewing-permissions) for the database.
`userCtx` | Context regardingthe currently authenticated user, such as `name` and `roles`.

>   **Note**: Update validators do not apply when a design document is updated by an admin user.
    This is to ensure that admins can never accidentally lock themselves out.

_Example design document with an update validator:_

```json
{
	"_id": "_design/validator_example",
	"validate_doc_update": "function(newDoc, oldDoc, userCtx, secObj) { ... }"
}
```
{:codeblock}

_Example of an update validator:_

```javascript
function(newDoc, oldDoc, userCtx, secObj) {
	if (newDoc.address === undefined) {
		throw({forbidden: 'Document must have an address.'});
	}
}
```
{:codeblock}

_Example response from an update validator:_

```json
{
	"error": "forbidden",
	"reason": "Document must have an address."
}
```
{:codeblock}

## Retrieving information about a design document

There are two endpoints available that provide you with more information about
design documents: [`_info`](#the-_info-endpoint) and [`_search_info`](#the-_search_info-endpoint).

### The `_info` endpoint

The `_info` endpoint returns information about a given design document,
including the index,
index size,
and current status of the design document and associated index information.

-	**Method**: `GET /db/_design/design-doc/_info`
-	**Request**: None
-	**Response**: JSON containing the design document information.
-	**Roles permitted**: `_reader`

_Example of retrieving information about the `recipesdd` design document from within the `recipes` database,
using HTTP:_

```http
GET /recipes/_design/recipesdd/_info HTTP/1.1
```
{:codeblock}

_Example of retrieving information about the `recipesdd` design document from within the `recipes` database,
using the command line:_

```sh
curl "https://$ACCOUNT.cloudant.com/recipes/_design/recipesdd/_info" \
     -u "$USERNAME:$PASSWORD"
```
{:codeblock}

The individual fields in the JSON response are as follows:

-	**name**: Name or ID of Design Document.
-	**view_index**: View Index
	-	**compact_running**: Indicates whether a compaction routine is currently running on the view.
	-	**disk_size**: Size in bytes of the view as stored on disk.
	-	**language**: Language used for defining views.
	-	**purge_seq**: The purge sequence that has been processed.
	-	**signature**: MD5 signature of the views for the design document.
	-	**update_seq**: The update sequence of the corresponding database that has been indexed.
	-	**updater_running**: Indicates if the view is currently being updated.
	-	**waiting_clients**: Number of clients waiting on views from this design document.
	-	**waiting_commit**: Indicates if there are outstanding commits to the underlying database that need to processed

_Example response in JSON format:_

```json
{
	"name" : "recipesdd",
	"view_index": {
		"compact_running": false,
		"updater_running": false,
		"language": "javascript",
		"purge_seq": 10,
		"waiting_commit": false,
		"waiting_clients": 0,
		"signature": "fc65594ee76087a3b8c726caf5b40687",
		"update_seq": 375031,
		"disk_size": 16491
	}
}
```
{:codeblock}

### The `_search_info` endpoint

The `_search_info` endpoint returns information about a specified search
that is defined within a given design document.

-	**Method**: `GET /db/_design/design-doc/_search_info/yourSearch`
-	**Request**: None
-	**Response**: JSON containing information about the specified search.
-	**Roles permitted**: `_reader`

_Example of getting information about the `description` search,
defined within the `app` design document stored in the `foundbite` database, using HTTP:_

```http
GET /foundbite/_design/app/_search_info/description HTTP/1.1
```
{:codeblock}

_Example of getting information about the `description` search,
defined within the `app` design document stored in the `foundbite` database, using the command line:_

```sh
curl "https://$USERNAME.cloudant.com/foundbite/_design/app/_search_info/description" \
	-u "$USERNAME:$PASSWORD"
```
{:codeblock}

The individual fields in the returned JSON structure are as follows:

-	**name**: Name or ID of the Search within the Design Document.
-	**search_index**: The Search Index
	-	**pending_seq**: The sequence number of changes in the database that have reached the Lucene index,
		both in memory and on disk.
	-	**doc_del_count**: Number of deleted documents in the index.
	-	**doc_count**: Number of documents in the index.
	-	**disk_size**: The size of the index on disk, in bytes.
	-	**committed_seq**: The sequence number of changes in the database that have been committed
		to the Lucene index on disk.

_Example response in JSON format:_

```json
{
	"name": "_design/app/description",
	"search_index": {
		"pending_seq": 63,
		"doc_del_count": 3,
		"doc_count": 10,
		"disk_size": 9244,
		"committed_seq": 63
	}
}
```
{:codeblock}
