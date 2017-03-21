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


# Consensus Test 4: Restart a Byzantine node
{: #pbft_test1}


Consensus Test 4 tests the PBFT protocol in a network scenario where one of the four nodes has come back online after being Byzantine: one node is restarted after going offline in an arbitrary and concurrent manner.

A previously Byzantine peer that has since rejoined a blockchain network will detect that its copy of the ledger lags behind that of the other peers. The lagging peer automatically updates its ledger by copying missing blocks from a peer with the current ledger; this process is referred to as state transfer.
{:shortdesc}

Note that this test case requires a large number of invoke operations. The peers notify each other of their current ledger states by sending internal *checkpoint* messages; the lagging peer determines that it is lagging by checking these messages.

Complete the following steps to test PBFT after restarting one Byzantine node:
1. Log in with your network user ID and password:  
   a. Run POST to ***VP0 URL***/registrar  
   b. Run Payload {“enrollId”: “**test\_user1**”, enrollSecret”: “**test\_user1\_enrollSecret**”}  
   c. The peer returns the payload
2. Verify that the network is up and running:  
   a. Query each peer for its blockchain height, specifying the URL for each peer:  
   b. Run **GET ***VP0 URL***/chain**  
   c. The command returns the payload:  
```json
{
"currentBlockHash": "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
"height": 1
}
```
   d. If this is the first operation against the blockchain, the chain height is 1 because the only block on the chain is the genesis block. The chain height increases as you append transactions to the ledger.
3. Deploy chaincode:  
   a. Run POST to ***VP0 URL***/chaincode  
   b. With payload:  
```json
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
   c. The peer returns the payload:
```json
{
"jsonrpc": "2.0",
"result": {
"status": "OK",
"message": "YOUR_CHAINCODE_ID"
},
"id": 1
}
```
   d. The request is transmitted to all four peers on the network. The peers run the PBFT consensus protocol, and agree to execute this request and store the result on their respective copies of the ledger.  
   e. All transactions are asynchronous. The return payload contains a chaincode hash, which you will use in later chaincode invocations. f. Completion of the deploy operation is dependent on factors such as processor speed and network latency.  
4. For test purposes, simulate peer VP2 going offline in a Byzantine (arbitrary and concurrent) manner, by manually stopping the node using the interface stop button.
5. Run an invoke operation on the chaincode:  
   a. For this example, chaincode_example02 moves 1 unit from a to b:  
   b. Run POST to ***VP0 URL***/chaincode with payload:
```json
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
  c. The peer returns the payload:
```json
{
"jsonrpc": "2.0",
"result": {
"status": "OK",
"message": "5a4540e5-902b-422d-a6ab-e70ab36a2e6d"
},
"id": 2
}
```
   d. The request is again transmitted to all four peers on the network. The peers run the PBFT consensus protocol, and agree to execute this request and append the result to their respective copies of the ledger.  
6. This request is also asynchronous. After a brief interval, check that the invoke operation has completed:  
   a. Run POST to ***VP0 URL***/chaincode with payload:
```json
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
"args":["a"]
}
“secureContext”: “***test\_user1***”
},
"id": 3
}
```
   b. The peer returns the payload:
```json
{
"jsonrpc": "2.0",
"result": {
"status": "OK",
"message": "999"
},
"id": 3
}
```
   c. As expected, the value of "a" is 1 or less.
7. Simulate peer **VP2** coming back online by manually restarting it, using the start button in the interface.
8. Send invoke operations to VP0.
9. Query the chaincode values of “a” on all four peers. All peers return the same value for “a".  (**Note**: The amount of time it takes for the restarted peer (**VP2**) to successfully execute the `stateTransfer` function is contingent upon a variety of parameters.  Recall that PBFT only requires 2f + 1 peers in order to reach consensus.  Therefore, it may take a large number of invokes for **VP2** to "catch up" due to the fact that it is not required for consensus in the current circumstances.  Visit the hyperledger/fabric [Protocol Specification](https://github.com/hyperledger/fabric/blob/v0.6/docs/protocol-spec.md#5-byzantine-consensus-1) from the Linux Foundation's Hyperledger Project for more information on this consensus implementation.)

(END of Consensus Test 4)
