---

copyright:
  years: 2017
lastupdated: "2017-03-12"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Transaction flow
{: #v10_txflow}

To ensure data consistency and integrity, Hyperledger Fabric v1.0 implements
multiple checkpoints throughout the transaction flow, from invocation and
endorsement to ordering and commitment to the ledger.
{:shortdesc}

On a Hyperledger Fabric v1.0 network, the flow of data for transactions and
queries is intitiated by a client-side application submitting a transaction
request to peers on a channel. The initial flow of data across the network is
common to both queries and transactions:

1. Through an SDK API, a client application converts the transaction request to
a **proposal**, which it submits to the **peers** on the specified channel.
2. Each peer on the channel verifies the identity and authority of submitting
client signature, and (if valid) executes the chaincode application specified in
the proposal.
3. Based on the transaction results and the **Endorsement Policy** for the
invoked chaincode, each peer returns a signed YES or NO response to the application.
Each signed YES response is an endorsement of the transaction.

At this point in the transaction flow, the process diverges for queries and
transactions. If the proposal invoked chaincode as a **query**, the application
simply returns the data to the client. If the proposal invoked chaincode as a
**transaction**, the data is routed for ordering and commitment to the channel
ledger:

1. Depending on the transaction responses and the **Endorsement Policy** for the
invoked chaincode, the application forwards an endorsed transaction to the
network **ordering service**.
2. The ordering service applies the network algorithm (Kafka) to order the
transactions, which are encrypted hashchains of key-value pairs.
3. The ordering service forwards the ordered transaction results, in a single
**block**, to the channel peers.
4. All channel peers validate each transaction in the block by applying the
chaincode-specific **Validation Policy** and running the **Concurrency Control
Version Check**.
5. Any transactions that fail the validation process are marked as invalid in
the block, and the block is committed (appended) to the channel ledger.
6. All **valid** transaction results in the block are copied to the LevelDB
database, for query support.
7. The **gossip data dissemination protocol** continually broadcasts ledger
data across the channel, to enable peers to sync their ledgers (if necessary).  

**Figure 1** depicts the transaction flow on a Hyperledger Fabric v1.0 blockchain
network:
![Transaction Flow](images/v10_txflow.png "Transaction flow on a Hyperledger Fabric
v1.0 network")
*Figure 1. Transaction flow on a Hyperledger Fabric v1.0 network*

Refer to the [Hyperledger Fabric documentation](http://hyperledger-fabric.readthedocs.io/en/latest/index.html)
for complete information on version 1.0.
