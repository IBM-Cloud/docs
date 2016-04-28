---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# About {{site.data.keyword.blockchain}}
{: #ibmblockchain_overview}
*Last updated: 28 April 2016*

You can use {{site.data.keyword.blockchain}} to create private and secure digital assets in test applications.  These assets can be traded quickly and securely over permissioned networks.
{:shortdesc}

## What is blockchain?
{: #what}

Blockchain is a technology for a new generation of transactional applications that establishes trust, accountability and transparency while streamlining business processes. It is a design pattern made famous by bitcoin, but its uses go far beyond. With it, we can reimagine the world's most fundamental business interactions and open the door to invent new styles of digital interactions. It has the potential to vastly reduce the cost and complexity of cross-enterprise business processes. The distributed ledger makes it easier to create cost-efficient business networks where virtually anything of value can be tracked and traded, without requiring a central point of control. The application of this emerging technology is showing great promise across a broad range of business applications. For example, blockchain allows securities to be settled in minutes instead of days. It can also be used to help companies manage the flow of goods and related payments, or enable manufacturers to share production logs with OEMs and regulators to reduce product recalls.
  
## Key concepts
{: #keyconcepts}

A blockchain has two main components. A **business network**, in which members exchange items of value through a **ledger**, which each member possesses and whose content is always in sync with the others. Blockchain applications are pieces of chaincode that are deployed in this business netwowrk.  These applications execute transactions, which, if successfully validated by the network's peers, are then recorded to the shared ledger.  The shared ledger is append-only.

**Business network**:

- A decentralized peer-to-peer architecture with nodes consisting of market participants (such as banks and securities firms).
- Protocol peers validate and commit transactions in order to reach consensus.

**Shared ledger**: Think of the shared ledger as a source of truth for businesses that are doing transactions on a blockchain. Often, companies have multiple ledgers for multiple business networks in which they participate. The shared ledger can be used for recording and totaling financial transactions. A shared ledger has the following attributes:
- It records all transactions across the business network.
- It is shared among participants.
- It is replicated so that each participant has their own copy.
- It is permissioned, so that participants see only appropriate transactions.

The following diagram depicts a shared ledger and its participants.

![Shared Ledger](images/share_ledger.png "Shared Ledger")

## Key terms 
{: #keyterms}
These terms are instrumental in gaining a holistic understanding of blockchain concepts.

**Transaction**: A request to the blockchain to execute a function on the ledger. The function is implemented by a chaincode.  `Init`, `Invoke`, and `Query` are the three functions that implement chaincode.

**Transactor**: An entity that issues transactions such as a client application.

**Ledger**: A sequence of cryptographically linked blocks, containing transactions and current world state.  In addition to data from previous transactions, the ledger (blockchain) also contains the data for currently running chaincode applications. 

**World state**: The collection of variables containing the results of executed transactions.

**Chaincode**: An application-level code (a.k.a. smart contract) stored on the ledger as a part of a transaction. Chaincode runs transactions that can modify the world state. A developer would generate a chaincode application and then deploy it to the network.

**Validating peer**: A computer node on the network responsible for running consensus, validating transactions, and maintaining the ledger.  When transactions are validated, the information is recorded to the ledger. When transactions are not validated, they are rejected and nothing is appended to the ledger.  A validating peer has the ability to deploy, invoke and query chaincode.

**Non-validating peer**: A computer node on the network which functions as a proxy connecting transactors to the neighboring validating peers. A non-validating peer (NVP) doesn't execute transactions but does verify them. The NVP does however, forward invocation requests to its connected validator.  It also hosts the event stream server and the REST service. **Note:** The terms peer and node are often used interchangably when discussing blockchain technology.
**Permissioned ledger**: A blockchain network where each entity or node is required to be a member of the network.

## Network and application architecture
{: #architecture}

The following image depicts a hypothetical blockchain network built upon a decentralized peer-to-peer architecture, with a Certificate Authority managing user roles and permissions to the network.  

![Blockchain Network](images/blockchain_network.png "Blockchain")

The following diagram shows the reference architecture of the core components that comprise the blockchain fabric.  The reference architecture is aligned in three categories: Membership, Blockchain, and Chaincode services. These categories are logical structures, not a physical depiction of partitioning of components into separate processes, address spaces, or virtual machines. 

![Reference Architecture](images/refarch.png "Reference Architecture")

**Membership services**: Membership provides services for managing identity on the network. In a non-permissioned blockchain, participation does not require authorization and all nodes can equally submit transactions and attempt to accumulate them into acceptable blocks; that is, there are no distinctions of roles. Membership services combine elements of Public Key Infrastructure (PKI) and decentralization or consensus to transform a non-permissioned blockchain into a permissioned blockchain. In the latter, entities register in order to acquire long-term identity credentials (enrollment certificates), and can be distinguished according to entity type. In the case of users, such credentials enable the Transaction Certificate Authority (TCA) to issue pseudonymous credentials. Such credentials, that is, transaction certificates, are used to authorize submitted transactions. Transaction certificates persist on the blockchain, and enable authorized auditors to cluster otherwise unlinkable transactions. 

**Blockchain services**: Blockchain services manage the distributed ledger through a peer-to-peer protocol, built on HTTP/2. The data structures are highly optimized to provide the most efficient hash algorithm for maintaining the world state replication. The NoOps consensus method is currently used for the Bluemix service.

**Chaincode services**: Chaincode services provides a secured and lightweight way to sandbox the chaincode execution on the validating nodes. The environment is a “locked down” and secured container along with a set of signed base images containing secure OS and chaincode language, runtime and SDK layers for Go, Java, and Node.js. Other languages can be enabled if required.

Visit the [protocol specification](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric) on the Hyperledger Project to learn more about the blockchain ecosystem and its various components.

