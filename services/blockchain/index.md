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
*Last updated: 28 April 2016*

With the {{site.data.keyword.blockchainfull}} service on Bluemix, you can quickly spin up a blockchain network and circumvent the complexities involved with manually creating a development environment.  Rather than creating and managing a network, developers can spend their time generating applications and working with chaincode.  The service is a peer-to-peer permissioned network built on top of the Linux Foundation's Hyperledger [fabric code](https://github.com/hyperledger/fabric).
{:shortdesc}

You can use a blockchain network to exchange financial records through a shared ledger. For more information about shared ledgers and business networks, see the [About {{site.data.keyword.blockchain}}](ibmblockchain_overview.html) topic.

To get started, follow these steps to create and deploy an unbound service instance of an {{site.data.keyword.blockchain}} network.  Once complete, you will have your own development environment with validating nodes and a security service.   From here, you can deploy chaincode, see results, and build your applications

1. From the landing page for the [{{site.data.keyword.blockchain}} DevOps Service](https://console.ng.bluemix.net/catalog/services/blockchain/), complete the following fields in the **Add Service** window.
  - Choose **dev** from the **Space** dropdown window.
  - Leave the **App** field as **Leave unbound**.
  - Change the **Service name** to **myblockchain123** without the quotation marks, or something unique to you.
  - Leave the **Credential name** field as its default value.
  - Leave the **Selected Plan** as its default value.
  - Click **CREATE**.
2.  You are now on the **Service Dashboard** screen for your new service.  From here you can **Manage** your instance of the network.
  - Click **LAUNCH** to see the blockchain monitor for your {{site.data.keyword.blockchain}} network.
3.  The blockchain monitor displays, network details, live logs, current ledger state, APIs, and chaincode templates.  Use the dashboard to do any of the following functions.
  - Access Discovery and API routes for the peers on your network.
  - View any currently running chaincode containers.
  - View real-time logs and troubleshoot chaincode that fails to execute.
  - View the world state for your ledger.
  - Access the Swagger UI and interact with your network via the REST API.
  - Deploy one of three available chaincode templates. 


# Related Links
{: #rellinks}
## Tutorials and Samples
{: #samples}
* [IBM Marbles Demo (GitHub)](https://github.com/IBM-Blockchain/marbles)
* [IBM Commercial Paper Demo (GitHub)](https://github.com/IBM-Blockchain/cp-web#readme)

## API Reference
{: #api}
* [API (Swagger UI)](https://ibmblockchainapi.mybluemix.net)
* [API (GitHub)](https://github.com/hyperledger/fabric/tree/master/docs/API)
* [IBM JS (Node.js SDK)](https://github.com/IBM-Blockchain/ibm-blockchain-js/blob/master/README.md)

## Related Links
{: #general}
* [Fabric Code](https://github.com/hyperledger/fabric)
* [Whitepaper](https://github.com/hyperledger/hyperledger/wiki/Whitepaper-WG)
* [Protocol Spec & Related Docs](https://github.com/hyperledger/fabric/tree/master/docs)
* [Linux Foundation](https://www.hyperledger.org/)
* [What's new in Bluemix Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}


<!-- 
[Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/) 
[IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs) -->
