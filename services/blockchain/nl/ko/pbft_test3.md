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


# 합의 테스트 3: 두 개의 비잔틴 노드
{: #pbft_test2}


합의 테스트 3은 4개 중 2개가 비잔틴 노드인 네트워크 시나리오에서 PBFT 합의 프로토콜을 테스트합니다. 2개의 노드는 임의의 동시 방식으로 오프라인 상태가 되었습니다.
{:shortdesc}

PBFT 프로토콜은 (N-1)/3 피어 이하가 비잔틴(임의의 동시) 방식으로 오프라인 상태가 되는 경우에 N 피어의 블록체인 네트워크가 계속 작동함을 보장합니다. Bluemix 블록체인 네트워크에 4개의 피어가 있으므로, 2개의 피어가 충돌하면 네트워크가 트랜잭션을 실행하거나 원장에 블록을 추가하지 않습니다. PBFT 공식을 적용하면 (4-1)/3 = 1 < 비잔틴 노드 수(2)임이 드러납니다. 따라서 트랜잭션 처리가 중지됩니다. 

다음 단계를 완료하여 비잔틴 노드가 두 개인 4노드 네트워크에서 PBFT를 테스트하십시오. 
1.  네트워크 사용자 ID 및 비밀번호로 로그인하십시오.   
a. ***VP0 URL***/registrar에 대해 POST를 실행하십시오.   
b. 페이로드 {“enrollId”: “***test\_user1***”, enrollSecret”: “***test\_user1\_enrollSecret***”}을 실행하십시오.   
c. 피어가 페이로드를 리턴합니다. 
2.  네트워크가 시작되어 실행 중인지 확인하십시오.   
a. 각 피어에 대한 URL을 지정하여 각 피어마다 해당 블록체인 높이를 조회하십시오.   
b. GET ***VP0 URL***/chain을 실행하십시오.   
c. 명령에서 페이로드를 리턴합니다. 
      ```
      {
      "currentBlockHash": "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 1
      }
      ```
d. 블록체인에 대한 첫 번째 오퍼레이션인 경우, 체인의 유일한 블록이 원천 블록이므로 체인 높이는 1입니다. 트랜잭션이 원장에 추가됨에 따라 체인 높이가 증가됩니다.
3.  체인코드 배치:   
a. ***VP0 URL***/chaincode에 대해 POST를 실행하십시오.   
b. 페이로드:   
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
c. 피어가 페이로드를 리턴합니다.
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
d. 요청이 네트워크의 모든 4개의 피어로 전송됩니다. 피어는 PBFT 합의 프로토콜을 실행하고 이 요청의 실행에 동의하며 원장의 개별 사본에 결과를 추가합니다.   
e. 참고로, 모든 트랜잭션은 비동기입니다. 리턴 페이로드에는 나중에 결과 조회에 사용할 수 있는 트랜잭션 ID만 포함되어 있습니다.
4.  테스트 용도로, 인터페이스 중지 단추를 사용하여 수동 중지하여 비잔틴(임의의 동시) 방식으로 오프라인 상태가 되는 노드 VP2 및 VP3을 시뮬레이션하십시오. (**참고**: VP2 맟 VP3이 "중지됨"을 인터페이스에서 반영하려면 30-60초 정도가 소요됩니다.)
5.  체인코드에서 호출 오퍼레이션을 실행하십시오.   
a. 이 예제의 경우, chaincode_example02는 a에서 b로 1 단위 이동합니다.   
b. 페이로드로 ***VP0 URL***/chaincode에 대해 POST를 실행하십시오. 
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
c. 피어가 페이로드를 리턴합니다.
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
d. 네트워크가 f=(N-1)/3 PBFT 테스트에 실패하므로, 호출 오퍼레이션이 입력으로 허용되지만 실행되지 않으며 아무 것도 공유 원장에 추가되지 않습니다.
6.  “a” 변수의 값을 조회하여 호출 오퍼레이션이 실행되지 않았는지 확인하십시오.   
a. 페이로드로 ***VP0 URL***/chaincode에 대해 POST를 실행하십시오. 
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
b. 피어가 페이로드를 리턴합니다.
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
c. 참고로, “a” 값은 변경되지 않고 유지됩니다.
  (합의 테스트 3 종료)
