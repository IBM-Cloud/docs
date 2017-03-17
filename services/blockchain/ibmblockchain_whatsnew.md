---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# What's new
{: #whatsnew}

The **HSBN vNext Beta** plan is built on a stable commit of the [Hyperledger Fabric v1.0](https://www.hyperledger.org/){:new_window} open source codebase. Hyperledger Fabric v1.0 implements a modular architecture that provides a resilient, secure and customizable platform for building enterprise blockchain networks.  
{: shortdesc}

The **HSBN vNext Beta** service moves beyond a single sandbox environment to deliver a distributed blockchain network with resource groups spanning across various Bluemix organizations.  See the [Overview](v10_netoverview.html) topic for more information on network architecture.

## New architecture in v1.0
{:why}

The Hyperledger Fabric architecture has evolved significantly in v1.0 to power enterprise-grade 
networks focused on security, scalability, confidentiality and performance.  Peers are split into 
two distinct runtimes - **endorsing** and **committing** - and responsibility for transaction ordering is
abstracted into a separate component.  Concerns of privacy and confidentiality are addressed through channels, which
provide data segregation.  Ledgers exist on a per-channel basis, so networks can be customized to 
support different combinations of bilateral, multilateral or even public transactions.

View the [Hyperledger architecture deep dive](http://hyperledgerdocs.readthedocs.io/en/latest/arch-deep-dive.html){: new_window} section for more information on network topology and interaction.

## Additional changes

The HSBN vNext Beta plan also includes the following changes:
* The [new dashboard](v10_dashboard.html) allows subscribers to create a blockchain
network, invite members, join another network, and manage resources and assets.
* The [new Marbles sample chaincode application for v1.0](https://github.com/hyperledger/fabric/blob/master/examples/chaincode/go/marbles02/marbles_chaincode.go){: new_window} enables experimentation with the latest codebase.
* The new [transaction flow](http://hyperledger-fabric.readthedocs.io/en/latest/txflow.html) in Hyperledger Fabric v1.0 ensures
data consistency and integrity by implementing multiple checkpoints throughout the transaction process.
