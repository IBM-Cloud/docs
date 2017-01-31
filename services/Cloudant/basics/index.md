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

# Cloudant Basics

If it's your first time here,
scan this section before you scroll further.
{:shortdesc}

The sections on [Client Libraries](../libraries/index.html#-client-libraries),
[API Reference](../api/index.html#-api-reference),
and [Guides](../guides/index.html#-guides) assume you know some basic things about Cloudant.

## Connecting to Cloudant

To access {{site.data.keyword.cloudant}},
you must have either a [{{site.data.keyword.cloudant}} account](../api/account.html),
or an [{{site.data.keyword.bluemix}} account](../offerings/bluemix.html).

## HTTP API

All requests to Cloudant go over the web.
This means any system that can speak to the web can speak to Cloudant.
All language-specific libraries for Cloudant are really just wrappers that provide
some convenience and linguistic niceties to help you work with a simple API.
Many users choose to use raw HTTP libraries for working with Cloudant.

Specific details about how Cloudant uses HTTP are
provided in the [HTTP topic of the API Reference](../api/http.html).

Cloudant supports the following HTTP request methods:

-   `GET`

    Request the specified item.
    As with normal HTTP requests,
    the format of the URL defines what is returned.
    With Cloudant this can include static items,
    database documents,
    and configuration and statistical information.
    In most cases the information is returned in the form of a JSON document.

-   `HEAD`

    The `HEAD` method is used to get the HTTP header of a `GET` request without the body of the response.

-   `POST`

    Upload data.
    Within Cloudant's API,
    the `POST` method is used to set values,
    upload documents,
    set document values,
    and start some administration commands.

-   `PUT`

    Used to 'store' a specific resource.
    In Cloudant's API,
    `PUT` is used to create new objects,
    including databases,
    documents,
    views,
    and design documents.

-   `DELETE`

    Deletes the specified resource,
    including documents,
    views,
    and design documents.

-   `COPY`

    A special method that can be used to copy documents and objects.

If the client (such as some web browsers) does not support using these HTTP methods,
`POST` can be used instead with the `X-HTTP-Method-Override` request header set to the actual HTTP method.

### Method not allowed error

If you use an unsupported HTTP request type with a URL that does not support the specified type,
a [405](../api/http.html#405) error is returned,
listing the supported HTTP methods, as shown in the following example.

_Example error message in response to an unsupported request:_

```json
{
    "error":"method_not_allowed",
    "reason":"Only GET,HEAD allowed"
}
```
{:codeblock}

## JSON

Cloudant stores documents using JSON (JavaScript Object Notation) encoding,
so anything encoded into JSON can be stored as a document.
Files containing media,
such as images,
videos,
and audio,
are called BLOBs (Binary Large OBjects),
and can be stored as attachments associated with documents.

More information about JSON can be found in the [JSON Guide](../guides/json.html).

<div id="distributed"></div>

## Distributed Systems

Cloudant's API enables you to interact with a collaboration of numerous machines,
called a cluster.
The machines in a cluster must be in the same datacenter,
but can be within different 'pods' in that datacenter.
Using different pods helps improve the High Availability characteristics of Cloudant.

An advantage of clustering is that when you need more computing capacity,
you just add more machines.
This is often more cost-effective and fault-tolerant than scaling up or enhancing an existing single machine.

For more information about Cloudant and distributed system concepts,
see the [CAP Theorem](../guides/cap_theorem.html) guide.

## Replication

[Replication](../api/replication.html) is a procedure followed by Cloudant,
[CouchDB ![External link icon](../images/launch-glyph.svg "External link icon")](http://couchdb.apache.org/){:new_window},
[PouchDB ![External link icon](../images/launch-glyph.svg "External link icon")](http://pouchdb.com/){:new_window},
and other distributed databases.
Replication synchronizes the state of two databases so that their contents are identical.

You can replicate continuously.
This means that a target database updates every time the source database changes.
Continuous replication can be used for backups of data,
aggregating data across multiple databases,
or for sharing data.

However,
continuous replication means testing continuously for any source database changes.
This testing requires continuous internal calls,
which might impact performance or the cost of using the database.

>   **Note**: Continuous replication can result in a large number of internal calls.
    This might affect costs for multi-tenant users of Cloudant systems.
    Continuous replication is disabled by default.
