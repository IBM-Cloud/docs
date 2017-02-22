---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Acrolinx: 2017-01-24 -->

<div id="cap_theorem"></div>

<div id="consistency"></div>

# CAP Theorem

Cloudant uses an ['Eventually Consistent' ![External link icon](../images/launch-glyph.svg "External link icon")](http://en.wikipedia.org/wiki/Eventual_consistency){:new_window} model.
{:shortdesc}

To understand how this model works,
and why it is an essential part of using Cloudant,
consider what is meant by Consistency.

Consistency is one of the four ['ACID' ![External link icon](../images/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/ACID){:new_window} properties
that are necessary for transactions within a database to be processed and reported reliably.

Additionally,
consistency is one of the three attributes in the
<a href="http://en.wikipedia.org/wiki/CAP_Theorem" target="_blank">'CAP' <img src="../images/launch-glyph.svg" alt="External link icon" title="External link icon"></a>
theorem.
The attributes are **C**onsistency,
**A**vailability, and **P**artition tolerance.
The theorem states that it is not possible for a distributed computer system such as Cloudant
to guarantee three attributes _simultaneously_:

-   Consistency,
    where all nodes see the same data at the same time.
-   Availability,
    which guarantees that every request receives a response about whether it succeeded or failed.
-   Partition tolerance,
    where the system continues to operate even if any one part of the system is lost or fails.

The impossibility of guaranteeing all three attributes at the same time
means that Cloudant does not guarantee the Consistency attribute.
In an eventually consistent model,
like Cloudant,
an update made to one part of the system is _eventually_ seen by other parts of the system.
As the update propagates,
the system is said to 'converge' on complete consistency.

Eventual consistency is good for performance.
With a strong consistency model,
a system must wait for any updates to propagate completely and successfully
before a write or update request can be completed.
With an eventually consistent model,
the write or update request can return almost immediately,
while the propagation across the system continues 'behind the scenes'.

A database can exhibit only two of these three attributes for both theoretical and practical reasons.
A database prioritizing consistency and availability is simple:
a single node stores a single copy of your data.
But this model is difficult to scale as you must upgrade the node to get more performance,
rather than use extra nodes.
And,
even a minor system failure can shut down a single-node system,
while any message loss means significant data loss.
To endure,
the system must become more sophisticated.

## Tradeoffs in Partition Tolerance

A database that prioritizes consistency and partition tolerance commonly employs a
<a href="http://en.wikipedia.org/wiki/Master/slave_(technology)" target="_blank">master-slave <img src="../images/launch-glyph.svg" alt="External link icon" title="External link icon"></a>
setup,
where one node of the many in the system is elected leader.
Only the leader can approve data writes,
while all secondary nodes replicate data from the leader to handle reads.
If the leader loses connection to the network,
or can't communicate with many of the system's nodes,
the remainder elects a new leader.
This election process differs between systems,
and can be a source of [significant problems ![External link icon](../images/launch-glyph.svg "External link icon")](http://aphyr.com/posts/284-call-me-maybe-mongodb){:new_window}.

Cloudant prioritizes availability and partition tolerance by employing a master-master setup,
such that every node can accept both writes and reads to its portion of your data.
Multiple nodes contain copies of each portion of your data.
Each node copies data with other nodes.
If a node becomes inaccessible,
others can serve in its place while the network heals.
This way,
the system returns your data in a timely manner despite arbitrary node failure,
and maintains [eventual consistency ![External link icon](../images/launch-glyph.svg "External link icon")](http://en.wikipedia.org/wiki/Eventual_consistency){:new_window}.
The tradeoff in deprioritizing absolute consistency is that it takes time for all nodes to see the same data.
As a result,
some responses might contain old data while the new data propagates through the system.

## Changing the approach

Maintaining one consistent view of data is logical and easy to understand
because a relational database does this work for you.
The expectation is that web-based services that interact with database systems behave in this way.
But that expectation does not mean that they do work this way.
Consistency is not a given,
and it takes a little work to change the approach.

In fact,
consistency isn't necessarily essential for many enterprise cloud services.
Large,
heavily used systems bring with them a high probability that a portion of the system might fail.
A database that is engineered around the need to prioritize availability and eventual consistency
is better suited to keeping your application online.
The consistency of application data can be addressed after the fact.
As Seth Gilbert and Nancy Lynch of MIT
[conclude ![External link icon](../images/launch-glyph.svg "External link icon")](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf){:new_window},
"most real-world systems today are forced to settle with returning 'most of the data, most of the time.'"

## Application availability versus consistency in the enterprise

A look at popular web-based services shows that people already expect high availability,
and happily trade this availability for eventually consistent data,
often without realizing they are doing so.

Many applications mislead users for the sake of availability.
Consider ATMs:
inconsistent banking data is why it's still possible to overdraft money without realizing it.
It is unrealistic to present a consistent view of your account balance throughout the entire banking system
if every node in the network must halt and record this figure before operations continue.
It's better to make the system highly available.

The banking industry figured it out back in the 1980s,
but many IT organizations are still worried about sacrificing consistency for the sake of availability.
Think about the number of support calls placed when your sales team can't access their CRM app.
Now consider whether they would even notice when it takes a few seconds for a database update
to propagate throughout the application.

Availability trumps consistency more than you might expect.
Online shopping cart systems,
HTTP caches,
and DNS are a few more examples.
Organizations must consider the cost of downtime such as user frustration,
productivity loss,
and missed opportunities.

## From theory to implementation

Addressing high availability is vital for cloud applications.
Otherwise,
global database consistency remains a major bottleneck as you scale.
Highly available applications need to maintain constant contact with their data,
even if that data isn't the most up-to-date.
That's the concept of eventual consistency,
and it's nothing to be scared of.
At large scale,
sometimes it's better to serve answers that are not perfectly correct than to not serve them at all.

Database systems hide the complexities of availability versus consistency in different ways,
but they are always there.
The view that is taken by the Cloudant database-as-a-service,
along with CouchDB and other NoSQL databases,
is that it's better to require developers to address these complexities early in the design process.
By doing the hard work up front,
you reduce surprises because applications are ready to scale from day one.
