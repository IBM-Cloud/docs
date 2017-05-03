---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-20"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Acrolinx: 2017-04-20 -->

# Replication

Data can be copied from one database to another in the same Cloudant account,
across accounts and across data centers.
{:shortdesc}

Data can even be replicated to and from a Cloudant account and a mobile device by
using [Cloudant Sync ![External link icon](../images/launch-glyph.svg "External link icon")](https://cloudant.com/product/cloudant-features/sync/){:new_window}
or [PouchDB ![External link icon](../images/launch-glyph.svg "External link icon")](http://pouchdb.com/){:new_window}.
Replication can run in one direction or in both directions,
as a 'single shot' or continuous operation,
and can be finely tuned by using parameters.

Cloudant’s replication protocol is compatible with a range of other databases and libraries,
making it a great fit for Internet of Things (IoT) and mobile applications.

This guide introduces Cloudant’s replication functions,
discusses common use-cases,
and shows how to make your application replicate successfully.

## What is Replication?

Cloudant is a distributed JSON data store with an HTTP API.
Cloudant can be run as a service on multiple clouds,
or in your server rack.
Documents are stored in databases and can grow to any size as Cloudant shards its data across many nodes.
Replication is the copying of data from a source database to a target database.
The source and target databases do not need to be on the same Cloudant account,
or even in the same data center.

![replication](../images/replication_guide_1.png)

Replication is complete when the most recent version of each document in the source transfers to the destination database.
Transfers include new documents,
updates to existing documents,
and deletions.
Only the most recent version of a document remains after replication;
older versions are omitted.

The source database remains unaltered by replication,
apart from checkpoint data that is written to it to allow partial replications to resume from the last known position.
Any pre-existing data in the destination database remains.

<div id="how-do-i-initiate-replication-via-the-dashboard-"></div>

## How to start replication by using the Dashboard

The Cloudant Dashboard provides a convenient user-interface to trigger replication.
Open the Replication tab of your Cloudant Dashboard and click the `New Replication` action button.
Complete the simple form:

![replication2](../images/replication_guide_2.png)

Using the form,
define the source and target databases,
then click "`Replicate`".

![replication3](../images/replication_guide_3.png)

The status of each replication task can be seen in the "`All Replications`" section of the Dashboard.
Each job changes state from "`Triggered`" to "`Complete`" as it progresses.

![replication4](../images/replication_guide_4.png)

<div id="how-do-i-run-replication-across-different-cloudant-accounts-"></div>

## How to run replication across different Cloudant accounts

The source and target of a replication are URLs of Cloudant databases,
as shown in the following example.

_Example of defining source and target URLs for replication:_

```json
{
    "source": "https://myfirstaccount.cloudant.com/a",
    "target": "https://mysecondaccount.cloudant.com/b"
}
```
{:codeblock}

The source and target do not need to be on the same account.
The source and target database names do not need to match.
You must be authorized to access both the source and target,
and you must be authorized to write to the target.

<div id="do-i-run-replication-on-the-source-or-the-destination-"></div>

## Is replication run on the source or the destination?

Replication can be started at either the source or the destination end.
This choice means that you can decide whether account A is pushing data to account B,
or account B is pulling data from account A.
In some cases,
it might not be possible to run replication in either configuration,
for example when one account is behind a firewall.
Replication happens over HTTP or HTTPS and so no non-standard ports need be opened.
The decision as to which device starts replication is yours.

<div id="how-do-i-initiate-replication-via-the-cloudant-api-"></div>

## How to start replication by using the Cloudant API

Every Cloudant account has a special database that is called `_replicator`,
into which replication jobs can be inserted.
Add a document into the `_replicator` database to start replication.
The document describes the wanted replication,
and contains the following fields:

Field           | Purpose
----------------|--------
`_id`           | Supplying an `_id` field is optional, but can be useful to identify replication tasks. Cloudant generates a value for you if you do not supply one.
`source`        | The URL of the source Cloudant database, including login credentials.
`target`        | The URL of the destination Cloudant database, including login credentials.
`create_target` | (Optional) Determine whether to create the destination database if it doesn't exist yet.

_Example of using HTTP to start a replication job:_

```http
POST /_replicator HTTP/1.1
Content-Type: application/json
Host: myaccount.cloudant.com
Authorization: ...
```
{:codeblock}

_Example of using the command line to start a replication job:_

```sh
curl -X POST \
    -H 'Content-type: application/json' \
    'https://myuser:mypassword@myaccount.cloudant.com/_replicator' \
    -d '@replication.json'
```
{:codeblock}

_Example JSON document that describes the wanted replication:_

```json
{
    "_id": "weekly_backup",
    "source": "https://username:password@myaccount1.cloudant.com/source",
    "target": "https://username:password@myaccount2.cloudant.com/destination",
    "create_target": true
}
```
{:codeblock}

## How does replication affect the list of changes?

You can get a list of changes made to a document by using
the [`_changes` endpoint](../api/database.html#get-changes).
However,
the distributed nature of Cloudant databases
means that the response that is provided by the `_changes` feed
cannot be a simple list of changes that occurred after a particular date and time.

The [CAP Theorem](cap_theorem.html) discussion makes it clear that
Cloudant uses an 'eventually consistent' model.
This model means that if you asked two different replicas of a database for a document,
at the same time,
you might get different results if one of the database copies is still waiting to finish replication.
_Eventually_,
the database copies complete their replication,
so that all the changes to a document are present in each copy.

This 'eventual consistency' model has two characteristics that affect a list of changes:

1.  A change that affects a document almost certainly takes place at different times in different copies of the database.
2.  The order in which changes affect documents might differ between different copies of the database,
    depending on when and from where the replication took place.

A consequence of the first characteristic is that,
when you ask for a list of changes,
it is meaningless to ask for a list of changes after a specific point in time.
The reason is that the list of changes might be supplied by a different database copy,
which resulted in document updates at different times.
However,
it _is_ meaningful to ask for a list of changes after a specific change,
which is specified by using a sequence identifier.

An extra consequence of the first characteristic is that
it might be necessary to 'look back' at preceding changes to agree on the list of changes.
In other words,
to get a list of changes,
you start from the most recent change that the database copies agree on.
The point of agreement between database copies is identified within
Cloudant by using the [checkpoint](#checkpoints) mechanism
that enables replication between database copies to be synchronized.

Finally,
a consequence of the second characteristic is that the individual changes that appear in the
list of changes might be presented in a different order
in subsequent requests that are answered by a different database copy.
In other words,
an initial list of changes might report changes `A`,
`B`,
then `C` in that order.
But a subsequent list of changes might report changes `C`,
`A`,
then `B` in that order.
All the changes are listed,
but in a different order.
This difference is because the sequence of changes that are received during replication
might vary between two different copies of the database.

<div id="what-this-means-for-the-list-of-changes"></div>

### What 'eventual consistency' means for the list of changes

When you request a list of changes,
the response you get might vary depending on which database copy supplies the list.

If you use the `since` option to obtain a list of changes after a specific update sequence identifier,
you always get the list of changes after that update _and_ you might also get some changes from before that update.
The reason is that the database copy that responds to the list request must ensure that it
lists the changes,
consistent with all the replicas.
To achieve that consistency,
the database copy might have to start the list of changes from the point
when all the copies agreed.
This point is identified by using checkpoints.

Therefore,
an application that uses the `_changes` feed must
be ['idempotent' ![External link icon](../images/launch-glyph.svg "External link icon")](http://www.eaipatterns.com/IdempotentReceiver.html){:new_window}.
Idempotency means that the application must be able safely to receive the same data multiple times,
and potentially if a different order for repeated requests.

## Checkpoints

Internally,
the replication process writes its state in "checkpoint" documents that are stored
in both the source and destination databases.
Checkpoints allow a replication task to be resumed from where it stopped,
without having to start from the beginning.
Checkpoint creation can be prevented by supplying the
[`"use_checkpoints": false`](../api/replication.html#checkpoints) option when you request replication.
It is helpful to leave the feature on if your replication is to resume efficiently from its last known position.

## Permissions

Admin access is necessary to insert a document into the `_replicator` database.
The login credentials that are supplied in the source and target parameters do not require full admin rights.
It is sufficient if the credentials are able to:

-   Write documents at the destination end.
-   Write checkpoint documents at both ends.

Cloudant has a special `_replicator` user permission.
This permission allows checkpoint documents to be created,
but does not allow the creation of ordinary documents in a database.
In general,
[create API keys](../api/authorization.html#creating-api-keys) that have:

-   `_reader` and `_replicator` access at the source side.
-   `_reader` and `_writer` access at the destination side.

API keys can be created and configured within the Cloudant Dashboard,
on a per-database basis.

![replication](../images/replication_guide_5.png)

They can also be created [programmatically](../api/authorization.html#creating-api-keys) by using the Cloudant API.

## Two-way replication

Data can be copied in both directions in a process that is known as two-way replication or synchronization.
You enable this synchronization by setting up two separate replication processes,
one taking the data from A to B,
the other taking data from B to A.
Both replication processes work independently,
with data moved seamlessly in both directions.

![replication6](../images/replication_guide_6.png)

## Continuous replication

So far,
the discussion deals only with one-shot replication,
which finishes when all of the source data is written to the target database.
With continuous replication,
data flows continuously.
All subsequent changes to the source database are transmitted to the target database in real time.

Continuous replication is triggered by clicking the
"`Make this replication continuous`" check box when you define a replication task in the Cloudant Dashboard,
or by setting the ["`continuous`"](../api/replication.html#checkpoints) flag in the Cloudant API.

Two-way replication can be made continuous in one or both of the directions,
by setting the "`continuous`" flag.

_Example of using HTTP to start a continuous replication:_

```http
POST /_replicator HTTP/1.1
Content-Type: application/json
Host: myaccount.cloudant.com
Authorization: ...
```
{:codeblock}

_Example of using the command line to start a continuous replication:_

```sh
curl -X POST \
    -H "Content-type: application/json" \
    https://myuser:mypassword@myaccount.cloudant.com/_replicator \
    -d @continuous-replication.json
```
{:codeblock}

_Example of a JSON document that defines a continuous replication:_

```json
{
    "_id": "weekly_continuous_backup",
    "source": "https://username:password@myaccount1.cloudant.com/source",
    "target": "https://username:password@myaccount2.cloudant.com/destination",
    "continuous": true
}
```
{:codeblock}

## Monitoring replication

You can check the status of Cloudant’s `_replicator` database at any time,
by using the Dashboard or the API.

If replication failed,
for example if the authentication credentials were invalid,
then the error state is recorded in the `_replicator` document.
In addition,
the Cloudant account's `/_active_tasks` endpoint can be used to see replication work as it progresses.
More details are available [here](../api/active_tasks.html).

_Example of using HTTP to monitor a replication process:_

```http
GET /_replicator/weekly_backup HTTP/1.1
HOST: myaccount.cloudant.com
Authorization: ...
```
{:codeblock}

_Example of using the command line to monitor a replication process:_

```sh
curl 'https://myaccount.cloudant.com/_replicator/weekly_backup'
```
{:codeblock}

_Example response to requesting the status of a replication:_

```json
{
    "_id": "weekly_backup",
    "_rev": "22-c57c18f7e761f1a76fa977caa03cd098",
    "source": "https://u:p@myaccount.cloudant.com/a",
    "create_target": false,
    "target": "https://u:p@myaccount.cloudant.com/b",
    "continuous": true,
    "_replication_state": "triggered",
    "_replication_state_time": "2014-12-01T15:19:01+00:00",
    "_replication_id": "4514b08cb4c2ded7da9ab04a87182ceb"
}
```
{:codeblock}

## Canceling replication

To stop an ongoing replication job,
delete the replication document from the `_replicator` database,
by using either the Dashboard or the API.

_Example of using HTTP to cancel a replication:_

```http
DELETE /_replicator/weekly_backup?rev=22-c57c18f7e761f1a76fa977caa03cd098 HTTP/1.1
Host: myaccount.cloudant.com
Authorization:
```
{:codeblock}

_Example of using the command line to cancel a replication:_

```sh
curl -X DELETE 'https://myaccount.cloudant.com/_replicator/weekly_backup?rev=22-c57c18f7e761f1a76fa977caa03cd098'
```
{:codeblock}

## Other replication use-cases

Replication isn’t just for Cloudant-to-Cloudant data transfer.
Cloudant’s replication protocol is compatible with other databases and libraries for various real-world applications.

### Apache CouchDB

[Apache CouchDB ![External link icon](../images/launch-glyph.svg "External link icon")](http://couchdb.apache.org/){:new_window} is an open source database
that can communicate with Cloudant,
and that requires minimal setup.
Applications include:

-   Backup: Replicate your data from Cloudant to your own CouchDB databases
    and take nightly snapshots of your data for archiving purposes.
    Send the data to a backup service such as
    [Amazon Glacier ![External link icon](../images/launch-glyph.svg "External link icon")](https://aws.amazon.com/glacier/){:new_window} for safe keeping.
-   Local-first data collection: Write your data to local Apache CouchDB first,
    then replicate it to Cloudant for long-term storage,
    aggregation,
    and analysis.

### PouchDB

[PouchDB ![External link icon](../images/launch-glyph.svg "External link icon")](http://pouchdb.com/){:new_window} is an open source,
in-browser database that allows data to be replicated in both directions between the browser and Cloudant.
Storing the data in a web browser on the client side allows web applications to function
even without an internet connection.
PouchDB can sync any changed data to and from Cloudant when an internet connection is present.
Setting up replication from the client side requires a few lines of JavaScript.

_Example JavaScript that uses PouchDB to enable replication:_

```javascript
var db = new PouchDB("myfirstdatabase");
var URL = "https://u:p@username.cloudant.com/my_database");
db.sync(URL, { live: true });
```
{:codeblock}

### CloudantSync

[CloudantSync ![External link icon](../images/launch-glyph.svg "External link icon")](https://cloudant.com/cloudant-sync-resources/){:new_window} is a set of libraries
for iOS and Android that allows data to be stored locally in a mobile device
and synced with Cloudant when mobile connectivity permits.
As with [PouchDB](#pouchdb),
setting up replication requires a few lines of code.

_Example JavaScript that uses CloudantSync to enable replication:_

```javascript
URI uri = new URI("https://u:p@username.cloudant.com/my_database");
Datastore ds = manager.openDatastore("my_datastore");
// Replicate from the local to remote database
Replicator replicator = ReplicatorFactory.oneway(ds, uri);
// Fire-and-forget (there are easy ways to monitor the state too)
replicator.start();
```
{:codeblock}

CloudantSync is used widely in mobile applications,
such as iPhone and Android games,
where the application's state is persisted to Cloudant by replication,
but the data is also available on the device for offline use.

## Filtered Replication

It is useful to be able to remove some data during the replication process,
when you replicate one database to another.
Examples include:

-   Removing all traces of deleted documents,
    making the target database smaller than the source.
-   Segregating data into smaller chunks,
    such as storing UK data in one database and US data in another.

<div id="replication-filter-function"></div>

### Replication filter functions

Cloudant’s filtered replication allows the definition of a JavaScript function that uses the return value
to determine whether each document in a database is to be filtered or not.
[Filter functions](../api/design_documents.html#filter-functions) are stored
in [design documents](../api/design_documents.html).

The following example is a filter function that allows only non-deleted documents to be replicated.

_Example filter function for replicating non-deleted documents:_

```javascript
function(doc, req) {
    if (doc._deleted) {
        return false;
    }
    return true;
}
```
{:codeblock}

When a replication job starts,
a filter function’s name is specified as a combination of the design document where it is stored,
and the filter function’s name.
You can also specify a `query_params` value.
This value is an object that contains properties that are passed to the
filter function in the `query` field of its second (`req`) argument.

_Example of using HTTP to start a filtered replication:_

```http
POST /_replicator HTTP/1.1
Content-Type: application/json
Host: myaccount.cloudant.com
Authorization: ...
```
{:codeblock}

_Example of using the command line to start a filtered replication:_

```sh
curl -X POST \
    -H "Content-type: application/json" \
    https://myuser:mypassword@myaccount.cloudant.com/_replicator \
    -d @filtered-replication.json
```
{:codeblock}

_Example of a JSON document that defines a filtered replication:_

```json
{
    "_id": "weekly_backup",
    "source": "https://username:password@myaccount1.cloudant.com/source",
    "target": "https://username:password@myaccount2.cloudant.com/destination",
    "filters": "mydesigndoc/myfilter",
    "query_params": {
        "foo": "bar",
        "baz": 5
    }
}
```
{:codeblock}

## Changes feed

Cloudant publishes the adds,
edits,
and deletes affecting a database through a single HTTP feed from
the [`_changes` endpoint](../api/database.html#get-changes).
This feed can be used by your application to trigger events.
You can access the feed by using HTTP or `curl`,
as shown in the examples.
Using the `feed=continuous` option means that the stream provides you with
every change that is necessary to get the most recent version of every document in the database.

_Example of using HTTP to query the changes feed:_

```http
GET /$db/_changes?feed=continuous HTTP/1.1
Host: myaccount.cloudant.com
Authorization: ...
```
{:codeblock}

_Example of using the command line to query the changes feed:_

```sh
curl "https://myaccount.cloudant.com/$db/_changes?feed=continuous"
```
{:codeblock}

The changes are described by using one line per change.
Each change consists of:

1.  A string that contains a sequence number (`seq`).
2.  A string that contains the ID of the document that was changed.
3.  An array of changes.

To see the document body itself,
append `&include_docs=true` to the curl command.

Each change is described by using the format that is shown in the following (abbreviated) example.

_Example `_changes` feed:_

```json
{
    "seq":"11-g1A...c1Q",
    "id":"6f8ab9fa52c117eb76240daa1a55827f",
    "changes":[
        {
          "rev":"1-619d7981d7027274a4b88810d318a7b1"
        }
    ]
}
```
{:codeblock}

<div id="changes-feed-since"></div>

To join the changes feed from a known position,
pass a [`since` argument](../api/database.html#the-since-argument) with the sequence number you want to start from.

_Example (abbreviated) of using HTTP to supply the `since` option to join a `_changes` feed at a known position:_

```http
GET /$db/_changes?feed=continuous&include_docs=true&since=11-g1A...c1Q HTTP/1.1
HOST: myaccount.cloudant.com
Authorization: ...
```
{:codeblock}

_Example (abbreviated) of using the command line to supply the `since` option to join a `_changes` feed at a known position,:_

```sh
curl "https://myaccount.cloudant.com/$db/_changes?feed=continuous&include_docs=true&since=11-g1A...c1Q"
```
{:codeblock}

<div id="changes-feed-since-now"></div>

To rejoin the changes feed from the current moment in time,
set `since=now`.

_Example of using HTTP to supply `since=now` to join a `_changes` feed at the current moment in time:_

```http
GET /$db/_changes?feed=continuous&include_docs=true&since=now HTTP/1.1
Host: myaccount.cloudant.com
Authorization: ...
```
{:codeblock}

_Example of using the command line to supply `since=now` to join a `_changes` feed at the current moment in time:_

```sh
curl "https://myaccount.cloudant.com/$db/_changes?feed=continuous&include_docs=true&since=now"
```
{:codeblock}

_Example of using JavaScript to supply `since=now` to join a `_changes` feed at the current moment in time:_

```javascript
var feed = db.follow({since: "now", include_docs: true})
feed.on('change', function (change) {
    console.log("change: ", change);
})
feed.follow();
```
{:codeblock}

Accessing the `_changes` data programmatically is straightforward.
For example,
use the [Cloudant Node.js library](../libraries/supported.html#node-js)
to follow changes with a few lines of code.

Example use cases might be:

-   Adding items to a message queue to trigger actions within your application,
    such as sending a customer email.
-   Update an in-memory database to record live counts of activity.
-   Writing data to a text file to push data into an SQL database.

<div id="changes-feed-filtering"></div>

The changes feed can be filtered with a filter function,
by using a similar technique to [filtering during replication](#filtered-replication).

_Example of using HTTP to filter the changes feed:_

```http
GET /$db/_changes?feed=continuous&include_docs=true&since=now&filter=mydesigndoc/myfilter HTTP/1.1
Host: myaccount.cloudant.com
Authorization: ...
```
{:codeblock}

_Example of using the command line to filter the changes feed:_

```sh
curl "https://myaccount.cloudant.com/$db/_changes?feed=continuous&include_docs=true&since=now&filters=mydesigndoc/myfilter"
```
{:codeblock}

>   **Note**: The ordering of documents within the `_changes` feed is not always the same.
    In other words, changes might not appear in strict time order.
    The reason is that data is returned from multiple Cloudant nodes,
    and eventual consistency rules apply.

## Replication Pitfalls

Several considerations apply when you use replication.

### Incorrect user permissions

For replication to proceed optimally when you replicate from database "a" to database "b",
the credentials that are supplied must have:

*   `_reader` and `_replicator` rights on database "a".
*   `_writer` rights on database "b".

API keys are generated in the Cloudant Dashboard or [through the API](../api/authorization.html#creating-api-keys).
Each key can be given individual rights that relate to a specific Cloudant database.
Cloudant must be able to write its checkpoint documents at the "read" end of replication,
otherwise no state is saved and replication cannot resume from where it stopped.
If the state is not saved,
it can lead to performance problems when replication of large data sets resumes.
The reason is that without checkpoints,
the replication process restarts from the beginning each time that it is resumed.

### Replication document is conflicted

Another consequence of setting user permissions incorrectly is that the `_replicator` document becomes conflicted.
The `_replicator` document records the current state of the replication process.
In an extreme case,
the document can become huge because it contains many unresolved conflicts.
Such a large document uses much of the available space and causes extra server load.

You can check the size of your `_replicator` database by sending a `GET` request to the `/_replicator` endpoint:

```http
GET https://myaccount.cloudant.com/_replicator
```
{:codeblock}

In the returned JSON,
look for the `disk_size` value.
If the value indicates a size of over 1 GB,
contact the [IBM Cloudant support team ![External link icon](../images/launch-glyph.svg "External link icon")](mailto:support@cloudant.com){:new_window} for further advice.

You can check an individual `_replicator` document for conflicts,
as shown in the following example:

```http
GET https://myaccount.cloudant.com/_replicator/<<docid>>?conflicts=true
```
{:codeblock}

<div id="resetting-replicator-database"></div>

If you want to cancel all replications and start with a new,
clean `_replicator` database,
delete then re-create the `replicator` database.

_Example of using HTTP to remove and re-create the `_replicator` database:_

```http
DELETE /_replicator HTTP/1.1
HOST: myaccount.cloudant.com
Authorization: ...

PUT /_replicator HTTP/1.1
HOST: myaccount.cloudant.com
Authorization: ...
```
{:codeblock}

_Example of using the command line to remove and re-create the `_replicator` database:_

```sh
curl -X DELETE 'https://myaccount.cloudant.com/_replicator'
curl -X PUT 'https://myaccount.cloudant.com/_replicator'
```
{:codeblock}

### Many simultaneous replications

It is easy to forget that you previously set-up replication between two databases,
and so create extra replication processes in error.
Each replication job is independent of the other,
so Cloudant does not prevent you from doing creating extra replication processes.
However, each replication task uses up system resources.

You can check your "active replications" in the Cloudant Dashboard
to ensure that there are no unwanted replication tasks in progress.
Delete any `_replicator` documents that are no longer needed.

## Tuning replication speed

By default,
Cloudant replication runs at an appropriate rate to get the data from the source to the target
without adversely affecting performance.
Choosing between replication rate and cluster performance for other tasks is a tradeoff.
Your use-case might require faster replication at the expense of other Cloudant services.
Alternatively,
you might require cluster performance to take priority,
with replication treated as a background process.

Advanced replication API options are [available](../api/advanced_replication.html),
which enable an increase or decrease in the amount of computing power that is used during replication.
For example:

*   If your documents contain attachments,
    you might want to consider reducing the batch_size and increasing the worker_processes,
    to accommodate larger documents in smaller batches.
*   If you have many tiny documents,
    then you might consider increasing the
    [`worker_process`](../api/advanced_replication.html#performance-related-options) and
    [`http_connections`](../api/advanced_replication.html#performance-related-options) values.
*   If you want to run replication with minimal impact,
    setting `worker_processes` and `http_connections` to 1 might be appropriate.

For further assistance about the best configuration for your use-case,
contact the [IBM Cloudant support team ![External link icon](../images/launch-glyph.svg "External link icon")](mailto:support@cloudant.com){:new_window}.
