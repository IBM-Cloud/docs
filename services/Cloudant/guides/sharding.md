---

copyright:
  years: 2017
lastupdated: "2017-05-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Acrolinx: 2017-05-15 -->

# How is data stored in Cloudant?

## Concepts

Every database in Cloudant is formed of one or more distinct _shards_,
where the number of shards is referred to as _Q_.
A shard is a distinct subset of documents from the database.
All _Q_ shards together contain the data within database.
Each shard is stored in three separate copies.
Each shard copy is called a shard _replica_.
Each shard replica is stored on a different server.
The servers are available within a single location data center.
The collection of servers in a data center is called a cluster.

![sharding](../images/sharding_database.png)

A document is assigned to a particular shard by using consistent hashing of its ID.
This assignment means that a document is always stored on a known shard and a known set of servers.

![document consistent hashing](../images/sharding_document.png)

Occasionally,
shards are _rebalanced_.
Rebalancing involves moving replicas to different servers.
It occurs for several reasons,
for example when server monitoring suggests that a server is more heavily or lightly used than other servers,
or when a server must be taken out of service temporarily for maintenance.
The number of shards and replicas stays the same,
and documents remain assigned to the same shard,
but the server storage location for a shard replica changes.

The default value for _Q_ varies for different clusters.
The value can be tuned over time.

The number of replicas (copies of a shard) is also configurable.
In practice,
observation and measurement of many systems suggests that three replicas is a pragmatic number in most cases
to achieve a good balance between performance and data safety.
It would be exceptional and unusual for a Cloudant system to use a different replica count.

## How does sharding affect performance?

The number of shards for a database is configurable
because it affects database performance in a number of ways.

When a request comes into the database from a client application,
one server or 'node' in the cluster is assigned as the _coordinator_ of the request.
This coordinator makes internal requests to the nodes that hold the data relevant to the request,
determines the response to the request,
and returns this response to the client.

The number of shards for a database can affect the performance in two ways:

1.	Each document in the database is stored on a single shard.
	Therefore,
	having many shards enables greater parallelism for any single document request.
	The reason is that the coordinator sends requests only to the nodes that hold the document.
	Therefore,
	if the database has many shards,
	there are likely to be many other nodes that do not need to respond to the request.
	These nodes can continue to work on other tasks without interruption from the coordinator request.
2.	To respond to a query request,
	a database must process the results from all the shards.
	Therefore,
	having more shards introduces a greater processing demand.
	The reason is that the coordinator must make one request per shard,
	then combine the results before it returns the response to the client.

To help determine a suitable shard count for your database,
begin by identifying the most common types of requests that are made by the applications.
For example,
consider whether the requests are mostly for single document operations,
or are the requests mostly queries?
Are any of the operations time-sensitive?

For all queries,
the coordinator issues read requests to all replicas.
This approach is used because each replica maintains its own copy of the indexes that help answer queries.
An important consequence of this configuration is that having more shards enables parallel index building _if_
document writes tend to be evenly distributed across the shards in the cluster.

In practice,
it is hard to predict the likely indexing load across the nodes in the cluster.
Furthermore,
predicting indexing load tends to be less useful than addressing request patterns.
The reason is that indexing might be required after a document write,
but not after a document request.
Therefore,
considering indexing alone does not provide sufficient information
to estimate an appropriate shard count.

