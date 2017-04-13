---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 합의 테스트 1: 비잔틴 노드 없음
{: #pbft_test1}
마지막 업데이트 날짜: 2016년 8월 4일
{: .last-updated}

합의 테스트 1은 4개 노드 중 어떤 노드도 비잔틴 노드가 아닌 블록체인 네트워크 시나리오의 PBFT 합의 프로토콜을 테스트합니다. 어떤 노드도 임의의 동시 방식으로 오프라인 상태가 되지 않습니다.
{:shortdesc}

개발자 네트워크 또는 고급 보안 비즈니스 네트워크를 실행한 후에는 다음 단계를 완료하여 비잔틴 노드 없이 PBFT를 테스트하십시오. 

(**참고**: 코드 스니펫 및 지시사항은 다양한 기호값을 활용합니다. **VPO URL**, **"test_user1"**, **"test_user1_enrollSecret"** 및 **YOUR_CHAINCODE_ID**는 단순히 플레이스홀더입니다. 네트워크 콘솔의 **API** 탭에서 **서비스 신임 정보** 및 **VP URL**의 리터럴 값에 액세스하십시오. 일단 체인코드 조각을 네트워크에 배치한 경우, **YOUR_CHAINCODE_ID** 값은 **네트워크** 탭에 나타납니다. 추가로, JSON 응답 페이로드의 해시 값은 이러한 예제와는 다릅니다.)

1.	네트워크 사용자 ID 및 비밀번호로 로그인하십시오.   
a. ***VP0 URL***/registrar에 대해 POST를 실행하십시오.   
    b.	페이로드 {“enrollId”: “test_user1”, enrollSecret”: “test_user1_enrollSecret”}을 실행하십시오.   
    c.	피어가 페이로드를 리턴합니다. 
2.	네트워크가 시작되어 실행 중인지 확인하십시오.   
    a.	각 피어에 대한 URL을 지정하여 각 피어마다 해당 블록체인 높이를 조회하십시오.   
b. GET ***VP0 URL***/chain을 실행하십시오.   
c. 피어가 페이로드를 리턴합니다. 
   ```
   {
     "currentBlockHash":
     "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
     "height": 1
   }
   ```
    d.	블록체인에 대한 첫 번째 오퍼레이션인 경우, 체인의 유일한 블록이 원천 블록이므로 체인 높이는 1입니다. 트랜잭션이 원장에 추가됨에 따라 체인 높이가 증가됩니다.
3.	체인코드 배치:   
    a.	***VP0 URL***/chaincode에 대해 POST를 실행하십시오.   
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
       "52b0d803fc395b5e34d8d4a7cd69fb6aa00099b8fabed83504ac1c5d61a425aca5b3ad3bf96643ea4fdaac132c417c37b00f88fa800de7ece387d008a76d3586"
       },
       "id": 1
       }
       ```
    d. 요청이 네트워크의 모든 4개의 피어로 전송됩니다. 피어는 PBFT 합의 프로토콜을 실행하고 이 요청의 실행에 동의하며 원장의 개별 사본에 결과를 저장합니다.   
    e.	참고로, 모든 트랜잭션은 비동기입니다. 리턴 페이로드에는 후속 체인코드 호출에서 사용될 체인코드 해시가 포함되어 있습니다.
4.  잠시 후에 배치 요청이 완료되었는지 확인하십시오.   
a. 차례로 각 피어에 대한 URL을 지정하여 각 피어마다 해당 블록체인 높이를 조회하십시오.   
b. GET ***VP0 URL***/chain을 실행하십시오.   
c. 명령에서 페이로드를 리턴합니다. 
      ```
      {
      "currentBlockHash":
      "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 2
      }
      ```
d. 배치 오퍼레이션의 완료는 프로세서 속도와 네트워크 대기 시간 등의 요인에 따라 결정됩니다.
5.  이제 체인코드를 배치했으므로 체인코드에서 오퍼레이션을 호출할 수 있습니다.   
a. chaincode_example02를 사용하여 a에서 b로 1 단위 이동하십시오.   
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
6.  이전 요청은 비동기입니다. 잠시 후에 체인코드에서 “a” 변수의 값을 조회하여 호출 오퍼레이션이 완료되었는지 확인하십시오.   
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
      "message": "999"
      },
      "id": 3
      }
      ```
c. 예상한 대로, "a" 값은 체인코드가 원래 배치된 때보다 1 아래입니다. 참고로, "a"에 지정된 원래 값은 1,000이며 "b"에 지정된 원래 값은 2,000입니다. 5단계에서 트리거된 호출 요청의 결과로 "a"에서 "b"로 하나의 단위가 전송됩니다.
7.  호출 및 조회 오퍼레이션을 계속 실행할 수 있습니다. 프로세스는 이전 단계에서와 동일합니다. 

  (합의 테스트 1 종료)
