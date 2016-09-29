---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with {{site.data.keyword.blockchain}} (Beta)
{: #gettingstartedtemplate}
Last updated: 19 September 2016
{: .last-updated}

The {{site.data.keyword.blockchainfull}} service on Bluemix&reg; delivers a four-node development and test blockchain network for you, at the click of a button. Rather than creating a blockchain network from scratch, your developers can immediately start writing applications and deploying chaincode. The IBM Blockchain on Bluemix service is a peer-to-peer permissioned network, built on top of the [Hyperledger Fabric 0.5](https://github.com/hyperledger/fabric) code from the Linux Foundation's Hyperledger Project.
{:shortdesc}

Blockchain networks are used to securely and efficiently exchange and track digital assets, and to permanently record all transactions on the shared ledger. For details on blockchain, see the [About blockchain](ibmblockchain_overview.html) topic.

## Choose your network plan

You have a choice between two IBM Blockchain on Bluemix plans: the **Starter Developer Network** or the **High Security Business Network**. Use the comparison chart below to choose the right environment for you.

![](images/red_alert.png)  **The High Security Business Network** plan is a limited Beta offering; to select this plan, you must first request preapproval at [IBM Blockchain on IBM Bluemix](http://www-stage.watson.ibm.com/files/blockchain/bluemix.html).

| Bluemix Service Plan:      | Starter Developer Network       | High Security Business Network  |
| ------------------------- |:--------------------------:|:-----:|
| Requires IBM preapproval: | No | Yes |
| Purpose:  |  Development, and test levels of security, performance and availability |  Simulate an enterprise network, and test levels of security, performance and availability |
| Nodes:    | 4 nodes + Certificate Authority     | 4 nodes + Certificate Authority |
| [Dashboard Monitor:](ibmblockchainmonitor.html) | Yes | Yes |
| Confidential Transactions: | Yes | Yes |
| [Consensus:](etn_pbft.html) | PBFT | PBFT |
| Environment:     | Shared multi-tenant | Isolated single tenant |
| [IBM Secure Service Container:](etn_ssc.html) | No | Yes |

## Launch your network plan

Use the following steps to create and deploy an unbound service instance of your blockchain network.  Your network includes a development environment with validating nodes and a security service, and  enables you to deploy chaincode, view logs and build applications:

1. From the [{{site.data.keyword.blockchain}} Service ](https://console.ng.bluemix.net/catalog/services/blockchain/) page, complete the **Add Service** form  in the right pane:
  - **Space:** Select **dev**.
  - **App:** Select either **Leave unbound**, or to bind your service to one of your Bluemix.org applications, **Select an application".
  - **Service name:** Enter a unique name or value, such as, **Blockchain Test Net123**.
  - **Credential name:** Leave the default value.
  - Selected Plan: Choose **Starter Developer plan** or **High Security** ( ![](images/green_dot.png) with preapproval).
  - Click the **CREATE** button.
2.  You are now on the **Service Dashboard** screen for your new service. From here, you can **Manage** your instance of the network; click **LAUNCH** to use your blockchain monitor.
3.  The blockchain monitor displays network details, live logs, current ledger state, APIs and chaincode templates. Use the dashboard for any of the following functions:
  - Access Discovery and API routes for network peers.
  - View any running chaincode containers.
  - View real-time logs and troubleshoot chaincode.
  - View the world state for the ledger.
  - Access the Swagger UI and interact with your network via the REST API.
  - Deploy one of the three chaincode examples.


# Related Links
{: #rellinks}
## Tutorials and Samples
{: #samples}
* [IBM Marbles Demo (GitHub)](https://github.com/IBM-Blockchain/marbles)
* [IBM Commercial Paper Demo (GitHub)](https://github.com/IBM-Blockchain/cp-web#readme)
* [IBM Car Lease Demo (Github)](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md)
* [Art Auction Demo (Github)](https://github.com/ITPeople-Blockchain/auction)

## API Reference
{: #api}
* [Swagger UI](https://obc-service-broker-staging.stage1.mybluemix.net/swagger)
* [Hyperledger fabric API (GitHub)](https://github.com/hyperledger/fabric/tree/master/docs/API)
* [HFC SDK for Node.js](https://github.com/hyperledger/fabric/tree/master/sdk/node)

## Related Links
{: #general}
* [Fabric Code](https://github.com/hyperledger/fabric)
* [Whitepaper](https://github.com/hyperledger/hyperledger/wiki/Whitepaper-WG)
* [Protocol Spec & Related Docs](https://github.com/hyperledger/fabric/tree/master/docs)
* [StackOverflow](http://stackoverflow.com/questions/tagged/hyperledger)
* [Linux Foundation](https://www.hyperledger.org/)
* [What's new in Bluemix Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}


<!--
[Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/)
[IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs) -->
