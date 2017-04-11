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


# Additional testing
{: #etn_next}


The following tests were run in the High Security Business Network environment (unless otherwise noted) to test chaincode function, ledger, long runs, concurrency and complex transactions.  The validators and membership services nodes were run as VM guests within the secure services container on the LinuxONE OS.  The values used below were chosen based on customer input and are not to be mistaken for maximum values. (Note: some of these tests are repeated in the [Node.js SDK](etn_txn.html) and [Testing consensus and availability](etn_pbft.html) sections.)

{:shortdesc}

1. Chaincode function - Chaincode interfaces were exercised to ensure `Deploy`, `Invoke` and `Query` transactions work properly using the REST API and CLI. Both the REST API and CLI were utilized to test all endpoint functions, including Block, Blockchain, Chaincode, Network, Registrar, and Transactions, as described in the Hyperledger Protocol Specification.
2. Ledger - The creation of 20,000 records of 1K payloads in the ledger based on different driving environments. The tests included one client creating 20K records in a serialized manner.
3. Long Runs - This testing was done by sending invokes, chain height and queries across multiple nodes for 72 hours using the example02 demo chaincode.
4. Node.js SDK - The enhanced Node.js SDK was used to register and enroll users, and perform deploy, invokes, and query on both a peer in development mode (starting peer with: `peer node start –peer -chaincodedev`) and network mode (starting peer with: `peer node start`).
5. Basic concurrency - This testing was done by sending concurrent invokes to each of the four peers for a duration of 10 minutes, with 1KB payloads, and measuring chain height and querying ledger state.
6. Complex Transactions - This testing was done by randomly submitting a mix of queries and invokes of various payload sizes, ranging from 10k to 500K, to peers for a duration of 10 minutes. The chain height and query of world state were measured to ensure synchronization of the shared ledger across network peers.
