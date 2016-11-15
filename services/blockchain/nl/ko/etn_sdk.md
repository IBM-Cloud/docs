---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# HFC SDK for Node.js
{: #etn_sdk}
마지막 업데이트 날짜: 2016년 10월 7일
{: .last-updated}

애플리케이션 개발자는 HFC(Hyperledger Fabric Client) SDK를 사용하여 블록체인 네트워크와 상호작용하는 Node.js 애플리케이션을 빌드할 수 있습니다. HFC SDK를 활용하는 Node.js 애플리케이션을 사용하면 다음의 네트워크 태스크를 수행할 수 있습니다.
{:shortdesc}

* 사용자를 안전하게 등록하고 등록접수합니다. `registrar` 권한이 있는 웹 애플리케이션 관리자는 웹 애플리케이션에 대해 인증된 사용자를 동적으로 등록하고 등록접수할 수 있습니다. 
* 블록체인 네트워크에 트랜잭션을 제출합니다(배치, 호출 및 조회). 모든 트랜잭션은 익명이고 기밀이며 '감사자' 권한이 없으면 연결을 끊을 수 없습니다. 
* 임의의 위치에서 민감한 개인 키와 인증서를 저장합니다(예: 오프-블록체인 데이터베이스). 여기서는 단순 키-값 저장소 인터페이스를 구현해야 합니다. 

HFC SDK는 API를 제공하며, 이를 통해 애플리케이션은 Hyperledger Fabric 블록체인 네트워크와 상호작용합니다. 이러한 API는 두 개의 플러그 가능 컴포넌트를 지원하도록 설계되었습니다. 

1. 플러그 가능 키 값 저장소: 멤버와 연관된 키를 검색하고 저장하는 데 사용됩니다. `chain.setKeyValStore()` 메소드는 기본 파일 기반 키 값 저장소 구현을 대체합니다. 체인 키 값 저장소가 민감한 개인 키를 저장하는 데 사용되므로, 액세스는 알맞게 보호되어야 합니다. 
2. 플러그 가능 멤버 서비스: 멤버를 등록하고 등록접수하는 데 사용됩니다. `chain.setMemberServices()` 메소드는 `MemberServices`의 기본 구현을 대체합니다. 멤버 서비스는 익명성, 트랜잭션의 비연결성 및 기밀성을 제공하는 권한 부여된 블록체인 네트워크로서 Hyperledger Fabric을 구현합니다. 

오프라인 메소드 또는 npm 메소드를 사용하여 Node.js 앱에 HFC SDK를 포함할 수 있습니다. 
*  오프라인 메소드: 우선 Hyperledger Fabric 소스 트리의 파일을(https://github.com/hyperledger/fabric/tree/master/sdk/node/lib) Node.js 앱 `/lib` 디렉토리에 복사합니다. 그리고 다음 코드 스니펫을 추가하여 애플리케이션에 HFC SDK를 포함합니다. 

```js
var hfc = require("./lib/hfc");
```

* npm 메소드: 명령행에서 우선 다음 스니펫으로 npm에서 HFC SDK를 설치합니다. 

```
npm install hfc@0.5.3
```

그리고 다음 코드 스니펫으로 애플리케이션에 HFC SDK를 포함합니다. 

```js
var hfc = require('hfc');
```  
<br>
## HFC 오브젝트
{: #objects}

다음 HFC 오브젝트(클래스 및 인터페이스)는 오브젝트 계층 구조를 전체적으로 안내하는 데 도움이 되도록 상위 레벨에서 설명됩니다. 

* 최상위 레벨 클래스는 블록체인 네트워크의 클라이언트 표현인 `Chain`입니다. HFC를 사용하면 다중 네트워크와 상호작용할 수 있으며, 필요하면 단일 `KeyValStore` 및 `MemberServices` 오브젝트를 다중 `Chain` 오브젝트와 공유할 수 있습니다. 각 블록체인 네트워크마다, 트랜잭션을 제출하기 위해 HFC가 연결하는 엔드포인트를 표시하는 하나 이상의 `Peer` 오브젝트를 추가합니다. 
* `KeyValStore` 인터페이스는 모든 지속적 데이터를 저장하고 검색하기 위해 HFC에 의해 사용됩니다. 이 데이터에는 보안 유지가 필요한 개인 키가 포함됩니다. 기본 구현은 `FileKeyValStore` 클래스에 위치한 파일 기반 버전입니다. 
* `MemberServices` 인터페이스는 `MemberServicesImpl` 클래스에 의해 구현되며, 보안 및 ID 기반 기능(예: 개인정보 보호정책, 비연결성 및 기밀성)을 제공합니다. 이 구현은 *eCerts*(멤버 등록접수 인증서) 및 *tCerts*(각 멤버의 트랜잭션 인증서)를 발행합니다. 
* `Member`는 네트워크에서 거래하는 일반 사용자 및 피어(노드)와 같은 기타 유형의 멤버를 표시합니다. `MemberServices` 오브젝트와 상호작용하는 `Member` 클래스를 사용하면 멤버 및 사용자를 *등록*하고 *등록접수*할 수 있습니다. `Peer` 오브젝트로 거래하여 '멤버' 클래스에서 직접 체인코드를 배치, 조회하고 호출할 수도 있습니다. 이 구현은 단순히 임시 `TransactionContext` 오브젝트에 작업을 위임합니다. 
* `TransactionContext` 클래스는 대량의 배치, 호출 및 조회 로직을 구현합니다. 각 `TransactionContext` 인스턴스는 트랜잭션 제출에 항상 사용되는 `MemberServices`에서 고유 tCert를 수신합니다. 동일한 tCert로 다중 트랜잭션을 발행하려면, 멤버 오브젝트에서 직접 `TransactionContext` 오브젝트를 검색하고 다중 배치, 호출 및 조회 오퍼레이션을 실행하십시오. 그러나 다중 트랜잭션에 대해 단일 tCert를 사용하면 트랜잭션이 연결되므로, 이는 동일한 익명 사용자를 포함하는 것으로 식별됩니다. 트랜잭션 연결을 피하려면 `User` 또는 `Member` 오브젝트에서 배치, 호출 및 조회를 호출하십시오.   

<br>
## 샘플 Node.js 애플리케이션
{: #nodesample}

다음 샘플 Node.js 애플리케이션은 Bluemix 블록체인 네트워크와의 상호작용을 위해 HFC SDK API를 활용합니다. 프로그램은 네트워크 플랜(스타터 및 HSBN) 및 클라이언트 측 운영 체제에서 작동합니다. 

목적은 Javascript 애플리케이션([helloblockchain.js](https://github.com/IBM-Blockchain/SDK-Demo/blob/master/helloblockchain.js))을 사용하여 체인코드([chaincode_example02](https://github.com/IBM-Blockchain/SDK-Demo/blob/master/chaincode_example02.go))를 Bluemix 네트워크에 성공적으로 배치한 후에 호출 및 조회를 수행하는 것입니다.   

1. 이 프로그램에서는 Node.js 및 npm JavaScript 패키지 관리자가 둘 다 필요합니다. [Node.js](https://nodejs.org/en/)의 최신 버전을 설치하면 자동으로 npm이 포함됩니다.   

1. 터미널을 열고 helloblockchain.js 소스 코드 및 노드 모듈이 배치될 디렉토리(작업공간)를 작성하십시오. 예를 들면, 다음과 같습니다. 

    ```
    mkdir -p $HOME/workspace
    ```

1. 새로 작성된 작업공간 폴더로 이동하여 다음 명령으로 HFC v0.5.3을 설치하십시오.

     ```
     cd $HOME/workspace
     npm install hfc@0.5.3
     ```

1. [helloblockchain.js](https://github.com/IBM-Blockchain/SDK-Demo/blob/master/helloblockchain.js) 프로그램을 복사하고 이를 작업공간 폴더에 저장하십시오.
   `/workspace` 디렉토리는 아래의 스크린샷과 유사해야 합니다. 

   ![노드 작업공간](images/nodeworkspace.PNG "노드 작업공간")

1. 아직 수행하지 않았으면, Bluemix의 [Blockchain](https://console.ng.bluemix.net/catalog/services/blockchain/) 타일에 액세스하고 서비스 인스턴스를 작성하십시오. **스타터 개발자** 플랜 또는 **고급 보안 비즈니스 네트워크** 플랜을 선택하십시오(승인된 경우 ![](images/green_dot.png)). 
**작성** 단추를 클릭한 후에 JSON 파일을 복사하고 붙여넣어 **서비스 신임 정보**를 가져오십시오. 그리고 로컬 '/workspace' 디렉토리에 ServiceCredentials.json으로 이를 저장하십시오. 전체 JSON 페이로드를 복사했는지 확인하십시오. 이는 표준 편집기에서 202행이어야 합니다. **참고**: Bluemix [새 콘솔](https://new-console.ng.bluemix.net/#overview) 형식에 대해 블록체인 인스턴스를 실행 중일 때는 **서비스 신임 정보**의 출력에서 차이가 나타납니다. 즉, "신임 정보" 행이 오브젝트에서 제거됩니다. 이를 수정하려면 다음 스니펫을 ServiceCredentials.json 파일의 2행에 추가하십시오. 

	```
	"credentials": {
	```

1. 그리고 마지막 닫기 부호 `}`를 202행에 추가하여 오브젝트를 닫으십시오. ServiceCredentials.json의 레이아웃은 예제 [ServiceCredentials.json](https://github.com/IBM-Blockchain/SDK-Demo/blob/master/ServiceCredentials.json)의 레이아웃을 미러링해야 합니다(202행의 페이로드 유지). Bluemix [기존 콘솔](https://console.ng.bluemix.net/) 형식에서 파생된 블록체인 인스턴스에서 신임 정보를 가져오는 경우에는 이러한 불일치에 대해 염려할 필요가 없습니다. 아래의 스크린샷은 두 레이아웃의 차이를 보여줍니다. 처음은 *새 콘솔*을 표시하며 그 뒤에는 *기존 보기*를 표시합니다.

     ![서비스 신임 정보 새 콘솔](images/servicecreds1.png "서비스 신임 정보 새 콘솔")

     ![서비스 신임 정보](images/servicecreds.png "서비스 신임 정보")

1. ServiceCredentials.json 추가 시에 `/workspace` 디렉토리는 다음 스크린샷과 유사해야 합니다. 

     ![노드 작업공간2](images/nodeworkspace2.PNG "노드 작업공간 2")

1. 프로그램이 실행될 때 HFC SDK는 $HOME/workspace 내에서 `keyValStore` 디렉토리를 작성합니다. 이 `keyValStore` 디렉토리에는 각각의 등록접수된 사용자에 대한 암호화 키가 포함되어 있습니다. 새 Bluemix 네트워크에 연결할 때 `keyValStore` 디렉토리를 삭제할 필요는 없습니다. 대신에 고유 `keyValStore` 디렉토리가 각 Bluemix 인스턴스마다 작성됩니다.   

1. 아래에 표시된 대로 $GOPATH 아래에 체인코드 디렉토리를 작성하십시오. 시스템에서 $GOPATH를 아직 설정하지 않았으면 [여기](https://github.com/golang/go/wiki/GOPGATH)의 지시사항을 따르십시오. 

	```
	mkdir -p $GOPATH/src/chaincode_example02
	```

1. [chaincode_example02.go](https://github.com/IBM-Blockchain/SDK-Demo/blob/master/chaincode_example02.go)를 이 새 디렉토리 `$GOPATH/src/chaincode_example02`에 복사하십시오. 이는 일단 프로그램이 실행되면 Bluemix 네트워크에 배치될 실제 체인코드 조각입니다.   

1. [vendor.zip](https://github.com/IBM-Blockchain/SDK-Demo/blob/master/vendor.zip)을 검색하고 이를 동일 디렉토리 `$GOPATH/src/chaincode_example02`에 저장하십시오. vendor.zip 패키지에는 Hyperledger Fabric v0.5 코드 베이스의 라이브러리 및 종속 항목이 포함되어 있습니다. 기본 Windows 추출에서는 **C:\GOPATH\src\chaincode_example02\vendor**와 유사한 경로를 작성합니다. 추출하기 전에, 우선 이 경로의 `\vendor` 디렉토리를 삭제해야 합니다. 그렇지 않으면, 체인코드 배치에 실패합니다. Windows의 올바른 경로는 **C:\GOPATH\src\chaincode_example02\vendor\github.com\hyperledger\fabric**과 유사합니다. (참고: 하나의 `\vendor` 디렉토리가 올바릅니다.) 두 번째 `\vendor` 디렉토리의 변칙은 Linux 또는 OS X에서는 발생하지 않습니다. 

1. 이제 다음 예제와 유사한 디렉토리가 $GOPATH 내에 있어야 합니다. 

    ![노드 $GOPATH](images/nodegopath.PNG "노드 $GOPATH")

1. 로컬 '/workspace' 디렉토리에서 노드 프로그램을 실행하십시오. 

	```
	node helloblockchain.js -c chaincode_example02
	```
	디버그 로그 사용:
	```
	DEBUG=hfc node helloblockchain.js -c chaincode_example02
	```

	gRPC 추적 사용:
	```
	GRPC_TRACE=all DEBUG=hfc node helloblockchain.js -c chaincode_example02
	```

`deploy`, `invoke` 및 `query` 트랜잭션에 성공하면 터미널에 다음 메시지가 표시됩니다. 

```
Successfully deployed chaincode: request={"fcn":"init","args":["a","100","b","200"],"certificatePath":"/certs/blockchain-cert.pem","chaincodePath":"github.com/chaincode_example02/"}, response={"uuid":"2d6ad8d6-1390-4c60-a01b-f4c301175eb7","chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","result":"TODO: get actual results; waited 120 seconds and assumed deploy was successful"}

Successfully submitted chaincode invoke transaction: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"invoke","args":["a","b","1"]}, response={"uuid":"f9a902d2-44d8-4b68-b43d-419470ba73ae"}

Successfully completed chaincode invoke transaction: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"invoke","args":["a","b","1"]}, response={"result":"waited 20 seconds and assumed invoke was successful"}

Successfully queried  chaincode function: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"query","args":["a"]}, value=99
```

스타터 개발자 네트워크를 실행할 때 체인코드 컨테이너가 시작하는 데는 종종 10분까지 소요됩니다. 그러나 일단 시작되면 후속 배치 및 호출이 즉시 실행됩니다. 전제조건 파일이 블록체인 인스턴스의 호스트 시스템에 저장되어 있기 때문입니다.  

**네트워크 콘솔**에서 **블록체인** 탭으로 이동하십시오. 이 보기는 helloblockchain.js 프로그램이 배치 및 호출 트랜잭션을 발행할 때 블록체인 원장에 추가되는 블록을 표시합니다. 다음 스크린샷은 "a" 및 "b"의 기본 인수로 실행 중인 helloblockchain.js의 결과를 두 번 보여줍니다. 

   ![노드 작업공간3](images/nodeworkspace3.PNG "노드 작업공간 3")  

<br>
## 문제점 해결
**/workspace** 디렉토리에서 다음 명령 중 하나를 실행하여 **hfc@0.5.3**을 실행 중인지 확인하십시오. 
  * npm list | grep hfc
  * npm list -g | grep hfc(글로벌 `-g` 플래그를 사용하여 설치한 경우)

조회 메시지를 수신하는 경우 다음 프로시저를 사용하십시오. 

  ```
Failed to query chaincode, function: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"query","args":["a"]}, error={"error":{"status":"FAILURE","msg":{"type":"Buffer","data":[69,114,114,111,114,58,70,97,105,108,101,100,32,116,111,32,108,97,117,110,99,104,32,99,104,97,105,110,99,111,100,101,32,115,112,101,99,40,112,114,101,109,97,116,117,114,101,32,101,120,101,99,117,116,105,111,110,32,45,32,99,104,97,105,110,99,111,100,101,32,40,57,98,101,48,97,48,101,100,51,102,49,55,56,56,101,56,55,50,56,99,56,57,49,49,99,55,52,55,100,50,102,54,100,48,101,50,48,53,102,97,54,51,52,50,50,100,99,53,57,56,100,52,57,56,102,101,55,48,57,98,57,98,56,100,41,32,105,115,32,98,101,105,110,103,32,108,97,117,110,99,104,101,100,41]}},"msg":"Error:Failed to launch chaincode spec(premature execution - chaincode (9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d) is being launched)"}
  ```

Node.js 애플리케이션에서 배치 대기 시간을 늘리십시오. 기본값은 60초로 설정되지만, 코드가 제대로 배치, 컴파일하고 Docker 컨테이너에서 실행을 시작하려면 더 오랜 시간이 걸릴 수 있습니다. 배치 대기 시간을 120초로 늘려 보십시오. 이 특성은 블록체인 인스턴스를 호스팅하는 시스템에서 공유 계산 자원의 결과로서 스타터 개발자 플랜에서만 관찰됩니다. 

  ```js
chain.setDeployWaitTime(120);
  ```

일단 체인코드가 네트워크에 성공적으로 배치되면, 배치 대기 시간을 얼마 안 되는 양(예: 수 초)으로 줄일 수 있습니다. 

핸드쉐이크 오류를 수신하는 경우에는 다른 `grpc` 버전을 시도하십시오. 다음 명령 중 하나를 사용하여 grpc 버전에 액세스할 수 있습니다. 
    - `npm list | grep grpc`
    - `npm list -g | grep grpc`  

<br>
## 공개 및 개인 키
{: #keys}

Hyperledger Fabric은 인증 기관 및 이의 기본 공개 및 개인 키를 사용하여 공유 블록체인에서 운용 중인 비즈니스의 보안 요구사항을 충족합니다. 멤버 ID 관리, 역할 관리 및 트랙잭션 개인정보 보호정책은 모두 HFC SDK를 통해 제어가 가능합니다. 

공유 블록체인의 사용자 및 트랜잭션 개인정보 보호정책은 PKI(Public Key Infrastructure) 프레임워크의 구현을 통해 관리됩니다. PKI는 인증 기관을 통해 키와 디지털 인증서의 생성, 배포 및 폐기를 관리합니다. PKI 및 멤버십 서비스의 전체 기술 스펙은 Hyperledger Fabric v0.5 [프로토콜 스펙](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md)의 보안 섹션에서 설명되어 있습니다. Hyperledger Fabric PKI의 기본 원칙은 아래에 설명되어 있습니다. 

1. 등록 기관(RA)은 블록체인 네트워크에 대한 액세스를 요청 중인 사용자의 ID를 유효성 검증합니다. 이는 `registrar` 권한의 사용자에 의해 동적으로 또는 membersrvc.yaml 파일을 편집하여 수동으로 수행될 수 있습니다. 등록 프로세스는 외부(out-of-band)에서 발생하며 `RegisterUser` 함수를 통해 실행됩니다. RA는 등록접수 신임 정보(`<enrollID>` 및 `<enrollPWD>`)를 사용자에게 지정합니다.

2. 그리고 사용자는 `CreateCertificatePair` 함수를 사용하여 등록접수 인증 기관(ECA)에 등록접수 요청을 전송합니다. 이 페이로드에는 사용자의 일회성 `<enrollPWD>`, 공용 서명 검증 키와 공용 암호화 키가 포함되며, 사용자의 개인용 서명 검증 키로 서명됩니다. <br><br>등록접수 요청을 수신하면, ECA가 사용자의 개인용 암호화 키로만 복호화될 수 있는 암호화된 인증 확인을 사용자에게 발행합니다. 인증 확인을 복호화한 후에 사용자는 인증 요청을 다시 전송합니다. 정확히 복호화된 응답 여하에 따라, ECA는 디지털 서명으로 서명된 인증된 인증서 쌍을 리턴합니다. <br><br>디지털 서명은 "다이제스트"를 생성하는 SHA-2 알고리즘을 사용하여 인증 요청(메시지)을 암호화를 통해 해싱함으로써 생성됩니다. 그리고 이 "메시지 다이제스트"는 ECA의 개인용 서명 키로 암호화됩니다. 그리고 네트워크 멤버는 ECA의 공용 서명 키로 복호화하여 디지털 서명을 인증합니다. 리턴된 등록접수 인증서(eCert) 쌍에는 데이터 서명용 인증서 하나(개인용)와 데이터 암호화용 인증서 하나(공용)가 포함되어 있습니다. 이 eCert 쌍은 정적이고 장기적이며 트랜잭션에 보이거나 보이지 않을 수 있습니다. 

3. 블록체인 네트워크에서 거래하려면 각 사용자에게 트랜잭션 인증서(tCerts)도 있어야 합니다. 등록접수에 성공하면 사용자는 tCerts의 일괄처리에 대해 트랜잭션 인증 기관(TCA)에 요청을 제출합니다. tCert는 단기적이고 하나의 트랜잭션에 특정하며 API를 사용하여 클라이언트에 의해 수정될 수 있습니다. 사용자의 eCert를 확인한 후에 TCA는 tCerts의 일괄처리 및 KeyDF_Key(키 유도 기능 키)를 지정하며, 이는 사용자가 해당 개인 키를 복호화할 수 있도록 허용합니다. 단일 KeyDF_Key가 일괄처리의 각 tCert에 사용되는 동안, 생성되는 후속 개인 키는 각 tCert에 고유합니다. 거래를 위해 클라이언트는 복호화된 개인 키로 트랜잭션 페이로드를 서명할 수 있어야 합니다. 이 경우에만 트랜잭션이 합의를 위해 네트워크 유효성 검증 피어에 전달됩니다. 
