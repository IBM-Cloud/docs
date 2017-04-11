---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Testing consensus and availability
{: #etn_pbft}

Both the Starter Developer plan and the High Security Business Network plan enable you to test the Practical Byzantine Fault Tolerance (PBFT) consensus protocol on a four-node blockchain network. The following topics provide details about consensus in general, and PBFT in particular. Once you are ready to start testing, PBFT test cases are provided.  
{:shortdesc}  

## What is consensus?

Consensus is a method for validating the order of requests, or transactions (deploy and invoke), on a blockchain network. The correct ordering of transactions is critical, because many transactions have a dependency on one or more prior transactions (account debits often have a dependency on prior credits, for example).

On a blockchain network, there is no centralized authority that determines the transaction order; instead, many validating nodes (or peers) implement the network consensus protocol. Consensus ensures that a quorum of nodes agree on the order in which transactions are appended to the shared ledger. By resolving any discrepancies in the proposed transaction order, consensus guarantees that all blockchain network nodes are operating on an identical ledger. In other words, consensus guarantees* the integrity and consistency of all blockchain network transactions.

* This guarantee is dependent upon variables such as the specific consensus protocol implemented, and the number of nodes in the blockchain network. Both Blockchain on Bluemix plans implement the PBFT consensus protocol.  

<br>
## What is PBFT?

Practical Byzantine Fault Tolerance (PBFT) is one flavor of consensus protocol. The function of a consensus protocol is to maintain the order of transactions on a blockchain network, despite threats to this order. One such threat is the arbitrary concurrent failure (a type of Byzantine fault) of multiple network nodes. Using PBFT, a blockchain network of (N) nodes can withstand (f) number of Byzantine nodes, where f = (N-1)/3. In other words, PBFT ensures that a minimum of 2\*f + 1 nodes reach consensus on the order of transactions before appending them to the shared ledger. Deriving either formula reveals the rule that a PBFT network guarantees data consistency and integrity despite Byzantine faults on fewer than one-third of all network nodes.  

<br>
## PBFT and your blockchain network

The 2\*f + 1 PBFT rule has the following implications for both the Starter Developer plan and the High Security Business Network plan:

1. The network can tolerate no more than one Byzantine node. Each network contains N=4 nodes, so applying the formula for the maximum number of tolerated Byzantine nodes results in: f=(4-1)/3=1. If two or more Byzantine nodes (f>1) exist, a the 4-node PBFT network cannot guarantee consistency or integrity of the ledger across all nodes. (For comparison, tolerating two Byzantine nodes would require f=(7-1)/3=2, or a minimum 7-node PBFT blockchain network.)
2. If fewer than 2\*f + 1 nodes are online, the network ceases appending to the ledger, because PBFT cannot guarantee data consistency or integrity across nodes. The network will resume appending to the ledger when at least 2\*f + 1 nodes are online (three or four nodes, in this case).
3. Because only a minimum of 2\*f + 1 nodes must reach consensus before proceeding to the next block of transactions, the ledger on any additional nodes (beyond 2\*f + 1) will temporarily lag behind. This lag in syncing the shared ledger across all nodes is an inevitable limitation on any PFBT network.
<br>

## Consensus test cases
The following consensus test cases have been vetted by IBM as meeting network availability standards for PBFT:

1. [Testing PBFT with no Byzantine nodes](pbft_test1.html). The consensus process executes transactions and appends to the ledger.
2. [Simulating one Byzantine node](pbft_test2.html) by stopping one node and continuing to send deploy, invoke and query transactions. The PBFT consensus process executes transactions and appends to the ledger. This test was repeated for each node in a  four-node environment.
3. [Simulating two Byzantine nodes](pbft_test3.html) by stopping two nodes and continuing to send deploy, invoke and query transactions. Due to the failure to reach PBFT consensus, transactions are not executed or appended to the ledger.
4. [Restarting one node that was stopped](pbft_test4.html) in the previous test case (Test 3). The PBFT consensus process resumes executing transactions and appending to the ledger. The node that was restarted syncs its ledger with the shared ledger.  

Attention: Review the following notes before starting your consensus testing:

- All consensus test cases use the REST API to interact with the network peers.
- HTTP/2 is the communication protocol; the test cases use the peer URLs. For example: 'VP0–api.dev.blockchain.ibm.com:80'. The symbolic values ***VP0, VP1, VP2 and VP3*** are used as placeholders for the literal peer URLs.
-  To log in to a peer, use the credentials that were provided when you deployed your Bluemix service. For the test cases, **test\_user1** and **test\_user1\_enrollSecret** are used as the values for *enrollID* and *enrollSecret*, respectively.
-  Simulate node crashes by manually stopping and restarting peers with the **Actions** buttons on the network console. Figure 1 below shows the **Actions** on the **Network** tab:

![](images/stopstartpeer.png "Stop and start peers")
*Figure 1. Stop and start peers*

- The test cases use **chaincode_example02**, by default, from: https://github.com/hyperledger/fabric/tree/v0.6/examples/chaincode/go/chaincode_example02. However, you can use your own chaincode, or any of the chaincode examples at: https://github.com/hyperledger/fabric/tree/v0.6/examples/chaincode/go.
- Requests are batched into one transaction for processing. However, you can ensure immediate processing by relying on the batch timeout value; waiting at least two seconds before submitting the next request will process the transaction immediately.
