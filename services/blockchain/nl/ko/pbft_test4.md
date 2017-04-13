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


# 합의 테스트 4: 비잔틴 노드 다시 시작
{: #pbft_test1}


합의 테스트 4는 비잔틴이 된 후에 4개 노드 중 하나가 온라인 상태로 돌아온 네트워크 시나리오에서 PBFT 프로토콜을 테스트합니다. 하나의 노드는 임의의 동시 방식으로 오프라인 상태가 된 후에 다시 시작됩니다. 

나중에 블록체인 네트워크를 재결합한 이전 비잔틴 피어는 원장의 해당 사본이 기타 피어의 경우보다 지연됨을 발견합니다. 지연 중인 피어는 현재 원장의 피어에서 누락된 블록을 복사하여 해당 원장을 자동으로 업데이트합니다. 이 프로세스를 상태 전이라고 합니다.
{:shortdesc}

참고로, 이 테스트 케이스에서는 많은 수의 호출 오퍼레이션이 필요합니다. 피어는 내부 *체크포인트* 메시지를 전송하여 현재 원장 상태를 서로 간에 알립니다. 지연 중인 피어는 이러한 메시지를 확인하여 현재 지연 중임을 판별합니다. 

다음 단계를 완료하여 하나의 비잔틴 노드를 다시 시작한 후에 PBFT를 테스트하십시오. 
1. 네트워크 사용자 ID 및 비밀번호로 로그인하십시오.   
   a. ***VP0 URL***/registrar에 대해 POST를 실행하십시오.   
   b. 페이로드 {“enrollId”: “**test\_user1**”, enrollSecret”: “**test\_user1\_enrollSecret**”}를 실행하십시오.   
   c.	피어가 페이로드를 리턴합니다. 
2. 네트워크가 시작되어 실행 중인지 확인하십시오.   
   a.	각 피어에 대한 URL을 지정하여 각 피어마다 해당 블록체인 높이를 조회하십시오.   
   b. **GET ***VP0 URL***/chain**를 실행하십시오.   
   c. 명령은 페이로드를 리턴합니다.   
```json
{
"currentBlockHash": "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
"height": 1
}
```
   d. 블록체인에 대한 첫 번째 오퍼레이션인 경우, 체인의 유일한 블록이 원천 블록이므로 체인 높이는 1입니다. 트랜잭션이 원장에 추가됨에 따라 체인 높이가 증가됩니다.
3. 체인코드 배치:   
   a.	***VP0 URL***/chaincode에 대해 POST를 실행하십시오.   
   b. 페이로드 사용:  
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
   c. 피어가 페이로드를 리턴합니다.
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
   d. 요청이 네트워크의 모든 4개의 피어로 전송됩니다. 피어는 PBFT 합의 프로토콜을 실행하고 이 요청의 실행에 동의하며 원장의 개별 사본에 결과를 저장합니다.   
   e. 모든 트랜잭션은 비동기입니다. 리턴 페이로드에는 후속 체인코드 호출에서 사용될 체인코드 해시가 포함되어 있습니다.
   f. 배치 오퍼레이션의 완료는 프로세서 속도와 네트워크 대기 시간 등의 요인에 따라 결정됩니다.   
4. 테스트 용도로, 인터페이스 중지 단추를 사용하여 수동 중지하여 비잔틴(임의의 동시) 방식으로 오프라인 상태가 되는 피어 VP2를 시뮬레이션하십시오. 
5. 체인코드에서 호출 오퍼레이션을 실행하십시오.   
   a. 이 예제의 경우, chaincode_example02는 a에서 b로 1 단위 이동합니다.   
   b. 페이로드로 ***VP0 URL***/chaincode에 대해 POST를 실행하십시오. 
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
  c. 피어가 페이로드를 리턴합니다.
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
   d. 요청이 다시 네트워크의 모든 4개의 피어로 전송됩니다. 피어는 PBFT 합의 프로토콜을 실행하고 이 요청의 실행에 동의하며 원장의 개별 사본에 결과를 추가합니다.   
6. 이 요청 또한 비동기입니다. 잠시 후에 호출 오퍼레이션이 완료되었는지 확인하십시오.   
   a. 페이로드로 ***VP0 URL***/chaincode에 대해 POST를 실행하십시오. 
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
   b. 피어가 페이로드를 리턴합니다.
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
   c. 예상한 대로, "a" 값은 1 이하입니다.
7. 인터페이스의 시작 단추를 사용하여 수동으로 다시 시작하지 않고 다시 온라인 상태가 되는 피어 **VP2**를 시뮬레이션하십시오. 
8. 호출 오퍼레이션을 VP0에 전송하십시오. 
9. 모든 4개 피어에서 “a”의 체인코드 값을 조회하십시오. 모든 피어는 “a"에 대해 동일 값을 리턴합니다. (**참고**: 다시 시작된 피어(**VP2**)가 `stateTransfer` 함수를 성공적으로 실행하는 데 걸리는 시간의 양은 다양한 매개변수에 달려 있습니다. 참고로, 합의에 도달하기 위해 PBFT에서는 2f + 1개 피어만 필요합니다. 따라서 현재 상황에서 합의에 필요하지 않다는 사실 때문에 **VP2**의 "캐치업"을 위해 많은 수의 호출이 필요할 수 있습니다. 이 합의 구현에 대한 자세한 정보는 Linux Foundation의 Hyperledger 프로젝트에서 Hyperledger/패브릭 [프로토콜 스펙](https://github.com/hyperledger/fabric/blob/v0.6/docs/protocol-spec.md#5-byzantine-consensus-1)을 방문하십시오.) 

(합의 테스트 4 종료)
