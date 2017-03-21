---

copyright:
  years: 2016
lastupdated: "2016-07-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Blockchain on z
{: #zblockchain}


You can use blockchain service in the Bluemix dedicated offering with z/OS to create private and secure digital assets, which can then be traded quickly and securely over permissioned networks.  *(Additional info as part of short description)*
{:shortdesc}


* Does the amount of content merit this being its own section?  Or do we want to leave it as an embedded topic under "About?"
* Expect information regarding PBFT, Security, Performance, Support.


## PBFT
{: #PBFT}

Practical Byzantine Fault Tolerance (PBFT) is a seminal consensus protocol that can be plugged in and configured per deployment. The ``obcpbft`` package is an implementation of the seminal [PBFT](http://dl.acm.org/citation.cfm?id=571640 "PBFT") consensus protocol, which provides consensus among validators despite a threshold of validators acting as _Byzantine_, i.e., being malicious or failing in an unpredictable manner. In the default configuration, both PBFT and Sieve are designed to run on at least *3t+1* validators (replicas), tolerating up to *t* potentially faulty (including malicious, or *Byzantine*) replicas. To learn more about core PBFT functions, see the [protocol specification](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric) section of the Linux Foundation's Hyperledger Project. 

Watch a [![preview](http://img.youtube.com/vi/EKa5Gh9whgU/0.jpg)](http://www.youtube.com/watch?v=EKa5Gh9whgU)

*(Need to indicate a practical reason why users need to know PBFT. What role PBFT plays in blockchain on z support and its relation to this support.)*


### Supported failure cases
{: #failure}

*What failure cases we support and what we don't support here.*

*(Barry Mosakowski/Raleigh/IBM or Tuan Dang/Raleigh/IBM can provide more details.)*

### Availability of the dedicated offering with z/OS
{: #Availability}

*Availability and expectations around availability based on PBFT testing.*

*(Need more details.)*

### Verifying basic functionality of PBFT
{: #Test PBFT}

*(Input from Gari. Need more details from Jason about how to perform the testing steps, including screenshots.)*

To verify basic PBFT functionality, take the following steps:

1. Submit transactions against one or more peers in the network.
2. Verify that at least *2f+1* (3 in this case) peers have the same state. *(How to verify? Need test case details.)*

  *An example using the REST API*
3. On the dashboard, click the button to stop peer 4. *(Use the "stop peer" functionality in the dashboard to stop peer 4. Need test case to describe the detailed operation.)*
4. Verify that the network continues processing. *(How to verify?)*
5. On the dashboard, click the button to stop peer 3.
6. Verify that the network stops processing.
7. On the dashboard, click the button to restart peer 3.

If peer 3 catches up and the network continues processing, you can use basic PBFT functions.

**Notes:**
* After restarting peer 3, you need to wait for the timeout before you submit new transactions to peer 3.

* Transactions, which are sent to active peers when the network stops processing, are buffered and submitted to the network after the network continues processing.

## Environment for blockchain on z
{: #z environment}

To use blockchain service in the Bluemix dedicated offering with z/OS, ensure that your environment meets the following requirements:

* Four peer networks that are running PBFT with membership services. To learn more about membership services, see the [protocol specification](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric) section of the Linux Foundation's Hyperledger Project. 
* An isolated network that does not have shared computers or memory.
* Isolated peers within the network.
* A system that is protected from cloud system administrators.

The blockchain monitor provides an overview of your blockchain environment and retrieve details about your network. To learn more about your blockchain environment and how to monitor it, see [Managing chaincode with the blockchain monitor](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchainmonitor.html) and [Sample apps and tutorials for blockchain](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchain_tutorials.html).

## Security

*Do not provide security information in the doc?*

## Performance

*Do not provide performance information in the doc?*

## Getting customer support

If you experience problems with blockchain service in the Bluemix dedicated offering with z/OS, follow the IBM Bluemix troubleshooting process. See [Troubleshooting](https://new-console.ng.bluemix.net/docs/troubleshoot/troubleshoot.html) for more information on how to get help.
