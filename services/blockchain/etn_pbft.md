---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Testing consensus and availability
{: #etn_pbft}

*Last updated: 15 July 2016*
{: .last-updated}

Both the Developer Network and the High Security Business Network plans enable you to test the Practical Byzantine Fault Tolerance (PBFT) consensus protocol on a four-node blockchain network. The following topics provide details about consensus in general, and PBFT in particular. When you are ready to start testing, four PBFT test cases are provided.
{:shortdesc}

## What is consensus?

Consensus is a method for validating the order of network requests, or transactions (deploy and invoke), on a blockchain network. The correct ordering of transactions is critical, because many types of network transactions have a dependency on one or more prior transactions (account debits often have a dependency on prior credits, for example). On a blockchain network, there is no single authority that determines the transaction order; instead, each blockchain node (or peer) has an equal say in establishing the order, by implementing the network consensus protocol. Consensus, therefore, ensures that a quorum of nodes agree on the order in which transactions are appended to the shared ledger. By resolving any discrepancies in the proposed transaction order, consensus guarantees that all network nodes are operating on an identical blockchain. In other words, consensus guarantees the integrity and consistency of blockchain network transactions.

## What is PBFT?

Practical Byzantine Fault Tolerance (PBFT) is one of various consensus protocols which maintain the order of transactions on a blockchain network, despite threats to this order. One such threat is the arbitrary concurrent failure (a type of Byzantine fault) of multiple network nodes. Using PBFT, a blockchain network of (N) nodes can withstand (f) number of Byzantine nodes, where f = (N-1)/3. Put another way, PBFT requires that a minimum of 2\*f + 1 nodes agree on the order of transaction requests before appending them, as a block, to the shared ledger. Deriving either formula reveals the rule that a PBFT network can withstand Byzantine faults on fewer than one-third of all network nodes.

## How does PBFT operate in the Bluemix Network Plans?

The 2\*f + 1 PBFT rule has the following implications for the Developer Network and the High Security Business Network:

1. Either network can tolerate no more than one Byzantine node. Each network contains N=4 nodes, so applying the formula for the maximum number of Byzantine nodes results in f=(4-1)/3=1. If two or more Byzantine nodes (f>1) exist, a 4-node PBFT network cannot guarantee consistency of the ledger across nodes. (By comparison, note that tolerating two Byzantine nodes would require f=(7-1)/3=2, or a minimum 7-node blockchain network.)
2. If fewer than 2\*f + 1 nodes are online, either network ceases operation, because PBFT cannot guarantee consistency of the ledger across nodes. Either network will resume operation when at least 2\*f + 1 nodes are online.
3. Because only a minimum of 2\*f + 1 nodes must reach consensus before proceeding to the next block of transactions, the ledger on any additional nodes (beyond 2\*f + 1) will temporarily lag behind. This lag in syncing the shared ledger across all nodes is an inevitable limitation on any PFBT network.

## What are the consensus test cases?
The following four consensus test cases have been fully tested and are guaranteed by IBM to meet network availability standards for PBFT:

1. Testing PBFT with no Byzantine nodes. Consensus executes transactions and appends to the ledger.
2. Simulating one Byzantine node by stopping one node and continuing to send deploy, invoke and query transactions. Consensus executes the transactions and appends to the ledger. This test was repeated for each node in the four-node environment.
3. Simulating two Byzantine nodes by stopping two nodes and continuing to send deploy, invoke and query transactions. Due to the failure to reach consensus, transactions are not executed or appended to the ledger.
4. Restarting one of the nodes which were stopped in Test 3. The network will resume, and the node that was restarted will sync its ledger with the other validating peers.  

Please review the following notes before starting your consensus testing:

- The four consensus test cases use the REST API to interact with the network peers.
- Because HTTP is the communication protocol for the peers, the tests use the peer URLs. For example: VP0–api.dev.blockchain.ibm.com:80.
Note: Symbolic values ***VP0, VP1, VP2 and VP3*** are used as placeholders for the literal peer URLs.
-  To log in to a peer, use the credentials that were provided when you deployed the bluemix service. For the test cases, **test\_user1** and **test\_user1\_enrollSecret** are used as values for *enrollID* and *enrollSecret*, respectively.
-  Simulate node crashes by manually stopping and restarting peers with the **Actions** buttons from the network console.  Seen in Figure 1, the **Actions** button is on the far-right when you are on the **Network** tab: 

![](images/stopstartpeer.png)
*Figure 1. stop start options*

- The test cases use ***chaincode_example02*** by default, from  https://github.com/hyperledger/fabric/blob/master/examples/chaincode/go/chaincode_example02/chaincode_example02.go. However, you can use your own chaincode, or any of the chaincode examples at https://github.com/hyperledger/fabric/tree/master/examples/chaincode/go.
- Requests are batched into one transaction for processing. However, you can ensure immediate processing by relying on the batch timeout value; waiting at least two seconds before the next request will process transactions immediately.
