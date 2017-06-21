---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using Views

Use views to search for content within a database that matches specific criteria.
The criteria are specified within the view definition,
or supplied as arguments when you use the view.
{:shortdesc}

## Querying a view

To query a view,
submit a `GET` request with the following format:

-   **Method**: `GET /$DATABASE/_design/$DDOC/_view/$VIEW-NAME`
-   **Request**: None
-   **Response**: JSON of the documents that are returned by the view
-   **Roles permitted**: `_reader`

The request runs the specified `view-name` from the specified `design-doc` design document within the database.

### Query Arguments

Argument         | Description | Optional | Type | Default | Supported values
-----------------|-------------|----------|------|---------|-----------------
`conflicts`      | Can be set only if `include_docs` is `true`. Adds information about conflicts to each document. | yes | Boolean | false |
`descending`     | Return the documents in 'descending by key' order. | yes | Boolean | false | 
`endkey`         | Stop returning records when the specified key is reached. | yes | String or JSON array | | 
`endkey_docid`   | Stop returning records when the specified document ID is reached. | yes | String | | 
`group`          | Using the `reduce` function, group the results to a group or single row. | yes | Boolean | false | 
`group_level`    | Only applicable if the view uses complex keys: keys that are JSON arrays. Groups reduce results for the specified number of array fields. | yes | Numeric | | 
`include_docs`   | Include the full content of the documents in the response. | yes | Boolean | false | 
`inclusive_end`  | Include rows with the specified `endkey`. | yes | Boolean | true | 
`key`            | Return only documents that match the specified key. **Note**: Keys are JSON values, and must be URL encoded. | yes | JSON strings or arrays | | 
`keys`           | Return only documents that match the specified keys. **Note**: Keys are JSON values, and must be URL encoded. | yes | Array of JSON strings or arrays | |
`limit`          | Limit the number of returned documents to the specified count. | yes | Numeric | | 
`reduce`         | Use the `reduce` function. | yes | Boolean | true | 
`skip`           | Skip this number of rows from the start. | yes | Numeric | 0 | 
`stable`         | Prefer view results from a 'stable' set of shards. The results are from a view that is less likely to be updated soon. | yes | Boolean | false | 
`stale`          | Allow the results from a stale view to be used. The request returns immediately, even if the view is not yet built. If this parameter is not given, a response is returned only after the view has been built. | yes | String | false | `ok`: Allow stale views.<br/>`update_after`: Allow stale views, but update them immediately after the request.
`startkey`       | Return records, starting with the specified key. | yes | String or JSON array | | 
`startkey_docid` | Return records, starting with the specified document ID. | yes | String | |
 `update`        | Ensure that the view is updated before results are returned. | yes | String | `true` | `false`: Return results before updating the view.<br/>`true`: Return results after updating the view.<br/>`lazy`: Return the view results without waiting for an update, but update them immediately after the request.

