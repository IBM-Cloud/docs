---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Verified performance
{: #etn_performance}


The following behaviors have been tested and verified by IBM. The results were achieved on a High Security network, unless otherwise noted:
{:shortdesc}

### Performance/Stress

This testing was done to obtain the TPS (transactions per-second) of invokes and queries under short duration test intervals - 10 minutes, and long duration test intervals - 60 minutes, with PBFT / Security & Privacy enabled.  Performance can vary based on the environment, application type, configuration/security settings, transaction batch size, and other factors.  (**Note:** these metrics were achieved on a multi-tenant distributed network.)

- chaincode example02
- logging level: error
- thread number: 100
- batch size: 1000
- duration: 10 min. and 60 min.
- transaction types: invoke a->b, invoke b->a, then repeat & query a, query b, then repeat

| Transaction type | Number of peers | Number of threads | Run duration (min) | Transactions per second |
| ---------- |:-------:|:-----:|:------:|:------:|
| invokes   |  4  | 100 | 10 | 72  |
| invokes   |  4  | 100 | 60 | 66  |
| queries   |  4  | 100 | 10 | 252 |
| queries   |  4  | 100 | 60 | 248 |

### Resiliency/Consensus

This testing was done to ensure the stability and resiliency of PBFT when Byzantine faults occur.  The tests included:

- Stopping 1 node and continue sending deploy, invoke, and query transactions.  The network continues to operate. Performed on each node in the network.
- Stopping 2 nodes, the network halts due to a lack of consensus.
- Restarting one of the nodes stopped in the previous test.  The network resumes and the node that restarted syncs with the other validating peers. For detailed steps on PBFT testing, see the [Testing consensus and availability](etn_pbft.html) topic.

Continue to the [Additional testing](etn_next.html) topic for additional tests and verified functionality.  
