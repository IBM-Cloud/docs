---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Consensus Test 2: One Byzantine node
{: #pbft_test2}

Last updated: 4 August 2016
{: .last-updated}

Consensus Test 2 tests the PBFT protocol in a network scenario where one of the four nodes is Byzantine: one node has gone offline in an arbitrary and concurrent manner.
{:shortdesc}

The PBFT protocol guarantees that a blockchain network with N peers will continue to function if no more than (N-1)/3 peers go offline in a Byzantine (arbitrary and concurrent) manner. Your Bluemix blockchain environment has four peers, so if one peer crashes, the network will continue to run consensus and append transactions to the ledger. Applying the PBFT formula reveals that (4-1)/3 = 1 = number of Byzantine nodes, so transaction processing on the blockchain network continues.

Complete the following steps to test PBFT on a four-node network with one Byzantine node:
1.	Log in with your network user ID and password:  
    a.  Run POST to ***VP0 URL***/registrar  
    b.  Run Payload: {“enrollId”: “***test\_user1***”, enrollSecret”: “***test\_user1\_enrollSecret***”}
    c.  The peer returns with the payload
2.  Verify that the network is up and running:  
    a.  Query each peer for its blockchain height, specifying the URL for each peer:  
    b   Run GET ***VP0 URL***/chain  
    c.  The command returns payload:
      ```
      {
      "currentBlockHash":
      "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 1
      }
      ```  
    d.  If this is the first operation against the blockchain, the chain height is 1 because the only block on the chain is the genesis block. The chain height increases as transactions are appended to the ledger.
3.  Deploy chaincode:  
    a.  Run POST to ***VP0 URL***/chaincode  
    b.  With payload:  
      ```
      {
      "jsonrpc": "2.0",
      "method": "deploy",
      "params": {
      "type": 1,
      "chaincodeID":{
      "path":"github.com/hyperledger/fabric/examples/chaincode/go/chaincode_example02"
      },
      "ctorMsg": {
      "function":"init",
      "args": ["a", "1000", "b", "2000"]
      },
      "secureContext": "***test\_user1***"
      },
      "id": 1
      }
      ```  
    c.  The peer returns the payload:  
      ```
      {
      "jsonrpc": "2.0",
      "result": {
      "status": "OK",
      "message":
      "YOUR_CHAINCODE_ID_RETURNED_HERE"
      },
      "id": 1
      }
      ```  
    d. The request is transmitted to all four peers on the network. The peers run the PBFT consensus protocol, and agree to execute this request and store the result on their respective copies of the ledger.  
    e.  Note that all transactions are asynchronous. The return payload contains a chaincode hash, which you will use in later chaincode invocations.  
    f.  Completion of the deployment is dependent on factors such as processor speed and network latency.  
4.  For test purposes, simulate Byzantine node VP2 by manually stopping it, using the stop button in the interface.  (**Note**:  It may take between 30-60 seconds before your interface will reflect that VP2 has been "Stopped".)
5.  Run an invoke operation on the chaincode:  
    a.  For this example, chaincode_example02 moves 1 unit from a to b:  
    b.  Run POST to ***VP0 URL***/chaincode with payload:
      ```
      {
      "jsonrpc": "2.0",
      "method": "invoke",
      "params": {
      "type": 1,
      "chaincodeID":{
      "name":"YOUR_CHAINCODE_ID"
      },
      "ctorMsg": {
      "function":"invoke",
      "args": ["a", "b", "1"]
      }
      “secureContext”: “***test\_user1***”
      },
      "id": 2
      }
      ```
    c.  The peer returns the payload:
      ```
      {
      "jsonrpc": "2.0",
      "result": {
      "status": "OK",
      "message": "5a4540e5-902b-422d-a6ab-e70ab36a2e6d"
      },
      "id": 2
      }
      ```
    d.  The request is again transmitted to all four peers. The peers run the PBFT consensus protocol, and agree to execute this request and store the result on their respective copies of the ledger.
6.  This request is also asynchronous. After a brief interval, check that the invoke operation has completed, by querying the value of the “a” variable on the chaincode:  
    a.  Run POST to ***VP0 URL***/chaincode with payload:
      ```
      {
      "jsonrpc": "2.0",
      "method": "query",
      "params": {
      "type": 1,
      "chaincodeID":{
      "name":"YOUR_CHAINCODE_ID"
      },
      "ctorMsg": {
      "function":"query",
      "args": ["a"]
      }
      “secureContext”: “***test\_user1***”
      },
      "id": 3
      }
      ```
    b.  The peer returns with payload:
      ```
      {
      "jsonrpc": "2.0",
      "result": {
      "status": "OK",
      "message": "999"
      },
      "id": 3
      }
      ```
7.  As expected, the value of “a” is 1 less than when the chaincode was originally deployed.
8.  You can continue to issue additional invoke and query operations. The process is the same as in the previous steps.

(END of Consensus Test 2)
