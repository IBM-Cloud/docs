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
Last updated: 13 October 2016
{: .last-updated}

**ATTENTION:** You must review the following information before using either IBM Blockchain on Bluemix plan: Starter Developer (Beta) or High Security Business Network (GA).
<br><br>

## IBM support statement

IBM has a long history of leadership in innovation, which continues with the latest IBM Blockchain offerings. Blockchain is a rapidly-progressing technology that is projected to disrupt a number of industries, from finance to logistics. Through various early adoption programs, IBM customers and business partners are already influencing the future direction of blockchain. IBM Blockchain on Bluemix is one such program. **As with any new technology, IBM Blockchain on Bluemix users should be prepared for rapid and fundamental changes**.  
{:shortdesc}

The architecture behind IBM Blockchain is the Linux Foundation's Hyperledger Project. The Hyperledger Fabric is an open source project under active development, currently in *Incubation* status. Each open source community contribution makes the Hyperledger Fabric more robust, but can present adoption challenges. During the *Incubation* cycle, clients can use Hyperledger Fabric v0.5 for network testing and simulation, but **IBM cautions against running financial assets of value directly on a Hyperledger Fabric v0.5 blockchain network**.  
<br>

## Open source statement

IBM Blockchain on Bluemix&mdash;both the Starter Developer plan and the High Security Business Network plan&mdash;use the Linux Foundation's Hyperledger Fabric v0.5 open source code. Hyperledger Project members, including IBM, contribute code to the fabric, after which it is reviewed, vetted and tested by the community. Hyperledger Fabric v0.5 is currently in the *Incubation* state; details on the *Incubation* state, and on the entire lifecycle for the Hyperledger Project, are available at https://github.com/hyperledger/hyperledger/wiki/Project-Lifecycle.
<br><br>

## Chaincode support statement

IBM Blockchain does not support [non-deterministic chaincode](ibmblockchain_tutorials.html#ndcc), which introduces risk to data consistency and integrity on any blockchain network. Before deploying new chaincode to your IBM Blockchain on Bluemix network, review the details on [non-deterministic chaincode](ibmblockchain_tutorials.html#ndcc).

In addition to [non-deterministic chaincode](ibmblockchain_tutorials.html#ndcc), the following coding practices are NOT supported on IBM Blockchain networks:

1. Using associative arrays with iteration (the order is randomized in Go).
2. Reading a list of items from a KVS table (the order is not guaranteed).
3. Writing thread-unsafe chaincode (query and invoke may be called in parallel).
4. Substituting global memory or cache storage for ledger state vars in chaincode.
5. Accessing external services, such as databases, directly from chaincode.
6. Using libraries or global variables that could introduce non-determinism (such as using “random” or "time").
<br><br>

## Getting help

For support and help with your IBM Blockchain on Bluemix network, see [Getting support](ibmblockchain_support.html).
