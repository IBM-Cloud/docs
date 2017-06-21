
---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Acrolinx: 2017-04-25 -->

<div id="ReplicationAPI"></div>

# Replication

Cloudant replication is the process that synchronizes ('syncs') the state of two databases.
{:shortdesc}

Any change that occurred in the source database is reproduced in the target database.
You can create replications between any number of databases, whether continuous or not.

Depending on your application requirements,
you use replication to share and aggregate state and content.

Replication takes place in one direction only.
To keep two databases synchronized with each other,
you must replicate in both directions.
Do this by replicating from `database1` to `database2`,
and separately from `database2` to `database1`.

## Important notes

Replications can severely impact the performance of a Cloudant cluster.
Performance testing helps you understand the impact on your environment
under an increasing number of concurrent replications.

Continuous replication can result in many internal calls.
Requiring many calls might affect the costs for multi-tenant users of Cloudant systems.
By default,
continuous replication is not enabled.

The target database must exist.
It is not automatically created if it does not exist.
Add `"create_target":true` to the JSON document that describes the replication
if the target database does not exist before replication.

Replicator databases must be maintained and looked after,
just like any other valuable data store.
For more information,
see [replication database maintenance](#replication-database-maintenance).

## Creating replications

Replications are created in one of two ways:

1.	A replication can be created by using a [replication document](#replication-document-format)
	in the `_replicator` database.
	Creating and modifying replications in this way enables control of a replication
	in the same as working with other documents.
	Replication jobs created this way are resumed automatically after a node restart.
2.	A replication can be started by `POST`ing a JSON document that describes the wanted replication
	directly to the `/_replicate` endpoint.
	Replication jobs created this way are not resumed if the node they run on is restarted. 

## Replication document format

>	**Note**: You must use the *full* URL
	when you specify the source and target databases in a replication document.

The format of the document that is used to describe a replication is as follows:

<div id="checkpoints"></div>

Field Name | Required | Description
-----------|----------|-------------
`source` | yes | Identifies the database to copy revisions from. Can be a database URL, or an object whose url property contains the full URL of the database.
`target` | yes | Identifies the database to copy revisions to. Same format and interpretation as source. Does not have to be the same value as the `source` field.
`continuous` | no | Continuously syncs state from the `source` to the `target`, stopping only when deleted.
`create_target` | no | A value of `true` tells the replicator to create the `target` database if it does not exist.
`doc_ids` | no | Array of document IDs; if given, only these documents are replicated.
`filter` | no | Name of a [filter function](design_documents.html#filter-functions), defined in a design document. The filter function determines which documents get replicated. Using the `selector` option provides performance benefits when compared with using the `filter` option. Use the `selector` option where possible.
`proxy` | no | Proxy server URL.
`query_params` | no | A field that contains key:value pairs, for use in [filter function](design_documents.html#filter-functions).
`selector` | no | Provide a simple filter to select the documents that are included in the replication. Using the `selector` option provides performance benefits when compared with using the `filter` option. More information about `selector` is available [here](#selector-field).
`since_seq` | no | Override the incremental nature of replication. More information about `since_seq` is available [here](#since-seq-field).
`use_checkpoints` | no | Indicate whether to create checkpoints. Checkpoints greatly reduce the time and resources that are needed for repeated replications. Setting this field to `false` removes the requirement for write access to the `source` database. Defaults to `true`.
`user_ctx` | no | An object that contains the user name and optionally an array of roles, for example: `"user_ctx": {"name": "jane", "roles": ["admin"]} `. This object is needed for the replication to show up in the output of `/_active_tasks`.

<div id="selector-field"></div>

### The `selector` field

If you do not want to replicate the entire contents of a database,
you can specify a simple filter in the `selector` field.
The filter takes the form of a [Cloudant Query](cloudant_query.html) selector object.

Using a selector object provides performance benefits when compared with using a
[filter function](design_documents.html#filter-functions).
Use the `selector` option where possible.


The selector object identifies a field (such as `_id` in the following example),
and an expression (such as `"$gte": "d2"`) that must be true for that field
in order for the selector to allow the document to be replicated.
In the following example,
only documents that have a `_id` field with a value greater than or equal to `"d2"` are replicated.

_Example `selector` object in a replication document:_

```json
{
	"source": "https://$ACCOUNT1.cloudant.com/$DATABASE1",
	"target": "https://$ACCOUNT2.cloudant.com/$DATABASE2",
	"selector": {
		"_id": {
			"$gte": "d2"
		}
	},
	"continuous": true
}
```
{:codeblock}


A problem with the replication request results in the return of
an HTTP [`400`](http.html#400) error.
The error includes more details about the problem in the `"reason"` field of the response.
The reason might be one of:

-	The Cloudant Query selector object is missing.
-	The selector object is not valid JSON.
-	The selector object does not describe a valid Cloudant Query.

More information about using a `selector` object is available in the
[Apache CouchDB documentation ![External link icon](../images/launch-glyph.svg "External link icon")](http://docs.couchdb.org/en/2.0.0/api/database/changes.html#selector){:new_window}.

_Example error response if the selector is not valid:_

```json
{
	"error": "bad request",
	"reason": "<details of the problem>"
}
```
{:codeblock}

<div id="since-seq-field"></div>

### The `since_seq` field

If you do not want to replicate the entire contents of a database,
you can specify a 'replication sequence value' in the `since_seq` field.

The replication sequence value indicates how far to step 'through' a database,
for example as part of a replication.
Setting the contents of the `since_seq` field to this value ensures that the replication starts from that point,
rather than from the very beginning.

This field might be used for creating incremental copies of databases. To do this:

1.	Find the ID of the [checkpoint](#checkpoints) document for the last replication. It is stored in the  `_replication_id` field of the replication document in the [`_replicator` database](#replicator-database).
2.	Open the checkpoint document at `/$DATABASE/_local/$REPLICATION_ID`, where `$REPLICATION_ID` is the ID you found in the previous step, and `$DATABASE` is the name of the source or the target database. The document usually exists on both databases but might only exist on one.
3.	Search for the `recorded_seq` field of the first element in the history array.
4.	Set the `since_seq` field in the replication document to the value of the `recorded_seq` field.
5.	Replicate to a new database.

>   **Note**: By definition, using `since_seq` disables the normal replication checkpointing facility, so use `since_seq` with caution.

<div id="replicator-database"></div>

## The `_replicator` database

The `_replicator` database is a special database where you can `PUT` or `POST` documents to trigger replications,
or `DELETE` to cancel ongoing replications.
These documents have the same content as the JSON documents you can `POST` to the
[`/_replicate`](#the-_replicate-endpoint) endpoint.
The fields that are supplied in the replication document are `source`,
`target`,
`continuous`,
`create_target`,
`doc_ids`,
`filter`,
`proxy`,
`query_params`,
and`use_checkpoints`.
These fields are described in the [Replication document format](#replication-document-format).

Optionally,
replication documents have a user-defined `_id`.

The names of the source and target databases do not have to be the same.

>	**Note**: All design documents and `_local` documents added to the `/_replicator` database are ignored.

### Creating a replication

To start a replication,
add a [replication document](#replication-document-format) to the `_replicator` database.

_Example instructions for using HTTP to create a replication document:_

```http
PUT /_replicator/replication-doc HTTP/1.1
Content-Type: application/json
```
{:codeblock}

_Example instructions for using the command line to create a replication document:_

```sh
curl -X PUT https://$ACCOUNT.cloudant.com/_replicator/replication-doc -H 'Content-Type: application/json' -d @replication-document.json
#assuming replication-document.json is a json file with valid replication information.
```
{:codeblock}

_Example replication document:_

```json
{
	"source": "https://$ACCOUNT1:$PASSWORD1@$ACCOUNT1.cloudant.com/$DATABASE1",
	"target": "https://$ACCOUNT2:$PASSWORD2@$ACCOUNT2.cloudant.com/$DATABASE2",
	"create_target": true,
	"continuous": true
}
```
{:codeblock}

### (Optional) Creating a replication to two Bluemix environments

You can replicate a Cloudant database to multiple Bluemix environments.
When you set up the replication job for each environment,
the source database and target database names you provide must use the following format:

```http
https://$ACCOUNT:$PASSWORD@$REMOTE_USERNAME.cloudant.com/$DATABASE_NAME
```
{:codeblock}

You create the database within Bluemix by using the name: `$DATABASE_NAME`,
and add it to the URL format.
Do not copy the `URL` field from the `VCAP_SERVICES` environment variable.

### Monitoring a replication

To monitor replicators currently in process,
make a `GET` request to `https://$ACCOUNT.cloudant.com/_active_tasks`.
This returns any active tasks,
including replications.
To filter for replications,
look for documents with `"type": "replication"`.

If you monitor the `_active_tasks` and find that the state of a replication is not changing,
you might have a 'stalled' replication.
If you are sure that the replication stalled,
contact Cloudant support for assistance.

For more information,
see [Active tasks](active_tasks.html).

_Example instructions for using HTTP to monitor a replication:_

```http
GET /_active_tasks HTTP/1.1
```
{:codeblock}

_Example instructions for using the command line to monitor a replication:_

```http
curl https://$ACCOUNT.cloudant.com/_active_tasks
```
{:codeblock}

<!--

_Example instructions for  using Javascript to monitor a replication:_

```javascript
var nano = require('nano');
var account = nano("https://"+$ACCOUNT+":"+$PASSWORD+"@"+$ACCOUNT+".cloudant.com");

account.request(
	{ path: '_active_tasks' },
	function (err, body, headers) {
		if (!err) {
			console.log( body.filter( function (task) {
						return (task.type === 'replication');
					} ) ); 
		}
	}
);
```
{:codeblock}

-->

_Example response (abbreviated) after an active task request, including continuous replication:_

```json
[
	{
		"user": null,
		"updated_on": 1363274088,
		"type": "replication",
		"target": "https://$USERNAME2:$PASSWORD2@$ACCOUNT2.cloudant.com/user-3dg...imy/",
		"docs_read": 0,
		"doc_write_failures": 0,
		"doc_id": "tsm-admin__to__user-3dg...imy",
		"continuous": true,
		"checkpointed_source_seq": "403-g1AAA...SStc",
		"changes_pending": 134,
		"pid": "<0.1781.4101>",
		"node": "dbcore@db11.julep.cloudant.net",
		"docs_written": 0,
		"missing_revisions_found": 0,
		"replication_id": "d0cdbfee50a80fd43e83a9f62ea650ad+continuous",
		"revisions_checked": 0,
		"source": "https://$USERNAME1:$PASSWORD1@$ACCOUNT1.cloudant.com/tsm-admin/",
		"source_seq": "537-g1A...LVQ",
		"started_on": 1363274083
	}
]
```
{:codeblock}

_Example response after an active task request, including single replication:_

```json
[
	{
		"pid": "<0.1303.0>",
		"replication_id": "e42a443f5d08375c8c7a1c3af60518fb+create_target",
		"checkpointed_source_seq": 17333,
		"continuous": false,
		"doc_write_failures": 0,
		"docs_read": 17833,
		"docs_written": 17833,
		"missing_revisions_found": 17833,
		"progress": 3,
		"revisions_checked": 17833,
		"source": "http://$ACCOUNT.cloudant.com/$DATABASE/",
		"source_seq": 551202,
		"started_on": 1316229471,
		"target": "test_db",
		"type": "replication",
		"updated_on": 1316230082
	}
]
```
{:codeblock}

<div id="delete"></div>
<div id="cancelling-a-replication"></div>

### Canceling a replication

To cancel a replication,
[delete its replication document](document.html#delete) from the `_replicator` database.

If the replication is in an [`error` state](advanced_replication.html#replication-status),
the replicator makes repeated attempts to achieve a successful replication.
A consequence is that the replication document is updated with each attempt.
This also changes the document revision value.
Therefore,
get the revision value immediately before you delete the document,
otherwise you might get an [HTTP 409 "document update conflict"](http.html#409) response.

_Example instructions for using HTTP to delete a replication document:_

```http
DELETE /_replicator/replication-doc?rev=1-... HTTP/1.1
```
{:codeblock}

_Example instructions for deleting a replication document, the command line:_

```sh
curl -X DELETE https://$ACCOUNT.cloudant.com/_replicator/replication-doc?rev=1-...
```
{:codeblock}

## The `/_replicate` endpoint

You can use this endpoint to request,
configure,
or stop,
a replication operation.

You do this by sending a `POST` request directly to the `/_replicate` endpoint.
The `POST` contains a JSON document that describes the wanted replication.

-	**Method**: `POST`
-	**Path**: `/_replicate`
-	**Request**: Replication specification
-	**Response**: TBD
-	**Roles**: `_admin`

The specification of the replication request is controlled through the JSON content of the request.
The JSON document must contain fields that define the source,
target,
and other options.

The fields of the JSON request are as follows:

Field           | Purpose                                                     | Optional
----------------|-------------------------------------------------------------|---------
`cancel`        | Cancels the replication.                                    | Yes
`continuous`    | Configure the replication to be continuous.                 | Yes
`create_target` | Creates the target database.                                | Yes
`doc_ids`       | Array of document IDs to be synchronized.                   | Yes
`proxy`         | Address of a proxy server through which replication occurs. | Yes
`source`        | Source database URL, including user name and password.      | No
`target`        | Target database URL, including user name and password.      | No

>	**Note**: It is preferable to use the [Replicator database](#the-_replicator-database) to manage replication.
	Details of why are provided [here](#avoiding-the-_replicate-endpoint).

_Example instructions for using HTTP to start a replication through the `_replicate` endpoint:_

```http
POST /_replicate HTTP/1.1
Content-Type: application/json
```
{:codeblock}

_Example instructions for using the command line to start a replication through the `_replicate` endpoint:_

```sh 
curl -H 'Content-Type: application/json' -X POST "https://$ACCOUNT.cloudant.com/_replicate" -d @replication-doc.json
# with the file replication-doc.json containing the required replication information.
```
{:codeblock}

_Example JSON document that describes the required replication:_

```json
{
	"source": "http://$ACCOUNT:$PASSWORD@username.cloudant.com/example-database",
	"target": "http://$ACCOUNT2:$PASSWORD2@example.org/example-target-database"
}
```
{:codeblock}

### Return Codes

Code  | Description
------|------------
`200` | Replication request successfully completed.
`202` | Continuous replication request has been accepted.
`404` | Either the source or target database was not found.
`500` | JSON specification was invalid.

### Avoiding the `/_replicate` endpoint

>   **Note**: Use the [`_replicator` database](#replicator-database) in preference to the `/_replicate` endpoint.

A significant reason is that if there was a problem during replication,
such as a stall,
timeout,
or application crash,
then a replication that is defined within the `_replicator` database is automatically restarted by the system.

If you defined a replication by sending a request to the `/_replicate` endpoint,
it cannot be restarted by the system if a problem occurs because the replication request does not persist.

In addition,
replications that are defined in the `_replicator` database are easier to [monitor](advanced_replication.html#replication-status).

## Replication Operation

The aim of replication is that at the end of the process,
all active documents in the source database are also in the destination or 'target' database,
_and_ that all documents that are deleted from the source databases are also
deleted from the destination database (if they existed there).

Replication has two forms: push or pull replication:

-	*Push replication* is where the source is a local database,
	and the destination is a remote database.
-	*Pull replication* is where the source is a remote database instance,
	and the destination is the local database.

Pull replication is helpful if your source database has a permanent IP address,
and your destination database is local and has a dynamically assigned IP address,
for example, obtained through DHCP.
Pull replication is especially appropriate if you are replicating to a mobile or other device from a central server.

In all cases,
the requested databases in the source and target specification must exist.
If they do not,
an error is returned within the JSON object.

_Example request to replicate between a database on the source server `example.com`,
and a target database on Cloudant:_

```http
POST /_replicate
Content-Type: application/json
Accept: application/json

{
	"source" : "http://$USERNAME1:$PASSWORD1@example.com/db",
	"target" : "http://$USERNAME2:$PASSWORD2@$ACCOUNT2.cloudant.com/db",
}
```
{:codeblock}

_Example error response if one of the requested databases for a replication does not exist:_

```json
{
	"error" : "db_not_found",
	"reason" : "could not open http://$ACCOUNT.cloudant.com/ol1ka/"
}
```
{:codeblock}

## Creating a target database during replication

If your user credentials allow it,
you can create the target database during replication by adding the `create_target` field to the request object.

The `create_target` field is not destructive.
If the database exists,
the replication proceeds as normal.

_Example request to create a target database and replicate onto it:_

```http
POST http://$ACCOUNT.cloudant.com/_replicate
Content-Type: application/json
Accept: application/json

{
	"create_target" : true
	"source" : "http://$USERNAME:$PASSWORD@example.com/db",
	"target" : "http://$USERNAME2:$PASSWORD2@$ACCOUNT.cloudant.com/db",
}
```
{:codeblock}

## Canceling replication

A replication that is triggered by `POST`ing to `/_replicate` can be canceled
by `POST`ing the exact same JSON object but with the additional `cancel` property set to `true`.

>	**Note**: If a replication is canceled,
the request that initiated the replication fails with [error 500 (shutdown)](http.html#500).

The replication ID can be obtained from the original replication request if it is a continuous replication.
Alternatively,
the replication ID can be obtained from [`/_active_tasks`](active_tasks.html).

_Example of using HTTP to cancel a replication:_

```http
POST /_replicate HTTP/1.1
Content-Type: application/json
```
{:codeblock}

_Example of using the command line to cancel a replication:_

```sh
curl -H 'Content-Type: application/json' -X POST 'https://$ACCOUNT.cloudant.com/_replicate HTTP/1.1' -d @replication-doc.json
# the file replication-doc.json must be supplied.
```
{:codeblock}

_Example JSON document that describes the replication to be canceled:_

```json
{
	"source": "https://$USERNAME:$PASSWORD@$ACCOUNT.cloudant.com/example-database",
	"target": "https://$USERNAME2:$PASSWORD2@example.org/example-database",
	"cancel": true
}
```
{:codeblock}

## Single Replication

Replication of a database means that the two databases,
the 'source' and the 'target',
are synchronized.
By default,
the replication process occurs one time,
and synchronizes the two databases together.

The response to a request for a single replication is a JSON structure
containing the success or failure status of the synchronization process.
The response also contains statistics about the process.

Field             | Purpose
------------------|--------
`history`         | An array containing the replication history.
`ok`              | Replication status.
`session_id`      | Unique session ID.
`source_last_seq` | The last sequence number read from source database.

The `history` array contains the following information:

Field                | Purpose
---------------------|--------
`doc_write_failures` | Number of document write failures.
`docs_read`          | Number of documents read.
`docs_written`       | Number of documents written to target.
`end_last_seq`       | Last sequence number in changes stream.
`end_time`           | Date/Time replication operation completed.
`missing_checked`    | Number of missing documents checked.
`missing_found`      | Number of missing documents found.
`recorded_seq`       | Last recorded sequence number.
`session_id`         | Session ID for this replication operation.
`start_last_seq`     | First sequence number in changes stream.
`start_time`         | Date/Time replication operation started.

_Example instructions for using HTTP to request a single replication:_

```http
POST /_replicate HTTP/1.1
Content-Type: application/json
Accept: application/json
```
{:codeblock}

_Example instructions for using the command line to request a single replication:_

```sh
curl -H 'Content-Type: application/json' -X POST 'https://$ACCOUNT.cloudant.com/_replicate HTTP/1.1' -d @replication-doc.json
# the file replication-doc.json must be supplied.
```
{:codeblock}

_Example JSON document that describes a single replication between the source database `recipes` and the target database `recipes2`:_

```json
{
	"source" : "http://$USERNAME:$PASSWORD@$ACCOUNT.cloudant.com/recipes",
	"target" : "http://$USERNAME2:$PASSWORD2@$ACCOUNT2.cloudant.com/recipes2"
}
```
{:codeblock}

_Example response that follows a request for a single replication:_

```json
{
	"ok" : true,
	"history" : [
		{
			"docs_read" : 1000,
			"session_id" : "52c2370f5027043d286daca4de247db0",
			"recorded_seq" : 1000,
			"end_last_seq" : 1000,
			"doc_write_failures" : 0,
			"start_time" : "Thu, 28 Oct 2010 10:24:13 GMT",
			"start_last_seq" : 0,
			"end_time" : "Thu, 28 Oct 2010 10:24:14 GMT",
			"missing_checked" : 0,
			"docs_written" : 1000,
			"missing_found" : 1000
		}
	],
	"session_id" : "52c2370f5027043d286daca4de247db0",
	"source_last_seq" : 1000
}
```
{:codeblock}

## Continuous Replication

By default,
the synchronization of a database during replication happens one time when the replicate request is made.
To ensure that replication from the source database to the target database takes place continually,
set the `continuous` field of the JSON object within the request to `true`.

With continuous replication,
changes in the source database are replicated to the target database forever,
until you specifically cancel the replication.

Changes are replicated between the two databases
while a network connection is available between the two instances.

When in operation,
the replication process does not stop when it finishes processing all current updates.
Instead,
the replication process continues to wait for further updates to the source database,
and applies them to the target.

>	**Note**: Continuous replication forces checks to be made continuously on the source database.
This results in an increasing number of database accesses,
even if the source database content did not change.
Database accesses are counted as part of the work that is done within a multi-tenant database configuration.

_Example instructions for using HTTP to request continuous replication:_

```http
POST /_replicate HTTP/1.1
Content-Type: application/json
Accept: application/json
```
{:codeblock}

_Example instructions for using the command line to request continuous replication:_

```sh
curl -H 'Content-Type: application/json' -X POST 'https://$ACCOUNT.cloudant.com/_replicate HTTP/1.1' -d @replication-doc.json
# the file replication-doc.json must be supplied.
```
{:codeblock}

_Example JSON document that describes continuous replication between the source database `recipes` and the target database `recipes2`:_

```json
{
	"source" : "http://$USERNAME:$PASSWORD@$ACCOUNT.cloudant.com/recipes",
	"target" : "http://$USERNAME2:$PASSWORD2@$ACCOUNT2.cloudant.com/recipes2", 
	"continuous": true
}
```
{:codeblock}

### Canceling Continuous Replication

Cancel continuous replication by including the `cancel` field in the JSON request object,
and setting the value to `true`.

>	**Note**: For the cancellation request to succeed,
the structure of the request must be identical to the original request.
In particular,
if you requested continuous replication,
the cancellation request must also contain the `continuous` field.

Requesting cancellation of a replication that does not exist results in a [404 error](http.html#404).

_Example replication request to create the target database if it does not exist, and to replicate continuously:_

```json
{
	"source" : "http://$USERNAME:$PASSWORD@example.com/db",
	"target" : "http://$USERNAME2:$PASSWORD2@$ACCOUNT.cloudant.com/db",
	"create_target" : true,
	"continuous" : true
}
```
{:codeblock}

_Example request to cancel the replication, providing matching fields to the original request:_

```json
{
	"cancel" : true,
	"continuous" : true,
	"create_target" : true,
	"source" : "http://$USERNAME:$PASSWORD@example.com/db",
	"target" : "http://$USERNAME2:$PASSWORD2@$ACCOUNT.cloudant.com/db"
}
```
{:codeblock}

## Example replication sequence

The following examples go through all the steps of creating a replication task,
then canceling it.

_Example of using HTTP to send a request to start a replication:_

```http
POST /_replicate HTTP/1.1
Content-Type: application/json
```
{:codeblock}

_Example of using the command line to send a request to start a replication:_

```sh
curl -H 'Content-Type: application/json' -X POST 'http://$ACCOUNT.cloudant.com/_replicate' -d @replication-doc.json
# the file replication-doc.json describes the intended replication.
```
{:codeblock}

_Example JSON document that describes the intended replication:_

```json
{
	"source": "https://$USERNAME:$PASSWORD@example.com/foo", 
	"target": "https://$USERNAME2:$PASSWORD2@$ACCOUNT.cloudant.com/bar", 
	"create_target": true, 
	"continuous": true
}
```
{:codeblock}

_Example response after the replication starts successfully:_

```json
{
	"ok": true,
	"_local_id": "0a81b645497e6270611ec3419767a584+continuous+create_target"
}
```
{:codeblock}

_Example of using HTTP to send a request to cancel a replication:_

```http
POST /_replicate HTTP/1.1
Content-Type: application/json
```
{:codeblock}

_Example of using the command line to send a request to cancel a replication:_

```sh
curl -H 'Content-Type: application/json' -X POST http://$ACCOUNT.cloudant.com/_replicate -d @replication-doc.json
# where the file replication-doc.json specifies the replication task to be canceled.
```
{:codeblock}

_Example document that specifies the replication to be canceled:_

```json
{
	"replication_id": "0a81b645497e6270611ec3419767a584+continuous+create_target",
	"cancel": true
}
```
{:codeblock}

_Example response after successfully canceling the replication, indicated by the `"ok":true` content:_

```json
{
	"ok": true,
	"_local_id": "0a81b645497e6270611ec3419767a584+continuous+create_target"
}
```
{:codeblock}

## Replication database maintenance

A replication database must be looked after like any other database.
Without regular database maintenance,
you might accumulate invalid documents that were caused by interruptions to the replication process.
Having many invalid documents can result in an excess load on your cluster
when the replicator process is restarted by Cloudant operations.

The main action that you can do to maintain a replication database is to remove old documents.
This can be done by determining the age of documents,
and [deleting them](document.html#delete) if they are no longer needed.
