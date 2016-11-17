---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# What you need to know
{: #etn_overview}
Last updated: 10 November 2016
{: .last-updated}

**ATTENTION:** You must review the following information before using either IBM Blockchain on Bluemix plan: Starter Developer (Beta) or High Security Business Network (GA).
<br><br>

## IBM support statement

IBM has a long history of leadership in innovation, which continues with the latest IBM Blockchain offerings. Blockchain is a rapidly-progressing technology that is projected to disrupt a number of industries, from finance to logistics. Through various early adoption programs, IBM customers and business partners are already influencing the future direction of blockchain. IBM Blockchain on Bluemix is one such program. **As with any new technology, IBM Blockchain on Bluemix users should be prepared for rapid and fundamental changes**.  
{:shortdesc}

The architecture behind IBM Blockchain is the Linux Foundation's Hyperledger Project. The Hyperledger Fabric is an open source project under active development, currently in *Incubation* status. Each open source community contribution makes the Hyperledger Fabric more robust, but can present adoption challenges. During the *Incubation* cycle, clients can use Hyperledger Fabric v0.6 for network testing and simulation, but **IBM cautions against running financial assets of value directly on a Hyperledger Fabric v0.6 (or earlier) blockchain network**.  
<br>

## Open source statement

IBM Blockchain on Bluemix&mdash;both the Starter Developer plan and the High Security Business Network plan&mdash;use the Linux Foundation's Hyperledger Fabric v0.6.1 open source code. Hyperledger Project members, including IBM, contribute code to the fabric, after which it is reviewed, vetted and tested by the community. Hyperledger Fabric v0.6.1 is currently in the *Incubation* state; details on the *Incubation* state, and on the entire lifecycle for the Hyperledger Project, are available at https://github.com/hyperledger/hyperledger/wiki/Project-Lifecycle.
<br><br>

## Chaincode support statement

IBM Blockchain does not support non-deterministic chaincode, which introduces risk to data consistency and integrity on any blockchain network. Before deploying new chaincode to your IBM Blockchain on Bluemix network, review the details on [non-deterministic chaincode](nondeterministic.html).

In addition to [non-deterministic chaincode](nondeterministic.html), the following coding practices are NOT supported on IBM Blockchain networks:

1. Using associative arrays with iteration (the order is randomized in Go).
2. Reading a list of items from a KVS table (the order is not guaranteed).
3. Writing thread-unsafe chaincode (query and invoke may be called in parallel).
4. Substituting global memory or cache storage for ledger state vars in chaincode.
5. Accessing external services, such as databases, directly from chaincode.
6. Using libraries or global variables that could introduce non-determinism (such as using "random" or "time").
7. Iterating using GetRows.  

See the examples library for supported chaincode examples; the directory contains samples written in Go and Java.
<br><br>

## Migration considerations

There are several programming changes that need to be implemented in order for code developed on Hyperledger Fabric v0.5-developer-preview to function with the Bluemix backend (built against Hyperledger Fabric v0.6.1).  See the [Migration considerations](http://hyperledger-fabric.readthedocs.io/en/v0.6/v0.6_migration/) section in the Hyperledger Fabric documentation for more details on new features and code changes.  

## HSBN known issues

1. When using the High Security Business Network, which utilizes Hyperledger Fabric v0.6.1, resetting the network periodically during a development phase is suggested if there have been more than roughly fifty chaincode deployments.  Resetting the network removes deployed chaincode and the data that has been collected.  This provides a chance to remove older chaincode that has been superseded by improvements made during an iterative development phase.  If you are in a post-development phase, then the number of chaincode deployments should be monitored to leave capacity for the most important chaincode.
2. Sporadic "503 Service Unavailable" and "502 Bad Gateway" errors received when performing a status query of the network and the peers.
3. Potential for "Server.Serve failed to complete security handshake" messages in the logs for vp1. This is a non-fatal error and not related to network operation.
4. The **Service Credentials** might not self-populate; in this case, generate the credentials as follows:

 a) From your Service Dashboard, click the **Service Credentials** tab:

  ![Service Credentials HSBN](images/hsbn.png "Service Credentials HSBN")

 b) From the **Service Credentials** tab, click the button for **New Credential**:

  ![New Credential HSBN](images/hsbn1.png "New Credential HSBN")

c) A new window titled **Add New Credential** is displayed; click the **Add** button at the bottom of this window:

  ![Add New Credential HSBN](images/hsbn2.png "Add New Credential HSBN")

 d) Now your screen should look similar to the following example. Clicking on **View Credentials** will reveal a JSON payload containing the Service Credentials for your HSBN instance.  

  ![Credentials Generated HSBN](images/hsbn3.png "Credentials Generated")



## Getting help

For support and help with your IBM Blockchain on Bluemix network, see [Getting support](ibmblockchain_support.html).
