---

copyright:
  years: 2017
lastupdated: "2017-03-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Disclaimer
{: #etn_overview}

**ATTENTION:** You must review the following information before using any IBM Blockchain on Bluemix plan.

## IBM support statement

IBM has a long history of leadership in innovation, which continues with the IBM Blockchain on Bluemix offering plans. Blockchain is a rapidly-progressing technology that is projected to disrupt a number of industries, from finance to supply chain to logistics. Through various early adoption programs, IBM customers and business partners have been actively driving blockchain as an industrial solution. IBM Blockchain on Bluemix is one such program. **As with any new technology, IBM Blockchain on Bluemix users should be aware of the potential for rapid and fundamental change**.  
{:shortdesc}

The architecture behind IBM Blockchain is the Linux Foundation's Hyperledger Fabric project. Fabric is currently in *Active* status and undergoing continued development. Each open source community contribution improves Hyperledger Fabric, but can present adoption challenges. During the *Active* project cycle, clients can use Hyperledger Fabric v1.0 for network testing and simulation. **IBM cautions against defining or exchanging financial assets, or any assets of value, directly on any Hyperledger Fabric blockchain network**.  

## Open source statement

The **High Security Business Network (HSBN) vNext Beta** plan is built on the Linux Foundation's Hyperledger Fabric v1.0 open source code. The Starter Developer and High Security Business Network (HSBN) plans are built on Hyperledger Fabric v0.6 code. Hyperledger Project members, including IBM, continue to contribute to the source code, after which it is reviewed, vetted and tested by the community. Hyperledger Fabric v1.0 is currently *Active*; details on the *Active* status, and on the lifecycle of the Hyperledger Project, are available at https://wiki.hyperledger.org/community/project-lifecycle.  

## Chaincode support statement

The following coding practices are NOT supported on IBM Blockchain networks:

1. Using associative arrays with iteration (the order is randomized in Go).
2. Reading a list of items from a KVS table (the order is not guaranteed).
3. Writing thread-unsafe chaincode (query and invoke may be called in parallel).
4. Substituting global memory or cache storage for ledger state vars in chaincode.
5. Accessing external services, such as databases, directly from chaincode.
6. Using libraries or global variables that could introduce non-determinism (such as using "random" or "time").
7. Iterating using GetRows.  

In addition, the HSBN and Starter plans (Hyperledger Fabric v0.6) do not support non-deterministic chaincode, which introduces risk to data consistency and integrity; for details see [non-deterministic chaincode](nondeterministic.html).
