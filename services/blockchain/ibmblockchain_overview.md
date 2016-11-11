---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# About blockchain
{: #ibmblockchain_overview}
Last updated: 03 November 2016
{: .last-updated}

## What is blockchain?
{: #what}

Blockchain is a technology for a new generation of transactional applications that establishes trust, accountability and transparency, while streamlining business processes. The blockchain network was first introduced by bitcoin, but its practical uses extend far beyond cryptocurrency exchanges. With blockchain, IBM is reimagining the most fundamental business exchanges, and opening the door to a new world of digital interactions.

Blockchain is projected to vastly reduce the cost and complexity of cross-enterprise business processes. Its distributed ledger makes it easier to create cost-efficient business networks, where virtually anything of value can be tracked and traded, without a centralized point of control. Blockchain is already showing great promise across a broad range of business applications. As just one example, blockchain networks allow securities trades to be settled in minutes, rather than days. Blockchain is also helping companies streamline the flow of goods and payments, and enabling  manufacturers to reduce product recalls by openly sharing production logs with OEMs and regulators.  
<br>

## Key terms
{: #keyterms}
The following terms are instrumental in gaining a holistic understanding of blockchain concepts:

**Transactor**: A network participant connected to the blockchain network through a node, who submits transactions from a client using an SDK or API.

**Transaction**: A request by a transactor to execute a function on the blockchain network. The transaction types are deploy, invoke, and query, which are implemented through the chaincode functions set forth in the fabric's API contract.

**Ledger**: A sequence of cryptographically-linked blocks, containing transactions and the current world state. In addition to data from previous transactions, the ledger also contains the data for currently-running chaincode applications.

**World state**:  Key-value database used by chaincodes to store their state when executed by a transaction.

**Chaincode**: Embedded logic that encodes the rules for specific types of network transactions. Developers write chaincode applications and deploy them to the network. End users then invoke chaincode through a client-side application that interfaces with a network peer, or node. Chaincode runs network transactions, which if validated, are appended to the shared ledger and modify world state.

**Validating peer**: A network node that runs the consensus protocol for the network to validate transactions and maintain the ledger. Validated transactions are appended to the ledger, in blocks. If a transaction fails consensus, it is purged from the block and therefore, not written to the ledger. A validating peer (VP) has authority to deploy, invoke and query chaincode.

**Non-validating peer**: A network node that functions as a proxy, connecting transactors to validating peers. A non-validating peer (NVP) forwards invocation requests to its connected validating peer (VP). It also hosts the event stream server and the REST service.

**Consensus**: A protocol that maintains the order of blockchain network transactions (deploy and invoke). Validating nodes work collectively to approve transactions by implementing the consensus protocol. Consensus ensures that a quorum of nodes agree on the order of transactions on the shared ledger. By resolving any discrepancies in this order, consensus ensures that all nodes operate on an identical blockchain ledger. See the [consensus](etn_pbft.html) topic for more information and test cases.  

**Permissioned network**: A blockchain network where each node is required to maintain a member identity on the network, and each node has access to only the transactions that its permissions allow.  

## Key concepts
{: #keyconcepts}

**Overview**: Blockchain is a specific type of network, over which members track and exchange digitized assets. A shared ledger contains the single record of all network transactions, and is replicated across all network members. Chaincode applications contain self-executing contracts and client-side applications which interface with the network through an SDK or API.

Two or more transacting parties, as members of a blockchain network, implicitly agree on the terms of the smart contract that governs the transaction (e.g. upon receipt of asset "a", asset "b" is due). Once deployed to the blockchain, functions in the contract can be invoked (i.e. a transaction can be triggered). Ensuing invocation(s) are ordered by a leading node and broadcast to validating peers for consensus. Following validation, transactions are executed and recorded to the ledger in blocks. The ledger is then distributed to all network nodes through replication. Once appended to the ledger, transactions can never be altered or deleted; the only way to undo or change the effects of an approved transaction is to submit a subsequent transaction.

**Network**: A blockchain network is characterized as follows:

- A distributed, decentralized peer-to-peer network, with nodes that represent network participants, such as banks, government agencies, manufacturers and securities firms.
- A group of peers that validate transactions through a consensus protocol before committing them to a shared ledger.

**Shared ledger**: The shared ledger is the single source of truth, or the entire history of validated transactions, on a blockchain network. Any discrepancies in the shared ledger across nodes are resolved through consensus. The ledger has the following attributes:
- It records all validated transactions on the network.
- It is shared across all network participants.
- It is replicated, so that each participant has their own copy.
- It is permissioned, so that participants can only view their own transactions.

**Example**: Figure 1 depicts an example equities blockchain network and the shared ledger:
![Shared Ledger](images/Architecture_shared_ledger.png "Example equities blockchain network")
*Figure 1. A shared ledger example*

Figure 1 shows typical network participants in an equities market: Asset Custodian (bank), Front Office, Operations, securities depository (CSD) and a clearing party (Clearing/CCP):
1. Using a client application, the custodian invokes chaincode to buy and sell blocks of securities.  
2. Transactions can be triggered from any network node, but are always forwarded to the primary (leading) validating node, which orders the transactions. The primary node broadcasts the ordered transactions to all validating peers for consensus, or agreement, on the proposed order.
3. If the order of transactions is agreed upon, the transactions are executed and appended to the ledger on each validating node. The ledger is then replicated to all network nodes.  

<br>
## Network and application architecture
{: #architecture}

Figure 2 depicts an example permissioned blockchain network, which features a distributed, decentralized peer-to-peer architecture and a Certificate Authority managing user roles and permissions:
![Blockchain Network](images/Architecture_network_and_application.png "Example permissioned blockchain network")
*Figure 2. A permissioned blockchain network: data flow and network access are governed by member roles*

The following descriptions correspond to the architecture and flow shown in Figure 2, which do not represent a sequential process:

**A:** A Blockchain User submits a transaction to the Permissioned Blockchain network. The transaction can be a deploy, invoke or query, and is issued through a client-side application leveraging an SDK, or directly through a REST API.  

**B:** Trusted business networks provide access to regulators and auditors, such as the SEC in a U.S. equities market.  

**C:** A Blockchain Network Operator manages member permissions, such as enrolling the Regulator (B) as an "auditor" and the Blockchain User (A) as a "client." An auditor could be restricted to query transactions, whereas a client could be authorized to deploy, invoke and query certain types of chaincode.

**D:** A Blockchain Developer writes chaincode (smart contracts), and client-side applications to invoke smart contracts. The Blockchain Developer could deploy chaincode directly to the network, through a REST interface. To include credentials from a Traditional Data source in chaincode, the developer could use an out-of-band connection to access the data (G).

**E:** A Blockchain User connects to the network through a peer node (A). Before proceeding with any transactions, the node retrieves the user's enrollment and transaction certificates from the Certificate Authority. Users must possess these digital certificates in order to transact on a permissioned network.

**F:** A user attempting to drive chaincode could be required to verify their credentials on a Traditional Data source (G). To confirm the user's authorization, chaincode can use an out-of-band connection to this data, through a Traditional Processing platform.

Figure 3 shows the IBM Blockchain core components. Membership Services, Blockchain Services and Chaincode Services are logical structures, not a physical partitioning of components into separate processes, address spaces or virtual machines:
![Reference Architecture](images/Architecture_core_com.png "Reference Architecture")
*Figure 3. Hyperledger fabric reference architecture*

**Membership Services**: Membership Services manages user identities on a permissioned blockchain network through the Certificate Authority peer. Membership Services provides a distinction of roles by combining elements of Public Key Infrastructure (PKI) and decentralization (consensus). By contrast, non-permissioned networks do not provide member-specific authority or a distinction of roles.

A permissioned blockchain requires entities to register for long-term identity credentials (Enrollment Certificates), which can be distinguished according to entity type. For users, an Enrollment Certificate authorizes  the Transaction Certificate Authority (TCA) to issue pseudonymous credentials; these certificates authorize transactions submitted by the user. Transaction certificates persist on the blockchain, and enable authorized auditors to associate otherwise unlinkable transactions.

**Blockchain Services**: Blockchain Services manages the shared ledger using a peer-to-peer protocol, which is built on HTTP/2. The data structures are highly optimized to provide the most efficient hash algorithm for maintaining replication of the shared ledger. PBFT is implemented as the consensus protocol.    

**Chaincode Services**: Chaincode Services provides a secured and lightweight method to sandbox chaincode execution on the validating nodes. The environment is a “locked down” and secured container, along with a set of signed base images containing secure OS and chaincode language, runtime and SDK layers for Go, Java and Node.js. Additional languages can be enabled, if required.

Refer to the [protocol specification](https://github.com/hyperledger/fabric/blob/v0.6/docs/protocol-spec.md#fabric) for   Hyperledger Fabric 0.5 to learn more about IBM's implementation of blockchain.
