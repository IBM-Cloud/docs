---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Further testing
{: #etn_next}

*Last updated: 14 July 2016*
{: .last-updated}

The following tests were run in the High Security Business Network environment to test chaincode function, ledger, long runs, concurrency and complex transactions. (Note: some of these tests are repeated in the [Node.js SDK](etn_txn.html) and [Testing consensus and availability](etn_pbft.html) sections.)

{:shortdesc}

1. Chaincode function - Chaincode interfaces were exercised to ensure `Deploy`, `Invoke` and `Query` transactions work properly using the REST API and CLI. Both the REST API and CLI were utilized to test all endpoint functions, including Block, Blockchain, Chaincode, Network, Registrar, and Transactions, as described in the Hyperledger Protocol Specification.
2. Ledger - The creation of 20,000 records of 1K payloads in the ledger based on different driving environments. The tests included:
	- 1 client creating 20K records in a serialized manner.
	- 2 clients connecting to the same peer concurrently.  Each creating 10K records.
	- 2 clients connecting to different peers concurrently.  Each creating 10K records.
	- 4 clients connecting to the same peer concurrently.  Each creating 5K records.
	- 4 clients connecting to 4 different peers concurrently.  Each creating 5K records.
	- 2 clients connecting to the same peer concurrently.  Each creating 500K records.
	- 1 client creating 2.8 million records using 1K payload.  Only one peer used for this case.  
3. Long Runs - This testing was done by sending invokes, chain height and queries across multiple nodes for 72 hours with 1KB payloads.
4. Node.js SDK - The enhanced Node.js SDK was used to register and enroll users, and perform deploy, invokes, and query on both a peer in development mode (starting peer with: `peer node start –peer-chaincodedev`) and network mode (starting peer with: `peer node start`).
5. Concurrency - This testing was done by sending 1000 concurrent invokes to each of the four peers for a duration of 10 minutes, with 1KB payloads, and measuring chain height and querying ledger state.
6. Complex Transactions - This testing was done by randomly submitting a mix of queries and invokes of various payload sizes ranging from 10k to 500K to the different peers for a duration of 10 minutes. The chain height and query of world state were measured for consistency.
