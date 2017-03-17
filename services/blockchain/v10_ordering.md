---

copyright:
  years: 2017
lastupdated: "2017-03-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Ordering service
{: #v10_ordering}

The **HSBN vNext Beta** plan includes a Kafka-based service for ordering and broadcasting network transactions. Kafka also provides crash fault tolerance to your network; if a limited number of ordering service nodes are unavailable, the service continues to order and distribute blocks of transactions to channel peers.
{:shortdesc}

Client-side applications, through an SDK API, forward endorsed transactions to the ordering service. Ordering service nodes then exploit the Kafka service, and its associated ZooKeeper server, to order the transactions in a block. The ordered block of transactions is eventually forwarded to the channel peers, for validation and commmitment to the ledger.

Ordering service nodes also provide the following services:

1. Authentication of clients
2. Read-write operations of **chains** (encrypted key-value pairs that represent transaction results)
3. Filtering and validation for configuration transactions that reconfigure or create a channel.

For details on the Apache Kafka distributed streaming platform, refer to [Apache Kafka](http://kafka.apache.org){: new_window}.
