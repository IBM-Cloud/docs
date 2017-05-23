---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Acrolinx: 2017-01-13 -->

# Search

Search indexes,
which are defined in design documents,
allow databases to be queried by using
[Lucene Query Parser Syntax ![External link icon](../images/launch-glyph.svg "External link icon")](http://lucene.apache.org/core/4_3_0/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Overview){:new_window}.
{:shortdesc}

Search indexes are defined by an index function,
similar to a map function in [MapReduce views](creating_views.html#creating-views).
The index function decides what data to index and store in the index.

_Example design document that defines a search index:_

```json
{
	"_id": "_design/search_example",
	"indexes": {
		"animals": {
			"index": "function(doc){ ... }"
		}
	}
}
```
{:codeblock}

## Index functions

>	**Note**: Attempting to index by using a data field that does not exist fails.
To avoid this problem,
use an appropriate [guard clause](#index-guard-clauses).

The function that is contained in the index field is a JavaScript function that is called for each document in the database.
The function takes the document as a parameter,
extracts some data from it,
and then calls the function that is defined in the `index` field to index that data.

The `index` function takes three parameters, where the third parameter is optional.

The first parameter is the name of the field you intend to use when querying the index,
and which is specified in the Lucene syntax portion of subsequent queries.
An example appears in the following query:

```
query=color:red
```
{:codeblock}

The Lucene field name `color` is the first parameter of the `index` function.

The `query` parameter can be abbreviated to `q`,
so another way of writing the query is as follows:

```
q=color:red
```
{:codeblock}

If the special value `"default"` is used when you define the name,
you do not have to specify a field name at query time.
The effect is that the query can be simplified:

```
query=red
```
{:codeblock}

The second parameter is the data to be indexed.

The third, optional parameter is a JavaScript object with the following fields:

<table border='1'>

<tr>
    <th>Option</th><th>Description</th><th>Values</th><th>Default</th>
</tr>
<tr>
    <td><code>boost</code></td>
    <td>A number that specifies the relevance in search results.
    Content that is indexed with a boost value greater than 1
    is more relevant than content that is indexed without a boost value.
    Content with a boost value less than one is not so relevant.</td>
    <td>A positive floating point number</td>
    <td>1 (no boosting)</td>
</tr>
<tr>
    <td><code>facet</code></td>
    <td>Creates a faceted index.
    For more information,
    see <a href="#faceting">Faceting</a>.</td>
    <td><code>true</code>,
    <code>false</code></td>
    <td><code>false</code></td>
</tr>
<tr>
    <td><code>index</code></td>
    <td>Whether the data is indexed,
    and if so,
    how.
    If set to <code>false</code> or <code>no</code>,
    the data cannot be used for searches,
    but can still be retrieved from the index if <code>store</code> is set to <code>true</code>.
    For more information,
    see <a href="#analyzers">Analyzers</a>.</td>
    <td><code>analyzed</code>,
    <code>analyzed_no_norms</code>,
    <code>false</code>,
    <code>no</code>,
    <code>not_analyzed</code>,
    <code>not_analyzed_no_norms</code></td>
    <td><code>analyzed</code></td>
</tr>
<tr>
    <td><code>store</code></td>
    <td>If <code>true</code>,
    the value is returned in the search result;
    otherwise,
    the value is not returned.</td>
    <td><code>true</code>,
    <code>false</code></td>
    <td><code>false</code></td>
</tr>
</table>

>	**Note**: If you do not set the `store` parameter,
the index data results for the document are not returned in response to a query.

_Example search index function:_

```javascript
function(doc) {
	index("default", doc._id);
	if (doc.min_length) {
		index("min_length", doc.min_length, {"store": true});
	}
	if (doc.diet) {
		index("diet", doc.diet, {"store": true});
	}
	if (doc.latin_name) {
		index("latin_name", doc.latin_name, {"store": true});
	}
	if (doc.class) {
		index("class", doc.class, {"store": true});
	}
}
```
{:codeblock}

### Index Guard Clauses

The `index` function requires the name of the data field to index as the second parameter.
However,
if that data field does not exist for the document,
an error occurs.
The solution is to use an appropriate 'guard clause' that checks if the field exists,
and contains the expected type of data,
_before_ any attempt to create the corresponding index.

_Example of failing to check whether the index data field exists:_

```javascript
if (doc.min_length) {
	index("min_length", doc.min_length, {"store": true});
}
```
{:codeblock}

You might use the JavaScript '`typeof`' function to implement the guard clause test.
If the field exists _and_ has the expected type,
the correct type name is returned,
so the guard clause test succeeds and it is safe to use the index function.
If the field does _not_ exist,
you would not get back the expected type of the field,
therefore you would not attempt to index the field.

JavaScript considers a result to be false if one of the following values is tested:

-	'undefined'
-	null
-	The number +0
-	The number -0
-	NaN (not a number)
-	"" (the empty string)

_Using a guard clause to check whether the required data field exists,
and holds a number,
before an attempt to index:_

```javascript
if (typeof(doc.min_length) === 'number') {
	index("min_length", doc.min_length, {"store": true});
}
```
{:codeblock}

Use a generic guard clause test to ensure that the type of the candidate data field is defined.

_Example of a 'generic' guard clause:_

```javascript
if (typeof(doc.min_length) !== 'undefined') {
	// The field exists, and does have a type, so we can proceed to index using it.
	...
}
```
{:codeblock}

## Analyzers

Analyzers are settings that define how to recognize terms within text.
Analyzers can be helpful if you need to [index multiple languages](#language-specific-analyzers).

Here's the list of generic analyzers that are supported by Cloudant search:

Analyzer     | Description
-------------|------------
`classic`    | The standard Lucene analyzer, circa release 3.1.
`email`      | Like the `standard` analyzer, but tries harder to match an email address as a complete token.
`keyword`    | Input is not tokenized at all.
`simple`     | Divides text at non-letters.
`standard`   | The default analyzer. It implements the Word Break rules from the [Unicode Text Segmentation algorithm ![External link icon](../images/launch-glyph.svg "External link icon")](http://www.unicode.org/reports/tr29/){:new_window}.
`whitespace` | Divides text at white space boundaries.

_Example analyzer document:_

```json
{
	"_id": "_design/analyzer_example",
	"indexes": {
		"INDEX_NAME": {
			"index": "function (doc) { ... }",
			"analyzer": "$ANALYZER_NAME"
		}
	}
}
```
{:codeblock}

### Language-Specific Analyzers

These analyzers omit common words in the specific language,
and many also [remove prefixes and suffixes ![External link icon](../images/launch-glyph.svg "External link icon")](http://en.wikipedia.org/wiki/Stemming){:new_window}.
The name of the language is also the name of the analyzer.

*	`arabic`
*	`armenian`
*	`basque`
*	`bulgarian`
*	`brazilian`
*	`catalan`
*	`cjk` (Chinese, Japanese, Korean)
*	`chinese` ( [smartcn ![External link icon](../images/launch-glyph.svg "External link icon")](http://lucene.apache.org/core/4_2_1/analyzers-smartcn/org/apache/lucene/analysis/cn/smart/SmartChineseAnalyzer.html){:new_window} )
*	`czech`
*	`danish`
*	`dutch`
*	`english`
*	`finnish`
*	`french`
*	`german`
*	`greek`
*	`galician`
*	`hindi`
*	`hungarian`
*	`indonesian`
*	`irish`
*	`italian`
*	`japanese` ( [kuromoji ![External link icon](../images/launch-glyph.svg "External link icon")](http://lucene.apache.org/core/4_2_1/analyzers-kuromoji/overview-summary.html){:new_window} )
*	`latvian`
*	`norwegian`
*	`persian`
*	`polish` ( [stempel ![External link icon](../images/launch-glyph.svg "External link icon")](http://lucene.apache.org/core/4_2_1/analyzers-stempel/overview-summary.html){:new_window} )
*	`portuguese`
*	`romanian`
*	`russian`
*	`spanish`
*	`swedish`
*	`thai`
*	`turkish`

>	**Note**: Language-specific analyzers are optimized for the specified language.
    You cannot combine a generic analyzer with a language-specific analyzer.
    Instead,
    you might use a ['`perfield`' analyzer](#per-field-analyzers) to select different analyzers
    for different fields within the documents.

### Per-Field Analyzers

The '`perfield`' analyzer configures multiple analyzers for different fields.

_Example of defining different analyzers for different fields:_

```json
{
	"_id": "_design/analyzer_example",
	"indexes": {
		"INDEX_NAME": {
			"analyzer": {
				"name": "perfield",
				"default": "english",
				"fields": {
					"spanish": "spanish",
					"german": "german"
				}
			},
			"index": "function (doc) { ... }"
		}
	}
}
```
{:codeblock}

### Stop Words

Stop words are words that do not get indexed.
You define them within a design document by turning the analyzer string into an object.

>	**Note**: The `keyword`,
`simple`,
 and `whitespace` analyzers do not support stop words.

_Example of defining non-indexed ('stop') words:_

```json
{
	"_id": "_design/stop_words_example",
	"indexes": {
		"INDEX_NAME": {
			"analyzer": {
				"name": "portuguese",
				"stopwords": [
					"foo",
					"bar",
					"baz"
				]
			},
			"index": "function (doc) { ... }"
		}
	}
}
```
{:codeblock}

### Testing analyzer tokenization

You can test the results of analyzer tokenization by posting sample data to the `_search_analyze` endpoint.

_Example of using HTTP to test the `keyword` analyzer:_

```http
Host: <account>.cloudant.com
POST /_search_analyze HTTP/1.1
Content-Type: application/json
{"analyzer":"keyword", "text":"ablanks@renovations.com"}
```
{:codeblock}

_Example of using the command line to test the `keyword` analyzer:_

```sh
curl 'https://<account>.cloudant.com/_search_analyze' -H 'Content-Type: application/json'
	-d '{"analyzer":"keyword", "text":"ablanks@renovations.com"}'
```
{:codeblock}

_Result of testing the `keyword` analyzer:_

```json
{
	"tokens": [
		"ablanks@renovations.com"
	]
}
```
{:codeblock}

_Example of using HTTP to test the `standard` analyzer:_

```http
Host: <account>.cloudant.com
POST /_search_analyze HTTP/1.1
Content-Type: application/json
{"analyzer":"standard", "text":"ablanks@renovations.com"}
```
{:codeblock}

_Example of using the command line to test the `standard` analyzer:_

```sh
curl 'https://<account>.cloudant.com/_search_analyze' -H 'Content-Type: application/json'
	-d '{"analyzer":"standard", "text":"ablanks@renovations.com"}'
```
{:codeblock}

_Result of testing the `standard` analyzer:_

```json
{
	"tokens": [
		"ablanks",
		"renovations.com"
	]
}
```
{:codeblock}

## Queries

After you create an index,
you can query it with a `GET` request to
`https://$USERNAME.cloudant.com/$DATABASE/_design/$DESIGN_ID/_search/$INDEX_NAME`.
Specify your search by using the `query` parameter.

_Example of using HTTP to query an index:_

```http
GET /$DATABASE/_design/$DESIGN_DOC/_search/$INDEX_NAME?include_docs=true\&query="*:*"\&limit=1 HTTP/1.1
Content-Type: application/json
Host: account.cloudant.com
```
{:codeblock}

_Example to using the command line to query an index:_

```sh
curl https://$USERNAME.cloudant.com/$DATABASE/_design/$DESIGN_DOC/_search/$INDEX_NAME?include_docs=true\&query="*:*"\&limit=1 \
	-u $USERNAME
```
{:codeblock}

<!--

_Example of using JavaScript to query an index:_

```javascript
var nano = require('nano');
var account = nano("https://"+$USERNAME+":"+$PASSWORD+"@"+$USERNAME+".cloudant.com");
var db = account.use($DATABASE);

db.search($DESIGN_ID, $SEARCH_INDEX, {
	q: $QUERY
}, function (err, body, headers) {
	if (!err) {
		console.log(body);
	}
});
```
{:codeblock}

-->

### Query Parameters

>	**Note**: You must enable [faceting](#faceting) before you can use the following parameters:
	-	`counts`
	-	`drilldown`

<table border='1'>

<tr>
<th>Argument</th><th>Description</th><th>Optional</th><th>Type</th><th>Supported Values</th>
</tr>
<tr>
<td><code>bookmark</code></td>
<td>A bookmark that was received from a previous search.
This parameter enables paging through the results.
If there are no more results after the bookmark,
you get a response with an empty rows array and the same bookmark,
confirming the end of the result list.</td>
<td>yes</td>
<td>string</td>
</tr>
<tr>
<td><code>counts</code></td>
<td>This field defines an array of names of string fields,
for which counts are requested.
The response contains counts for each unique value of this field name among the documents that match the search query.
<a href="#faceting">Faceting</a> must be enabled for this parameter to function.</td>
<td>yes</td>
<td>JSON</td>
<td>A JSON array of field names.</td>
</tr>
<tr>
<td><code>drilldown</code></td>
<td>This field can be used several times.
Each use defines a pair of a field name and a value.
The search matches only documents containing the value that was provided in the named field.
It differs from using <code>"fieldname:value"</code> in
the <code>q</code> parameter only in that the values are not analyzed.
<a href="#faceting">Faceting</a> must be enabled for this parameter to function.</td>
<td>yes</td>
<td>JSON</td>
<td>A JSON array with two elements:
the field name and the value.</td>
</tr>
<tr>
<td><code>group_field</code></td>
<td>Field by which to group search matches.</td>
<td>yes</td>
<td>String</td>
<td>A string that contains the name of a string field.
Fields containing other data such as numbers, objects, or arrays cannot be used.</td>
</tr>
<tr>
<td><code>group_limit</code></td>
<td>Maximum group count.
This field can be used only if <code>group_field<code> is specified.</td>
<td>yes</td>
<td>Numeric</td>
<td></td>
</tr>
<tr>
<td><code>group_sort</code></td>
<td>This field defines the order of the groups in a search that uses <code>group_field</code>.
The default sort order is relevance.</td>
<td>yes</td>
<td>JSON</td>
<td>This field can have the same values as the sort field,
so single fields and arrays of fields are supported.</td>
</tr>
<tr>
<td><code>highlight_fields</code></td>
<td>Specifies which fields to highlight.
If specified,
the result object contains a <code>highlights</code> field with an entry for each specified field.</td>
<td>yes</td>
<td>Array of strings</td>
<td></td>
</tr>
<tr>
<td><code>highlight_pre_tag</code></td>
<td>A string that is inserted before the highlighted word in the highlights output.</td>
<td>yes, defaults to <code>&lt;em&gt;</code></td>
<td>String</td>
<td></td>
</tr>
<tr>
<td><code>highlight_post_tag</code></td>
<td>A string that is inserted after the highlighted word in the highlights output.</td>
<td>yes, defaults to <code>&lt;/em&gt;</code></td>
<td>String</td>
<td></td>
</tr>
<tr>
<td><code>highlight_number</code></td>
<td>Number of fragments that are returned in highlights.
If the search term occurs less often than the number of fragments that are specified,
longer fragments are returned.</td>
<td>yes, defaults to 1</td>
<td>Numeric</td>
<td></td>
</tr>
<tr>
<td><code>highlight_size</code></td>
<td>Number of characters in each fragment for highlights.</td>
<td>yes, defaults to 100 characters</td>
<td>Numeric</td>
<td></td>
</tr>
<tr>
<td><code>include_docs</code></td>
<td>Include the full content of the documents in the response.</td>
<td>yes</td>
<td>Boolean</td>
<td></td>
</tr>
<tr>
<td><code>include_fields</code></td>
<td>A JSON array of field names to include in search results.
Any fields that are included must be indexed with the <code>store:true</code> option.</td>
<td>yes, the default is all fields</td>
<td>Array of strings</td>
<td></td>
</tr>
<tr>
<td><code>limit</code></td>
<td>Limit the number of the returned documents to the specified number.
For a grouped search,
this parameter limits the number of documents per group.</td>
<td>yes</td>
<td>Numeric</td>
<td>The limit value can be any positive integer number up to and including 200.</td>
</tr>
<tr>
<td><code>q</code></td>
<td>Abbreviation for <code>query</code>.
Runs a Lucene query.</td>
<td>no</td>
<td>string or number</td>
<td></td>
</tr>
<tr>
<td><code>query</code></td>
<td>Runs a Lucene query.</td>
<td>no</td>
<td>string or number</td>
<td></td>
</tr>
<tr>
<td><code>ranges</code></td>
<td>This field defines ranges for faceted,
numeric search fields.
The value is a JSON object where the fields names are faceted numeric search fields,
and the values of the fields are JSON objects.
The field names of the JSON objects are names for ranges.
The values are strings that describe the range,
for example <code>"[0 TO 10]"</code></td>
<td>yes</td>
<td>JSON</td>
<td>The value must be an object with fields that have objects as their values.
These objects must have strings with ranges as their field values.</td>
</tr>
<tr>
<td><code>sort</code></td>
<td>Specifies the sort order of the results.
In a grouped search (when <code>group_field</code> is used),
this parameter specifies the sort order within a group.
The default sort order is relevance.</td>
<td>yes</td>
<td>JSON</td>
<td>A JSON string of the form <code>"fieldname&lt;type&gt;"</code>
or <code>-fieldname&lt;type&gt;</code> for descending order,
where <code>fieldname</code> is the name of a string or number field,
and <code>type</code> is either a number,
a string,
or a JSON array of strings.
The <code>type</code> part is optional,
and defaults to <code>number</code>.
Some examples are <code>"foo"</code>,
<code>"-foo"</code>,
<code>"bar&lt;string&gt;"</code>,
<code>"-foo&lt;number&gt;"</code> and <code>["-foo&lt;number&gt;",
"bar&lt;string&gt;"]</code>.
String fields that are used for sorting must not be analyzed fields.
Fields that are used for sorting must be indexed by the same indexer that is used for the search query.</td>
</tr>
<tr>
<td><code>stale</code></td>
<td>Do not wait for the index to finish building to return results.</td>
<td>yes</td>
<td>string</td>
<td>ok</td>
</tr>
</table>

>	**Note**: Do not combine the `bookmark` and `stale` options.
	These options constrain the choice of shard replicas to use for the response.
	When used together,
	the options might cause problems when contact is attempted with replicas that are slow or not available.

>	**Note**: Using `include_docs=true` might have [performance implications](using_views.html#include_docs_caveat).

### Relevance

When more than one result might be returned,
it is possible for them to be sorted.
By default,
the sorting order is determined by 'relevance'.

Relevance is measured according to
[Apache Lucene Scoring ![External link icon](../images/launch-glyph.svg "External link icon")](https://lucene.apache.org/core/3_6_0/scoring.html){:new_window}.
As an example,
if you search a simple database for the word "`example`",
two documents might contain the word.
If one document mentions the word "`example`" 10 times,
but the second document mentions it only twice,
then the first document is considered to be more 'relevant'.

If you do not provide a `sort` parameter,
relevance is used by default.
The highest scoring matches are returned first.

If you provide a `sort` parameter,
then matches are returned in that order,
ignoring relevance.

If you want to use a `sort` parameter,
and also include ordering by relevance in your search results,
use the special fields `-<score>` or `<score>` within the `sort` parameter.

### POSTing search queries

Instead of using the `GET` HTTP method,
you can also use `POST`.
The main advantage of `POST` queries is that they can have a request body,
so you can specify the request as a JSON object.
Each parameter in the previous table corresponds to a field in the JSON object in the request body.

_Example of using HTTP to `POST` a search request:_

```http
POST /db/_design/ddoc/_search/searchname HTTP/1.1
Content-Type: application/json
Host: account.cloudant.com
```
{:codeblock}

_Example of using the command line to `POST` a search request:_

```sh
curl 'https://account.cloudant.com/db/_design/ddoc/_search/searchname' -X POST -H 'Content-Type: application/json' -d @search.json
```
{:codeblock}

_Example JSON document that contains a search request:_

```json
{
    "q": "index:my query",
    "sort": "foo",
    "limit": 3
}
```
{:codeblock}

## Query Syntax

The Cloudant search query syntax is based on the
[Lucene syntax ![External link icon](../images/launch-glyph.svg "External link icon")](http://lucene.apache.org/core/4_3_0/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Overview){:new_window}.
Search queries take the form of `name:value` unless the name is omitted,
in which case they use the default field,
as demonstrated in the following examples:

> Example search query expressions:

```
// Birds
class:bird

// Animals that begin with the letter "l"
l*

// Carnivorous birds
class:bird AND diet:carnivore

// Herbivores that start with letter "l"
l* AND diet:herbivore

// Medium-sized herbivores
min_length:[1 TO 3] AND diet:herbivore

// Herbivores that are 2m long or less
diet:herbivore AND min_length:[-Infinity TO 2]

// Mammals that are at least 1.5m long
class:mammal AND min_length:[1.5 TO Infinity]

// Find "Meles meles"
latin_name:"Meles meles"

// Mammals who are herbivore or carnivore
diet:(herbivore OR omnivore) AND class:mammal

// Return all results
*:*
```
{:codeblock}

Queries over multiple fields can be logically combined,
and groups and fields can be further grouped.
The available logical operators are case-sensitive and are `AND`,
`+`,
`OR`,
`NOT` and `-`.
Range queries can run over strings or numbers.

If you want a fuzzy search,
you can run a query with `~` to find terms like the search term.
For instance,
`look~` finds the terms `book` and `took`.

>   **Note**: If the lower and upper bounds of a range 
> query are both strings that contain only numeric digits, 
> the bounds are treated as numbers not as strings.
> 
> For example, this search: 
> mod_date:["20170101" TO "20171231"]
> returns documents for which mod_date is between 20170101 and 20171231 (not between "20170101" and "20171231").

You can alter the importance of a search term by adding `^` and a positive number.
This alteration makes matches containing the term more or less relevant,
proportional to the power of the boost value.
The default value is 1,
which means no increase or decrease in the strength of the match.
A decimal value of 0 - 1 reduces importance.
making the match strength weaker.
A value greater than one increases importance,
making the match strength stronger.

Wildcard searches are supported,
for both single (`?`) and multiple (`*`) character searches.
For example,
`dat?` would match `date` and `data`,
whereas `dat*` would match `date`,
`data`,
`database`,
and `dates`.
Wildcards must come after the search term.

Use `*:*` to return all results.

Result sets from searches are limited to 200 rows,
and return 25 rows by default.
The number of rows that are returned can be changed
by using the [`limit` parameter](#query-parameters).

If the search query does _not_ specify the `"group_field"` argument,
the response contains a bookmark.
If this bookmark is later provided as a URL parameter,
the response skips the rows that were seen already,
making it quick and easy to get the next set of results.

>   **Note**: The response never includes a bookmark if the [`"group_field"` parameter](#query-parameters)
    is included in the search query.

The following characters require escaping if you want to search on them:

```
+ - && || ! ( ) { } [ ] ^ " ~ * ? : \ /
```
{:codeblock}

To escape one of these characters,
use a preceding backslash character (`\`).

The response to a search query contains an `order` field for each of the results.
The `order` field is an array where the first element is the field or fields that are specified
in the [`sort` parameter](#query-parameters).
If no [`sort` parameter](#query-parameters) is included in the query,
then the `order` field contains the [Lucene relevance score ![External link icon](../images/launch-glyph.svg "External link icon")](https://lucene.apache.org/core/3_6_0/scoring.html){:new_window}.
If you use the 'sort by distance' feature as described in [Geographical Searches](#geographical-searches),
then the first element is the distance from a point.
The distance is measured by using either kilometers or miles.

>   **Note**: The second element in the order array can be ignored.
    It is used for troubleshooting purposes only.

## Faceting

Cloudant Search also supports faceted searching,
enabling discovery of aggregate information about matches quickly and easily.
You can match all documents by using the special `?q=*:*` query syntax,
and use the returned facets to refine your query.
To indicate that a field must be indexed for faceted queries,
set `{"facet": true}` in its options.

_Example of search query, specifying that faceted search is enabled:_

```javascript
function(doc) {
    index("type", doc.type, {"facet": true});
    index("price", doc.price, {"facet": true});
}
```
{:codeblock}

>   **Note**: To use facets,
    all the documents in the index must include all the fields that have faceting enabled.
    If your documents do not include all the fields,
    you receive a `bad_request` error with the following reason, "Dim `field_name` does not exist."
    If each document does not contain all the fields for facets,
    create separate indexes for each field.
    If you do not create separate indexes for each field,
    you must include only documents that contain all the fields.
    Verify that the fields exist in each document by using a single `if` statement.

_Example `if` statement to verify that the required fields exist in each document:_

```javascript
if (typeof doc.town == "string" && typeof doc.name == "string") {
        index("town", doc.town, {facet: true});
        index("town", doc.town, {facet: true});        
    }
```
{:codeblock}

### Counts

The `counts` facet syntax takes a list of fields,
and returns the number of query results for each unique value of each named field.

>   **Note**: The `count` operation works only if the indexed values are strings.
    The indexed values cannot be mixed types.
    For example,
    if 100 strings are indexed,
    and one number,
    then the index cannot be used for `count` operations.
    You can check the type by using the '`typeof`' operator,
    and convert it by using the `parseInt`,
    `parseFloat`,
    or `.toString()` functions.

_Example of a query using the `counts` facet syntax:_ 

```http
?q=*:*&counts=["type"]
```
{:codeblock}

_Example response after using of the `counts` facet syntax:_

```json
{
    "total_rows":100000,
    "bookmark":"g...",
    "rows":[...],
    "counts":{
        "type":{
            "sofa": 10,
            "chair": 100,
            "lamp": 97
        }
    }
}
```
{:codeblock}

### `drilldown`

You can restrict results to documents with a dimension equal to the specified label.
Restrict the results by adding `drilldown=["dimension","label"]` to a search query.
You can include multiple `drilldown` parameters to restrict results along multiple dimensions.

Using a `drilldown` parameter is similar to using `key:value` in the `q` parameter,
but the `drilldown` parameter returns values that the analyzer might skip.

For example,
if the analyzer did not index a stop word like `"a"`,
using `drilldown` returns it when you specify `drilldown=["key","a"]`.

### Ranges

The `range` facet syntax reuses the standard Lucene syntax for ranges
to return counts of results that fit into each specified category.
Inclusive range queries are denoted by brackets (`[`, `]`).
Exclusive range queries are denoted by curly brackets (`{`, `}`).

>   **Note**: The `range` operation works only if the indexed values are numbers.
    The indexed values cannot be mixed types.
    For example,
    if 100 strings are indexed,
    and one number,
    then the index cannot be used for `range` operations.
    You can check the type by using the '`typeof`' operator,
    and convert it by using the `parseInt`,
    `parseFloat`,
    or `.toString()` functions.

_Example of a request that uses faceted search for matching `ranges`:_

```http
?q=*:*&ranges={"price":{"cheap":"[0 TO 100]","expensive":"{100 TO Infinity}"}}
```
{:codeblock}

_Example results after a `ranges` check on a faceted search:_

```json
{
    "total_rows":100000,
    "bookmark":"g...",
    "rows":[...],
    "ranges": {
        "price": {
            "expensive": 278682,
            "cheap": 257023
        }
    }
}
```
{:codeblock}

## Geographical searches

In addition to searching by the content of textual fields,
you can also sort your results by their distance from a geographic coordinate.

To sort your results in this way,
you must index two numeric fields,
representing the longitude and latitude.

You can then query by using the special `<distance...>` sort field,
which takes five parameters:

-   Longitude field name: The name of your longitude field ('`mylon`' in the example).
-   Latitude field name: The name of your latitude field ('`mylat`' in the example).
-   Longitude of origin: The longitude of the place you want to sort by distance from.
-   Latitude of origin: The latitude of the place you want to sort by distance from.
-   Units: The units to use: '`km`' for kilometers or '`mi`' for miles. The distance is returned in the order field.

You can combine sorting by distance with any other search query,
such as range searches on the latitude and longitude,
or queries that involve non-geographical information.

That way,
you can search in a bounding box,
and narrow down the search with extra criteria.

_Example geographical data:_

```json
{
    "name":"Aberdeen, Scotland",
    "lat":57.15,
    "lon":-2.15,
    "type":"city"
}
```
{:codeblock}

_Example of a design document that contains a search index for the geographic data:_

```javascript
function(doc) {
    if (doc.type && doc.type == 'city') {
        index('city', doc.name, {'store': true});
        index('lat', doc.lat, {'store': true});
        index('lon', doc.lon, {'store': true});
    }
}
```
{:codeblock}

_An example of using HTTP for a query that sorts cities in the northern hemisphere by their distance to New York:_

```http
GET /examples/_design/cities-designdoc/_search/cities?q=lat:[0+TO+90]&sort="<distance,lon,lat,-74.0059,40.7127,km>" HTTP/1.1
Host: $ACCOUNT.cloudant.com
```
{:codeblock}

_An example of using the command line for a query that sorts cities in the northern hemisphere by their distance to New York:_

```sh
curl 'https://$ACCOUNT.cloudant.com/examples/_design/cities-designdoc/_search/cities?q=lat:[0+TO+90]&sort="<distance,lon,lat,-74.0059,40.7127,km>"'
```
{:codeblock}

_Example (abbreviated) response, containing a list of northern hemisphere cities sorted by distance to New York:_

```json
{
    "total_rows": 205,
    "bookmark": "g1A...XIU",
    "rows": [
        {
            "id": "city180",
            "order": [
                8.530665755719783,
                18
            ],
            "fields": {
                "city": "New York, N.Y.",
                "lat": 40.78333333333333,
                "lon": -73.96666666666667
            }
        },
        {
            "id": "city177",
            "order": [
                13.756343205985946,
                17
            ],
            "fields": {
                "city": "Newark, N.J.",
                "lat": 40.733333333333334,
                "lon": -74.16666666666667
            }
        },
        {
            "id": "city178",
            "order": [
                113.53603438866077,
                26
            ],
            "fields": {
                "city": "New Haven, Conn.",
                "lat": 41.31666666666667,
                "lon": -72.91666666666667
            }
        }
    ]
}
```
{:codeblock}

## Highlighting Search Terms

Sometimes it is useful to get the context in which a search term was mentioned
so that you can display more emphasized results to a user.

To get more emphasized results,
add the `search_highlights` parameter to the search query.
Specify the field names for which you would like excerpts,
with the highlighted search term returned.

By default,
the search term is placed in `<em>` tags to highlight it,
but the highlight can be overridden by using the `highlights_pre_tag` and `highlights_post_tag` parameters.

The length of the fragments is 100 characters by default.
A different length can be requested with the `highlights_size` parameter.

The `highlights_number` parameter controls the number of fragments that are returned,
and defaults to 1.

In the response,
a `highlights` field is added,
with one subfield per field name.

For each field,
you receive an array of fragments with the search term highlighted.

>   **Note**: For highlighting to work,
    store the field in the index by using the `store: true` option.

_Example of using HTTP to search with highlighting enabled:_

```http
GET /movies/_design/searches/_search/movies?q=movie_name:Azazel&highlight_fields=["movie_name"]&highlight_pre_tag="<b>"&highlight_post_tag="</b>"&highlights_size=30&highlights_number=2 HTTP/1.1
HOST: <account>.cloudant.com
Authorization: ...
```
{:codeblock}

_Example of using the command line to search with highlighting enabled:_

```sh
curl "https://$user:$password@$account.cloudant.com/movies/_design/searches/_search/movies?q=movie_name:Azazel&highlight_fields=\[\"movie_name\"\]&highlight_pre_tag=\"<b>\"&highlight_post_tag=\"</b>\"&highlights_size=30&highlights_number=2
```
{:codeblock}

_Example of highlighted search results:_

```json
{
    "highlights": {
        "movie_name": [
            " on the <b>Azazel</b> Orient Express",
            " <b>Azazel</b> manuals, you"
        ]
    }
}
```
{:codeblock}

## Search index metadata

To retrieve information about a search index,
you send a `GET` request to the `_search_info` endpoint,
as shown in the following example.
`DDOC` refers to the design document that contains the index,
and `INDEX` is the name of the index.

_Example of using HTTP to request search index metadata:_

```http
GET /<DATABASE>/_design/<DDOC>/_search_info/<INDEX> HTTP/1.1
```
{:codeblock}

_Example of using the command line to request search index metadata:_

```sh
curl "https://$ACCOUNT.cloudant.com/$DATABASE/_design/$DDOC/_search_info/$INDEX" \
     -X GET -u "$USERNAME:$PASSWORD"
```
{:codeblock}

The response contains information about your index,
such as the number of documents in the index and the size of the index on disk.

_Example response after requesting search index metadata:_

```json
{
    "name": "_design/DDOC/INDEX",
    "search_index": {
        "pending_seq": 7125496,
        "doc_del_count": 129180,
        "doc_count": 1066173,
        "disk_size": 728305827,
        "committed_seq": 7125496
    }
}
```
{:codeblock}
