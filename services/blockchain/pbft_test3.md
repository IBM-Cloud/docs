---

copyright:
  years: 2016
lastupdated: "2016-08-04"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Consensus Test 3: Two Byzantine nodes
{: #pbft_test2}


Consensus Test 3 tests the PBFT consensus protocol in a network scenario where two of the four nodes are Byzantine: two nodes have gone offline in an arbitrary and concurrent manner.
{:shortdesc}

The PBFT protocol guarantees that a blockchain network with N peers will continue to function if no more than (N-1)/3 peers go offline in a Byzantine (arbitrary and concurrent) manner. Your bluemix blockchain network has four peers, so if two peers crash, the network will NOT execute any transactions or append any blocks to the ledger. Applying the PBFT formula reveals that (4-1)/3 = 1 < the number of Byzantine nodes (2), so transaction processing stops.

Complete the following steps to test PBFT on a four-node network with two Byzantine nodes:
1.  Log in with your network user ID and password:  
    a.  Run POST to ***VP0 URL***/registrar  
    b.  Run Payload {“enrollId”: “***test\_user1***”, enrollSecret”: “***test\_user1\_enrollSecret***”}  
    c.  The peer returns the payload
2.  Verify that the network is up and running:  
    a.  Query each peer for its blockchain height, specifying the URL for each peer:  
    b.  Run GET ***VP0 URL***/chain  
    c.  The command returns the payload:
      ```
      {
      "currentBlockHash": "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
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
      "message": "YOUR_CHAINCODE_ID"
      },
      "id": 1
      }
      ```
    d.  The request is transmitted to all four peers on the network. The peers run the PBFT consensus protocol, and agree to execute this request and append the result to their respective copies of the ledger.  
    e.  Note that all transactions are asynchronous. The return payload contains a transaction ID only, which you can use later for querying the result.
4.  For test purposes, simulate nodes VP2 and VP3 going offline, in a Byzantine (arbitrary and concurrent) manner, by manually stopping them with the interface stop button.  (**Note**:  It may take between 30-60 seconds before your interface will reflect that VP2 and VP3 have been "Stopped".)
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
    d.  Because the network fails the f=(N-1)/3 PBFT test, the invoke operation is accepted as input but is not executed, and nothing is appended to the shared ledger.
6.  Verify that the invoke operation has not been executed, by querying the value of the “a” variable:  
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
    b.  The peer returns the payload:
      ```
      {
      "jsonrpc": "2.0",
      "result": {
      "status": "OK",
      "message": "1000"
      },
      "id": 3
      }
      ```
    c.  Note that the value of “a” remains unchanged.

  (END of Consensus Test 3)
