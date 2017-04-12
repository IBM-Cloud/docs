---

copyright:
  years: 2017
lastupdated: "2017-03-17"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Application Development
{: #v10_dashboard}


Use the marbles02 example chaincode and the corresponding javascript app as a template for creating your own business solution.
{:shortdesc}

The app leverages the Node.js SDK APIs to interact with your provisioned network components and ultimately target your peer with transaction requests.  Locate the API endpoints for your peer, Certificate Authority and the network Ordering Service within the **Service Credentials** tab on the **Resources** screen of the Monitor and plug these strings into a configuration file accompanying your app.  Note, however, that if you want to target additional peers in the network (this will be the case when you require endorsement from a peer not belonging to your Org) then you will need to obtain the correct API endpoints for those peers.  You also need to store the CA cert for the other Org in order to verify responses returned to your application.  This information is not exposed in your **Resources** view, therefore you must contact the appropriate admin for the Bluemix Org and acquire this data in an out-of-band operation.  The ordering service URL is common across the network; you don't need any member-specific info for this component.  

Visit the [Marbles](https://github.com/IBM-Blockchain/marbles/tree/v3.0) GitHub repo for the source code and prerequisites; follow the README and bring your app to life.  

Explore the [SDK repo](https://github.com/hyperledger/fabric-sdk-node) to experiment with the end-to-end tests and gain a better understanding of the APIs.
