---
 
copyright:
years: 2016
 
---
 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
 
 
# Network landscape
{: #etn_overview}
 
*Last updated: 15 July 2016*
{: .last-updated}

The Developer Network and High Security Business Network exploit the latest iterations of the Hyperledger fabric, which include a consensus protocol called Practical Byzantine Fault Tolerance (PBFT), and an enhanced Node.js SDK.  Both consist of four nodes and a Certificate Authority.  The Certificate Authority governs "Membership Services," and is responsible for managing identities, network permissions and confidential transactions through the issuance of digital certificates.
{:shortdesc}

* A consensus protocol (PBFT) manages the ordering of all transactions written to the ledger.  PBFT is unable to run (i.e. peers cannot reach consensus) in an environment with fewer than three nodes.  For more information on consensus and suggested tests, see [Testing consensus and availability](etn_pbft.html).
* A Node SDK allows for client-side Node.js applications to interact with the blockchain. Client-side apps can securely enroll users via Membership Services, issue transactions and cryptographically exchange assets through the usage of tCerts. For more information about Membership Services and user privacy, see the enhanced [Node.js SDK](etn_sdk.html) section and the Fabric [Protocol Specification](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md) section of the Linux Foundation's Hyperledger Project.
* You can access details about your network and environment through your Bluemix Monitor Dashboard.  See [Network Console](ibmblockchainmonitor.html) for information on your monitor.

Use the following terminology along with the diagram below to contextualize and visualize some of the more granular portions of your blockchain network:

* Member - An identity for participating in the blockchain network. There are different types of members (users, peers, validators, and auditors).
* Membership services - Services related to obtaining and managing members.  Member services is governed by the various Certificate Authorities in your network.  
* Registration - The act of adding a new member identity to the network. A member can be dynamically added to the network by a user with 'registrar' privilege. Members may also be assigned roles and attributes, which dictate and control a member's access and operability in the network. Note: Neither roles nor attributes can be assigned dynamically. You must instead edit the membersrvc.yaml.
* Enrollment - Think of this as completing the registration process. It may be done by the new member with a secret that was obtained out-of-band from a registrar, or by a middle-man who has been delegated the authority to act on behalf of the new member.

Figure 1 depicts the network architecture, and the data flow for member services, transactions, consensus and appending to the ledger:

![Dedicated Network](images/Architecture_BMX_dedicated.png "Dedicated Network")
Figure 1.

Use the following steps to understand the network flow:

1. A registered user enrolls through the PKI (Member Services) and receives a long-term enrollment certificate (eCert) and a batch of transactional certificates (tCerts).
2. The user deploys a piece of chaincode onto the network.  The chaincode (aka smart contract) contains business logic embedded within its code.  **Note**: All transactions (deploy, invoke, query) require a tCert, and must be signed with the user's private key.  The user derives this private key from his batch of tCerts.
3. The user invokes the smart contract.  Invoke simply means that the user is triggering the contract to self-execute the logic that is coded into it.
4. A transaction (deploy or invoke) is submitted to the network.  Transactions can come in to any network peer.  Once a peer receives a transaction request, it submits the request to the network's primary peer (VP1 in diagram).  The primary peer will order a batch of transactions and re-broadcast this order to its fellow peers.
5. The peers use a predetermined consensus protocol (PBFT) to agree upon the order.  The process of reaching an agreement on the transaction order is referred to as consensus.  
6. Once the peers have agreed upon the order, the requests are executed and appended to the ledger.  


<!---Both the developer and high-security networks unlock several features in the Hyperledger fabric which robustly enhance security, confidentiality and privacy.  The only fundamental difference between the two is their operating/hosting environment.  The developer network runs in a shared multi-tenant environment on Softlayer, whereas the high-security network exists as an isolated single-tenant running in a secure services container.  Each network leverages the same capabilities from the fabric, including a PBFT consensus protocol and the enhanced Node.js SDK.~~

~~The High-Security business network runs in an isolated and highly secured environment, distinguishing it from other cloud-hosted offerings. The operating system, fabric, and nodes all exist in a secure services container (SSC), providing your enterprise with the security and impregnability that customers have come to expect from system Z technology.  The SSC delivers performance optimization in - peer to peer communication, availability, scalability, hardware encryption, tamper-proof crypto keys, and securely encrypted VMs.  See the [Secure Services Container](etn_ssc.html) section for more details on the security features provided through the SSC.  Additionally, the high security network unlocks numerous features of the Hyperledger fabric (unavailable in the developer service), which robustly enhance security, confidentiality and privacy.  The configuration is such that you are able to test and affirm these features.~~  
{:shortdesc}

~~The high security plan augments the developer plan by delivering several enhancements that help meet the security requirements and concerns of an enterprise-level participant:~~--->

<!---The environment (LinuxONE on z) consists of a four-peer network implementing PBFT with Membership Services enabled, running in an application container.  The application container protects blockchain software, chaincode, and data running within the system. The blockchain software within the secure boot can be signed, attested, and encrypted; and once installed in the application container, is tamper-resistant.  Root users of the platform and system administrators cannot access or see z secure container contents.  In addition, the LinuxOne on z provides you with FIPS compliance, high Evaluation Assurance Level protection, a highly auditable operating environment, and crypto optimization--->




