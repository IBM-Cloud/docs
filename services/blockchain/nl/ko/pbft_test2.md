---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 합의 테스트 1: 하나의 비잔틴 노드
{: #pbft_test2}

마지막 업데이트 날짜: 2016년 8월 4일
{: .last-updated}

합의 테스트 2는 4개 노드 중 하나가 비잔틴 노드인 네트워크 시나리오에서 PBFT 프로토콜을 테스트합니다. 하나의 노드는 임의의 동시 방식으로 오프라인 상태가 되었습니다.
{:shortdesc}

PBFT 프로토콜은 (N-1)/3 피어 이하가 비잔틴(임의의 동시) 방식으로 오프라인 상태가 되는 경우에 N 피어의 블록체인 네트워크가 계속 작동함을 보장합니다. Bluemix 블록체인 환경에는 4개 피어가 있습니다. 따라서 하나의 피어가 충돌하면 네트워크는 계속해서 합의를 실행하며 트랜잭션을 원장에 추가합니다. PBFT 공식을 적용하면 (4-1)/3 = 1 = 비잔틴 노드 수임이 드러납니다. 따라서 블록체인 네트워크의 트랜잭션 처리가 계속됩니다. 

다음 단계를 완료하여 비잔틴 노드가 하나인 4노드 네트워크에서 PBFT를 테스트하십시오. 
1.	네트워크 사용자 ID 및 비밀번호로 로그인하십시오.   
a. ***VP0 URL***/registrar에 대해 POST를 실행하십시오.   
b. 페이로드 실행: {“enrollId”: “***test\_user1***”, enrollSecret”: “***test\_user1\_enrollSecret***”}
    c.  피어가 페이로드에서 리턴됩니다. 
2.  네트워크가 시작되어 실행 중인지 확인하십시오.   
a. 각 피어에 대한 URL을 지정하여 각 피어마다 해당 블록체인 높이를 조회하십시오.   
    b   GET ***VP0 URL***/chain을 실행하십시오.   
c. 명령에서 페이로드를 리턴합니다. 
      ```
      {
      "currentBlockHash":
      "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
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
      "message":
      "YOUR_CHAINCODE_ID_RETURNED_HERE"
      },
      "id": 1
      }
      ```  
    d. 요청이 네트워크의 모든 4개의 피어로 전송됩니다. 피어는 PBFT 합의 프로토콜을 실행하고 이 요청의 실행에 동의하며 원장의 개별 사본에 결과를 저장합니다.   
e. 참고로, 모든 트랜잭션은 비동기입니다. 리턴 페이로드에는 후속 체인코드 호출에서 사용될 체인코드 해시가 포함되어 있습니다.   
f. 배치의 완료는 프로세서 속도와 네트워크 대기 시간 등의 요인에 따라 결정됩니다.   
4.  테스트 용도로, 인터페이스의 중지 단추를 사용하여 수동 중지함으로써 비잔틴 노드 VP2를 시뮬레이션하십시오. (**참고**: VP2가 "중지됨"을 인터페이스에서 반영하려면 30-60초 정도가 소요됩니다.)
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
d. 요청이 다시 모든 4개의 피어에 전송됩니다. 피어는 PBFT 합의 프로토콜을 실행하고 이 요청의 실행에 동의하며 원장의 개별 사본에 결과를 저장합니다.
6.  이 요청 또한 비동기입니다. 잠시 후에 체인코드의 “a” 변수 값을 조회하여 호출 오퍼레이션이 완료되었는지 확인하십시오.   
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
b. 피어가 페이로드에서 리턴됩니다.
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
7.  예상한 대로, "a" 값은 체인코드가 원래 배치된 때보다 1 아래입니다. 
8.  추가 호출 및 조회 오퍼레이션을 계속 실행할 수 있습니다. 프로세스는 이전 단계에서와 동일합니다. 

(합의 테스트 2 종료)
