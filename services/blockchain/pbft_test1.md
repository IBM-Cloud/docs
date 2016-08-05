---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Consensus Test 1: No Byzantine nodes
{: #pbft_test1}
Last updated: 4 August 2016
{: .last-updated}

Consensus Test 1 tests the PBFT consensus protocol in a blockchain network scenario where none of the four nodes are Byzantine: none of the nodes have gone offline in an arbitrary and concurrent manner.
{:shortdesc}

After launching your Developer Network or High Security Business Network, complete the following steps to test PBFT with no Byzantine nodes:

(**Note**:  The code snippets and instructions make use of various symbolic values.  **VPO URL**, **"test_user1"**, **"test_user1_enrollSecret"**, and **YOUR_CHAINCODE_ID** are simply placeholders.  Access the literal values for your **Service Credentials** and **VP URLs** from the **APIs** tab on your network console.  The value for **YOUR_CHAINCODE_ID** will appear on the **Network** tab once you have deployed a piece of chaincode to the network.  Additonally, the hash values in your JSON response payloads will be different than these examples.)

1.	Log in with your network user ID and password:  
    a.  Run POST to ***VP0 URL***/registrar  
    b.	Run Payload {“enrollId”: “test_user1”, enrollSecret”: “test_user1_enrollSecret”}  
    c.	The peer returns the payload
2.	Verify that the network is up and running:  
    a.	Query each peer for its blockchain height, specifying the URL for each peer:  
    b.  Run GET ***VP0 URL***/chain  
    c.  The peer returns the payload:
   ```
   {
     "currentBlockHash":
     "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
     "height": 1
   }
   ```
    d.	If this is the first operation against the blockchain, then the chain height is 1, because the only block on the chain is the genesis block. The chain height increases as transactions are appended to the ledger.
3.	Deploy chaincode:  
    a.	Run POST to ***VP0 URL***/chaincode  
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
       "52b0d803fc395b5e34d8d4a7cd69fb6aa00099b8fabed83504ac1c5d61a425aca5b3ad3bf96643ea4fdaac132c417c37b00f88fa800de7ece387d008a76d3586"
       },
       "id": 1
       }
       ```
    d. The request is transmitted to all four peers on the network. The peers run the PBFT consensus protocol, and agree to execute this request and store the result on their respective copies of the ledger.  
    e.	Note that all transactions are asynchronous. The return payload contains a chaincode hash, which you will use in later chaincode invocations.
4.  After a brief interval, check that the deploy request has completed:  
    a.  Query each peer for its blockchain height, specifying the URL for each peer in turn:  
    b.  Run GET ***VP0 URL***/chain  
    c.  The command returns the payload:
      ```
      {
      "currentBlockHash":
      "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 2
      }
      ```
    d.  Completion of the deploy operation is dependent on factors such as processor speed and network latency.
5.  Now that you have deployed chaincode, you can invoke operations on the chaincode:  
    a.  Using chaincode_example02, move 1 unit from a to b:  
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
6.  The previous request is asynchronous. After a brief interval, check that the invoke operation has completed by querying the value of the “a” variable from the chaincode:  
    a.  POST to ***VP0 URL***/chaincode with payload:
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
      "message": "999"
      },
      "id": 3
      }
      ```
    c.  As expected, the value of "a" is 1 less than when the chaincode was originally deployed.  Recall that the original value assigned to "a" was 1,000 and the original value assigned to "b" was 2,000.  The invocation request which you triggered in Step 5 results in one unit being transferred from "a" to "b".
7.  You can continue to issue invoke and query operations. The process is the same as in the previous steps.

  (END of Consensus Test 1)