>   **Note**: Using `include_docs=true` might have [performance implications](#include_docs_caveat).

_Example of using HTTP to retrieve a list of the first five documents from a database, applying the user-created `by_title` view:_

```http
GET /$DATABASE/_design/$DDOC/_view/by_title?limit=5 HTTP/1.1
Accept: application/json
Content-Type: application/json
```
{:codeblock}

_Example of using the command line to retrieve a list of the first five documents from a database,
applying the user-created `by_title` view:_

```sh
curl https://$ACCOUNT.cloudant.com/$DATABASE/_design/$DDOC/_view/by_title?limit=5 \
     -H "Content-Type: application/json"
```
{:codeblock}

_Example response to request:_

```json
{
    "offset" : 0,
    "rows" : [
        {
            "id" : "3-tiersalmonspinachandavocadoterrine",
            "key" : "3-tier salmon, spinach and avocado terrine",
            "value" : [
                null,
                "3-tier salmon, spinach and avocado terrine"
                ]
        },
        {
            "id" : "Aberffrawcake",
            "key" : "Aberffraw cake",
            "value" : [
                null,
                "Aberffraw cake"
            ]
        },
        {
            "id" : "Adukiandorangecasserole-microwave",
            "key" : "Aduki and orange casserole - microwave",
            "value" : [
                null,
                "Aduki and orange casserole - microwave"
            ]
        },
        {
            "id" : "Aioli-garlicmayonnaise",
            "key" : "Aioli - garlic mayonnaise",
            "value" : [
                null,
                "Aioli - garlic mayonnaise"
            ]
        },
        {
            "id" : "Alabamapeanutchicken",
            "key" : "Alabama peanut chicken",
            "value" : [
                null,
                "Alabama peanut chicken"
            ]
        }
    ],
    "total_rows" : 2667
}
```
{:codeblock}

## Indexes

When a view is defined in a design document,
a corresponding index is also created,
based on the information defined within the view.
Use indexes to find documents by criteria other than their `_id` field.
For example,
you might select by a field,
or combination of fields,
or by a value that is computed by using the contents of the document.
The index is populated as soon as the design document is created.
On large databases,
this process might take a while.

The index content is updated incrementally and automatically when any one of the following three events occurs:

-   A new document is added to the database.
-   An existing document is deleted from the database.
-   An existing document in the database is updated.

View indexes are rebuilt entirely when the view definition changes,
or when another view definition in the same design document changes.
The rebuild ensures that changes to the view definitions are reflected in the view indexes.
To ensure the rebuild happens,
a 'fingerprint' of the view definition is created whenever the design document is updated.
If the fingerprint changes,
then the view indexes are rebuilt.

>   **Note**: View index rebuilds occur whenever a change occurs to any one view
    from all the views that are defined in the design document.
    For example,
    if you have a design document with three views,
    and you update the design document,
    all three view indexes within the design document are rebuilt.

If the database was updated recently,
the results might be delayed when the view is accessed.
The delay is affected by the number of changes to the database,
and whether the view index is not current because the database content was modified.

It is not possible to eliminate these delays.
For newly created databases,
you might reduce the delays by creating the view definition in the design document in your database
before you insert or update documents.
Creating the view definition in the design document
causes incremental updates to the index when the documents or inserted.

If speed of response is more important than having up-to-date data,
an alternative is to allow users to access an old version of the view index.
In effect,
the user has an immediate response from 'stale' index content,
rather than waiting for the index to be updated.
Depending on the document contents,
a stale view might not return the most recent information.
Nevertheless, a stale view returns the results of the view query quickly,
by using an existing version of the index.

<div id="accessing-a-stale-view"></div>

## View freshness

By default, all index results reflect the current state of the database. Cloudant builds its indexes automatically and asynchronously in the background.
This usually means the index is fully up-to-date 
when you query it. If this is not the case, we call the database "stale" and the remaining updates are made when you query the index. 
The results of your query include these updates. Cloudant builds three copies of every index in 
alignment with the three copies of your primary data.

Cloudant supplies better results and
performance with the defaults for these parameters. If the performance of your view and your application can tolerate inconsistent results when queried with the 
default `stale=false` setting, use `stable=false&update=false`. These settings avoid directing all queries to a single copy of 
your index, which would, in effect, reduce some aspects of performance to a third of what it should be.

Option   | Purpose                                                                                                                               | Default value
---------|---------------------------------------------------------------------------------------------------------------------------------------|--------------
`stable` | Determine whether view results are obtained from a consistent or 'stable' set of shards. Possible values include `true`, and `false`. | `false`
`stale`  | Determine whether results from a stale view are permitted. Possible values include `false`, `ok`, and `update_after`.                 | `false`
`update` | Determine whether the view is updated before the results are returned. Possible values include `true`, `false`, and `lazy`.           | `true`

## Combining parameters

When you specify `stable=true` with `update=false` or `update=lazy`,
responses are consistent from request to request because a single,
consistent set of shards is used to respond to the query.
However, when one of the shards is heavily loaded or slow to respond,
the response time is adversely affected.

When the default `stable=false` value applies,
and you use either `update=false` or `update=lazy`,
indexes between shard replicas are no longer synchronized.
The results are different based on which replica responds first. 

When you use a stale view, the results return the existing version of the data in the view index without waiting for an update. 
The results can be different from different nodes in the cluster.

### Parameters

The `stable` option indicates whether you would prefer to get results from a single,
consistent set of shards. The `false` value means that all available shard replicas are queried. Cloudant uses the first response returned. 
The benefit is that the response is not delayed when an individual shard replica is slow to respond.
By contrast, setting `stable=true` forces the database to use a single,
consistent set of shards to respond to the query.

The `stale` option allows the results from a stale view to be used. The option makes the request return immediately,
even if the view is still building. If this parameter is not given, or the value `false` is supplied, a response is returned only after the view is built.
The value `ok` allows stale views. The value `update_after` allows stale views
but updates them immediately after a response to the request is provided.

The `update` option indicates whether you are prepared to accept
view results without waiting for the view to be updated. The default value is `true`,
meaning that the view is updated before results are returned. The `lazy` value means that the results are returned before the view is updated,
but that the view must then be updated anyway.

## Sorting Returned Rows

The data returned by a view query are in the form of an array.
Each element within the array is sorted by using standard
[UTF-8 ![External link icon](../images/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/UTF-8){:new_window} sorting.
The sort is applied to the key defined in the view function.

The basic order of output is as follows:

Value                                                                                             | Order
--------------------------------------------------------------------------------------------------|------
`null`                                                                                            | First
`false`                                                                                           |
`true`                                                                                            |
Numbers                                                                                           |
Text (lowercase)                                                                                  |
Text (uppercase)                                                                                  |
Arrays (according to the values of each element, by using the order given in this table)          |
Objects (according to the values of keys, in key order by using the order given in this table)    | Last

You can reverse the order of the returned view information by setting the `descending` query value `true`.

_Example of using HTTP to request the last five records in reversed sort order:_

```http
GET /$DATABASE/_design/$DDOC/_view/by_title?limit=5&descending=true HTTP/1.1
Accept: application/json
Content-Type: application/json
```
{:codeblock}

_Example of requesting the last five records in reversed sort order, that uses the command line:_

```sh
curl https://$ACCOUNT.cloudant.com/$DATABASE/_design/$DDOC/_view/by_title?limit=5&descending=true \
     -H "Content-Type: application/json"
```
{:codeblock}

_Example response of requesting the last five records in reversed sort order:_

```json
{
    "offset" : 0,
    "rows" : [
        {
            "id" : "Zucchiniinagrodolcesweet-sourcourgettes",
            "key" : "Zucchini in agrodolce (sweet-sour courgettes)",
            "value" : [
                null,
                "Zucchini in agrodolce (sweet-sour courgettes)"
            ]
        },
        {
            "id" : "Zingylemontart",
            "key" : "Zingy lemon tart",
            "value" : [
                null,
                "Zingy lemon tart"
            ]
        },
        {
            "id" : "Zestyseafoodavocado",
            "key" : "Zesty seafood avocado",
            "value" : [
                null,
                "Zesty seafood avocado"
            ]
        },
        {
            "id" : "Zabaglione",
            "key" : "Zabaglione",
            "value" : [
                null,
                "Zabaglione"
            ]
        },
        {
            "id" : "Yogurtraita",
            "key" : "Yogurt raita",
            "value" : [
                null,
                "Yogurt raita"
            ]
        }
    ],
    "total_rows" : 2667
}
```
{:codeblock}

## Specifying Start and End Keys

The `startkey` and `endkey` query arguments can be used to specify the range of values
that are returned when querying the view.

The sort direction is always applied first.

Next,
filtering is applied by using the `startkey` and `endkey` query arguments.
The combination of sorting and filtering means that it is possible to have empty view results because
the sorting and filtering do not make sense when combined.

_Example of using HTTP to make a query that includes `startkey` and `endkey` query arguments:_

```http
GET /recipes/_design/recipes/_view/by_ingredient?startkey="alpha"&endkey="beta" HTTP/1.1
Accept: application/json
Content-Type: application/json
```
{:codeblock}

_Example of a query using the command line that includes `startkey` and `endkey` query arguments:_

```sh
curl https://$ACCOUNT.cloudant.com/$DATABASE/_design/$DDOC/_view/by_ingredient?startkey="alpha"&endkey="beta" \
     -H "Content-Type: application/json"
```
{:codeblock}

For example,
if you have a database that returns 10 results when you use a `startkey` of `alpha` and an `endkey` of `beta`,
you would get no results with a reversed order.
The reason is that the entries in the view are reversed before the key filter is applied.

_Example that uses HTTP to illustrate why reversing the order of `startkey` and `endkey` might not yield any results:_

```http
GET /recipes/_design/recipes/_view/by_ingredient?descending=true&startkey="beta"&endkey="alpha" HTTP/1.1
Accept: application/json
Content-Type: application/json
```
{:codeblock}

_Example illustrating why reversing the order of `startkey` and `endkey` might not yield any results,
that uses the command line:_

```sh
curl https://$ACCOUNT.cloudant.com/$DATABASE/_design/$DDOC/_view/by_ingredient?descending=true&startkey="beta"&endkey="alpha" \
     -H "Content-Type: application/json"
```
{:codeblock}

The `endkey` of `beta` is seen before the `startkey` of `alpha`, resulting in an empty list.

_Example showing that the view request returns no entries,
because `alpha` is alphabetically before `beta`,
therefore the returned result is empty:_

```json
{
    "total_rows" : 26453,
    "rows" : [],
    "offset" : 21882
}
```
{:codeblock}

The solution is to reverse not just the sort order,
but also the `startkey` and `endkey` parameter values.

The following example shows correct filtering and reversing the order of output,
by using the `descending` query argument,
and reversing the `startkey` and `endkey` query arguments.

_Example that uses HTTP to apply correct filtering and sorting:_

```http
GET /recipes/_design/recipes/_view/by_ingredient?descending=true&startkey="egg"&endkey="carrots" HTTP/1.1
Accept: application/json
Content-Type: application/json
```
{:codeblock}

_Example that uses the command line to apply correct filtering and sorting:_

```sh
curl https://$ACCOUNT.cloudant.com/$DATABASE/_design/$DDOC/_view/by_ingredient?descending=true&startkey="egg"&endkey="carrots" \
    -H "Content-Type: application/json"
```
{:codeblock}

## Querying a view by using a list of keys

You can also run a query by providing a list of keys to use.

Requesting information from a database in this way uses
the specified `view-name` from the specified `design-doc` design document.
Like the `keys` parameter for the [`GET`](#querying-a-view) method,
the `POST` method lets you specify the keys to use to retrieve the view results.
In all other aspects,
the `POST` method is identical to the [`GET`](#querying-a-view) API request.
In particular,
you can use any of its query parameters.

_Example HTTP request that returns all recipes,
where the key for the view matches either `claret` or `clear apple juice`:_

```http
POST /$DATABASE/_design/$DDOC/_view/$VIEWNAME HTTP/1.1
Content-Type: application/json
```
{:codeblock}

_Example of a request that returns all recipes,
where the key for the view matches either `claret` or `clear apple juice`,
that uses the command line:_

```sh
curl -X POST "https://INDEX_NAME$ACCOUNT.cloudant.com/$DATABASE/_design/$DDOC/_view/$VIEWNAME" -d @request.json
```
{:codeblock}

_Example JSON document that provides a list of keys to use in the query:_

```json
{
    "keys" : [
        "claret",
        "clear apple juice"
    ]
}
```
{:codeblock}

The response contains the standard view information,
but only documents where the keys match.

_Example response after running a query that uses a list of keys:_

```json
{
    "total_rows" : 26484,
    "rows" : [
        {
            "value" : [
              "Scotch collops"
            ],
            "id" : "Scotchcollops",
            "key" : "claret"
        },
        {
            "value" : [
              "Stand pie"
            ],
            "id" : "Standpie",
            "key" : "clear apple juice"
        }
    ],
    "offset" : 6324
}
```
{:codeblock}

<div id="include_docs_caveat"></div>

## Multi-document Fetching

Combining a `POST` request to a view with the `include_docs=true` query argument
enables you to retrieve multiple documents from a database.

For a client application,
this technique is more efficient than using multiple [`GET`](#querying-a-view) API requests.

However,
`include_docs=true` might require extra processing time when compared to accessing the view on its own.

The reason is that by using `include_docs=true` in a search,
all of the result documents must be retrieved to construct the response for the client application.
In effect,
a whole series of document `GET` requests are run,
each of which competes for resources with other application requests.

One way to mitigate this effect is by retrieving results directly from the Lucene index files.
Do this by omitting `include_docs=true`.
Instead,
in your design document specify `store=true` and `index=false` on the fields you want retrieved by your query.

For example,
in your index function,
you might use the following design specification:

```javascript
index("name", doc.name, {"store": true, "index": false});
```
{:codeblock}

You might use the same approach for view indexes.

_Example request using HTTP to obtain the full content of documents that match the listed keys:_

```http
POST /recipes/_design/recipes/_view/by_ingredient?include_docs=true HTTP/1.1
Content-Type: application/json
```
{:codeblock}

_Example JSON document that lists the keys to match:_

```json
{
    "keys" : [
        "claret",
        "clear apple juice"
    ]
}
```
{:codeblock}

_Example request using the command line to obtain the full content of documents that match the listed keys:_

```sh
curl "https://INDEX_NAME$ACCOUNT.cloudant.com/$DATABASE/_design/$DDOC/_view/by_ingredient?include_docs=true"
    -X POST \
    -H "Content-Type: application/json" \
    -d "{ "keys" : [ "claret", "clear apple juice" ] }"
```
{:codeblock}

_Example (abbreviated) response, returning the full document for each recipe that matches a provided key:_

```json
{
    "offset" : 6324,
    "rows" : [
        {
            "doc" : {
                "_id" : "Scotchcollops",
                "_rev" : "1-bcbdf724f8544c89697a1cbc4b9f0178",
                "cooktime" : "8",
                "ingredients" : [
                    {
                        "ingredient" : "onion",
                        "ingredtext" : "onion, peeled and chopped",
                        "meastext" : "1"
                    },
                    ...
                ],
                "keywords" : [
                    "cook method.hob, oven, grill@hob",
                    "diet@wheat-free",
                    "diet@peanut-free",
                    "special collections@classic recipe",
                    "cuisine@british traditional",
                    "diet@corn-free",
                    "diet@citrus-free",
                    "special collections@very easy",
                    "diet@shellfish-free",
                    "main ingredient@meat",
                    "occasion@christmas",
                    "meal type@main",
                    "diet@egg-free",
                    "diet@gluten-free"
                ],
                "preptime" : "10",
                "servings" : "4",
                "subtitle" : "This recipe ... short time.",
                "title" : "Scotch collops",
                "totaltime" : "18"
            },
            "id" : "Scotchcollops",
            "key" : "claret",
            "value" : [
                "Scotch collops"
            ]
        },
        {
            "doc" : {
                "_id" : "Standpie",
                "_rev" : "1-bff6edf3ca2474a243023f2dad432a5a",
                "cooktime" : "92",
                "ingredients" : [
                  ...
                ],
                "keywords" : [
                    "diet@dairy-free",
                    "diet@peanut-free",
                    "special collections@classic recipe",
                    "cuisine@british traditional",
                    "diet@corn-free",
                    "diet@citrus-free",
                    "occasion@buffet party",
                    "diet@shellfish-free",
                    "occasion@picnic",
                    "special collections@lunchbox",
                    "main ingredient@meat",
                    "convenience@serve with salad for complete meal",
                    "meal type@main",
                    "cook method.hob, oven, grill@hob / oven",
                    "diet@cow dairy-free"
                ],
                "preptime" : "30",
                "servings" : "6",
                "subtitle" : "Serve this pie with pickled vegetables and potato salad.",
                "title" : "Stand pie",
                "totaltime" : "437"
            },
            "id" : "Standpie",
            "key" : "clear apple juice",
            "value" : [
              "Stand pie"
            ]
        }
    ],
    "total_rows" : 26484
}
```
{:codeblock}

## Sending several queries to a view

To send several view queries in one request,
use a `POST` request to `/$DATABASE/_design/$DDOC/_view/$VIEWNAME`.

The request body is a JSON object that contains only the `queries` field.
It holds an array of query objects with fields for the parameters of the query.
The field names and their meaning are the same as the query parameters of a regular view request.

The JSON object that is returned in the response contains only the `results` field,
which holds an array of result objects: one result for each query.

Each result object contains the same fields as the response to a regular view request.

_Example request using HTTP that contains several queries:_

```http
POST /$DATABASE/_design/$DDOC/_view/$VIEWNAME HTTP/1.1
Content-Type: application/json
```
{:codeblock}

_Example request containing several queries, that uses the command line:_

```sh
curl https://$ACCOUNT.cloudant.com/$DATABASE/_design/$DDOC/_view/$VIEWNAME -H 'Content-Type: application/json' -d @request-body.json
    # where request-body.json is a file containing JSON data describing the queries
```
{:codeblock}

_Example JSON document that contains several queries:_

```json
{
    "queries": [
        {
            ...
        },
        {
            "startkey": 1,
            "limit": 2
        }
    ]
}
```
{:codeblock}

_Example response:_

```json
{
    "results": [
        {
            "total_rows": 3,
            "offset": 0,
            "rows": [
                {
                    "id": "8fbb1250-6908-42e0-8862-aef60dc430a2",
                    "key": 0,
                    "value": {
                        "_id": "8fbb1250-6908-42e0-8862-aef60dc430a2",
                        "_rev": "1-ad1680946839206b088da5d9ac01e4ef",
                        "foo": 0,
                        "bar": "foo"
                    }
                },
                {
                    "id": "d69fb42c-b3b1-4fae-b2ac-55a7453b4e41",
                    "key": 1,
                    "value": {
                        "_id": "d69fb42c-b3b1-4fae-b2ac-55a7453b4e41",
                        "_rev": "1-abb9a4fc9f0f339efbf667ace66ee6a0",
                        "foo": 1,
                        "bar": "bar"
                    }
                },
                {
                    "id": "d1fa85cd-cd18-4790-8230-decf99e1f60f",
                    "key": 2,
                    "value": {
                        "_id": "d1fa85cd-cd18-4790-8230-decf99e1f60f",
                        "_rev": "1-d075a71f2d47af7d4f64e4a367160e2a",
                        "foo": 2,
                        "bar": "baz"
                    }
                }
            ]
        },
        {
            "total_rows": 3,
            "offset": 1,
            "rows": [
                {
                    "id": "d69fb42c-b3b1-4fae-b2ac-55a7453b4e41",
                    "key": 1,
                    "value": {
                        "_id": "d69fb42c-b3b1-4fae-b2ac-55a7453b4e41",
                        "_rev": "1-abb9a4fc9f0f339efbf667ace66ee6a0",
                        "foo": 1,
                        "bar": "bar"
                    }
                },
                {
                    "id": "d1fa85cd-cd18-4790-8230-decf99e1f60f",
                    "key": 2,
                    "value": {
                        "_id": "d1fa85cd-cd18-4790-8230-decf99e1f60f",
                        "_rev": "1-d075a71f2d47af7d4f64e4a367160e2a",
                        "foo": 2,
                        "bar": "baz"
                    }
                }
            ]
        }
    ]
}
```
{:codeblock}
