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

# Document Versioning and MVCC

[Multi-version concurrency control (MVCC) ![External link icon](../images/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/Multiversion_concurrency_control){:new_window}
is how Cloudant databases ensure that all of the nodes in a database's cluster contain
only the [newest version](../api/document.html) of a document.
{:shortdesc}

Since Cloudant databases are [eventually consistent](cap_theorem.html),
this is necessary to prevent inconsistencies arising between nodes
as a result of synchronizing between outdated documents.

Multi-Version Concurrency Control (MVCC) enables concurrent read and write access to a Cloudant database.
MVCC is a form of [optimistic concurrency ![External link icon](../images/launch-glyph.svg "External link icon")](http://en.wikipedia.org/wiki/Optimistic_concurrency_control){:new_window}.
It makes both read and write operations on Cloudant databases faster because
there is no need for database locking on either read or write operations.
MVCC also enables synchronization between Cloudant database nodes.

## Revisions

Every document in a Cloudant database has a `_rev` field indicating its revision number.

A revision number is added to your documents by the server when you insert or modify them.
The number is included in the server response when you make changes or read a document.
The `_rev` value is constructed using a combination of a simple counter and a hash of the document.

The two main uses of the revision number are to help:

1.  Determine what documents must be replicated between servers.
2.  Confirm that a client is trying to modify the latest version of a document.

You must specify the previous `_rev` when [updating a document](../api/document.html#update)
or else your request fails and returns a [409 error](../api/http.html#409).

>   **Note**: `_rev` should not be used to build a version control system.
    The reason is that it is an internal value used by the server.
    In addition,
    older revisions of a document are transient,
    and therefore removed regularly.

You can query a particular revision using its `_rev`,
however,
older revisions are regularly deleted by a process called
[compaction ![External link icon](../images/launch-glyph.svg "External link icon")](http://en.wikipedia.org/wiki/Data_compaction){:new_window}.
A consequence of compaction is that
you cannot rely on a successful response when querying a particular document revision
using its `_rev` in order to obtain a history of revisions to your document.
If you need a version history of your documents,
a solution is to [create a new document](../api/document.html#documentCreate) for each revision.

## Distributed Databases and Conflicts

Distributed databases work without a constant connection to the main database on Cloudant,
which is itself distributed,
so updates based on the same previous version can still be in conflict.

To find conflicts,
add the query parameter [`conflicts=true`](../api/database.html#get-changes) when retrieving a document.
The response contains a `_conflicts` array with all conflicting revisions.

To find conflicts for multiple documents in a database,
write a view.

The following map function is is an example that emits all conflicting revisions for every document that has a conflict.

_Example of a map function to find documents with a conflict:_

```javascript
function (doc) {
    if (doc._conflicts) {
        emit(null, [doc._rev].concat(doc._conflicts));
    }
}
```
{:codeblock}

You could regularly query this view and resolve conflicts as needed,
or query the view after each replication.

## How to resolve conflicts

Once you've found a conflict,
you can resolve it in 4 steps.

1.  [Get](#get-conflicting-revisions) the conflicting revisions.
2.  [Merge](#merge-the-changes) them in your application or ask the user what he wants to do.
3.  [Upload](#upload-the-new-revision) the new revision.
4.  [Delete](#delete-old-revisions) old revisions.

Let's consider an example of how this can be done.
Suppose you have a database of products for an online shop.
The first version of a document might look like the following example:

```json
{
    "_id": "74b2be56045bed0c8c9d24b939000dbe",
    "_rev": "1-7438df87b632b312c53a08361a7c3299",
    "name": "Samsung Galaxy S4",
    "description": "",
    "price": 650
}
```
{:codeblock}

As the document doesn't have a description yet,
someone might add one:

_Second version of the document, created by adding a description:_

```json
{
    "_id": "74b2be56045bed0c8c9d24b939000dbe",
    "_rev": "2-61ae00e029d4f5edd2981841243ded13",
    "name": "Samsung Galaxy S4",
    "description": "Latest smartphone from Samsung",
    "price": 650
}
```
{:codeblock}

At the same time, someone else - working with a replicated database - reduces the price:

_A different revision, conflicting with the previous one, because of different `price` value:_

```json
{
    "_id": "74b2be56045bed0c8c9d24b939000dbe",
    "_rev": "2-f796915a291b37254f6df8f6f3389121",
    "name": "Samsung Galaxy S4",
    "description": "",
    "price": 600
}
```
{:codeblock}

The two databases are then replicated.
The difference in document versions results in a conflict.

### Get conflicting revisions

You identify documents with with conflicts by using the `conflicts=true` option.

_Example of finding documents with conflicts:_

```http
http://$ACCOUNT.cloudant.com/products/$_ID?conflicts=true
```
{:codeblock}

_Example response showing conflicting revisions affecting documents:_

```json
{
    "_id":"74b2be56045bed0c8c9d24b939000dbe",
    "_rev":"2-f796915a291b37254f6df8f6f3389121",
    "name":"Samsung Galaxy S4",
    "description":"",
    "price":600,
    "_conflicts":["2-61ae00e029d4f5edd2981841243ded13"]
}
```
{:codeblock}

The version with the changed price has been chosen arbitrarily as the latest version of the document
and the conflict with another version is noted by providing the ID of that other version in the `_conflicts` array.
In most cases this array has only one element,
but there might be many conflicting revisions.

### Merge the changes

To compare the revisions to see what has been changed,
your application gets all of the versions from the database.

_Example commands to retrieve all versions of a document from the database:_

```http
http://$ACCOUNT.cloudant.com/products/$_ID
http://$ACCOUNT.cloudant.com/products/$_ID?rev=2-61ae00e029d4f5edd2981841243ded13
http://$ACCOUNT.cloudant.com/products/$_ID?rev=1-7438df87b632b312c53a08361a7c3299
```
{:codeblock}

Since the conflicting changes are for different fields of the document,
it is easy to merge them.

For more complex conflicts,
other resolution strategies might be required:

*   Time based: use the first or last edit.
*   User intervention: report conflicts to users and let them decide on the best resolution.
*   Sophisticated algorithms: for example, 3-way merges of text fields.

For a practical example of how to implement a merge of changes,
see [this project with sample code ![External link icon](../images/launch-glyph.svg "External link icon")](https://github.com/glynnbird/deconflict){:new_window}.

### Upload the new revision

The next step is to create a document that resolves the conflicts,
and update the database with it.

_An example document that merges changes from the two conflicting revisions:_

```json
{
    "_id": "74b2be56045bed0c8c9d24b939000dbe",
    "_rev": "3-daaecd7213301a1ad5493186d6916755",
    "name": "Samsung Galaxy S4",
    "description": "Latest smartphone from Samsung",
    "price": 600
}
```
{:codeblock}

### Delete old revisions

Finally,
you delete the old revisions by sending a `DELETE` request to the URLs with the revision we want to delete.

_Example request to delete an old document revision, using HTTP:_

```http
DELETE https://$ACCOUNT.cloudant.com/products/$_ID?rev=2-61ae00e029d4f5edd2981841243ded13
```
{:codeblock}

_Example request to delete an old document revision, using the command line:_

```sh
curl "https://$ACCOUNT.cloudant.com/products/$_ID?rev=2-f796915a291b37254f6df8f6f3389121" -X DELETE
```
{:codeblock}

At this point,
conflicts affecting the document are resolved.
You can verify this by `GET`ting the document again with the `conflicts` parameter set to `true`.
