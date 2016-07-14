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
*Last updated: 14 July 2016*
{: .last-updated}

With the {{site.data.keyword.blockchainfull}} service on Bluemix, you can quickly spin up a blockchain network and circumvent the complexities involved with manually creating a development environment.  Rather than creating and managing a network, developers can spend their time generating applications and working with chaincode.  The service is a peer-to-peer permissioned network built on top of the Linux Foundation's Hyperledger [fabric code](https://github.com/hyperledger/fabric).
{:shortdesc}

You can use a blockchain network to exchange digital assets through a shared ledger. For more information about shared ledgers and business networks, see the [About](ibmblockchain_overview.html) blockchain topic.

There are currently two versions available for the blockchain service - **Starter Developer** and **High Security Business Network**.  Use the comparisons in the table below to choose the right environment for your needs.

![](images/red_alert.png) **You must be approved by IBM to receive access to the High Security plan.**  Visit [IBM Blockchain on IBM Bluemix](http://www-stage.watson.ibm.com/files/blockchain/bluemix.html) and follow the steps to request a provisioning of the High Security network.

|                           | Starter Developer               | High Security Business Network  |
| ------------------------- |:--------------------------:|:-----:|
| Purpose   |  development/experimentation and test levels of security, performance and availability  |  simulate enterprise network and test levels of security, performance and availability |
| Environment     | shared multi-tenant in SoftLayer| isolated single tenant in LinuxONE on z |
| Nodes     | 4 nodes + Certificate Authority     | 4 nodes + Certificate Authority, running in a [secure services container](etn_ssc.html)|
| Confidential Transactions | Yes | Yes |
| Consensus  |  [PBFT](etn_pbft.html)    |    [PBFT](etn_pbft.html) |
| Dashboard Monitor | Same | Same |
 


To get started, follow these steps to create and deploy an unbound service instance of a {{site.data.keyword.blockchain}} network.  Once complete, you will have your own development environment with validating nodes and a security service. From there, you can deploy chaincode, see results, and build your applications:

1. From the landing page for the [{{site.data.keyword.blockchain}} DevOps Service](https://console.ng.bluemix.net/catalog/services/blockchain/), complete the following fields in the **Add Service** dialog on the far right of your screen:
  - Choose **dev** from the **Space** drop-down window.
  - Leave the **App** field as **Leave unbound**.
  - Change the **Service name** to a name or value unique to you.  For example, **MyBlockchainABC123**.
  - Leave the **Credential name** field as its default value.
  - Choose **Starter Developer Plan** or **High Security** ( ![](images/green_dot.png) if approved) under the **Selected Plan** field.
  - Click **CREATE**.
2.  You are now on the **Service Dashboard** screen for your new service.  From here you can **Manage** your instance of the network:
  - Click **LAUNCH** to see the blockchain monitor for your {{site.data.keyword.blockchain}} network.
3.  The blockchain monitor displays network details, live logs, current ledger state, APIs, and chaincode templates.  Use the dashboard for any of the following functions:
  - Access Discovery and API routes for the peers on your network.
  - View any currently-running chaincode containers.
  - View real-time logs and troubleshoot chaincode that fails to execute.
  - View the world state for your ledger.
  - Access the Swagger UI and interact with your network via the REST API.
  - Deploy one of three available chaincode examples.


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
* [Enhanced Node.js SDK](https://github.com/hyperledger/fabric/tree/master/sdk/node)

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
