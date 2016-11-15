---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 샘플 앱 및 튜토리얼
{: #1stanchor}
마지막 업데이트 날짜: 2016년 10월 5일
{: .last-updated}

다음 샘플은 애플리케이션 및 체인코드가 IBM Blockchain 네트워크에서 어떻게 작동하는지 예시합니다. 블록체인 네트워크의 기반이 되는 Hyperledger Fabric v0.5 코드에 대해 자세히 알아보려면 Linux Foundation의 Hyperledger 프로젝트의 [Fabric Docs](https://github.com/hyperledger/fabric/tree/master/docs) 섹션을 방문하십시오.  
{:shortdesc}

작동 중인 체인코드 애플리케이션을 경험하기 위해 아래의 Marbles, Commercial Paper 또는 Car Lease 데모를 바로 배치할 수 있습니다(Bluemix에 배치 단추 클릭). 또는 읽기를 계속하여 "Hello Chaincode" 튜토리얼을 탐색하십시오. 

- [![Bluemix에 배치](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  **Marbles**
- [![Bluemix에 배치](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  **Commercial Paper**
- [![Bluemix에 배치](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  **Car Lease**  

<br>
## "Hello Chaincode" 튜토리얼 사용
{: #hellocc}
이 튜토리얼에서는 기본 구성 요소를 사용한 기본 체인코드 애플리케이션 코딩을 전체적으로 안내합니다. 네트워크에서 교환하기 위한 일반 자산을 작성하는 작업 체인코드를 점진적으로 빌드할 수 있습니다. 그리고 네트워크 API를 통해 체인코드와 상호작용할 수 있습니다. 이 튜토리얼을 마치면 다음 질문에 응답할 수 있습니다. 
- 체인코드란 무엇입니까?
- 체인코드를 어떻게 구현합니까?
- 어떤 종속 항목이 존재합니까?
- 기본 기능은 무엇입니까?
- 내 인수에 서로 다른 값을 어떻게 전달합니까?
- 내 네트워크에서 사용자를 어떻게 안전하게 등록접수합니까? 
- 내 체인코드를 어떻게 컴파일합니까?
- REST API를 통해 내 체인코드와 어떻게 상호작용합니까?

### 체인코드의 개념
체인코드는 사용자가 블록체인 네트워크와 상호작용할 수 있도록 하는 Go(GoLang) 또는 Java 코드입니다. 네트워크에서 트랜잭션을 '호출'할 때마다 원장에 대해 값을 읽고 쓰는 체인코드에서 함수를 호출합니다. 

### 첫 번째 체인코드 구현
다음 주제를 완료하여 Bluemix 네트워크의 IBM Blockchain에서 체인코드를 구현할 수 있습니다. 
#### 환경 설정
1. [GoLang](https://golang.org/dl/)에서 운영 체제에 맞는 Golang을 다운로드하여 설치하십시오. 
2. GOPATH를 설정하십시오. 
	- $GOPATH는 Go 코드 및 프로젝트에 대한 **환경 변수** 경로입니다. 표준 Go 트리 외부에서 패키지를 가져와서 빌드하고 설치하려면 $GOPATH를 설정해야 합니다. 따라서 $GOPATH는 원래 Go 트리가 상주하는 $GOROOT 경로에서 고유해야 합니다. 단순히 디렉토리를 작성한 후에 $GOPATH가 이를 지시하도록 하십시오. 
	- Windows에서 $GOPATH를 설정하십시오. 
		- 프로젝트의 작업공간 디렉토리를 작성하십시오(예: C:\Users\ADMIN\Documents\GoProjects). 
		- Windows **시작** 메뉴를 클릭하고 "시스템 환경 변수"를 검색하십시오. 
		- **시스템 환경 변수 편집**을 클릭하십시오. 
		- **고급** 탭에서 **환경 변수**를 클릭하십시오. 
		- 시스템 환경 변수 GOPATH 및 GOROOT를 찾으십시오. GOPATH를 작성해야 하는 경우에는 **새로 작성**을 클릭하십시오.   
		- GOROOT 및 GOPATH 값은 고유해야 합니다. Go를 설치하면 GOROOT가 자동 생성되며, 이는 C:\Go\여야 합니다. 
		- 작성한 작업공간 디렉토리로 GOPATH를 설정하십시오. 이 예제에서 **GOPATH**는 **C:\Users\ADMIN\Documents\GoProjects**입니다.   
		- 세부사항을 보려면 `go help gopath` 명령을 실행하거나 [Go 문서](https://golang.org/doc/install)를 방문하십시오. 
3. 다음 명령을 실행하여 Hyperledger Faric v0.5 shim 코드를 Go 경로에 추가하십시오.

	```
	go get github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview/core/chaincode/shim
	```

4. **참고**: v0.5 hyperledger-archives shim 코드를 가져오려면 위의 링크를 따르십시오. Bluemix 백엔드는 이 동일한 버전화를 사용하여 빌드됩니다. 결과적으로 shim 버전 및 Bluemix 버전이 맞아야 합니다.

#### GitHub 설정
Blockchain on Bluemix 플랜에서는 체인코드가 [GitHub](https://Github.com/) 저장소에 위치해야 합니다. GitHub 계정을 작성하고, [Git 설정](https://help.github.com/articles/set-up-git/)에서 설명한 대로 Git를 설정하십시오. GitHub를 설정한 후에 다음 단계를 완료하십시오. 
1. [체인코드 알아보기](https://github.com/IBM-Blockchain/learn-chaincode)로 이동하여 repo를 분기하십시오.   
2. $GOPATH에 지정된 디렉토리로 분기를 복제하십시오.   
3. repo에는 두 개의 체인코드 디렉토리가 포함되어 있습니다. [Start](https://github.com/IBM-Blockchain/learn-chaincode/blob/master/start/chaincode_start.go)는 빌드가 시작될 체인코드입니다. [Finished](https://github.com/IBM-Blockchain/learn-chaincode/blob/master/finished/chaincode_finished.go)는 빌드가 완료될 체인코드입니다. 
4. 체인코드가 로컬 환경에서 빌드되는지 확인하십시오. 명령 프롬프트를 열고 `chaincode_start.go`가 포함된 폴더로 이동하십시오. 다음 명령을 입력하십시오.

	```
	go build ./
	```
명령은 오류 또는 메시지 없이 리턴해야 합니다.


#### 체인코드 인터페이스 구현
다음 단계는 Golang 코드로 체인코드 shim 인터페이스 구현입니다. 3개의 기본 함수는 **Init**, **Invoke** 및 **Query**입니다. 세 함수는 모두 함수 이름 및 문자열 배열을 입력으로 취하지만, 호출된 시점에 따라 다를 수 있습니다. 블록체인 네트워크에서 교환할 일반 자산을 작성하는 작업 체인코드를 빌드합니다. 

### 종속 항목
`import`문은 체인코드 빌드에 필요한 종속 항목을 나열합니다. 
1. `fmt` - 디버깅/로깅을 위한 `Println`이 포함됩니다. 
2. `errors` - 표준 Go 오류 형식입니다. 
3. `github.com/hyperledger/fabric/core/chaincode/shim` - Golang 코드를 네트워크 피어와 인터페이스하는 코드입니다. 

### 값 전달

다음의 체인코드 값이 전달됩니다. 
#### Init()
Init은 네트워크에 처음 배치할 때 체인코드를 초기화하기 위해 호출됩니다. 이 예제에서는 `Init`을 사용하여 원장에서 한 변수의 초기 상태를 구성합니다. 

첫 번째 `args` 요소를 "hello_world" 키에 저장하도록 `chaincode_start.go` 파일에서 `Init` 함수를 변경하십시오. 

```go
func (t *SimpleChaincode) Init(stub *shim.ChaincodeStub, function string, args []string) ([]byte, error) {
	if len(args) != 1 {
		return nil, errors.New("Incorrect number of arguments. Expecting 1")
	}

	err := stub.PutState("hello_world", []byte(args[0]))
	if err != nil {
		return nil, err
	}

	return nil, nil
}
```

이는 shim 함수 `stub.PutState`를 사용하여 수행됩니다. 첫 번째 인수는 문자열로서 키이며, 두 번째 인수는 바이트 배열로서 값입니다. 이 함수는 오류를 리턴할 수 있으며, 사용자 코드는 오류를 검사하고 존재하는 경우 이를 리턴합니다.

#### Invoke()
`Invoke`는 체인에 트랜잭션 요청을 추가하기 위해 호출됩니다. `Invoke`의 구조는 단순합니다.
이는 `function` 인수를 수신하며, 이 인수를 기반으로 체인코드에서 Go 함수를 호출합니다. 

`chaincode_start.go` 파일에서, 일반 쓰기 함수를 호출하도록 `Invoke` 함수를 변경하십시오. 

```go
func (t *SimpleChaincode) Invoke(stub *shim.ChaincodeStub, function string, args []string) ([]byte, error) {
	fmt.Println("invoke is running " + function)

	// Handle different functions
	if function == "init" {
		return t.Init(stub, "init", args)
	} else if function == "write" {
		return t.write(stub, args)
	}
	fmt.Println("invoke did not find func: " + function)

	return nil, errors.New("Received unknown function invocation")
}
```

코드에서 이제 `write`를 찾으므로, 해당 함수를 `chaincode_start.go` 파일에 추가하십시오. 

```go
func (t *SimpleChaincode) write(stub *shim.ChaincodeStub, args []string) ([]byte, error) {
	var name, value string
	var err error
	fmt.Println("running write()")

	if len(args) != 2 {
		return nil, errors.New("Incorrect number of arguments. Expecting 2. name of the variable and value to set")
	}

	name = args[0]                            //rename for fun
	value = args[1]
	err = stub.PutState(name, []byte(value))  //write the variable into the chaincode state
	if err != nil {
		return nil, err
	}
	return nil, nil
}
```

`write` 함수는 이전 `Init` 변경사항과 유사해야 합니다. 이제 `PutState`에 대한 키/값을 설정할 수 있으며, 이는 블록체인 원장에서 키/값 쌍을 저장할 수 있도록 허용합니다. 

#### Query()
`Query`는 체인코드 상태를 조회하기 위해 호출되며, 체인에 블록을 추가하지 않습니다. 배치 및 호출 함수만 새 블록을 추가합니다. `Query`를 사용하여 체인코드 상태의 키/값 쌍에 대한 값을 읽을 수 있습니다. 

`chaincode_start.go` 파일에서 일반 읽기 함수를 호출하도록 `Query` 함수를 변경하십시오. 

```go
func (t *SimpleChaincode) Query(stub *shim.ChaincodeStub, function string, args []string) ([]byte, error) {
	fmt.Println("query is running " + function)

	// Handle different functions
	if function == "read" {                            //read a variable
		return t.read(stub, args)
	}
	fmt.Println("query did not find func: " + function)

	return nil, errors.New("Received unknown function query")
}
```

코드에서 이제 `read`를 찾으므로, 해당 함수를 `chaincode_start.go` 파일에 추가하십시오. 

```go
func (t *SimpleChaincode) read(stub *shim.ChaincodeStub, args []string) ([]byte, error) {
	var name, jsonResp string
	var err error

	if len(args) != 1 {
		return nil, errors.New("Incorrect number of arguments. Expecting name of the var to query")
	}

	name = args[0]
	valAsbytes, err := stub.GetState(name)
	if err != nil {
		jsonResp = "{\"Error\":\"Failed to get state for " + name + "\"}"
		return nil, errors.New(jsonResp)
	}

	return valAsbytes, nil
}
```

`read` 함수는 `PutState`를 보완하는 `GetState`를 사용합니다. 이 shim 함수는 검색할 키의 이름인 하나의 문자열 인수만 취합니다. 그 다음에 이 함수는 값을 바이트 배열로서 `Query`에 리턴하며, 이는 다시 값을 REST 핸들러에 전송합니다. 

#### Main()
`main` 함수는 각 피어가 체인코드의 해당 인스턴스를 배치할 때 실행됩니다. 이 함수는 체인코드를 시작하며 이를 피어에 등록합니다. 'main'에는 코드 업데이트가 필요하지 않습니다. chaincode_start.go 및 chaincode_finished.go 모두에는 각 파일의 맨 위에 `main` 함수가 포함되어 있습니다. 

```go
func main() {
	err := shim.Start(new(SimpleChaincode))
	if err != nil {
		fmt.Printf("Error starting Simple chaincode: %s", err)
	}
}
```

### 체인코드와 상호작용
체인코드를 테스트하는 가장 빠른 방법은 피어에서 REST 인터페이스를 사용하는 것입니다.
Bluemix 대시보드 모니터에서 Swagger UI를 사용하면 추가 코드를 작성하지 않고도 체인코드의 배치를 시험해 볼 수 있습니다.   

<br>
#### Swagger API
Swagger API를 사용하려면 다음 단계를 완료하십시오. 

1. [Bluemix](https://console.ng.bluemix.net/login)에 로그인하여 현재 위치가 **대시보드** 탭인지 확인하십시오. 
1. 현재 위치가 IBM Blockchain 서비스를 포함하는 동일 Bluemix "영역"인지 확인하십시오. 영역 탐색은 왼쪽에 있습니다. 
1. 맨 아래 부근에는 **서비스** 패널이 있습니다. IBM Blockchain 서비스를 클릭하십시오. 
1. "IBM Blockchain을 시작합니다..." 메시지가 나타나야 합니다. 오른쪽의 **시작** 단추를 클릭하십시오. 
1. 모니터 페이지에서 두 개의 테이블이 나타나야 합니다. 맨 아래 테이블은 비어 있을 수 있습니다. 
	- **네트워크 탭:**
		- **피어 로그**는 맨 위 테이블에 있습니다. **피어 1**의 행에서 파일 아이콘을 클릭하여 로그를 보십시오. 이 정적 보기와 함께, 페이지 맨 위 근처의 **로그 보기** 탭에는 라이브 **스트리밍 피어 로그**가 있습니다. 
		- **체인코드 로그**는 맨 아래 테이블에 있습니다. 각 체인코드는 배치 시에 리턴된 체인코드 해시로 레이블 지정됩니다. 체인코드 행에서 피어를 선택한 후에 파일 아이콘을 클릭하여 로그를 보십시오. 
	- **API 탭**: Swagger API 문서 페이지를 표시합니다. 
1. 다음 단계를 진행하여 보안 등록접수를 구현하십시오. REST 인터페이스에서 `/chaincode` 엔드포인트를 호출하려면 보안 컨텍스트 ID가 필요합니다. 대부분의 REST 호출을 허용하려면, 서비스 신임 정보 목록에서 등록된 *enrollID*를 전달해야 합니다. 
  - **+ 네트워크 등록접수 ID**를 클릭하여 *enrollID* 값과 해당 시크릿의 목록을 펼치십시오. 
  - 나중에 사용할 수 있도록 신임 정보 세트를 텍스트 파일에 복사하십시오. 
  - **등록자** API 섹션을 펼치십시오. 
  - `POST /registrar` 섹션을 펼치십시오. 
  - ``Value`` 필드를 신임 정보의 `enrollSecret' 및 `enrollID`를 지정하는 JSON으로 채우십시오.

  ![등록 예](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/registrar.PNG "등록 예")

  *응답 본문*은 다음 예와 같이 표시됩니다.

  ![등록 예](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/register_response.PNG "등록 예 응답 본문")

이제 `enrollID`가 설정되었으므로, 다음 단계에서 체인코드를 배치, 호출 및 조회할 때는 이 ID를 사용할 수 있습니다. 
### 체인코드 배치
REST 인터페이스를 통해 체인코드를 배치하려면 체인코드를 공용 GitHub 저장소에 저장해야 합니다. 피어에 배치 요청을 전송할 때는 체인코드 저장소의 URL 및 체인코드를 초기화하는 매개변수를 지정하십시오. 

체인코드를 **배치하기 전에**, 체인코드가 로컬로 빌드되는지 확인하십시오. 
1. 명령 프롬프트를 열고 `chaincode_start.go`가 포함된 디렉토리를 찾아보십시오. 다음 명령을 입력하십시오.
	```
	go build ./
	```
1. **체인코드** API 섹션을 펼치십시오. 
1. `POST /chaincode` 섹션을 펼치십시오. 
1. 이전 `/registrar` 단계의 `enrollID` 및 체인코드 저장소 경로를 지정하여, 아래의 예제 코드에서 `DeploySpec` 텍스트 필드를 설정하십시오(기타 필드는 공백으로 둠). `"path":`는 `"https://github.com/johndoe/learn-chaincode/finished"`와 유사해야 합니다. 이는 chaincode_finished.go 파일에 대한 경로 및 저장소 분기에 대한 경로입니다. 

	```
	{
		"jsonrpc": "2.0",
		"method": "deploy",
		"params": {
			"type": 1,
			"chaincodeID": {
				"path": "https://github.com/ibm-blockchain/learn-chaincode/finished"
			},
			"ctorMsg": {
				"function": "init",
				"args": [
					"hi there"
				]
			},
			"secureContext": "user_type1_xxxxxxxxx"
		},
		"id": 1
	}
	```

  *응답 본문*은 다음 예와 같이 표시됩니다.

  ![배치 예](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/deploy_response.PNG "배치 예 응답 본문")

  배치에 대한 응답에는 이 체인코드의 ID가 포함됩니다. ID는 128자 영숫자 해시이며, 이는 향후 호출 및 조회 요청에 사용될 수 있습니다. 이 ID를 텍스트 편집기에 복사하십시오. 

#### 조회
`Init` 함수에서 설정한 `hello_world` 키의 값에 대해 체인코드를 조회하십시오. 
1. **체인코드** API 섹션을 펼치십시오. 
1. `POST /chaincode` 섹션을 펼치십시오. 
1. 이전 `/registrar` 단계의 `enrollID` 및 이전 배치 단계의 체인코드 ID를 지정하여 다음 예제에서 `QuerySpec` 텍스트 필드를 채우십시오(기타 필드는 공백으로 둠). 

	```
	{
		"jsonrpc": "2.0",
		"method": "query",
		"params": {
			"type": 1,
			"chaincodeID": {
				"name": "CHAINCODE_HASH_HERE"
			},
			"ctorMsg": {
				"function": "read",
				"args": [
					"hello_world"
				]
			},
			"secureContext": "user_type1_xxxxxxxxx"
		},
		"id": 2
	}
	```
  *응답 본문"은 다음 예와 같이 표시됩니다.

  ![조회 예](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query_response.PNG "조회 예 응답 본문")

  `hello_world`의 값은 "hi there"이며, 이전 배치 호출의 본문으로 설정됩니다.

#### 호출
`invoke`로 일반 쓰기 함수를 호출하십시오. `hello_world`의 값을 "go away"로 변경하십시오. 
1. **체인코드** API 섹션을 펼치십시오. 
1. `POST /chaincode` 섹션을 펼치십시오. 
1. 이전 `/registrar` 단계의 `enrollID` 및 이전 배치 단계의 체인코드 ID를 지정하여 다음 예제에서 `InvokeSpec` 텍스트 필드를 채우십시오(기타 필드는 공백으로 둠). 

	```
	{
		"jsonrpc": "2.0",
		"method": "invoke",
		"params": {
			"type": 1,
			"chaincodeID": {
				"name": "CHAINCODE_HASH_HERE"
			},
			"ctorMsg": {
				"function": "write",
				"args": [
					"hello_world",
					"go away"
				]
			},
			"secureContext": "user_type1_xxxxxxxxx"
		},
		"id": 3
	}
	```
  *응답 본문"은 다음 예와 같이 표시됩니다.

  ![호출 예](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/invoke_response.PNG "호출 예 응답 본문")

  위의 조회를 다시 실행하면 다음 응답을 받게 됩니다.

  ![조회2 예](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query2_response.PNG "호출 예 응답")

이제 일부 기본 체인코드 작성이 완료되었습니다.   

<br>
## Marbles, Commercial Paper 및 Car Lease 데모의 요구사항
{: #requirements}

다음 전제조건은 Marbles, Commercial Paper 및 Car Lease 애플리케이션을 로컬로 실행하기 위한 Bluemix 서비스에 포함되어 있습니다. Bluemix 환경은 이러한 종속 항목에 제공하기 위해 Hyperledger Fabric을 복제합니다. 

- Bluemix ID https://console.ng.bluemix.net/(IBM Blockchain 네트워크를 작성하고 피어 및 인증 기관에 대한 서비스 신임 정보를 제공하는 데 필요함)
- Node.js 0.12.0+ 및 npm v2+
- Golang 환경(자체 체인코드를 빌드하는 데만 필요함)

데모는 Node.js 및 express 모듈의 숙련을 필요로 합니다. 또한 블록체인 컨텍스트에서 '체인코드', '원장' 및 '피어'의 개념적 이해도 필요합니다. [Hyperledger Fabric 용어집](https://github.com/hyperledger/fabric/blob/master/docs/glossary.md)을 참조하십시오.   

<br>
## Marbles 데모 사용
{: #marbles}

Marbles 애플리케이션은 두 당사자 간에 단순 자산 이동을 예시합니다. 이 애플리케이션은 Javascript SDK를 테스트하고 이의 개발을 안내하며 개발자가 SDK 및 체인코드에 친숙해지는 데 도움이 되도록 설계되었습니다. 

웹 애플리케이션, SDK 및 체인코드가 함께 작동하는 방법을 알아보려면 [Marbles 튜토리얼](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md)을 탐색하십시오. 체인코드 및 IBM Blockchain을 이미 잘 알고 있는 경우에는 Bluemix에 데모를 [수동으로 배치](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md#)할 수 있습니다. 또는 "Bluemix에 배치" 단추를 클릭하여 웹 애플리케이션을 사용할 수 있습니다.  
[![Bluemix에 배치](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  

<br>
## Commercial Paper 데모 사용
{: #commercialpaper}

Commercial Paper 애플리케이션은 IBM Blockchain을 사용하여 기업어음 거래 네트워크를 구현하는 방법을 예시합니다. Commercial Paper 데모는 권한 부여된 블록체인 네트워크를 탐색하며, 여기서 해당 참가자에는 역할 및 대응되는 액세스 레벨이 지정됩니다. [Commercial Paper README](https://github.com/IBM-Blockchain/cp-web#readme)를 방문하여 이 데모의 컴포넌트에 대해 자세히 학습하거나, 이를 Bluemix에 직접 배치하여 실행 중인 거래 네트워크를 볼 수 있습니다.  
[![Bluemix에 배치](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  

<br>
## Car Lease 데모 사용
{: #carlease}

Car Lease 애플리케이션은 제조에서부서 일련의 소유자를 거쳐 폐차에 이르기까지 차량의 라이프사이클을 예시합니다. 데모는 서버 측 프로그래밍에 Node.js를 사용하며, IBM Blockchain 네트워크에서 실행 중인 체인코드에 Golang을 사용합니다. 데모에는 두 개의 체인코드 인스턴스가 포함됩니다. 하나는 차량 트랜잭션의 규칙을 정의하며, 다른 하나는 해당 수명 중의 모든 차량 거래를 로그합니다. 두 체인코드 프로그램은 모두 JSON 오브젝트를 사용하여 데이터를 저장합니다. [Car Lease README](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md)를 방문하여 이 데모와 연관된 애플리케이션 아키텍처 및 차량 속성에 대해 자세히 알아보거나 Bluemix에 즉시 데모를 배치하십시오.  
[![Bluemix에 배치](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  

<br>
## 비결정적 체인코드
{: #ndcc}

IBM Blockchain 네트워크는 결정적 체인코드만 지원합니다. 비결정적 체인코드의 사용은 지원되지 않으며, 블록체인 네트워크에서 서버 오류가 발생합니다. 

**비결정적 체인코드**는 블록체인 원장에서 시간이 지나면서 노드 간에 동일한 추가 값이 결과로 나타나지 **않는** 체인코드입니다. 이와는 대조적으로, **결정적 체인코드**는 블록체인 원장에서 시간이 지나면서 노드 간에 항상 동일한 추가 값을 생성합니다. 

### 결정적 체인코드 예제
변화 없이 모든 노드에서 결과가 항상 동일하므로, 항상 하나씩 변수 값을 증가시키는 **호출** 트랜잭션은 결정적입니다. 예를 들어, 이 트랜잭션이 5의 고정 값에 대해 실행될 때마다 추가된 값은 언제나 항상 모든 노드에서 6입니다. 결정적 체인코드의 네트워크 출력은 블록체인에서 서로 차이가 없습니다. 각 노드에서 원장의 사본은 항상 값이 이전 호출보다 1만큼 크다는 것을 표시합니다(동기화 이후). 

### 비결정적 체인코드 예제
시작일(00:00) 이후의 경과 시간(초)으로 블록체인 변수의 값을 증가시키는 **호출** 트랜잭션은 비결정적입니다. 시간이 지나면서 값이 노드 간에 변하기 때문입니다. 예를 들어, 이 트랜잭션이 고정 값 5에 대해 실행될 때마다 추가된 값은 노드 간에 분산됩니다(거의 예외가 없음). 시작일(00:00) 이후의 경과 시간(초)이 필연적으로 변하기 때문입니다. 이 비결정적 체인코드의 네트워크 출력은 분기하는 블록체인입니다. 모든 노드는 5 + 시작일(00:00) 이후의 경과 시간 값에서 일치하지 않습니다. 

### 무작위성
체인코드는 시간이 지나면서 노드 간에 추가된 값에서 무작위성을 드러내지 않아야 합니다. 무작위성은 노드 간에 분기하는 블록체인을 생성하며, 이는 다시 네트워크에 의해 해결되어야 합니다. 무작위성을 피하려면, 병렬 체인코드가 호출 체인코드의 입력 값에 영향을 줄 수 없음을 확인해야 합니다. 예를 들어, 병렬 조회가 노드 간에 호출 값에서 변화를 생성할 수 있으므로 **호출** 트랜잭션과 병렬로 **조회** 트랜잭션을 실행하지 마십시오. 

### 글로벌 변수 사용
글로벌 또는 인스턴스 변수를 사용하여 원장에서 검색된 값을 저장하거나 원장에 값을 설정하면 비결정성이 나타날 수 있습니다. 체인코드는 체인코드 컨테이너의 재시작 시 해당 상태를 유지하지 않는 글로벌 또는 인스턴스 변수에 의존해서는 안 됩니다. 다음은 글로벌 변수를 사용하는 예입니다. `stub.PutState` 함수를 통해 원장에 기록되는 `key` 값은 글로벌 변수에서 파생됩니다.

```go
//declare global variable
var INVOICE_COUNTER int64

//increment the counter and save the state
		INVOICE_COUNTER =INVOICE_COUNTER+1
		key := INVOICE+strconv.FormatInt(INVOICE_COUNTER, 10)
		ccLogger.Infof("The key formed for saving the state: %s", key)
		stub.PutState(key,[]byte(invoiceID))
```

### 맵 유형에 대해 반복
Go 프로그래밍 언어에서 순서가 결정적이지 않으므로, 맵 유형에 대해 반복하면 비결정성이 나타날 수 있습니다. 다음은 `columnTypes` 맵에 대한 반복 예입니다.

```go
 func generateColumns(colTypes map[string]string, colKeys []bool) ([]*shim.ColumnDefinition, error) {
	var tableColumns []*shim.ColumnDefinition
	keyIndex := 0
	for k, _ := range colTypes {
		tableColumns = append(tableColumns, &shim.ColumnDefinition{k, shim.ColumnDefinition_STRING, colKeys[keyIndex]})

		keyIndex++
	}
	return tableColumns, nil
}
```

<!---## Using the Node.js SDK
{: #nodesdk}

Use the [Hyperledger fabric client SDK ](https://github.com/IBM-Blockchain/ibm-blockchain-js/blob/master/README.md) library for easier interaction with an IBM Blockchain network.  The SDK, through importing packages and libraries, allows for an application developer to build Node.js applications that can invoke functionality on the blockchain network from the client side.  Member services and asset management are now pluggable components on client side applications.  See the [Enhanced Node.js SDK](etn_sdk.html) section for full documentation and application examples.--->