When you consider data size,
an important consideration is the number of documents per shard.
Each shard holds its documents in a large
[B-tree ![External link icon](../images/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/B-tree){:new_window}
on disk.
Indexes are stored in the same way.
As more documents are added to a shard,
the number of steps that are used to traverse the B-tree
during a typical document lookup or query increases.
This 'depth increase' tends to slow down requests
because more data must be read from caches or disk.

In general,
avoid having more than 10 million documents per shard.
In terms of overall shard size,
keeping shards under 10 GB is helpful for operational reasons.
For example,
smaller shards are easier to move over the network during rebalancing.

Given the conflicting requirements to avoid having too many documents and keeping shard size low,
a single _Q_ value cannot work optimally for all cases.
Cloudant tunes the defaults for clusters over time as usage patterns change.

Nevertheless,
for a specific database,
it is often useful to take the time to consider observed request patterns and sizing,
and use this information to guide the future selection of an appropriate number of shards.
Testing with representative data and request patterns is essential for better estimation of good _Q_ values.
Be prepared for production experience to alter those expectations.

<div id="summary"></div>

The following simple guidelines might be helpful during the early planning stages.
Remember to validate your proposed configuration by testing with representative data,
particularly for larger databases:

*	If your data is trivial in size,
	such as a few tens or hundreds of MB,
	or thousands of documents,
	then there is little need for more than a single shard.
*	For databases of a few GB or few million documents,
	then a single-digit shard count such as 8 is likely to be acceptable.
*	For larger databases of tens to hundreds of millions of documents or tens of GB,
	consider configuring your database to use 16 shards.
*	For even larger databases,
	consider manually sharding your data into several databases.
	For such large databases,
	contact [Cloudant support ![External link icon](../images/launch-glyph.svg "External link icon")](mailto:support@cloudant.com){:new_window} for advice.

>	**Note:** The numbers in these guidelines are derived from observation and experience
	rather than precise calculation.

<div id="API"></div>

## Working with shards

### Setting shard count

The number of shards,
_Q_,
for a database is set when the database is created.
The _Q_ value cannot be changed later.

To specify the _Q_ when you create a database,
use the `q` query string parameter.

In the following example,
a database that is called `mynewdatabase` is created.
The `q` parameter specifies that eight shards are created for the database.

```sh
curl -X PUT -u myusername https://myaccount.cloudant.com/mynewdatabase?q=8
```
{:codeblock}

>	**Note:** Setting _Q_ for databases is not enabled for Cloudant databases on Bluemix.
	The _Q_ value is not available on most `cloudant.com` multi-tenant clusters.

If you attempt to set the _Q_ value where it is not available,
the result is a [`403` response](../api/http.html#403) with a JSON body
similar to the following example:

```json
{
	"error": "forbidden",
	"reason": "q is not configurable"
}
```
{:codeblock}

### Setting the replica count

In CouchDB version 2 onwards,
you are allowed to [specify the replica count ![External link icon](../images/launch-glyph.svg "External link icon")](http://docs.couchdb.org/en/2.0.0/cluster/databases.html?highlight=replicas#creating-a-database){:new_window}
when you create a database.
However,
you are not allowed to change the replica count value from the default of 3.
In particular,
it is not possible to specify a different replica count value when you create a database.
For further help, contact [Cloudant support ![External link icon](../images/launch-glyph.svg "External link icon")](mailto:support@cloudant.com){:new_window}.

### What are the _R_ and _W_ arguments?

Some requests can have arguments that affect the coordinator's behavior when it answers the request.
These arguments are known as _R_ and _W_ after their names in the request query string.
They can be used for single document operations only.
They have no effect on general 'query style' requests.

In practice,
it is rarely useful to specify _R_ and _W_ values.
For example,
specifying either _R_ or _W_ does not alter consistency for the read or write.

#### What is _R_?

The _R_ argument can be specified on single document requests only.
_R_ affects how many responses must be received by the coordinator before it replies to the client.
The responses must come from the nodes that host the replicas of the shard that contains the document. 

Setting _R_ to _1_ might improve the overall response time
because the coordinator can return a response more quickly.
The reason is that the coordinator must wait only for a single response
from any one of the replicas that host the appropriate shard.

>	**Note:** Reducing the _R_ value increases the likelihood that the response that is
	returned is not based on the most up-to-date data
	because of the [eventual consistency](cap_theorem.html) model used by Cloudant.
	Using the default _R_ value helps mitigate this effect.

The default value for _R_ is _2_.
This value corresponds to most of the replicas for a typical database that uses three shard replicas.
If the database has a number of replicas that is higher or lower than 3,
the default value for _R_ changes correspondingly.

#### What is _W_?

_W_ can be specified on single document write requests only.

_W_ is similar to _R_,
because it affects how many responses must be received by the coordinator before it replies to the client.

>	**Note:** _W_ does not affect the actual write behavior in any way.

The value of _W_ does not affect whether the document is written within the database or not.
By specifying a _W_ value,
the client can inspect the HTTP status code in the response to determine whether _W_ replicas responded to the coordinator.
The coordinator waits up to a pre-determined timeout for _W_ responses from nodes that host copies of the document,
before it returns the response to the client.
