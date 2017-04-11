---

copyright:
  years: 2017
lastupdated: "2017-03-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# HSBN vNext Beta network overview
{: #v10_netoverview}


The HSBN vNext Beta service leverages Hyperledger Fabric v1.0 to provide a secure and permissioned blockchain network upon which authenticated members can easily define assets and create the business solutions for modifying and exchanging them.
{:shortdesc}

This service **greatly simplifies** the otherwise arcane and tedious process of bootstrapping an enterprise-grade blockchain network.  We provide the framework and tooling to invite members, aggregate various cryptographic identity materials, establish rules of governance and so on...  These complicated processes become intuitive and effortless.  In minutes you can spawn a fully-functional high security network with channels, policies and different flavors of business logic.  

**High availability** for the integral components of the network (peers, ordering service, Certificate Authority, chaincode) eliminates the crippling effects that can arise from single points of failure.  A built-in dashboard monitor allows for easy management of these components and provides a powerful mechanism to visualize assets and smart contracts.

The **modularity** of the Hyperledger Fabric v1.0 architecture and the distinct separation of network roles provides an infrastructure enabling scalability and high-performant compute.  

The checks and balances that occur throughout the lifecycle of a transaction ensure consistent and fully-vetted results; and ledgers constantly stay synchronized through an implementation of the well-known gossip protocol.  Identity and access control are easily enforced through **sign/verify** operations that occur perpetually throughout the network.  

**Governance tooling** is provided allowing for members to administer and manage the critical business rules for their network.  For example, you may wish to implement a policy defining how many members of a network must agree in order for a new member to join.  Or perhaps there is an asset that requires endorsement from every participant in order for a modification to take place.  Rules of governance are a fundamental necessity for any type of business network and they can oftentimes be extremely elaborate.  Governance tooling (e.g. policy editors) greatly simplifies this process.

The service runs in a **highly-secure and isolated** environment with no external access (including root access) to network components.  Data is encrypted in flight and at rest, and support available for hardware security modules allows for digital keys to be protected in accordance with industry regulations.  **Dedicated compute** is provided for network interactions, thereby ensuring high performance and data protection.  Hashing, sign/verify operations and component-to-component communications are accelerated thanks to advanced cryptography implementations.

**Figure 1** depicts an example of a deployed blockchain network consisting of four members (each owning two peers), a Certificate Authority responsible for distributing cryptographic identity material, and an Ordering Service defining policies and network participants.  The blue channel contains all four network members, whereas the yellow channel is restricted to Members 2, 3 and 4:

![Blockchain Network](images/blockchain_network.png "Example blockchain network")

*Figure 2. An example blockchain network consisting of four members leveraging channels to isolate data*

For complete details on all Hyperledger Fabric v1.0 features and functionality,
see the full release documentation at: http://hyperledger-fabric.readthedocs.io/en/latest/
