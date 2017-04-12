---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-09"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Blockchain basics
{: #ibmblockchain_overview}

Blockchain is a distributed ledger technology (DLT) for a new generation of transactional applications that establishes trust, accountability and transparency, while streamlining business processes. The blockchain network was first introduced to the market for bitcoin exchanges, but its practical uses extend far beyond cryptocurrency transactions. In conjunction with the Linux Foundation's Hyperledger Project, IBM Blockchain is reimagining the most fundamental business exchanges, opening the door to a new world of digital interactions.

Blockchain has already reduced the cost and complexity of cross-enterprise transactions, and the rate of adoption is quickening. Its distributed ledger enables the creation of highly secure and cost-efficient business networks, where virtually anything of value can be tracked and traded without reliance on a centralized point of control. Blockchain is showing great promise across a broad range of business applications. In finance, blockchain networks allow securities trades to be settled in minutes, rather than days. Blockchain is also streamlining the flow of goods and payments for retailers, and limiting product recalls for manufacturers.

## Key terms
{: #keyterms}
The following terms are instrumental in gaining a holistic understanding of the blockchain concepts applied in Hyperledger Fabric v1.0:

**Block**: A batch of ordered transactions that is delivered to peers for validation and commitment to the ledger.

**Hyperleger fabric network**: A Hyperledger fabric network consists of, at minimum, one peer (responsible for endorsing and committing transactions) leveraging an ordering service, and a membership services component (certificate authority) that distributes and revokes cryptographic certificates representative of user identities and permissions.

**Bootstrap**: The initial setup of a network. There is the bootstrap of a peer network, during which policies, system chaincodes, and cryptographic materials (certs) are disseminated amongst participants, and the bootstrap of an ordering network. The bootstrap of the ordering network must precede the bootstrap of the peer network, as a peer network is contingent upon the presence of an ordering service. A network need only be “bootstrapped” once.

**Chaincode**: Chaincode is software that encodes key value pairs or text-based data (JSON) and transaction instructions for modifying this information.

**Channel**: A Channel is formed as an offshoot of the system chain; and best thought of as a “topic” for peers to subscribe to, or rather, a subset of a broader blockchain network. A peer may subscribe on various channels and can only access the transactions on the subscribed channels. Each channel has a unique ledger, thus accommodating confidentiality and execution of multilateral contracts.

**Configuration Block**: Contains the configuration data defining members and policies for a system chain or channel(s). Any changes to the channel(s) or overall network (for example, a new member successfully joining) will result in a new configuration block being appended to the appropriate chain.  This block will contain the contents of the genesis block, plus the delta. The policy to alter or edit a channel-level configuration block is defined through the Configuration System Chaincode (CSCC).

**Committer**: A specific peer role, where the Committing peer appends the validated transactions to the channel-specific ledger. A peer can act as both an endorser and committer, but in more regulated circumstances might only serve as a committer.

**Consensus**: A broader term overarching the entire transactional flow, which serves to generate an agreement on the order and to confirm the correctness of the set of transactions constituting a block.

**Dynamic membership**: Hyperledger fabric network supports the addition/removal of members, peers, and ordering service nodes, without compromising the operationality of the overall network. Dynamic membership is critical when business relationships adjust and entities need to be added/removed for various reasons.

**User**: A user is someone who would interact with the blockchain through a set of published APIs (for example, the hfc SDK). You can have an admin user who typically grants permissions to the Member’s components, and a client user, who, upon proper authentication through the admin user, drives chaincode applications (deploy, invoke, query) on various channels. In the case of self-executing transactions, the application itself can also be thought of as the end user.

**Endorsement**: Refers to the process where specific peer nodes execute a transaction and return a YES/NO response to the client application that generated the transaction proposal. Chaincode applications have corresponding endorsement policies, in which the endorsing peers are specified.

**Endorsement policy**: A Hyperledger fabric network must establish rules that govern the endorsement (or not) of proposed, simulated transactions. This endorsement policy could require that a transaction be endorsed by a minimum number of endorsing peers, a minimum percentage of endorsing peers, or by all endorsing peers that are assigned to a specific chaincode application. Policies can be curated based on the application and the desired level of resilience against misbehavior (deliberate or not) by the endorsing peers. A distinct endorsement policy for deploy transactions, which install new chaincode, is also required.

**Endorser**: A specific peer role, where the Endorser peer is responsible for simulating transactions, and in turn preventing unstable or non-deterministic transactions from passing through the network.  A transaction is sent to an endorser in the form of a transaction proposal. All endorsing peers are also committing peers (for example, they write to the ledger).

**Genesis Block**: The configuration block that initializes a Hyperledger fabric network or channel, and also serves as the first block on a chain.

**Gossip Protocol**: A communication protocol used among peers in a channel, to maintain their network and to elect Leaders, through which funnels all communications with the Ordering Service. Gossip allows for data dissemination, therein providing support for scalability due to the fact that not all peers are required to execute transactions and communicate with the ordering service.

**Initialize**: A method to initialize a chaincode application prior to it being instantiated.

**Install**: The process of placing a chaincode on a peer’s file system.

**Instantiate**: The process of starting a chaincode container.

**Invoke**: Used to call chaincode functions. Invocations are captured as transaction proposals, which then pass through a modular flow of endorsement, ordering, validation, committal.  The structure of invoke is a function and an array of arguments.

**Ledger**: An append-only transaction log managed by peers. Ledger keeps the log of ordered transaction batches. There are two denotations for ledger; peer and validated. The peer ledger contains all batched transactions coming out of the ordering service, some of which may in fact be invalid. The validated ledger will contain fully endorsed and validated transaction blocks. In other words, transactions in the validated ledger have passed the entire gamut of “consensus” - i.e. they have been endorsed, ordered, and validated.

**Member**: A legally distinct entity that owns a unique root certificate for the network. Network components such as peers, application clients and user identities are linked to a member.

**Membership Services**: Membership Services authenticates, authorizes, and manages identities on a permissioned Hyperledger fabric network. The membership services code that runs in peers and orderers both authenticates and authorizes blockchain operations. It is a PKI-based implementation of the Membership Services Provider (MSP) abstraction.

**Membership Service Provider**: The Membership Service Provider (MSP) refers to an abstract component of the system that provides credentials to clients, and peers for them to participate in a Hyperledger Fabric network. Clients use these credentials to authenticate their transactions, and peers use these credentials to authenticate transaction processing results (endorsements). While strongly connected to the transaction processing components of the systems, this interface aims to have membership services components defined, in such a way that alternate implementations of this can be smoothly plugged in without modifying the core of transaction processing components of the system.

**Multi-channel**: The fabric supports multiple channels with a designated ledger per channel. This capability allows for multilateral contracts where only the restricted participants on the channel will submit, endorse, order, or commit transactions on that channel.  As such, a single peer can maintain multiple ledgers without compromising privacy and confidentiality.

**Orderer**: One of the network entities that form the ordering service. A collection of ordering service nodes (OSNs) will order transactions into blocks according to the network’s chosen ordering implementation. In the case of “solo”, only one OSN is required. Transactions are “broadcast” to orderers, and then “delivered” as blocks to the appropriate channel.

**Ordering service**: A defined collective of nodes that orders transactions into a block. The ordering service exists independent of the peer processes and orders transactions on a first-come-first-serve basis for all channel’s on the network. The ordering service is designed to support pluggable implementations beyond the out-of-the-box SOLO and Kafka varieties. The ordering service is a common binding for the overall network; it contains the cryptographic identity material tied to each Member.

**Peer**: A network entity that maintains a ledger and runs chaincode containers in order to perform read/write operations to the ledger. Peers are owned and maintained by members.

**Policy**: There are policies for endorsement, validation, block committal, chaincode management and network/channel management. Policies are defined through system chaincodes, and contain the requisite specifications for a network action to succeed.  For example, an endorsement policy may require that 100% of endorsers achieve the same result upon transaction simulation.

**Proposal**: A request for endorsement that is aimed at specific peers on a channel. Each proposal is either an instantiate or an invoke (read/write) request.

**Query**: A query requests the value of a key(s) against the current state.

**Transaction**: An invoke or instantiate operation. Invokes are requests to read/write data from the ledger. Instantiate is a request to start a chaincode container on a peer.


For the terms from the previous Hyperledger Fabric v0.6 or earlier, see [this page](etn_overview.html) for the details.

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

**Figure 1** depicts an example equities blockchain network and the shared ledger:
![Shared Ledger](images/Architecture_shared_ledger.png "Example equities blockchain network")
*Figure 1. A shared ledger example*

Figure 1 shows typical network participants in an equities market: Asset Custodian (bank), Front Office, Operations, securities depository (CSD) and a clearing party (Clearing/CCP):
1. Using a client application, the custodian invokes chaincode to buy and sell blocks of securities.  
2. Transactions can be triggered from any network node, but are always forwarded to the primary (leading) validating node, which orders the transactions. The primary node broadcasts the ordered transactions to all validating peers for consensus, or agreement, on the proposed order.
3. If the order of transactions is agreed upon, the transactions are executed and appended to the ledger on each validating node. The ledger is then replicated to all network nodes.  

<br>
## Network and application architecture
{: #architecture}

**Figure 2** depicts an example permissioned blockchain network, which features a distributed, decentralized peer-to-peer architecture and a Certificate Authority managing user roles and permissions:
![Blockchain Network](images/Architecture_network_and_application.png "Example permissioned blockchain network")
*Figure 2. A permissioned blockchain network: data flow and network access are governed by member roles*

The following descriptions correspond to the architecture and flow shown in Figure 2, which do not represent a sequential process:

**A:** A Blockchain User submits a transaction to the Permissioned Blockchain network. The transaction can be a deploy, invoke or query, and is issued through a client-side application leveraging an SDK, or directly through a REST API.  

**B:** Trusted business networks provide access to regulators and auditors, such as the SEC in a U.S. equities market.  

**C:** A Blockchain Network Operator manages member permissions, such as enrolling the Regulator (B) as an "auditor" and the Blockchain User (A) as a "client." An auditor could be restricted to query transactions, whereas a client could be authorized to deploy, invoke and query certain types of chaincode.

**D:** A Blockchain Developer writes chaincode (smart contracts), and client-side applications to invoke smart contracts. The Blockchain Developer could deploy chaincode directly to the network, through a REST interface. To include credentials from a Traditional Data source in chaincode, the developer could use an out-of-band connection to access the data (G).

**E:** A Blockchain User connects to the network through a peer node (A). Before proceeding with any transactions, the node retrieves the user's enrollment and transaction certificates from the Certificate Authority. Users must possess these digital certificates in order to transact on a permissioned network.

**F:** A user attempting to drive chaincode could be required to verify their credentials on a Traditional Data source (G). To confirm the user's authorization, chaincode can use an out-of-band connection to this data, through a Traditional Processing platform.

**Figure 3** shows the IBM Blockchain core components. Membership Services, Blockchain Services and Chaincode Services are logical structures, not a physical partitioning of components into separate processes, address spaces or virtual machines:
![Reference Architecture](images/Architecture_core_com.png "Reference Architecture")
*Figure 3. Hyperledger fabric reference architecture*

**Membership Services**: Membership Services manages user identities on a permissioned blockchain network through the Certificate Authority peer. Membership Services provides a distinction of roles by combining elements of Public Key Infrastructure (PKI) and decentralization (consensus). By contrast, non-permissioned networks do not provide member-specific authority or a distinction of roles.

A permissioned blockchain requires entities to register for long-term identity credentials (Enrollment Certificates), which can be distinguished according to entity type. For users, an Enrollment Certificate authorizes  the Transaction Certificate Authority (TCA) to issue pseudonymous credentials; these certificates authorize transactions submitted by the user. Transaction certificates persist on the blockchain, and enable authorized auditors to associate otherwise unlinkable transactions.

**Blockchain Services**: Blockchain Services manages the shared ledger using a peer-to-peer protocol, which is built on HTTP/2. The data structures are highly optimized to provide the most efficient hash algorithm for maintaining replication of the shared ledger. PBFT is implemented as the consensus protocol.    

**Chaincode Services**: Chaincode Services provides a secured and lightweight method to sandbox chaincode execution on the validating nodes. The environment is a “locked down” and secured container, along with a set of signed base images containing secure OS and chaincode language, runtime and SDK layers for Go, Java and Node.js. Additional languages can be enabled, if required.

Refer to the [Hyperledger Fabric documentation](http://hyperledger-fabric.readthedocs.io/en/latest/index.html) for complete information on version 1.0.
