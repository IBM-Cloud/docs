---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-20"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Acrolinx: 2017-03-20 -->

# Query

Cloudant Query is a declarative JSON querying syntax for Cloudant databases.
{:shortdesc}

Cloudant Query wraps several index types, starting with the Primary Index type,
which is available for immediate use.
Cloudant Query indexes can also be built by using MapReduce Views (where the index type is `json`),
and Search Indexes (where the index type is `text`).

If you know exactly what data you want to look for,
or you want to keep storage and processing requirements to a minimum,
you can specify how the index is created,
by making it of type `json`.

But for maximum flexibility when you search for data,
you would typically create an index of type `text`.
Indexes of type `text` have a simple mechanism for automatically indexing all the fields in the documents.

>	**Note**: While more flexible,
`text` indexes might take longer to create and require more storage resources than `json` indexes.

## Creating an index

You can create an index with one of two types:

-	`"type": "json"`
-	`"type": "text"`

### Creating a "type=json" index

To create a JSON index in the database `$DATABASE`,
make a `POST` request to `/$DATABASE/_index` with a JSON object that describes the index in the request body.
The `type` field of the JSON object must be set to `"json"`.

_Example of using HTTP to request an index of type `JSON`:_

```http
POST /db/_index HTTP/1.1
Content-Type: application/json
```
{:codeblock}

_Example of JSON object that requests an index that is called `foo-index`, for the field that is called `foo`:_

```json
{
	"index": {
		"fields": ["foo"]
	},
	"name" : "foo-index",
	"type" : "json"
}
```
{:codeblock}

_Example of returned JSON, confirming that the index was created:_

```json
{
	"result": "created"
}
```
{:codeblock}

#### Request Body format

