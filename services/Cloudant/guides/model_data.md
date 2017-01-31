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

# My top 5 tips for modelling your data to scale

This article considers the finer 
points of modelling your application's data to work efficiently at large scale.
{:shortdesc}

_(This guide is based on a Blog article by Mike Rhodes:
["My top 5 tips for modelling your data to scale" ![External link icon](../images/launch-glyph.svg "External link icon")](https://cloudant.com/blog/my-top-5-tips-for-modelling-your-data-to-scale/){:new_window},
originally published December 17, 2013.)_

The way you model data on Cloudant will significantly impact how your application is able to 
scale. Our underlying data model differs substantially from a relational model, and ignoring 
this distinction can be the cause of performance issues down the road.

As always, successful modelling involves achieving a balance between ease of use vs. the 
performance characteristics you're hoping to achieve.

Without further ado, let’s jump in.

## Consider Immutable Data

If you are changing the same piece of state at a rate of once per second or more, consider 
making your documents immutable. This significantly decreases the chance that you’ll create 
conflicted documents.

Conversely, if you are updating a given document less than once every ten seconds, an 
update-in-place data model - that is, updating existing documents - will simplify your 
application code considerably.

Typically, data models based on immutable data require the use of views to summarize 
the documents which comprise the current state. As views are precomputed, this shouldn’t 
adversely affect application performance.

## Why this helps

Behind our `https://<account>.cloudant.com/` interface is a distributed database. 
Within the cluster, documents are bucketed into a number of shards which collectively form the 
database. These shards are then distributed across nodes in the cluster. This is what 
allows us to support databases many terabytes in size.

By default, in addition to the splitting of a database into shards, all shards have three 
copies, or shard replicas, each of which resides on a different node of the database cluster. 
This allows the database to continue serving requests if a node should fail. Therefore, 
saving a document involves writing to three nodes. What this means is that if two updates are 
made concurrently to the same document, it’s possible for a subset of nodes to accept the first 
update and another subset to accept the second update. When the cluster discovers this 
discrepancy, it will combine the documents in the same way as normal replication does for 
concurrent updates by creating a conflict.

Conflicted documents harm performance; see below for more details on just why this happens. 
A highly concurrent update-in-place pattern also increases the likelihood that writes will 
be rejected because the `_rev` parameter isn’t the expected one, which will force your 
application to retry and so delay processing.

We've found that this conflicted-document scenario is significantly more likely to happen 
for updates more often than once a second, but recommend immutable documents for updates of 
more than once every ten seconds to be on the safe side.

## Use Views To Pre-Calculate Results Rather Than As Search Indexes

Rather than using views as glorified search indexes - "get me all `person` documents" - try 
to get the database to do work for you. For example, rather than retrieving all ten thousand 
person documents to calculate their combined hours worked, use a view with a composite key to 
pre-calculate this by year, month, day, half-day and hour using the `_sum` built-in reduce. 
You'll save work in your application and allow the database to concentrate on serving many 
small requests rather than reading huge amounts of data from disk to service a single large 
request.

## Why this helps

It's quite straightforward. First, note that both maps and reduces are precomputed. This means 
that asking for the result of a reduce function is a cheap operation, particularly when 
compared to the significant amounts of IO required to stream hundreds or even thousands of 
documents from the on-disk storage.

At a lower level, when a node receives a view request, it asks the nodes holding the shard 
replicas for the view's database for the results of the view request for the documents in 
each shard. As it receives the answers - taking the first for each shard replica - the node 
servicing the view request combines the results and streams the final result to the client. 
As more documents are involved, it takes longer for each replica to stream the results from 
disk and across the network. In addition, the node servicing the request has much more work to 
do in combining the results from each database shard.

Overall, the goal is for a view request to require the minimum amount of data from each shard, 
minimizing the time the data is in transit and being combined to form the final result. Using 
the power of views to precompute aggregate data is one way to achieve this aim. This obviously 
decreases the time your application spends waiting for the request to complete.

## De-Normalise Your Data

In relational databases, normalising data is often the most efficient way to store data. 
This makes a lot of sense when you can use JOINs to easily combine data from multiple tables. 
In Cloudant, you're more likely to need a HTTP GET request for each piece of data, so reducing 
the number of requests you need to build up a complete picture of a modeled entity will allow 
you to present information to your users more quickly.

Using views allows you to get many of the benefits of normalised data while maintaining the 
de-normalised version for efficiency.

As an example, in a relational schema you'd normally represent tags in a separate table and use 
a connecting table to join tags with their associated documents, allowing quick look up of all 
documents with a given tag.

In Cloudant, you'd store tags in a list in each document. You would then use a view to get the 
documents with a given tag by 
[emitting each tag as a key in your view's map function](../api/creating_views.html). 
Querying the view for a given key will then provide all the documents with that tag.

## Why this helps

It all comes down to the number of HTTP requests your application makes. There's a cost to 
opening HTTP connections - particularly HTTPS - and, while re-using connections helps, making 
fewer requests overall will speed up the rate at which your application can process data.

As a side benefit, de-normalised documents and pre-computed views often allow you to have the 
value your application requires generated ahead of time, rather than being constructed on the 
fly at query time.

## Avoid Conflicts By Using Finer-Grained Documents

In tension with the advice to de-normalise your data is this next piece of advice: use 
fine-grained documents to reduce the chance of concurrent modifications creating conflicts. 
This is somewhat like normalising your data. There's a balance to strike between reducing the 
number of HTTP requests and avoiding conflicts.

For example, take a medical record containing a list of operations:

```json
{
    "_id": "Joe McIllness",
    "operations": [
        { "surgery": "heart bypass" },
        { "surgery": "lumbar puncture" }
    ]
}
```
{:codeblock}

If Joe is unfortunate enough to be having a lot of operations at the same time, the many 
concurrent updates to a document is likely to create conflicted documents, as described above. 
Better to break the operations out into separate documents which refer to Joe's person document 
and use a view to connect things together. To represent each operation, you’d upload documents 
like the following two example:

```json
{
    "type": "operation",
    "patient": "Joe McIllness",
    "surgery": "heart bypass"
}
```
{:codeblock}

```json
{
    "type": "operation",
    "patient": "Joe McIllness",
    "surgery": "lumbar puncture"
}
```
{:codeblock}

Emitting the `"patient"` field as the key in your view would then allow querying for all 
operations for a given patient. Again, views are used to help knit together a full picture of 
a given entity from separate documents, helping to keep the number of HTTP requests low even 
though we’ve split up the data for a single modeled entity.

## Why this helps

Avoiding conflicted documents helps speed up many operations on your Cloudant databases. 
This is because there’s a process which works out the current winning revision used each time 
the document is read: single document retrievals, calls with `include_docs=true`, view building 
and so on.

The winning revision is a particular revision from the document’s overall tree. Recall that 
documents on Cloudant are in fact trees of revisions. An arbitrary but deterministic algorithm 
selects one of the non-deleted leaves of this tree to return when a request is made for the 
document. Larger trees with a higher branching factor take longer to process than a document 
tree with no or few branches: each branch needs to be followed to see if it’s a candidate to 
be the winning revision. Potential victors then need to be compared against each other to make 
the final choice.

Cloudant obviously handles small numbers of branches well - after all, replication relies on 
the fact documents can branch to avoid discarding data - but when pathological levels are 
reached, particularly if the conflicts are not resolved, it becomes very time-consuming and 
memory-intensive to walk the document tree.

## Build In Conflict Resolution

In an eventually consistent system like Cloudant, conflicts will eventually happen. As 
described above, this is a price of our scalability and data resilience.

Structuring your data in such a way that resolving conflicts is quick and need not involve 
operator assistance will help keep your databases humming along smoothly. The ability to 
automatically resolve conflicts without your users needing to be involved will significantly 
improve their experience too and hopefully reduce the support burden on your organisation.

How you do this is very application specific, but here's a few tips:

-   Avoid invariants across document fields if possible. This makes it more likely that a simple
    merge operation, taking the changed field from each conflicted document revision, will be
    suitable. This makes for simpler and more robust application code.
-   Allow documents to stand alone. Needing to retrieve other documents to work out the correct
    resolution will increase latency in conflict resolution. There's also a chance you'll get a
    version of the other documents that are not consistent with the document you're resolving,
    making correct resolution difficult. And what if the other documents are conflicted?

## Why this helps

As described above, heavily conflicted documents exert a heavy toll on the database. Building 
in the capability to resolve conflicts from the beginning is a great help in avoiding 
pathologically conflicted documents.

## Summary

These tips demonstrate some of the ways modeling data will affect your application’s 
performance. Cloudant’s data store has some specific characteristics, both to watch out for 
and to take advantage of, to make sure the database performance scales as your application 
grows. We understand the shift can be confusing, so we’re always on-hand to give advice.

For further reading, see this discussion on the
["data model for Foundbite" ![External link icon](../images/launch-glyph.svg "External link icon")](https://cloudant.com/blog/foundbites-data-model-relational-db-vs-nosql-on-cloudant/){:new_window},
or this ["example from our friends at Twilio" ![External link icon](../images/launch-glyph.svg "External link icon")](https://www.twilio.com/blog/2013/01/building-a-real-time-sms-voting-app-part-3-scaling-node-js-and-couchdb.html){:new_window}.

