---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Documents

Documents are
[JSON objects ![External link icon](../images/launch-glyph.svg "External link icon")](http://en.wikipedia.org/wiki/JSON#Data_types.2C_syntax_and_example){:new_window}.
Documents are containers for your data,
and are the basis of the Cloudant database.
{:shortdesc}

Documents are limited to a maximum size of 64 MB.

>   **Note**: If you are using a [Cloudant service on IBM Bluemix](../offerings/bluemix.html),
    documents are limited to a maximum size of 1 MB.
    Exceeding this limit causes a [`413` error](http.html#413).

All documents must have two fields:
a unique `_id` field, and a `_rev` field.

The `_id` field is either created by you,
or generated automatically as a
[UUID ![External link icon](../images/launch-glyph.svg "External link icon")](http://en.wikipedia.org/wiki/Universally_unique_identifier){:new_window} by Cloudant.

The `_rev` field is a revision number,
and is [essential to Cloudant's replication protocol](../guides/mvcc.html).
In addition to these two mandatory fields,
documents can generally contain any other content that can be described using JSON.

Field names beginning with the underscore character (`_`) are reserved in Cloudant.
This means you cannot normally have your own field names that begin with an underscore.
For example,
the field `example` would be permitted,
but the field `_example` would result in a `doc_validation` error message.

_Example of JSON document attempting to create a topmost field with an underscore prefix:_

```json
{
	"_top_level_field_name": "some data"
}
```
{:codeblock}

_Error message returned when attempting to create a topmost field with an underscore prefix:_

```json
{
	"error": "doc_validation",
	"reason": "Bad special document member: _top_level_field_name"
}
```
{:codeblock}

However,
if the field name is for an object _nested within_ the document,
it is possible to use an underscore prefix for the field name.

_Example of JSON document attempting to create a field with an underscore prefix, nested within an object:_

```json
{
	"another_top_level_field_name": "some data",
	"another_field": {
		"_lower_level_field_name": "some more data"
	}
}
```
{:codeblock}

_Example success message (abbreviated) returned when creating a nested field with an underscore prefix:_

```json
{
	"ok": true,
	"id": "2",
	"rev": "1-9ce...8d4"
}
```
{:codeblock}

Cloudant uses an [eventually consistent](../guides/cap_theorem.html#consistency) model for data.
This means that under some conditions,
it is possible that if your application performs a document write or update,
followed immediately by a read of the same document,
older document content is retrieved.
In other words,
your application would see the document content as it was *before* the write or update occurred.
For more information about this,
see the topic on [Consistency](../guides/cap_theorem.html#consistency).

<div id="documentCreate"></div>

## Create

To create a document,
send a `POST` request with the document's JSON content to `https://$USERNAME.cloudant.com/$DATABASE`.

_Creating a document, using HTTP:_

```http
POST /$DATABASE HTTP/1.1
Content-Type: application/json
```
{:codeblock}

_Creating a document, using the command line:_

```sh
curl https://$USERNAME:$PASSWORD@$USERNAME.cloudant.com/$DATABASE \
	-X POST \
	-H "Content-Type: application/json" \
	-d "$JSON"
```
{:codeblock}

<!--

_Creating a document, using Javascript:_

```javascript
var nano = require('nano');
var account = nano("https://"+$USERNAME+":"+$PASSWORD+"@"+$USERNAME+".cloudant.com");
var db = account.use($DATABASE);

db.insert($JSON, function (err, body, headers) {
	if (!err) {
		console.log(body);
	}
});
```
{:codeblock}

-->

_Example document, specified using JSON:_

```json
{
	"_id": "apple",
	"item": "Malus domestica",
	"prices": {
		"Fresh Mart": 1.59,
		"Price Max": 5.99,
		"Apples Express": 0.79
	}
}
```
{:codeblock}

The response is a JSON document containing the ID of the created document,
the revision string,
and `"ok": true`.

If you did not provide an `_id` field,
Cloudant generates one automatically as a
[UUID ![External link icon](../images/launch-glyph.svg "External link icon")](http://en.wikipedia.org/wiki/Universally_unique_identifier){:new_window}.

If creation of the document failed,
the response contains a description of the error.

_Example response after successfully creating a document:_

```json
{
	"ok":true,
	"id":"apple",
	"rev":"1-2902191555"
}
```
{:codeblock}

>	**Note**: If the write [quorum](#quorum) cannot be met when creating a document,
a [`202` response](http.html#202) is returned.

## Read

To retrieve a document,
send a GET request to `https://$USERNAME.cloudant.com/$DATABASE/$DOCUMENT_ID`.

If you do not know the `_id` for a particular document,
you can [query the database](database.html#get-documents) for all documents.

>	**Note**: Due to the distributed,
eventually consistent nature of Cloudant,
reads might return stale data.
In particular,
data that has just been written,
even by the same client,
might not be returned from a read request immediately following the write request.
To work around this behavior,
a client can cache state locally.
Caching also helps to keep request counts down,
increase application performance,
and decrease load on the database cluster.
This also applies to other read requests such as to map-reduce and search indexes.

_Example of retrieving a document, using HTTP:_

```http
GET /$DATABASE/$DOCUMENT_ID HTTP/1.1
```
{:codeblock}

_Example of retrieving a document, using the command line:_

```sh
curl https://$USERNAME:$PASSWORD@$USERNAME.cloudant.com/$DATABASE/$DOCUMENT_ID
```
{:codeblock}

<!--

_Example of retrieving a document, using Javascript:_

```javascript
var nano = require('nano');
var account = nano("https://"+$USERNAME+":"+$PASSWORD+"@"+$USERNAME+".cloudant.com");
var db = account.use($DATABASE);

db.get($JSON._id, function (err, body, headers) {
	if (!err) {
		console.log(body);
	}
});
```
{:codeblock}

-->

The response contains the document you requested or a description of the error if the document could not be retrieved.

_Example response:_

```json
{
	"_id": "apple",
	"_rev": "1-2902191555",
	"item": "Malus domestica",
	"prices": {
		"Fresh Mart": 1.59,
		"Price Max": 5.99,
		"Apples Express": 0.79
	}
}
```
{:codeblock}

### Query Parameters

This is a list of parameters you can add to the URL in the usual way,
for example `/mydatabase/doc?attachments=true&conflicts=true`.

All parameters are *optional*.

Name                | Type | Description | Default
--------------------|------|-------------|--------
`attachments`       | boolean | Includes attachments bodies in response. | false
`att_encoding_info` | boolean | Includes encoding information in attachment stubs if the particular attachment is compressed. | false
`atts_since`        | array of revision strings | Includes attachments only since specified revisions. Doesn’t includes attachments for specified revisions. | []
`conflicts`         | boolean | Includes information about conflicts in document. | false
`deleted_conflicts` | boolean | Includes information about deleted conflicted revisions. | false
`latest`            | boolean | Forces retrieving latest “leaf” revision, no matter what rev was requested. | false
`local_seq`         | boolean | Includes last update sequence number for the document. | false
`meta`              | boolean | Acts same as specifying all conflicts, deleted_conflicts and open_revs query parameters. | false
`open_revs`         | array or `all` | Retrieves documents of specified leaf revisions. Additionally, it accepts value as all to return all leaf revisions. | []
`rev`               | string | Retrieves document of specified revision. | -
`revs`              | boolean | Includes list of all known document revisions. | false
`revs_info`         | boolean | Includes detailed information for all known document revisions. | false

## Read Many

To fetch more than one document at a time,
[query the database](database.html#get-documents),
using the `include_docs` option.

## Update

To update a document,
send a `PUT` request with the updated JSON content *and* the latest `_rev` value
to `https://$USERNAME.cloudant.com/$DATABASE/$DOCUMENT_ID`.
You can also use this `PUT` method to create a document,
in which case you do not need to supply the latest `_rev` value.

>   **Note**: If you fail to provide the latest `_rev` when updating an existing document,
    Cloudant responds with a [409 error](http.html#409).
    This error prevents you overwriting data changed by other processes.
    If the write [quorum](#quorum) cannot be met, a [`202` response](http.html#202) is returned.

>   **Note**: Any document update can lead to a conflict,
    especially when replicating updated documents.
    More information about avoiding and resolving conflicts is in
    the [Document Versioning and MVCC guide](../guides/mvcc.html).

_Example of updating a document, using HTTP:_

```http
PUT /$DATABASE/$DOCUMENT_ID HTTP/1.1
```
{:codeblock}

_Example of updating a document, using the command line:_

```sh
# make sure $JSON contains the correct `_rev` value!
curl https://$USERNAME:$PASSWORD@$USERNAME.cloudant.com/$DATABASE/$DOCUMENT_ID \
	-X PUT \
	-H "Content-Type: application/json" \
	-d "$JSON"
```
{:codeblock}

<!--

_Example of updating a document, using Javascript:_

```javascript
var nano = require('nano');
var account = nano("https://"+$USERNAME+":"+$PASSWORD+"@"+$USERNAME+".cloudant.com");
var db = account.use($DATABASE);

// make sure $JSON contains the correct `_rev` value!
$JSON._rev = $REV;

db.insert($JSON, $JSON._id, function (err, body, headers) {
	if (!err) {
		console.log(body);
	}
});
```
{:codeblock}

-->

_Example of JSON data containing an updated document:_

```json
{
	"_id": "apple",
	"_rev": "1-2902191555",
	"item": "Malus domestica",
	"prices": {
		"Fresh Mart": 1.59,
		"Price Max": 5.99,
		"Apples Express": 0.79,
		"Gentlefop's Shackmart": 0.49
	}
}
```
{:codeblock}

The response contains the ID and the new revision of the document,
or an error message if the update failed.

_Example response following a successful update:_

```json
{
	"ok":true,
	"id":"apple",
	"rev":"2-9176459034"
}
```
{:codeblock}

<div id="document-delete"></div>

## Delete

To delete a document,
send a `DELETE` request with the document's latest `_rev` in the query string,
to `https://$USERNAME.cloudant.com/$DATABASE/$DOCUMENT_ID`.

The response contains the ID and the new revision of the document,
or an error message if the delete failed.

>	**Note**: If you fail to provide the latest `_rev`,
Cloudant responds with a [409 error](http.html#409).
This error prevents you overwriting data changed by other clients.
If the write [quorum](#quorum) cannot be met,
a [`202` response](http.html#202) is returned.

>	**Note**: Cloudant does not completely delete the specified document.
Instead,
it leaves a [tombstone](#-tombstone-documents) with very basic information about the document.
The tombstone is required so that the delete action can be replicated to other copies of the database.
Since the tombstones stay in the database indefinitely,
creating new documents and deleting them increases the disk space usage of a database.
They might also increase the query time for the primary index,
which is used to look up documents by their ID.

_Example of a delete request, using HTTP:_

```http
DELETE /$DATABASE/$DOCUMENT_ID?rev=$REV HTTP/1.1
```
{:codeblock}

_Example of a delete request, using the command line:_

```sh
# make sure $JSON contains the correct `_rev` value!
curl https://$USERNAME:$PASSWORD@$USERNAME.cloudant.com/$DATABASE/$DOCUMENT_ID?rev=$REV -X DELETE
```
{:codeblock}

<!--

_Example of a delete request, using Javascript:_

```javascript
var nano = require('nano');
var account = nano("https://"+$USERNAME+":"+$PASSWORD+"@"+$USERNAME+".cloudant.com");
var db = account.use($DATABASE);

// make sure $JSON contains the correct `_rev` value!
db.destroy($JSON._id, $REV, function (err, body, headers) {
	if (!err) {
		console.log(body);
	}
});
```
{:codeblock}

-->

_Example response following a successful deletion request:_

```json
{
	"id" : "apple",
	"ok" : true,
	"rev" : "3-2719fd4118"
}
```
{:codeblock}

## 'Tombstone' documents

Tombstone documents are small documents retained in place within a database when the original document is deleted.
Their purpose is to allow the deletion to be replicated.

When the replication has completed,
the tombstones are no longer required.
Normally,
this is not a problem,
as automatic compaction helps ensure that only the minimal amount of data is retained and transferred during replication.
Nevertheless,
tombstone documents are not automatically removed,
or 'purged'.

Over time,
as documents are created and deleted,
the number of tombstone documents increases.
Each tombstone is small,
but gradually they add to database disk space usage,
and to the query time for the primary index.
To reduce these effects,
you might want to remove the tombstones.

### Simple removal of 'tombstone' documents

To remove tombstones manually,
perform the following steps:

1.	Create a new database to hold the required documents.
	The new database is intended to hold all documents _except_ the tombstone documents.
2.	Set up a [filtered replication](advanced_replication.html#filtered-replication) to
	replicate documents from the original database to the new database.
	Configure the filter so that documents with the '`_deleted`' attribute are not replicated.
3.	When replication is complete,
	switch your application logic to use the new database.
4.	Verify that your applications work correctly with the new database.
	When you are satisfied that everything is working correctly,
	you might wish to delete the old database.

>	**Note**: In general,
you should try to design and implement your applications to perform the minimum necessary amount of deletion.

_Example filter to exclude deleted documents during a replication:_

```json
{
	"_id": "_design/filters",
	"filters": {
		"deleted_filter": "function(doc, req) { return !doc._deleted; };"
	}
}
```
{:codeblock}

### Advanced removal of tombstone documents

The simple removal technique described [previously](#simple-removal-of-tombstone-documents) works well,
so long as documents are not being updated in the source database while the replication takes place.

If updates _are_ made during replication,
it is possible that a complete document is replicated to the target database as normal,
but is also deleted from the source database,
leaving a tombstone.
The problem is that the tombstone is not replicated across to the target database,
because it is excluded by the filter.
As a result,
the document that was deleted from the source database is not deleted from the target database,
causing an inconsistency.

A solution is to perform more advanced removal of tombstones using
a [`validate_doc_update` function ![External link icon](../images/launch-glyph.svg "External link icon")](http://docs.couchdb.org/en/1.6.1/couchapp/ddocs.html#validate-document-update-functions){:new_window}.

A `validate_doc_update` function is stored in a design document.
The function is executed every time a document is updated in the database.
The function can be used to prevent invalid or unauthorized document updates from being performed.

The function works using the following parameters:

-	The new version of the document.
-	The current version of the document in the database.
-	A user context,
	which provides details about the user supplying the updated document.

The function inspects the request to determine if the update should proceed.
If the update is permitted,
the function simply returns.
If the update is not permitted,
a suitable error object is returned.
In particular,
if the user is not authorized to make the update,
an `unauthorized` error object is returned,
along with an explanatory error message.
Similarly,
if the requested update is not allowed for some reason (such as some mandatory fields being absent from the new document),
then a `forbidden` error object is returned,
again with an explanatory error message.

For tombstone removal,
a suitable `validate_doc_update` function would work as follows:

1.	If the update is to apply a change to an existing document (`oldDoc`) within the target database,
	the function allows this by simply returning.
	The reason is that the update affected a document that was copied to the target database during the replication,
	but which has subsequently changed in the source database during the replication.
	It is possible that the change was a `DELETE`,
	resulting in a tombstone record in the target database.
	The tombstone record is removed by a subsequent replication process at some point in the future.
2.	If the target database does _not_ have a copy of the current document,
	_and_ the update document has the `_deleted` property (indicating that it is a tombstone),
	then the update must be a tombstone _and_ it has been encountered before,
	so the update should be rejected.
3.	Finally,
	if the function has not yet returned or thrown an error,
	allow the update to replicate to the target database,
	as some other condition applies.

_Example `validate_doc_update` function to reject deleted documents not already present in the target database:_

```javascript
function(newDoc, oldDoc, userCtx) {
	// any update to an existing doc is OK
	if(oldDoc) {
		return;
	}

	// reject tombstones for docs we don’t know about
	if(newDoc["_deleted"]) {
		throw({forbidden : "Deleted document rejected"});
	}

	return; // Not strictly necessary, but clearer.
}
```
{:codeblock}

To use a `validate-doc-update` function to remove tombstone documents:

1.	Stop replication from the source to the target database.
2.	If appropriate,
	delete the target database,
	then create a new target database.
3.	Add a suitable `validate_doc_update` function,
	similar to the example provided.
	Add it to a design document in the target database.
4.	Restart replication between the source and the (new) target database.
5.	When replication is complete,
	switch your application logic to use the new database.
6.	Verify that your applications work correctly with the new database.
	When you are satisfied that everything is working correctly,
	you might wish to delete the old database.

A variation for using the `validate_doc_update` function to remove tombstone documents if possible.
You might add some metadata to the tombstone documents,
for example to record the deletion date.
The function could then inspect the metadata and permit deletion documents through
if they have not been applied to the target database,
in order to replicate the deletion correctly.

### Performance implications of tombstone removal

Remember that tombstones are used for more consistent deletion of documents from databases.
This is especially important for mobile devices:
without tombstone documents,
a deletion might not replicate correctly to a mobile device,
with the result that documents might never be deleted from the device.

If you recreate a database,
for example to be a new target for a replication,
any clients that use the target database as a server _must_ work through _all_ the changes again,
because the database sequence numbers are likely to have changed.

>	**Note**: If you are using a `validate_doc_update` function,
you should avoid replicating that function to clients.
This is to prevent the possibility of unwanted side effects as a result of having the function present on the client.

>	**Note**: [Cloudant Sync](../libraries/supported.html#mobile) libraries do not replicate design documents,
so replication of `validate_doc_update` functions should not normally be a problem for Cloudant.
However,
other clients might replicate design documents or `validate_doc_update` functions,
potentially resulting in unwanted side effects.

## Bulk Operations

The bulk document API allows you to create and update multiple documents at the same time within a single request.
The basic operation is similar to creating or updating a single document,
except that you batch the document structure and information.

When creating new documents the document ID is optional.
For updating existing documents,
you must provide the document ID,
revision information,
and new document values.

<div id="request-body"></div>

### Bulk request structure

For both inserts and updates the basic structure of the JSON document in the request is the same:

Field  | Description             | Type             | Optional
-------|-------------------------|------------------|---------
`docs` | Bulk Documents Document | Array of objects | no

<div id="object-in-docs-array"></div>

Each `docs` array object has the following structure:

Field      | Description                             | Type    | Optional
-----------|-----------------------------------------|---------|---------
`_id`      | Document ID                             | String  | Optional only for new documents.
`_rev`     | Document revision                       | String  | Mandatory for updates and deletes, not used for new documents.
`_deleted` | Whether the document should be deleted. | Boolean | Yes

_Example request to create, update, or delete multiple documents, using HTTP:_

```http
POST /$DATABASE/_bulk_docs HTTP/1.1
Content-Type: application/json
```
{:codeblock}

_Example request to create, update, or delete multiple documents, using the command line:_

```sh
curl https://$USERNAME:$PASSWORD@$USERNAME.cloudant.com/$DATABASE/_bulk_docs \
	-X POST \
	-H "Content-Type: application/json" \
	-d "$JSON"
```
{:codeblock}

<!--

_Example request to create, update, or delete multiple documents, using Javascript:_

```javascript
var nano = require('nano');
var account = nano("https://$USERNAME:$PASSWORD@$USERNAME.cloudant.com");
var db = account.use($DATABASE);

db.bulk($JSON, function (err, body) {
	if (!err) {
		console.log(body);
	}
});
```
{:codeblock}

-->

_Example JSON describing the update, creation, and deletion of three documents in one bulk request:_

```json
{
	"docs": [
		{
			"name": "Nicholas",
			"age": 45,
			"gender": "female",
			"_id": "96f898f0-f6ff-4a9b-aac4-503992f31b01",
			"_rev": "1-54dd23d6a630d0d75c2c5d4ef894454e"
		},
		{
			"name": "Taylor",
			"age": 50,
			"gender": "female"
		},
		{
			"_id": "d1f61e66-7708-4da6-aa05-7cbc33b44b7e",
			"_rev": "1-a2b6e5dac4e0447e7049c8c540b309d6",
			"_deleted": true
		}
	]
}
```
{:codeblock}

<div id="response"></div>

### Bulk request responses

The HTTP status code received in response tells you whether the request was fully or partially successful.
In the response body itself,
you get an array with detailed information for each document in the request.

Code | Description
-|-
`201` | The request succeeded, but this does not imply all documents were updated. Inspect the response body to determine the status of each requested change, and [address any problems](#bulk-document-validation-and-conflict-errors).
`202` | For at least one document, the write [quorum](#quorum) has not been met.

_Example response from a bulk request:_

```json
[
	{
		"id": "96f898f0-f6ff-4a9b-aac4-503992f31b01",
		"rev": "2-ff7b85665c4c297838963c80ecf481a3"
	},
	{
		"id": "5a049246-179f-42ad-87ac-8f080426c17c",
		"rev": "2-9d5401898196997853b5ac4163857a29"
	},
	{
		"id": "d1f61e66-7708-4da6-aa05-7cbc33b44b7e",
		"rev": "2-cbdef49ef3ddc127eff86350844a6108"
	}
]
```
{:codeblock}

### Inserting documents in bulk

To insert documents in bulk into a database,
you need to supply a JSON structure with the array of documents that you want to add to the database.
You can either include a document ID for each document,
or allow the document ID to be automatically generated.

_Example JSON for a bulk insert of three documents:_

```json
{
	"docs": [
		{
			"name": "Nicholas",
			"age": 45,
			"gender": "male",
			"_id": "96f898f0-f6ff-4a9b-aac4-503992f31b01",
			"_attachments": {

			}
		},
		{
			"name": "Taylor",
			"age": 50,
			"gender": "male",
			"_id": "5a049246-179f-42ad-87ac-8f080426c17c",
			"_attachments": {

			}
		},
		{
			"name": "Owen",
			"age": 51,
			"gender": "male",
			"_id": "d1f61e66-7708-4da6-aa05-7cbc33b44b7e",
			"_attachments": {

			}
		}
	]
}
```
{:codeblock}

The return code from a successful bulk insertion is [`201`](http.html#201),
with the content of the returned structure indicating specific success
or other information messages on a per-document basis.

_Example response header after successful bulk insert of three documents:_

```http
201 Created
Cache-Control: must-revalidate
Content-Length: 269
Content-Type: application/json
Date: Mon, 04 Mar 2013 14:06:20 GMT
server: CouchDB/1.0.2 (Erlang OTP/R14B)
x-couch-request-id: e8ff64d5
```
{:codeblock}

The returned JSON contains a list of the documents created,
including their revision and ID values.

The content and structure of the returned JSON depends on the transaction semantics being used for the bulk update;
see [Bulk Documents Transaction Semantics](#bulk-documents-transaction-semantics) for more information.
Conflicts and validation errors when updating documents in bulk must be handled separately;
see [Bulk Document Validation and Conflict Errors](#bulk-document-validation-and-conflict-errors).

_Example response content after successful bulk insert of three documents:_

```json
[
	{
		"id": "96f898f0-f6ff-4a9b-aac4-503992f31b01",
		"rev": "1-54dd23d6a630d0d75c2c5d4ef894454e"
	},
	{
		"id": "5a049246-179f-42ad-87ac-8f080426c17c",
		"rev": "1-0cde94a828df5cdc0943a10f3f36e7e5"
	},
	{
		"id": "d1f61e66-7708-4da6-aa05-7cbc33b44b7e",
		"rev": "1-a2b6e5dac4e0447e7049c8c540b309d6"
	}
]
```
{:codeblock}

### Updating Documents in Bulk

The bulk document update procedure is similar to the insertion procedure,
except that you must specify the document ID and current revision for every document in the bulk update JSON string.

Optionally,
you can delete documents during a bulk update by adding a `_deleted` field with a value of `true`
to each affected document ID and revision combination within the request JSON structure.

_Example request to perform bulk update, using HTTP:_

```http
POST /test/_bulk_docs HTTP/1.1
Accept: application/json
```
{:codeblock}

_Example request to perform bulk update, using the command line:_

```sh
curl -X POST "https://$USERNAME.cloudant.com/$DATABASE/_bulk_docs" \
	-d @request.json
```
{:codeblock}

_Example JSON structure to request bulk update of documents:_

```json
{
	"docs": [
		{
			"name": "Nicholas",
			"age": 45,
			"gender": "female",
			"_id": "96f898f0-f6ff-4a9b-aac4-503992f31b01",
			"_attachments": {

			},
			"_rev": "1-54dd23d6a630d0d75c2c5d4ef894454e"
		},
		{
			"name": "Taylor",
			"age": 50,
			"gender": "female",
			"_id": "5a049246-179f-42ad-87ac-8f080426c17c",
			"_attachments": {

			},
			"_rev": "1-0cde94a828df5cdc0943a10f3f36e7e5"
		},
		{
			"name": "Owen",
			"age": 51,
			"gender": "female",
			"_id": "d1f61e66-7708-4da6-aa05-7cbc33b44b7e",
			"_attachments": {

			},
			"_rev": "1-a2b6e5dac4e0447e7049c8c540b309d6"
		}
	]
}
```
{:codeblock}

The return JSON structure summarizes the updated documents,
with the new revision and ID information.

_Example JSON structure returned after bulk update:_

```json
[
	{
		"id": "96f898f0-f6ff-4a9b-aac4-503992f31b01",
		"rev": "2-ff7b85665c4c297838963c80ecf481a3"
	},
	{
		"id": "5a049246-179f-42ad-87ac-8f080426c17c",
		"rev": "2-9d5401898196997853b5ac4163857a29"
	},
	{
		"id": "d1f61e66-7708-4da6-aa05-7cbc33b44b7e",
		"rev": "2-cbdef49ef3ddc127eff86350844a6108"
	}
]
```
{:codeblock}

### Bulk Documents Transaction Semantics

If your request receives a [`202` response](http.html#202),
the only guarantee is that some of the document tasks were processed completely.
The response body contains the list of documents successfully inserted or updated during the process.

A successful document update is indicated by the presence of a new `_rev` parameter for the document,
indicating that a new document revision was successfully created.

If a document update failed,
then you get an `error` of type `conflict` for that document.
In this case,
no new revision has been created.
You must submit the document update again,
with the same revision tag,
to re-try the document update.

_Example bulk update response with errors:_

```json
[
	{
		"id" : "FishStew",
		"error" : "conflict",
		"reason" : "Document update conflict."
	},
	{
		"id" : "LambStew",
		"error" : "conflict",
		"reason" : "Document update conflict."
	},
	{
		"id" : "7f7638c86173eb440b8890839ff35433",
		"error" : "conflict",
		"reason" : "Document update conflict."
	}
]
```
{:codeblock}

### Bulk Document Validation and Conflict Errors

The JSON returned by the `_bulk_docs` operation consists of an array of JSON structures,
one for each document in the original submission.
The returned JSON structure should be examined
to ensure that all of the documents submitted in the original request were successfully added to the database.

The structure of the returned information is as follows:

Field  | Description             | Type
-------|-------------------------|-----
`docs` | Bulk Documents Document | Array of objects

<div id="fields-of-objects-in-docs-array"></div>

Each `docs` array object has the following structure:

Field    | Description                        | Type
---------|------------------------------------|-----
`id`     | Document ID                        | String
`error`  | Error type.                        | String
`reason` | Error string with extended reason. | String

When a document (or document revision) is not correctly committed to the database because of an error,
you should check the `error` field to determine error type and course of action.
The error is one of [`conflict`](#conflict) or [`forbidden`](#forbidden).

### `conflict`

The document as submitted is in conflict.
If you used the default bulk transaction mode,
then the new revision was not created.
You must re-submit the document to the database.

Conflict resolution of documents added using the bulk docs interface is identical
to the resolution procedures used when resolving conflict errors during replication.

### `forbidden`

Entries with this error type indicate that the validation routine applied
to the document during submission has returned an error.

_Example javascript to produce `forbidden` error as part of a validation function:_

```javascript
throw({forbidden: 'invalid recipe ingredient'});
```
{:codeblock}

_Example error message from a validation function:_

```json
{
	"id" : "7f7638c86173eb440b8890839ff35433",
	"error" : "forbidden",
	"reason" : "invalid recipe ingredient"
}
```
{:codeblock}

<div id="quorum"></div>

## Quorum - writing and reading data

In a distributed system,
it is possible that a request might take some time to complete.
A 'quorum' mechanism is used to help determine when a given request,
such as a write or read,
has completed successfully.

For help understanding quorum settings and their implications on dedicated Cloudant systems,
contact Cloudant support.

## TTL - Time to Live

[Time to Live ![External link icon](../images/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/Time_to_live){:new_window} (TTL) is a property of data,
where after a relative amount of time,
or at an absolute time,
the data is deemed to have expired.
The data itself might be deleted or moved to an alternative (archive) location.

Cloudant does _not_ support Time to Live functionality.

The reason is that Cloudant documents are only 'soft' deleted,
not completely deleted.
The soft deletion involves replacing the original document with a [smaller record](#-tombstone-documents).
This small record or 'tombstone' is required for replication purposes;
it helps ensure that the correct revision to use can be identified during replication.

If TTL were available in Cloudant,
the resulting potential increase in short-lived documents and soft deletion records
would mean that the database size could grow in an unbounded fashion.