-	**index**:
    -	**fields**: A JSON array of field names that uses the [sort syntax](#sort-syntax).
    	Nested fields are also allowed, for example `"person.name"`.
-	**ddoc (optional)**: Name of the design document in which the index is created.
	By default,
	each index is created in its own design document.
	Indexes can be grouped into design documents for efficiency.
	However,
	a change to one index in a design document invalidates all other indexes in the same document.
-	**type (optional)**: Can be `json` or `text`.
	Defaults to `json`.
	Geospatial indexes will be supported in the future.
-	**name (optional)**: Name of the index.
	If no name is provided,
	a name is generated automatically.

#### Return Codes

Code | Description
-----|------------
200  | Index was created successfully or already existed
400  | Bad request: the request body does not have the specified format

### Creating a "type=text" index

While it is preferable to use default values when you create a single text index,
some useful index attributes can be modified.

>	**Note:** For Full Text Indexes (FTIs), `type` must be set to `text`.

The `name` and `ddoc` attributes are for grouping indexes into design documents.
Use the attributes to refer to index groups by using a custom string value.
If no values are supplied for these fields,
they are automatically populated with a hash value.

If you create multiple text indexes in a database,
with the same `ddoc` value,
you need to know at least the `ddoc` value and the `name` value.
Creating multiple indexes with the same `ddoc` value places them into the same design document.
Generally,
you must put each text index into its own design document.

For more information,
see the [note about `text` indexes](#note-about-text-indexes).

_Example of JSON document that requests index creation:_

```json
{
	"index": {
		"fields": [
			{
				"name": "Movie_name",
				"type": "string"
			}
		]
	},
	"name": "Movie_name-text",
	"type": "text"
}
```
{:codeblock}

_Example of JSON document that requests creation of a more complex index:_

```json
{
	"type": "text",
	"name": "my-index",
	"ddoc": "my-index-design-doc",
	"index": {
		"default_field": {
			"enabled": true,
			"analyzer": "german"
		},
		"selector": {},
		"fields": [
			{"name": "married", "type": "boolean"},
			{"name": "lastname", "type": "string"},
			{"name": "year-of-birth", "type": "number"}
		]
	}
}
```
{:codeblock}

#### The `index` field

The `index` field contains settings specific to text indexes.

To index all fields in all documents automatically,
use the simple syntax:

```json
"index": {}
```
{:codeblock}

The indexing process traverses all of the fields in all the documents in the database.

An example of creating a text index for all fields in all documents in a database is [available](#example-movies-demo-database).

> **Note**: Take care when you index all fields in all documents for large data sets,
as it might be a resource-consuming activity.

_Example of JSON document that requests creation of an index of all fields in all documents:_

```json
{
	"type": "text",
	"index": {}
}
```
{:codeblock}

#### The `default_field` field

The `default_field` value specifies how the `$text` operator can be used with the index.

The `default_field` contains two keys:

Key        | Description
-----------|------------
`analyzer` | Specifies the Lucene analyzer to use. The default value is `"standard"`.
`enabled`  | Enable or disable the `default_field index`. The default value is `true`.

The `analyzer` key in the `default_field` specifies how the index analyzes text.
Later,
the index can be queried by using the `$text` operator.
See the [Cloudant Search documentation](search.html#analyzers) for alternative analyzers.
You might choose to use an alternative analyzer when documents are indexed in languages other than English,
or when you have other special requirements for the analyzer such as matching email addresses.

If the `default_field` is not specified,
or is supplied with an empty object,
it defaults to `true` and the `standard` analyzer is used.

#### The `selector` field

The `selector` field can be used to limit the index to a specific set of documents that match a query.
It uses the same syntax that is used for selectors in queries.
This field can be used if your application requires different documents to be indexed in different ways,
or if some documents must not be indexed at all.
If you need to distinguish documents by type only,
it is easier to use one index and add the type to the search query.

#### The `fields` array

The `fields` array contains a list of fields that must be indexed for each document.
If you know that an index queries only on specific fields,
then this field can be used to limit the size of the index.
Each field must also specify a type to be indexed.
The acceptable types are:

-	`"boolean"`
-	`"string"`
-	`"number"`

#### The `index_array_lengths` field

Cloudant Query text indexes have a property that is called `index_array_lengths`.
If the property is not explicitly set,
the default value is `true`.

If the field is set to `true`,
the index requires extra work,
including a scan of every document for any arrays,
and creating a field to hold the length for each array found.

You might prefer to set the `index_array_lengths` field to `false` if:

-	You do not need to know the length of an array.
-	You do not use the [`$size` operator](#the-size-operator).
-	The documents in your database are complex,
	or not completely under your control,
	making it difficult to estimate the impact of the extra processing that is required to determine and store the array lengths.

> **Note**: The [`$size` operator](#the-size-operator) requires that the `index_array_lengths` field is set to `true`,
otherwise the operator cannot work.

_Example JSON document with suggested settings to optimize performance on production systems:_

```json
{
	"default_field": {
		"enabled": false
	},
	"index_array_lengths": false
}
```
{:codeblock}

## Query Parameters

The format of the `selector` field is as described in the [selector syntax](#selector-syntax),
except for the new `$text` operator.

The `$text` operator is based on a Lucene search with a standard analyzer.
The operator is not case-sensitive, and matches on any words.
However,
the `$text` operator does not support full Lucene syntax,
such as wildcards,
fuzzy matches,
or proximity detection.
For more information,
see [Cloudant Search documentation](search.html#search).
The `$text` operator applies to all strings found in the document.
It is invalid to place this operator in the context of a field name.

The `fields` array is a list of fields that must be returned for each document. The provided
field names can use dotted notation to access subfields.

_Example JSON document that uses all available query parameters:_

```json
{
	"selector": {
		"year": {
			"$gt": 2010
		}
	},
	"fields": ["_id", "_rev", "year", "title"],
	"sort": [{"year": "asc"}],
	"limit": 10,
	"skip": 0
	}
```
{:codeblock}

## Working with indexes

Cloudant endpoints can be used to create,
list,
update,
and delete indexes in a database,
and to query data by using these indexes.

The list of available methods and endpoints is as follows:

Method   | Path                | Description
---------|---------------------|------------
`DELETE` | `/$DATABASE/_index` | Delete an index.
`GET`    | `/$DATABASE/_index` | List all Cloudant Query indexes.
`POST`   | `/$DATABASE/_find`  | Find documents by using an index.
`POST`   | `/$DATABASE/_index` | Create an index.

## List all Cloudant Query indexes

-	**Method**: `GET`
-	**URL Path**: `/$DATABASE/_index`
-	**Response Body**: JSON object that describes the indexes
-	**Roles permitted**: `_reader`

When you make a `GET` request to `/$DATABASE/_index`,
you get a list of all indexes used by Cloudant Query in the database,
including the primary index.
In addition to the information available through this API,
indexes are also stored in design documents index functions.

Design documents are regular documents that have an ID starting with `_design/`.
They can be retrieved and modified in the same way as any other document,
although these actions are not usually necessary when you use Cloudant Query.

Design documents are discussed in more detail [here](design_documents.html).

### Response body format

-	**indexes**: Array of indexes
	-	**ddoc**: ID of the design document the index belongs to.
		This ID can be used to retrieve the design document that contains the index,
		by making a `GET` request to `/$DATABASE/$DDOC`, where `$DDOC` is the value of this field.
	-	**name**: Name of the index.
	-	**type**: Type of the index.
		Currently, `json` is the only supported type.
	-	**def**: Definition of the index that contains the indexed fields and the sort order: ascending or descending.

_Example of a response body with two indexes:_

```json
{
	"indexes": [
		{
			"ddoc": "_design/2ec1805041b2c3dcdef1d07a8ea1dc51ba3decfa",
			"name": "foo-bar-index",
			"type": "json",
			"def": {
				"fields": [
					{"foo":"asc"},
					{"bar":"asc"}
				]
			}
		},
		{
			"ddoc": "_design/1f003ce73056238720c2e8f7da545390a8ea1dc5",
			"name": "baz-index",
			"type": "json",
			"def": {
				"fields": [
					{"baz":"desc"}
				]
			}
		}
	]
}
```
{:codeblock}

## Deleting an index

-	**Method**: `DELETE`
-	**URL Path**: `/$DATABASE/_index/$DDOC/$TYPE/$NAME` where `$DATABASE` is the name of the database,
	$DDOC is the ID of the design document,
	$TYPE is the type of the index,
	for example `json`,
	and $NAME is the name of the index.
-	**Response Body**: JSON object that indicates successful deletion of the index,
	or that describes any error that was encountered.
-	**Request Body**: None
-	**Roles permitted**: `_writer`

<div id="finding-documents-using-an-index"></div>

## Finding documents by using an index

-	**Method**: `POST`
-	**URL Path**: `/$DATABASE/_find`
-	**Response Body**: JSON object that describes the query results.
-	**Roles permitted**: `_reader`

### Request body

-	**selector**: JSON object that describes the criteria that are used to select documents.
	More information is provided in the section on [selectors](#selector-syntax).
-	**limit (optional, default: 25)**: Maximum number of results returned.
-	**skip (optional, default: 0)**: Skip the first 'n' results, where 'n' is the value that is specified.
-	**sort (optional, default: [])**: JSON array,
	ordered according to the [sort syntax](#sort-syntax).
-	**fields (optional, default: null)**: JSON array that uses
	the field syntax as described in the following information.
	Use this parameter to specify which fields of an object must be returned.
	If it is omitted,
	the entire object is returned.
-	**r (optional, default: 1)**: The read quorum that is needed for the result.
	The value defaults to 1,
	in which case the document that was found in the index is returned.
	If set to a higher value,
	each document is read from at least that many replicas before it is returned in the results.
	The request is likely to take more time than using only the document that is stored locally with the index.
-	**bookmark (optional, default: null)**: A string that is used to specify which page of results you require.
	*Only for indexes of type `text`.*
-	**use_index (optional)**: Use this option to identify a specific index for query to run against,
	rather than by using the Cloudant Query algorithm to find the best index.
	For more information, see [Explain Plans](#explain-plans).

The `bookmark` field is used for paging through result sets.
Every query returns an opaque string under the `bookmark` key that can then
be passed back in a query to get the next page of results.
If any part of the query other than `bookmark` changes between requests,
the results are undefined.

The `limit` and `skip` values are exactly as you would expect.
Although `skip` is available,
it is not intended to be used for paging.
The reason is that the `bookmark` feature is more efficient.

_Example request in JSON format, for finding documents by using an index:_

```json
{
	"selector": {
		"year": {"$gt": 2010}
	},
	"fields": ["_id", "_rev", "year", "title"],
	"sort": [{"year": "asc"}],
	"limit": 10,
	"skip": 0
}
```
{:codeblock}

### Response body

-	**docs**: Array of documents that match the search.
	In each matching document,
	the fields that are specified in the `fields` part of the request body are listed,
	along with their values.

_Example response when you use an index to find documents:_

```json
{
	"docs":[
		{
			"_id": "2",
			"_rev": "1-9f0e70c7592b2e88c055c51afc2ec6fd",
			"foo": "test",
			"bar": 2600000
			},
		{
			"_id": "1",
			"_rev": "1-026418c17a353a9b73a6ccac19c142a4",
			"foo":"another test",
			"bar":9800000
		}
	]
}
```
{:codeblock}

## Selector Syntax

The Cloudant Query language is expressed as a JSON object that describes documents of interest.
Within this structure,
you can apply conditional logic by using specially named fields.

>   **Note**: While the Cloudant Query language has some similarities with MongoDB query documents,
    these similarities arise from a commonality of purpose and do not necessarily extend to equivalence of function or result.

### Selector basics

Elementary selector syntax requires you to specify one or more fields,
and the corresponding values required for those fields.
The following example selector matches all
documents that have a `director` field that contains the value `Lars von Trier`.

_Example of a simple selector:_

```json
{
	"selector": {
		"director": "Lars von Trier"
	}
}
```
{:codeblock}


If you created a full text index by specifying `"type":"text"` when the index was created,
you can use the `$text` operator to select matching documents.
In the following example,
the full text index is inspected to find any document that includes the word `Bond`.

_An example of a simple selector for a full text index:_

```json
{
	"selector": {
		"$text": "Bond"
	}
}
```
{:codeblock}

In the following example,
the full text index is inspected to find any document that includes the word "Bond".
In the response, the fields `title` or `cast` are returned for every matching object.

_Example of a simple selector, inspecting specific fields:_

```json
{
	"selector": {
		"$text": "Bond",
		"fields": [
			"title",
			"cast"
		]
	}
}
```
{:codeblock}

You can create more complex selector expressions by combining operators.
However,
for Cloudant Query indexes of type `json`,
you cannot use 'combination' or 'array logical' operators such as `$regex` as the *basis* of a query.
Only the equality operators such as `$eq`,
`$gt`,
`$gte`,
`$lt`,
and `$lte` - but _not_ `$ne` - can be used as the basis of a more complex query.
For more information about creating complex selector expressions,
see [Creating selector expressions](#creating-selector-expressions).

### Selector with two fields

In the following example,
the selector matches any document with a `name` field that contains `Paul`,
_and_ that also has a `location` field with the value "Boston".

_Example of a more complex selector:_

```json
{
	"selector": {
		"name": "Paul",
		"location": "Boston"
	}
}
```
{:codeblock}

## Subfields

Use a more complex selector to specify the values for field of nested objects,
or subfields.
For example,
you might use a standard JSON structure for specifying a field _and_ a subfield.

_Example of a field and subfield selector, within a JSON object:_

```json
{
	"selector": {
		"imdb": {
			"rating": 8
		}
	}
}
```
{:codeblock}

An abbreviated equivalent uses a dot notation to combine the field and subfield names into a single name.

_Example of an equivalent field and subfield selector that uses dot notation:_

```json
{
	"selector": {
		"imdb.rating": 8
	}
}
```
{:codeblock}

## Operators

Operators are identified by the use of a dollar sign (`$`) prefix in the name field.

The selector syntax has two core types of operators:

-	Combination operators.
-	Condition operators.

In general,
combination operators are applied at the topmost level of selection.
They are used to combine conditions,
or to create combinations of conditions,
into one selector.

Every explicit operator has the form:

```json
{
	"$operator": "argument"
}
```
{:codeblock}

A selector without an explicit operator is considered to have an implicit operator.
The exact implicit operator is determined by the structure of the selector expression.

## Implicit Operators

The two implicit operators are:

-	'Equality'.
-	'And'.

In a selector,
any field that contains a JSON value but that has no operators in it,
is considered to be an equality condition.
The implicit equality test also applies for fields and subfields.

Any JSON object that is not the argument to a condition operator is an implicit `$and` operator on each field.

_Example selector that uses an operator to match any document, where the `year` field has a value greater than 2010:_

```json
{
	"selector": {
		"year": {
			"$gt": 2010
		}
	}
}
```
{:codeblock}

In the following example,
a matching document must have a field that is called `director`,
*and* the field must have a value exactly equal to `Lars von Trier`.

_Example of the implicit equality operator:_

```json
{
	"director": "Lars von Trier"
}
```
{:codeblock}

You can also make the equality operator explicit,
as shown in the following example.

_Example of an explicit equality operator:_

```json
{
	"director": {
		"$eq": "Lars von Trier"
	}
}
```
{:codeblock}

In the following example that uses subfields,
the required field `imdb` in a matching document *must* also have
a subfield `rating`,
*and* the subfield *must* have a value equal to 8.

_Example of implicit operator that is applied to a subfield test:_

```json
{
	"imdb": {
		"rating": 8
	}
}
```
{:codeblock}

You can make the equality operator explicit.

_Example of an explicit equality operator:_

```json
{
	"selector": {
		"imdb": {
			"rating": { "$eq": 8 }
		}
	}
}
```
{:codeblock}

_Example of a `$eq` operator that is used with full text indexing:_

```json
{
	"selector": {
		"year": {
			"$eq": 2001
		}
	},
	"sort": [
		"title:string"
	],
	"fields": [
		"title"
	]
}
```
{:codeblock}

_Example of a `$eq` operator that is used with a database that is indexed on the field `year`:_

```json
{
	"selector": {
		"year": {
			"$eq": 2001
		}
	},
	"sort": [
		"year"
	],
	"fields": [
		"year"
	]
}
```
{:codeblock}


In the following example,
the field `director` must be present and contain the value `Lars von Trier`
_and_ the field `year` must exist and have the value `2003`.

_Example of an implicit `$and` operator:_

```json
{
	"director": "Lars von Trier",
	"year": 2003
}
```
{:codeblock}

<div id="combined-expressions"></div>

You can make both the `$and` operator and the equality operator explicit.

_Example that uses explicit `$and` and `$eq` operators:_

```json
{
	"$and": [
		{
			"director": {
				"$eq": "Lars von Trier"
			}
		},
		{
			"year": {
				"$eq": 2003
			}
		}
	]
}
```
{:codeblock}

## Explicit operators

All operators,
apart from the `$eq` (equality) and `$and` and operators,
must be stated explicitly.

## Combination Operators

Combination operators are used to combine selectors.
In addition to the common boolean operators found in most programming languages,
two combination operators (`$all` and `$elemMatch`) help you work with JSON arrays.

A combination operator takes a single argument.
The argument is either another selector, or an array of selectors.

The list of combination operators:

Operator     | Argument | Purpose
-------------|----------|--------
`$all`       | Array    | Matches an array value if it contains all the elements of the argument array.
`$and`       | Array    | Matches if all the selectors in the array match.
`$elemMatch` | Selector | Matches and returns all documents that contain an array field with at least one element that matches all the specified query criteria.
`$or`        | Array    | Matches if any of the selectors in the array match. All selectors must use the same index.
`$not`       | Selector | Matches if the selector does not match.
`$nor`       | Array    | Matches if none of the selectors in the array match.

### Examples of combination operators

#### The `$and` operator

The `$and` operator matches if all the selectors in the array match.

_Example of the `$and` operator used with full text indexing:_

```json
{
	"selector": {
		"$and": [
			{
				"$text": "Schwarzenegger"
			},
			{
				"year": {
					"$in": [1984, 1991]
				}
			}
		]
	},
	"fields": [
		"year",
		"title",
		"cast"
	]
}
```
{:codeblock}

_Example of the `$and` operator used with a primary index:_

```json
{
	"selector": {
		"$and": [
			{
				"_id": { "$gt": null }
			},
			{
				"year": {
					"$in": [2014, 2015]
				}
			}
		]
	},
	"fields": [
		"year",
		"_id",
		"title"
	],
	"limit": 10
}
```
{:codeblock}

#### The `$or` operator

The `$or` operator matches if any of the selectors in the array match.

_Example of the `$or` operator used with full text indexing:_

```json
{
	"selector": {
		"$or": [
			{ "director": "George Lucas" },
			{ "director": "Steven Spielberg" }
		]
	},
	"fields": [
		"title",
		"director",
		"year"
	]
}
```
{:codeblock}

_Example of the `$or` operator used with a database indexed on the field `year`:_

```json
{
	"selector": {
		"year": 1977,
		"$or": [
			{ "director": "George Lucas" },
			{ "director": "Steven Spielberg" }
		]
	},
	"fields": [
		"title",
		"director",
		"year"
	]
}
```
{:codeblock}

#### The `$not` operator

The `$not` operator matches if the selector does _not_ resolve to a value of `true`.

_Example of the `$not` operator used with full text indexing:_

```json
{
	"selector": {
		"year": {
			"$gte": 1900
		},
		"year": {
			"$lte": 1903
		},
		"$not": {
			"year": 1901
		}
	},
	"fields": [
		"title",
		"year"
	]
}
```
{:codeblock}

_Example of the `$not` operator used with a database indexed on the field `year`:_

```json
{
	"selector": {
		"year": {
			"$gte": 1900
		},
		"year": {
			"$lte": 1903
		},
		"$not": {
			"year": 1901
		}
	},
	"fields": [
		"title",
		"year"
	]
}
```
{:codeblock}

#### The `$nor` operator

The `$nor` operator matches if the selector does _not_ match.

_Example of the `$nor` operator used with full text indexing:_

```json
{
	"selector": {
		"year": {
			"$gte": 1900
		},
		"year": {
			"$lte": 1910
		},
		"$nor": [
			{ "year": 1901 },
			{ "year": 1905 },
			{ "year": 1907 }
		]
	},
	"fields": [
		"title",
		"year"
	]
}
```
{:codeblock}

_Example of the `$nor` operator used with a database indexed on the field `year`:_

```json
{
	"selector": {
		"year": {
			"$gte": 1900
		},
		"year": {
			"$lte": 1910
		},
		"$nor": [
			{ "year": 1901 },
			{ "year": 1905 },
			{ "year": 1907 }
		]
	},
	"fields": [
		"title",
		"year"
	]
}
```
{:codeblock}

#### The `$all` operator

The `$all` operator matches an array value if it contains _all_ the elements of the argument array.

_Example of the `$all` operator used with full text indexing:_

```json
{
	"selector": {
		"genre": {
			"$all": ["Comedy","Short"]
		}
	},
	"fields": [
		"title",
		"genre"
	],
	"sort": [
		"title:string"
	]
}
```
{:codeblock}

_Example of the `$all` operator used with a primary database index:_

```json
{
	"selector": {
		"_id": {
			"$gt": null
		},
		"genre": {
			"$all": ["Comedy","Short"]
		}
	},
	"fields": [
		"title",
		"genre"
	],
	"limit": 10
}
```
{:codeblock}

#### The `$elemMatch` operator

The `$elemMatch` operator matches and returns all documents that contain an array field
with at least one element that matches the supplied query criteria.

_Example of the `$elemMatch` operator used with full text indexing:_

```json
{
	"selector": {
		"genre": {
			"$elemMatch": {
				"$eq": "Horror"
			}
		}
	},
	"fields": [
		"title",
		"genre"
	]
}
```
{:codeblock}

_Example of the `$elemMatch` operator used with a primary database index:_

```json
{
	"selector": {
		"_id": { "$gt": null },
		"genre": {
			"$elemMatch": {
				"$eq": "Horror"
			}
		}
	},
	"fields": [
		"title",
		"genre"
	],
	"limit": 10
}
```
{:codeblock}

## Condition Operators

Condition operators are specific to a field,
and are used to evaluate the value that is stored in that field.
For instance,
the `$eq` operator matches when the specified field contains a value that is equal to the supplied argument.

The basic equality and inequality operators common to most programming languages are supported.
In addition,
some 'meta' condition operators are available.

Some condition operators accept any valid JSON content as the argument.
Other condition operators require the argument to be in a specific JSON format.

Operator type | Operator  | Argument             | Purpose
--------------|-----------|----------------------|--------
(In) equality | `$lt`     | Any JSON             | The field is less than the argument.
              | `$lte`    | Any JSON             | The field is less than or equal to the argument.
              | `$eq`     | Any JSON             | The field is equal to the argument.
              | `$ne`     | Any JSON             | The field is not equal to the argument.
              | `$gte`    | Any JSON             | The field is greater than or equal to the argument.
              | `$gt`     | Any JSON             | The field is greater than the argument.
Object        | `$exists` | Boolean              | Check whether the field exists or not, regardless of its value.
              | `$type`   | String               | Check the document field's type. Accepted values are `null`, `boolean`, `number`, `string`, `array`, and `object`.
Array         | `$in`     | Array of JSON values | The document field must exist in the list provided.
              | `$nin`    | Array of JSON values | The document field must not exist in the list provided.
              | `$size`   | Integer              | Special condition to match the length of an array field in a document. Non-array fields cannot match this condition.
Miscellaneous | `$mod`    | [Divisor, Remainder] | Divisor and Remainder are both positive or negative integers. Non-integer values result in a [404 status](http.html#404). Matches documents where the expression (`field % Divisor == Remainder`) is true, and only when the document field is an integer.
              | `$regex`  | String               | A regular expression pattern to match against the document field. Matches only when the field is a string value and matches the supplied regular expression.

> **Note**: Regular expressions do not work with indexes,
so they must not be used to filter large data sets.

### Examples of condition operators

#### The `$lt` operator

The `$lt` operator matches if the specified field content is less than the argument.

_Example of the `$lt` operator used with full text indexing:_

```json
{
	"selector": {
		"year": {
			"$lt": 1900
		}
	},
	"sort": [
		"year:number",
		"title:string"
	],
	"fields": [
		"year",
		"title"
	]
}
```
{:codeblock}

_Example of the `$lt` operator used with a database indexed on the field `year`:_

```json
{
	"selector": {
		"year": {
			"$lt": 1900
		}
	},
	"sort": [
		"year"
	],
	"fields": [
		"year"
	]
}
```
{:codeblock}

#### The `$lte` operator

The `$lte` operator matches if the specified field content is less than or equal to the argument.

_Example of the `$lte` operator used with full text indexing:_

```json
{
	"selector": {
		"year": {
			"$lte": 1900
		}
	},
	"sort": [
		"year:number",
		"title:string"
	],
	"fields": [
		"year",
		"title"
	]
}
```
{:codeblock}

_Example of the `$lte` operator used with a database indexed on the field `year`:_

```json
{
	"selector": {
		"year": {
			"$lte": 1900
		}
	},
	"sort": [
		"year"
	],
	"fields": [
		"year"
	]
}
```
{:codeblock}

#### The `$eq` operator

The `$eq` operator matches if the specified field content is equal to the supplied argument.

_Example of the `$eq` operator used with full text indexing:_

```json
{
	"selector": {
		"year": {
			"$eq": 2001
		}
	},
	"sort": [
		"title:string"
	],
	"fields": [
		"title"
	]
}
```
{:codeblock}

_Example of the `$eq` operator used with a database indexed on the field `year`:_

```json
{
	"selector": {
		"year": {
			"$eq": 2001
		}
	},
	"sort": [
		"year"
	],
	"fields": [
		"year"
	]
}
```
{:codeblock}

#### The `$ne` operator

The `$ne` operator matches if the specified field content is not equal to the supplied argument.

> **Note**: The `$ne` operator cannot be the basic (lowest level) element in a selector
when you use an index of type `json`.

_Example of the `$ne` operator used with full text indexing:_

```json
{
	"selector": {
		"year": {
			"$ne": 1892
		}
	},
	"fields": [
		"year"
	],
	"sort": [
		"year:number"
	]
}
```
{:codeblock}

_Example of the `$ne` operator used with a primary index:_

```json
{
	"selector": {
		"_id": {
			"$gt": null
		},
		"year": {
			"$ne": 1892
		}
	},
	"fields": [
		"year"
	],
	"limit": 10
}
```
{:codeblock}

#### The `$gte` operator

The `$gte` operator matches if the specified field content is greater than or equal to the argument.

_Example of the `$gte` operator used with full text indexing:_

```json
{
	"selector": {
		"year": {
			"$gte": 2001
		}
	},
	"sort": [
		"year:number",
		"title:string"
	],
	"fields": [
		"year",
		"title"
	]
}
```
{:codeblock}

_Example of the `$gte` operator used with a database indexed on the field `year`:_

```json
{
	"selector": {
		"year": {
			"$gte": 2001
		}
	},
	"sort": [
		"year"
	],
	"fields": [
		"year"
	]
}
```
{:codeblock}

#### The `$gt` operator

The `$gt` operator matches if the specified field content is greater than the argument.

_Example of the `$gte` operator used with full text indexing:_

```json
{
	"selector": {
		"year": {
			"$gt": 2001
		}
	},
	"sort": [
		"year:number",
		"title:string"
	],
	"fields": [
		"year",
		"title"
	]
}
```
{:codeblock}

_Example of the `$gt` operator used with a database indexed on the field `year`:_

```json
{
	"selector": {
		"year": {
			"$gt": 2001
		}
	},
	"sort": [
		"year"
	],
	"fields": [
		"year"
	]
}
```
{:codeblock}

#### The `$exists` operator

The `$exists` operator matches if the field exists,
regardless of its value.

_Example of the `$exists` operator used with full text indexing:_

```json
{
	"selector": {
		"year": 2015,
		"title": {
			"$exists": true
		}
	},
	"fields": [
		"year",
		"_id",
		"title"
	]
}
```
{:codeblock}

_Example of the `$exists` operator used with a database indexed on the field `year`:_

```json
{
	"selector": {
		"year": 2015,
		"title": {
			"$exists": true
		}
	},
	"fields": [
		"year",
		"_id",
		"title"
	]
}
```
{:codeblock}

#### The `$type` operator

The `$type` operator requires that the specified document field is of the correct type.

_Example of the `$type` operator used with full text indexing:_

```json
{
	"selector": {
		"year": {
			"$type": "number"
		}
	},
	"fields": [
		"year",
		"_id",
		"title"
	]
}
```
{:codeblock}

_Example of the `$type`, operator used with a primary index:_

```json
{
	"selector": {
		"_id": { "$gt": null },
		"year": {
			"$type": "number"
		}
	},
	"fields": [
		"year",
		"_id",
		"title"
	]
}
```
{:codeblock}

#### The `$in` operator

The `$in` operator requires that the document field _must_ exist in the list provided.

_Example of the `$in` operator used with full text indexing:_

```json
{
	"selector": {
		"year": {
			"$in": [2010,2015]
		}
	},
	"fields": [
		"year",
		"_id",
		"title"
	],
	"sort": [
		"year:number"
	]
}
```
{:codeblock}

_Example of the `$in` operator used with a primary index:_

```json
{
	"selector": {
		"_id": { "$gt": null },
		"year": {
			"$in": [2010, 2015]
		}
	},
	"fields": [
		"year",
		"_id",
		"title"
	],
	"limit": 10
}
```
{:codeblock}

#### The `$nin` operator

The `$nin` operator requires that the document field must _not_ exist in the list provided.

_Example of the `$nin` operator used with full text indexing:_

```json
{
	"selector": {
		"year": {
			"$gt": 2009,
			"$nin": [2010, 2015]
		}
	},
	"fields": [
		"year",
		"_id",
		"title"
	],
	"sort": [
		"year:number"
	]
}
```
{:codeblock}

_Example of the `$nin` operator used with a primary index:_

```json
{
	"selector": {
		"_id": { "$gt": null },
		"year": {
			"$nin": [2010, 2015]
		}
	},
	"fields": [
		"year",
		"_id",
		"title"
	],
	"limit": 10
}
```
{:codeblock}

#### The `$size` operator

The `$size` operator matches the length of an array field in a document.

_Example of the `$size` operator used with full text indexing:_

```json
{
	"selector": {
		"genre": {
			"$size": 4
		}
	},
	"fields": [
		"title",
		"genre"
	],
	"limit": 1000
}
```
{:codeblock}

_Example of the `$size` operator used with a primary index:_

```json
{
	"selector": {
		"_id": {
			"$gt": null
		},
		"genre": {
			"$size": 4
		}
	},
	"fields": [
		"title",
		"genre"
	],
	"limit": 25
}
```
{:codeblock}

#### The `$mod` operator

The `$mod` operator matches documents where the expression (`field % Divisor == Remainder`) is true,
and only when the document field is an integer.
The Divisor and Remainder must be integers.
They can be positive or negative integers.
A query where the Divisor or Remainder is a non-integer returns a [404 status](http.html#404).

>	**Note**: When you use negative integer values for the Divisor or Remainder,
the Cloudant `$mod` operator behaves in a similar way to the
[Erlang `rem` modulo operator ![External link icon](../images/launch-glyph.svg "External link icon")](http://erlang.org/doc/reference_manual/expressions.html){:new_window},
or the [`%` operator in C ![External link icon](../images/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/Operators_in_C_and_C%2B%2B){:new_window},
and uses [truncated division ![External link icon](../images/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/Modulo_operation){:new_window}.

_Example of the `$mod` operator used with full text indexing:_

```json
{
	"selector": {
		"year": {
			"$mod": [100,0]
		}
	},
	"fields": [
		"title",
		"year"
	],
	"limit": 50
}
```
{:codeblock}

_Example of the `$mod` operator used with a primary index:_

```json
{
	"selector": {
		"_id": {
			"$gt": null
		},
		"year": {
			"$mod": [100,0]
		}
	},
	"fields": [
		"title",
		"year"
	],
	"limit": 50
}
```
{:codeblock}

#### The `$regex` operator

The `$regex` operator matches when the field is a string value _and_ matches the supplied regular expression.

_Example of the `$regex` operator used with full text indexing:_

```json
{
	"selector": {
		"cast": {
			"$elemMatch": {
				"$regex": "^Robert"
			}
		}
	},
	"fields": [
		"title",
		"cast"
	],
	"limit": 10
}
```
{:codeblock}

_Example of the `$regex` operator used with a primary index:_

```json
{
	"selector": {
		"_id": {
			"$gt": null
		},
		"cast": {
			"$elemMatch": {
				"$regex": "^Robert"
			}
		}
	},
	"fields": [
		"title",
		"cast"
	],
	"limit": 10
}
```
{:codeblock}

## Creating selector expressions

In general,
whenever you have an operator that takes an argument,
that argument can itself be another operator with arguments of its own.
This expansion enables more complex selector expressions.

However,
not all operators can be used as the base or starting point of the selector expression
when you use indexes of type `json`.

>	**Note**: You cannot use combination or array logical operators such as `$regex` as the _basis_ of a query
when you use indexes of type `json`.
Only equality operators such as `$eq`, `$gt`, `$gte`, `$lt`, and `$lte` (but not `$ne`)
can be used as the basis of a query for `json` indexes.

For example,
if you try to run a query that attempts to match all documents that have a field that is called `afieldname`,
where the field contains a value beginning with the letter `A`,
you get an `error: "no_usable_index"` error message.

_Example of an unsupported selector expression:_

```json
	{
	"selector": {
		"afieldname": {
			"$regex": "^A"
		}
	}
}
```
{:codeblock}

_Example response to an unsupported selector expression:_

```json
{
	"error": "no_usable_index",
	"reason": "There is no operator in this selector can used with an index."
}
```
{:codeblock}

A solution is to use an equality operator as the basis of the query.
You can add a 'null' or 'always true' expression as the basis of the query.
For example,
you might first test that the document has an `_id` value:

```json
{
	"_id": {
		"$gt": null
	}
}
```
{:codeblock}

This expression is always true,
enabling the remainder of the selector expression to be applied.

>	**Note**: The use of `{"_id": { "$gt":null } }` forces a full table scan of the database,
and is not efficient for large databases.

Most selector expressions work exactly as you would expect for the operator.
The matching algorithms that are used by the `$regex` operator are currently _based_ on
the [Perl Compatible Regular Expression (PCRE) library ![External link icon](../images/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/Perl_Compatible_Regular_Expressions){:new_window}.
However,
not all of the PCRE library is implemented.
Additionally,
some parts of the `$regex` operator go beyond what PCRE offers.
For more information about what is implemented,
see the [Erlang Regular Expression ![External link icon](../images/launch-glyph.svg "External link icon")](http://erlang.org/doc/man/re.html){:new_window} information.

_Example use of an equality operator to enable a selector expression:_

```json
{
	"selector": {
		"_id": {
			"$gt": null
		},
		"afieldname": {
			"$regex": "^A"
		}
	}
}
```
{:codeblock}

## Sort Syntax

The `sort` field contains a list of field name and direction pairs,
expressed as a basic array.
The first field name and direction pair is the topmost level of sort.
The second pair,
if provided,
is the next level of sort.

The sort field can be any field.
Use dotted notation if wanted for subfields.

The direction value is `asc` for ascending, and `desc` for descending.

>	**Note**: If you omit the direction value,
the default `asc` is used.

_Example of simple sort syntax:_

```json
[
	{
		"fieldName1": "desc"
	},
	{
		"fieldName2": "desc"
	}
]
```
{:codeblock}

_Example of simple sort, assuming default direction of 'ascending' for both fields:_

```json
[
	"fieldNameA", "fieldNameB"
]
```
{:codeblock}

A typical requirement is to search for some content by using a selector,
then to sort the results according to the specified field,
in the required direction.

To use sorting, ensure that:

-	At least one of the sort fields is included in the selector.
-	An index is already defined,
	with all the sort fields in the same order.
-	Each object in the sort array has a single key.

>	**Note**: If an object in the sort array does not have a single key,
the resulting sort order is implementation-specific and might change.

>	**Note**: Currently,
Cloudant Query does not support multiple fields with different sort orders,
so the directions must be either all ascending or all descending.

If the direction is ascending,
you can use a string instead of an object to specify the sort fields.

For field names in text search sorts,
it is sometimes necessary for a field type to be specified,
for example:

```json
{
	"<fieldname>:string": "asc"
}
```
{:codeblock}

If possible,
an attempt is made to discover the field type based on the selector.
In ambiguous cases,
the field type must be provided explicitly.

The following table clarifies when the field type must be specified:

Index that is used by query               | Field type requirement
------------------------------------------|-----------------------
JSON index                                | It is not necessary to specify the type of sort fields in the query.
Text index of all fields in all documents | Specify the type of any sort field in the query if the database contains any documents in which the sort field has one type _and also_ contains some documents in which the sort field has a different type.
Any other text index                      | Specify the type of all sort fields in the query.

>	**Note**: A text index of all fields
in all documents is created when you use the syntax:
[`"index": {}`](#the-index-field).

>	**Note**: The sorting order is undefined when fields contain different data types.
This characteristic is an important difference between text and view indexes.
Sorting behavior for fields with different data types might change in future versions.

_Example of a simple query that uses sorting:_

```json
{
	"selector": {
		"Actor_name": "Robert De Niro"
	},
	"sort": [
		{
			"Actor_name": "asc"
		},
		{
			"Movie_runtime": "asc"
		}
	]
}
```
{:codeblock}

## Filtering fields

It is possible to specify exactly which fields are returned for a document when you select from a database.
The two advantages are:

- Your results are limited to only those parts of the document that are required for your application.
- A reduction in the size of the response.

The fields to be returned are specified as an array.

>	**Note**: Only the specified filter fields are included in the response.
`_id` or other metadata fields are not automatically included.

_Example of selective retrieval of fields from matching documents:_

```json
{
	"selector": {
		"Actor_name": "Robert De Niro"
	},
	"fields": [
		"Actor_name",
		"Movie_year",
		"_id",
		"_rev"
	]
}
```
{:codeblock}

## Explain Plans

Cloudant Query chooses which index to use for responding to a query,
unless you specify an index at query time.

When you specify an index to use,
Cloudant Query uses the following logic:

-	If two or more `json` type indexes exist for the same fields,
	the index with the smallest number of fields in the index is preferred.
	If the refinement still leaves two or more candidate indexes,
	the index with the first alphabetical name is chosen.
-	If a `json` type index _and_ a `text` type index might both satisfy a selector,
	the `json` index is chosen by default.
-	If a `json` type index _and_ a `text` type index the same field (for example `fieldone`),
	but the selector can be satisfied only by using a `text` type index,
	then the `text` type index is chosen.

For example,
assume that you have a `text` type index and a `json` type index for the field `foo`,
and you want to use a selector similar to the following sample:

```json
{
	"foo": {
		"$in": ["red","blue","green"]
	}
}
```
{:codeblock}

Cloudant Query uses the `text` type index because a `json` type index cannot satisfy the selector.

However,
you might use a different selector with the same indexes:

```json
{
	"foo": {
		"$gt": 2
	}
}
```
{:codeblock}

In this example,
Cloudant Query uses the `json` type index because both types of indexes can satisfy the selector.

To identify which index is being used by a particular query,
send a `POST` to the `_explain` endpoint for the database,
with the query as data.
The details of the index in use are shown in the `index` object within the result.

_Example that uses HTTP to show how to identify the index that was used to answer a query:_

```http
POST /movies/_explain HTTP/1.1
Host: examples.cloudant.com
Content-Type: application/json
{
	"selector": {
		"$text": "Pacino",
		"year": 2010
	}
}
```
{:codeblock}

_Example that uses the command line to show how to identify the index that was used to answer a query:_

```sh
curl 'https://examples.cloudant.com/movies/_explain' \
	-X POST \
	-H 'Content-Type: application/json' \
	-d '{
		"selector": {
			"$text": "Pacino",
			"year": 2010
		}
	}'
```
{:codeblock}

_Example response that shows which index was used to answer a query:_

```json
{
	"dbname": "examples/movies",
	"index": {
		"ddoc": "_design/32372935e14bed00cc6db4fc9efca0f1537d34a8",
		"name": "32372935e14bed00cc6db4fc9efca0f1537d34a8",
		"type": "text",
		"def": {
			"default_analyzer": "keyword",
			"default_field": {},
			"selector": {},
			"fields": []
		}
	},
	"selector": {
		"$and": [
			{
				"$default": {
					"$text": "Pacino"
				}
			},
			{
				"year": {
					"$eq": 2010
				}
			}
		]
	},
	"opts": {
		"use_index": [],
		"bookmark": [],
		"limit": 10000000000,
		"skip": 0,
		"sort": {},
		"fields": "all_fields",
		"r": [
			49
		],
		"conflicts": false
	},
	"limit": 200,
	"skip": 0,
	"fields": "all_fields",
	"query": "(($default:Pacino) AND (year_3anumber:2010))",
	"sort": "relevance"
}
```
{:codeblock}

To instruct a query to use a specific index,
add the `use_index` parameter to the query.

The value of the `use_index` parameter takes one of two formats:

-	`"use_index": "$DDOC"`
-	`"use_index": ["$DDOC","$INDEX_NAME"]`

_Example query with instructions to use a specific index:_

```json
{
	"selector": {
		"$text": "Pacino",
		"year": 2010
	},
	"use_index": "_design/32372935e14bed00cc6db4fc9efca0f1537d34a8"
}
```
{:codeblock}

## Note about `text` indexes

The basic premise for full text indexes is that a document
is "expanded" into a list of key:value pairs that are indexed by Lucene.
This expansion enables the use of Lucene's search syntax as a basis for the query capability.

This technique supports enhanced searches,
but does have certain limitations.
For example,
it might not always be clear whether content for an expanded document came
from individual elements or an array.

The query mechanism resolves this uncertainty by preferring to return 'false positive' results.
In other words,
if a match was found as a result of searching for either an individual element,
or an element from an array,
then the match is considered a success.

<div id="selector-translation"></div>

### Selector conversion

A standard Lucene search expression would not necessarily fully 'understand' the JSON-based Cloudant query syntax.
Therefore,
a conversion between the two formats takes place.

In the following example,
the JSON query approximates to the English phrase:
"match if the age expressed as a number is greater than five and less than or equal to infinity".
The Lucene query corresponds to that phrase,
where the text `_3a` within the fieldname corresponds to the `age:number` field,
and is an example of the document content expansion that was mentioned earlier.

_Example query to be converted:_

```json
{
	"age": {
		"$gt": 5
	}
}
```
{:codeblock}

_The corresponding Lucene query:_

```javascript
(age_3anumber:{5 TO Infinity])
```
{:codeblock}

### A more complex example

The following example illustrates some important points.

_JSON query to be converted to Lucene:_

```json
{
	"$or": [
		{
			"age": {
				"$gt": 5
			}
		},
		{
			"twitter": {
				"$exists":true
			}
		},
		{
			"type": {
				"$in": [
					"starch",
					"protein"
				]
			}
		}
	]
}
```
{:codeblock}

The first part of the JSON query is straightforward to convert to Lucene;
the test determines whether the `age` field has a numeric value greater than 5.
The `{` character in the range expression means that the value 5 is not considered a match.

To implement the `"twitter": {"$exists":true}` part of the JSON query in Lucene,
the first test is to determine whether a `twitter` field exists.
However,
the field might be either an array or an object.
Therefore,
the match must succeed when the value is an array _or_ an object.

This requirement means that the `$fieldnames` field must have entries that contain either `twitter.*` or `twitter:*`.
The `.` character is represented in the query as the ASCII character sequence `_2e`.
Similarly,
the `:` character is represented in the query as the ASCII character sequence `_3a`.
This representation requires the use of a two clause `OR` query for the `twitter` field,
ending in `_2e*` and `_3a*`.
Implementing this query as two phrases instead of a single `twitter*` query prevents an accidental match
with a field name such as `twitter_handle` or similar.

The last of the three main clauses is a search for `starch` or `protein`.
This search is more complicated.
The `$in` operator has some special semantics for array values that are inherited from the way MongoDB's behaves.
In particular,
the `$in` operator applies to the value **OR** any of the values that are contained in an array that is named by the field.
In our example,
the expression means that both `"type":"starch"` **AND** `"type":["protein"]` would match the example argument to `$in`.
Earlier,
the `type_3astring` expression was converted to `type:string`.
The second `type_2e_5b_5d_3astring` phrase converts to `type.[]:string`,
which is an example of the expanded array indexing.

_Corresponding Lucene query. The '#' comments are not valid Lucene syntax, but help explain the query construction:_

```javascript
(
	# Search for age > 5
	(age_3anumber:{5 TO Infinity])

	# Search for documents that contain the twitter field
	(($fieldnames:twitter_2e*) OR ($fieldnames:twitter_3a*))

	# Search for type = starch
	(
		((type_3astring:starch) OR (type_2e_5b_5d_3astring:starch))
		
		# Search for type = protein
		((type_3astring:protein) OR (type_2e_5b_5d_3astring:protein))
	)
)
```
{:codeblock}

<div id="example-movies-demo-database"></div>

## Example: Movies demonstration database

To describe full text indexes,
it is helpful to have a large collection of data to work with.
A suitable collection is available in the example Cloudant Query movie database: `query-movies`.
The sample database contains approximately 3,000 documents, and is just under 1 MB.

You can obtain a copy of this database in your database,
giving it the name `my-movies`,
by running one of the following commands:

_Example of using HTTP to obtain a copy of the Cloudant Query movie database:_

```http
POST /_replicator HTTP/1.1
Host: user.cloudant.com
Content-Type: application/json
{
	"source": "https://examples.cloudant.com/query-movies",
	"target": "https://$ACCOUNT.cloudant.com/my-movies",
	"create_target": true,
	"use_checkpoints": false
}
```
{:codeblock}

_Example of using the command line to obtain a copy of the Cloudant Query movie database:_

```sh
curl 'https://$ACCOUNT:$PASSWORD@$ACCOUNT.cloudant.com/_replicator' \
	-X POST \
	-H 'Content-Type: application/json' \
	-d '{
		"source": "https://examples.cloudant.com/query-movies",
		"target": "https://$ACCOUNT.cloudant.com/my-movies",
		"create_target": true,
		"use_checkpoints": false
	}'
```
{:codeblock}

_Results after successful replication of the Cloudant Query movie database:_

```json
{
	"ok": true,
	"use_checkpoints": false
}
```
{:codeblock}

Before you can search the content,
it must be indexed by creating a text index for the documents.

_Example of using HTTP to create a _text_ index for your sample database:_

```http
POST /my-movies/_index HTTP/1.1
Host: user.cloudant.com
Content-Type: application/json
{
	"index": {},
	"type": "text"
}
```
{:codeblock}

_Example of using the command line to create a _text_ index for your sample database:_

```sh
curl 'https://$ACCOUNT.cloudant.com/my-movies/_index' \
	-X POST \
	-H 'Content-Type: application/json' \
	-d '{"index": {}, "type": "text"}'
```
{:codeblock}

_Example response after a text index is created successfully:_

```json
{
	"result": "created"
}
```
{:codeblock}

The most obvious difference in the results you get when you use full text indexes is
the inclusion of a large `bookmark` field.
The reason is that text indexes are different from view-based indexes.
For more flexibility when you work with the results that are obtained from a full text query,
you can supply the `bookmark` value as part of the request body.
Use the `bookmark` to specify which page of results you require.

>	**Note**: The actual `bookmark` value is long,
so the examples here have values that are truncated for reasons of clarity.

_Example of using HTTP to search for a specific document within the database:_

```http
POST /my-movies/_find HTTP/1.1
Host: user.cloudant.com
Content-Type: application/json
{
  "selector": {
    "Person_name":"Zoe Saldana"
  }
}
```
{:codeblock}

_Example of using the command line to search for a specific document within the database:_

```sh
curl -X POST -H "Content-Type: application/json" \
	https://$ACCOUNT.cloudant.com/my-movies/_find \
	-d '{"selector": {"Person_name":"Zoe Saldana"}}'
```
{:codeblock}

_Example result from the search:_

```json
{
	"docs": [
		{
			"_id": "d9e6a7ae2363d6cfe81af75a3941110b",
			"_rev": "1-556aec0e89fa13769fbf59d651411528",
			"Movie_runtime": 162,
			"Movie_rating": "PG-13",
			"Person_name": "Zoe Saldana",
			"Movie_genre": "AVYS",
			"Movie_name": "Avatar",
			"Movie_earnings_rank": "1",
			"Person_pob": "New Jersey, USA",
			"Movie_year": 2009,
			"Person_dob": "1978-06-19"
		}
	],
	"bookmark": "g2wA ... Omo"
}
```
{:codeblock}

_Example of using HTTP for a slightly more complex search:_

```http
POST /my-movies/_find HTTP/1.1
Host: user.cloudant.com
Content-Type: application/json
{
	"selector": {
		"Person_name":"Robert De Niro",
		"Movie_year": 1978
	}
}
```
{:codeblock}

_Example of using the command line for a slightly more complex search:_

```sh
curl -X POST -H "Content-Type: application/json" \
	https://$ACCOUNT.cloudant.com/my-movies/_find \
	-d '{"selector": {"Person_name":"Robert De Niro", "Movie_year": 1978}}'
```
{:codeblock}

_Example result from the search:_

```json
{
	"docs": [
		{
			"_id": "d9e6a7ae2363d6cfe81af75a392eb9f2",
			"_rev": "1-9faa75d7ea524448b1456a6c69a4391a",
			"Movie_runtime": 183,
			"Movie_rating": "R",
			"Person_name": "Robert De Niro",
			"Movie_genre": "DW",
			"Movie_name": "Deer Hunter, The",
			"Person_pob": "New York, New York, USA",
			"Movie_year": 1978,
			"Person_dob": "1943-08-17"
		}
	],
	"bookmark": "g2w ... c2o"
}
```
{:codeblock}

_Example of using HTTP to search within a range:_

```http
POST /my-movies/_find HTTP/1.1
Host: user.cloudant.com
Content-Type: application/json
{
  "selector": {
    "Person_name":"Robert De Niro",
    "Movie_year": {
      "$in": [1974, 2009]
    }
  }
}
```
{:codeblock}

_Example of using the command line to search within a range:_

```sh
curl -X POST -H "Content-Type: application/json" \
	https://$ACCOUNT.cloudant.com/my-movies/_find \
	-d '{"selector": {"Person_name":"Robert De Niro", "Movie_year": { "$in": [1974, 2009]}}}'
```
{:codeblock}

_Example result from the search:_

```json
{
	"docs": [
		{
			"_id": "d9e6a7ae2363d6cfe81af75a392eb9f2",
			"_rev": "1-9faa75d7ea524448b1456a6c69a4391a",
			"Movie_runtime": 183,
			"Movie_rating": "R",
			"Person_name": "Robert De Niro",
			"Movie_genre": "DW",
			"Movie_name": "Deer Hunter, The",
			"Person_pob": "New York, New York, USA",
			"Movie_year": 1978,
			"Person_dob": "1943-08-17"
		}
	],
	"bookmark": "g2w ... c2o"
}
```
{:codeblock}
