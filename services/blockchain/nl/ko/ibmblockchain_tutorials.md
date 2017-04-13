---

copyright:
  years: 2016
lastupdated: "2016-11-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 샘플 앱 및 튜토리얼
{: #1stanchor}


다음 샘플은 애플리케이션 및 체인코드가 테스트 IBM Blockchain 네트워크에서 어떻게 작동하는지 보여줍니다. IBM Blockchain 네트워크의 기반이 되는 Hyperledger Fabric v0.6 코드에 대해 자세히 알아보려면 Linux Foundation의 Hyperledger 프로젝트의 [Fabric Docs](https://github.com/hyperledger/fabric/tree/v0.6/docs) 섹션을 방문하십시오.  
{:shortdesc}

작동 중인 체인코드 애플리케이션을 경험하기 위해 아래의 Marbles, Commercial Paper 또는 Car Lease 데모를 바로 배치할 수 있습니다(Bluemix에 배치 단추 클릭). 또는 읽기를 계속하여 "Hello Chaincode" 튜토리얼을 탐색하십시오. 

- [![Bluemix에 배치](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  **Marbles**
- [![Bluemix에 배치](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  **Commercial Paper**
- [![Bluemix에 배치](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  **Car Lease**  

<br>
## 체인코드 학습 튜토리얼
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
체인코드는 사용자가 블록체인 네트워크와 상호작용할 수 있도록 하는 Go(Golang) 또는 Java 코드입니다. 네트워크에서 트랜잭션을 '호출'할 때마다 원장에 대해 값을 읽고 쓰는 체인코드에서 함수를 호출합니다.   

<br>
## 개발 환경 설정
체인코드 개발을 시작하려면 먼저 다음 종속 항목과 권장 도구를 설치하십시오. 

### Git

- [Git 다운로드 페이지](https://git-scm.com/downloads)
- [Pro Git 서적](https://git-scm.com/book/en/v2)
- [Git 데스크탑(Git CLI의 대체)](https://desktop.github.com/)

Git은 체인코드 개발과 소프트웨어 개발에 일반적으로 사용하는 빠르고 강력한 버전 제어 도구입니다. Git for Windows와 함께 설치되는 Git bash는 권장 명령행 터미널입니다. 

Git 설치를 완료한 후에는 Git이 설치되었는지 확인하십시오. 

```
$ git version
git version 2.9.0.windows.1
```

Git을 설치한 후에는 [GitHub](https://github.com/)에 계정을 작성하십시오. Bluemix에서 IBM Blockchain 서비스를 사용하려면 REST API를 통해 배치할 수 있도록 체인코드가 GitHub 저장소에 있어야 합니다.   

## Go

Go는 현재 Bluemix에 체인코드를 작성할 때 지원되는 유일한 언어입니다. Go 설치에는 체인코드 작성에 사용할 수 있는 유용한 CLI 도구 세트가 포함되어 있습니다. 예를 들어, `go build` 명령을 사용하면 체인코드를 네트워크에 배치하기 전에 컴파일할 수 있습니다. Hyperledger Fabric v0.6 개발에 사용되는 Go v1.6 버전을 설치하십시오.   

- [Go 1.6 설치](https://golang.org/dl/#go1.6.3)
- [Go 설치 지시사항](https://golang.org/doc/install)
- [Go 문서 및 튜토리얼](https://golang.org/doc/)

다음 명령을 실행하여 Go가 올바르게 설치되었는지 확인하십시오. `go version` 명령의 출력은 운영 체제에 따라 달라집니다. 

```
$ go version
go version go1.6.3 windows/amd64

$ echo $GOPATH
C:\gopath
```

`GOPATH` 환경 변수는 앞의 예제와 꼭 일치하지 않아도 되지만 대신 파일 시스템의 올바른 디렉토리를 사용해야 합니다. `go build`를 실행하여 체인코드 컴파일을 확인하는 경우 Go에서 `$GOPATH/src` 디렉토리를 탐색하여 사용자가 체인코드의 `import` 블록에 나열한 비표준 종속 항목이 있는지 확인합니다. [Go 설치 지시사항](https://golang.org/doc/install)은 GOPATH 환경 변수 설정을 안내합니다.   

<br>
## Hyperledger Fabric

Blockchain on Bluemix에는 두 버전의 Hyperledger Fabric이 지원됩니다(v0.5 및 v0.6). 아래 설명과 같이, 체인코드 버전은 Bluemix 네트워크의 Hyperledger 버전에 맞추어야 합니다. 

주의:
1. 원장에 읽기 및 쓰기 기능을 사용하려면 체인코드에서 Hyperledger Fabric의 체인코드 shim을 가져와야 합니다. 
2. 체인코드를 로컬로 컴파일하려면 Hyperledger Fabric 코드 위치를 `GOPATH` 환경 변수에 지정해야 합니다. 

Bluemix 인스턴스에서 실행 중인 Hyperledger Fabric 버전을 판별하려면 대시보드 모니터의 **서비스 상태** 탭을 클릭하십시오. **릴리스 정보** 섹션으로 화면을 아래로 스크롤하십시오. `네트워크에서 이 버전을 사용 중입니다.` 패널에 실행 중인 **Hyperledger 커미트 레벨**이 표시됩니다. 

![Bluemix 백엔드 버전](images/fabricversion.png "Bluemix 백엔드 버전")
그림 1. Hyperledger Fabric 버전

체인코드 버전은 체인코드를 배치할 Hyperledger Fabric 버전에 맞추어야 합니다. 예를 들어, 그림 1에 표시된 네트워크에서는 Hyperledger Fabric v0.6-preview 코드 베이스를 복제해야 합니다. 각 버전의 패브릭 코드 베이스는 `$GOPATH/hyperledger/fabric` 경로에 저장해야 합니다. 

- [v0.5 Hyperledger Fabric](https://github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview)
- [v0.6 Hyperledger Fabric](https://gerrit.hyperledger.org/r/gitweb?p=fabric.git;a=shortlog;h=refs/heads/v0.6)

Hyperledger Fabric v0.5 코드 베이스를 설치하려면 다음 git clone 명령을 사용하십시오. 

```
# Create the parent directories on your GOPATH
mkdir -p $GOPATH/src/github.com/hyperledger
cd $GOAPTH/src/github.com/hyperledger

# Clone the appropriate release codebase into $GOPATH/src/github.com/hyperledger/fabric
# Note that the v0.5 release is a branch of the repository.  It is defined below after the -b argument
git clone -b v0.5-developer-preview https://github.com/hyperledger-archives/fabric.git
```

Hyperledger Fabric v0.6 코드 베이스를 설치하려면 다음 git clone 명령을 사용하십시오. 

```
# The v0.6 release exists as a branch inside the Gerrit fabric repository
git clone -b v0.6 http://gerrit.hyperledger.org/r/fabric
```

`GOPATH`에 패브릭이 올바르게 설치되지 않은 경우, 체인코드를 빌드하면 다음 예와 비슷한 오류가 리턴됩니다. 
```
$ go build .
chaincode_example02.go:27:2: cannot find package "github.com/hyperledger/fabric/core/chaincode/shim" in any of:
        C:\Go\src\github.com\hyperledger\fabric\core\chaincode\shim (from $GOROOT)
        C:\gopath\src\github.com\hyperledger\fabric\core\chaincode\shim (from $GOPATH)
```

### 개발 파이프라인 설정

다음 단계를 사용하여 체인코드의 작성, 빌드, 테스트를 위한 파이프라인을 설정하십시오. 체인코드는 로컬 시스템에 작성하며 컴파일 확인 후 GitHub에 업로드합니다. 그 후 패브릭 REST API를 사용하여 체인코드를 Bluemix 네트워크에 배치하고 테스트합니다. 

1. 네트워크 버전에 적합한 [체인코드 학습](https://github.com/IBM-Blockchain/learn-chaincode) 저장소 버전을 GitHub 계정으로 포크하십시오. v0.5 패브릭 네트워크에는 v1.0을, v0.6 패브릭 네트워크에는 v2.0을 포크하십시오. 이를 수행하는 한 가지 방법은 저장소 페이지의 오른쪽 상단에 있는 **Fork** 단추를 사용하는 것입니다. 포크하면 모든 분기를 비롯한 전체 저장소가 로컬 시스템에 복사되며 이는 페이지 왼쪽 상단의 **Branch:** 단추를 클릭하면 표시됩니다. CLI를 사용하여 포크하려면 다음 명령을 Git Bash 쉘에 입력하십시오. 

2. 포크를 $GOPATH에 복제하십시오.

  ```bash
  cd $GOPATH
  mkdir -p src/github.com/<YOUR_GITHUB_ID_HERE>/
  cd src/github.com/<YOUR_GITHUB_ID_HERE>/
  git clone -b v1.0 https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode.git
  OR
  git clone -b v2.0 https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode.git
  ```

  이제 로컬 시스템에 포크의 사본이 있습니다. 로컬 파일을 변경하거나 추가하여 체인코드를 작성하고 이를 GitHub의 포크로 푸시한 후 네트워크 피어의 REST API를 사용하여 체인코드를 블록체인 네트워크에 배치할 수 있습니다. 

3. 이 튜토리얼에 사용된 두 개의 체인코드 버전이 제공됩니다. **start**는 시작하는 스켈레톤 체인코드이며 **finished*는 빌드 준비가 완료된 체인코드입니다. 먼저, **start**가 로컬 환경에 빌드되었는지 확인하십시오. 

  ```bash
  cd $GOPATH/src/github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/start
  go build ./
  ```

learn-chaincode의 **start** 버전이 오류나 메시지가 표시되지 않고 컴파일되어야 합니다. 그렇지 않으면, 이전 지시사항을 검토하여 Go를 올바르게 설치하십시오. 

5. 로컬 체인코드 파일에 변경사항을 작성하고 업데이트된 파일을 GitHub 포크로 푸시하십시오. 

  ```bash
  cd $GOPATH/src/github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/
  # See what files have changed locally.  You should see chaincode_start.go
  git status
  # Stage all changes in the local repository for commit
  git add --all
  # Commit all staged changes.  Insert a short description after the -m argument
  git commit -m "Compiled my code"
  # Push local commits back to https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/
  git push
  ```

#### 체인코드 인터페이스 구현
다음 단계에서는 Go 코드로 체인코드 shim 인터페이스를 구현합니다. 3개의 기본 함수는 **Init**, **Invoke**, **Query**입니다. 세 함수는 모두 함수 이름과 문자열 배열을 입력으로 사용하지만 다른 지점에서 호출됩니다. 개발 과정의 마지막 단계로 블록체인 네트워크에서 교환할 일반 자산을 작성하는 작업 체인코드를 구성합니다. 

### 종속 항목
`import` 문은 체인코드 빌드에 사용하는 종속 항목을 나열합니다. 
1. `fmt` - 디버깅/로깅을 위한 `Println`이 포함됩니다. 
2. `errors` - 표준 Go 오류 형식입니다. 
3. `github.com/hyperledger/fabric/core/chaincode/shim` - Golang 코드를 네트워크 피어와 인터페이스하는 코드입니다. 

#### Init()
`Init` 함수는 체인코드를 처음 배치할 때 호출됩니다. 이름 그대로 이 함수는 체인코드를 초기화합니다. 이 예제에서 `Init` 함수는 원장의 단일 키/값 쌍에 대한 초기 상태를 구성합니다. 

첫 번째 `args` 요소를 "hello_world" 키에 저장하도록 `chaincode_start.go` 파일에서 `Init` 함수를 변경하십시오. 

```go
func (t *SimpleChaincode) Init(stub shim.ChaincodeStubInterface, function string, args []string) ([]byte, error) {
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

이는 stub 함수 `stub.PutState`를 사용하여 수행됩니다. 이 함수는 배치 요청에 전송된 첫 번째 인수를 'hello_world' 키에 저장할 값으로 해석합니다. 잘못된 개수의 인수를 전달하거나 원장 작성 중 문제가 있어 오류가 발생하는 경우 이 함수에서 오류를 리턴합니다. 그렇지 않은 경우에는 메시지가 표시되지 않고 정상 종료됩니다.   

#### Invoke()
`Invoke` 함수를 사용하여 블록체인 네트워크에서 "실제 작업"을 수행하는 체인코드 함수를 호출합니다. Invoke 함수는 트랜잭션으로 캡처되어 원장 작성에 사용하는 블록으로 그룹화됩니다. 원장 업데이트는 체인코드를 호출하여 수행됩니다. `Invoke`의 구조는 단순합니다. 함수와 인수 배열을 수신합니다. 호출 요청의 함수 매개변수에 따라 전달된 함수를 기반으로 `Invoke`에서 helper 함수를 호출하거나 오류를 리턴합니다. 

`chaincode_start.go` 파일에서 일반 쓰기 함수를 호출하도록 `Invoke` 함수를 변경하십시오. 

```go
func (t *SimpleChaincode) Invoke(stub shim.ChaincodeStubInterface, function string, args []string) ([]byte, error) {
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

코드에서 이제 `write`를 찾으므로, write 함수를 `chaincode_start.go` 파일에 추가하십시오. 

```go
func (t *SimpleChaincode) write(stub shim.ChaincodeStubInterface, args []string) ([]byte, error) {
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
`Query` 함수는 체인코드 상태를 조회하기 위해 호출되며, 체인(원장)에 블록을 추가하지 않습니다. 배치 및 호출 함수만 새 블록을 추가합니다. `Query`를 사용하여 체인코드 상태의 키/값 쌍에 대한 값을 읽을 수 있습니다. 

`chaincode_start.go` 파일에서 일반 읽기 함수를 호출하도록 `Query` 함수를 변경하십시오. 

```go
func (t *SimpleChaincode) Query(stub shim.ChaincodeStubInterface, function string, args []string) ([]byte, error) {
	fmt.Println("query is running " + function)

	// Handle different functions
	if function == "read" {                            //read a variable
		return t.read(stub, args)
	}
	fmt.Println("query did not find func: " + function)

	return nil, errors.New("Received unknown function query")
}
```

코드에서 이제 `read`를 찾으므로, 'read' 함수를 `chaincode_start.go` 파일에 추가하십시오. 

```go
func (t *SimpleChaincode) read(stub shim.ChaincodeStubInterface, args []string) ([]byte, error) {
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
  - `Value` 필드를 신임 정보의 `enrollSecret' 및 `enrollID`를 지정하는 JSON으로 채우십시오.

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
1. 이전 `/registrar` 단계의 `enrollID` 및 체인코드 저장소 경로를 지정하여, 아래의 예제 코드에서 `DeploySpec` 텍스트 필드를 설정하십시오(기타 필드는 공백으로 둠). `"path":`는 `"https://github.com/johndoe/learn-chaincode/finished"`와 유사해야 합니다. 이는 chaincode_finished.go 파일에 대한 경로 및 저장소 포크에 대한 경로입니다. 

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
## 데모 요구사항
{: #requirements}

다음 전제조건은 Bluemix 서비스에 포함되어 있으며 Marbles, Commercial Paper, Car Lease 데모 애플리케이션 실행에 필요합니다. Bluemix 환경은 이러한 종속 항목에 제공하기 위해 Hyperledger Fabric을 복제합니다. 

- Bluemix ID https://console.ng.bluemix.net/(IBM Blockchain 네트워크를 작성하고 피어 및 인증 기관에 대한 서비스 신임 정보를 제공하는 데 필요함)
- Node.js 0.12.0+ 및 npm v2+
- Golang 환경(자체 체인코드를 빌드하는 데만 필요함)

데모를 사용하려면 Node.js 및 express 모듈에 대해 잘 알아야 합니다. 또한 블록체인 컨텍스트에서 '체인코드', '원장' 및 '피어'의 개념적 이해도 필요합니다. [Hyperledger Fabric 용어집](https://github.com/hyperledger/fabric/blob/v0.6/docs/glossary.md)을 참조하십시오.   

<br>
## Marbles 데모
{: #marbles}

Marbles 애플리케이션은 두 당사자 간에 단순 자산 이동을 예시합니다. 이 애플리케이션은 Javascript SDK를 테스트하고 이의 개발을 안내하며 개발자가 SDK 및 체인코드에 친숙해지는 데 도움이 되도록 설계되었습니다. 

웹 애플리케이션, SDK 및 체인코드가 함께 작동하는 방법을 알아보려면 [Marbles 튜토리얼](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md)을 탐색하십시오. 체인코드 및 IBM Blockchain을 이미 잘 알고 있는 경우에는 Bluemix에 데모를 [수동으로 배치](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md#)할 수 있습니다. 또는 "Bluemix에 배치" 단추를 클릭하여 웹 애플리케이션을 사용할 수 있습니다.  
[![Bluemix에 배치](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  

<br>
## Commercial Paper 데모
{: #commercialpaper}

Commercial Paper 애플리케이션은 IBM Blockchain을 사용하여 기업어음 거래 네트워크를 구현하는 방법을 예시합니다. Commercial Paper 데모는 권한 부여된 블록체인 네트워크를 탐색하며, 여기서 해당 참가자에는 역할 및 대응되는 액세스 레벨이 지정됩니다. [Commercial Paper README](https://github.com/IBM-Blockchain/cp-web#readme)를 방문하여 이 데모의 컴포넌트에 대해 자세히 학습하거나, 이를 Bluemix에 직접 배치하여 실행 중인 거래 네트워크를 볼 수 있습니다.  
[![Bluemix에 배치](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  

<br>
## Car Lease 데모
{: #carlease}

Car Lease 애플리케이션은 제조에서부서 일련의 소유자를 거쳐 폐차에 이르기까지 차량의 라이프사이클을 예시합니다. 데모는 서버 측 프로그래밍에 Node.js를 사용하며, IBM Blockchain 네트워크에서 실행 중인 체인코드에 Golang을 사용합니다. 데모에는 두 개의 체인코드 인스턴스가 포함됩니다. 하나는 차량 트랜잭션의 규칙을 정의하며, 다른 하나는 해당 수명 중의 모든 차량 거래를 로그합니다. 두 체인코드 프로그램은 모두 JSON 오브젝트를 사용하여 데이터를 저장합니다. [Car Lease README](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md)를 방문하여 이 데모와 연관된 애플리케이션 아키텍처 및 차량 속성에 대해 자세히 알아보거나 Bluemix에 즉시 데모를 배치하십시오.  
[![Bluemix에 배치](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  

<br>

<!-- comment out - moving to separate file for now jh
## Non-deterministic chaincode
{: #ndcc}

IBM Blockchain networks support deterministic chaincode only. Using non-deterministic chaincode is not supported, and will cause severe errors, on any blockchain network.

**Non-deterministic chaincode** is any chaincode that does **not** result in the same appended value, over time and across nodes, on the blockchain ledger. By contrast, **deterministic chaincode** always produces the same appended value, over time and across nodes, on the blockchain ledger.

### Deterministic chaincode example
An **invoke** transaction that always increments the value of a variable by one is deterministic, because the result is always the same, on every node, without variance. Whenever this transaction is run against a fixed value of five, for example, the appended value is always six, on every node, every time. The network outcome for deterministic chaincode is no divergence in the blockchain; the copy of the ledger on each node always indicates (after syncing) that the value is one greater than the previous invocation.

### Non-deterministic chaincode example
An **invoke** transaction that increments the value of a blockchain variable with the number of elapsed seconds since the start of the day (00:00) is non-deterministic, because over time the value will vary across nodes. Each time this transaction is run against a fixed value of five, for example, the appended value diverges across nodes (with rare exceptions), because the number of elapsed seconds since 00:00 will inevitably vary. The network outcome for this non-deterministic chaincode is divergent blockchains; all nodes will not agree on the value of five + the number of elapsed seconds since 00:00.

### Randomness
Chaincode must exhibit no randomness in the appended values, over time and across nodes. Any randomness produces divergent blockchains across nodes, which must then be resolved by the network. To avoid randomness, you must ensure that no parallel chaincode can affect the input value from invocation chaincode. For example, do not run any **query** transactions in parallel with **invoke** transactions, because parallel queries could produce variance in the invocation values across nodes.

### Using a global variable
Using a global or instance variable to store a value that was retrieved from the ledger, or to set a value on the ledger, can lead to non-determinism. Chaincode should not rely on global or instance variables that will not retain their state across restarts of a chaincode container. The following is an example that uses a global variable; the value of `key`, which is written to the ledger via the `stub.PutState` function, is derived from a global variable:

```go
//declare global variable
var INVOICE_COUNTER int64

//increment the counter and save the state
		INVOICE_COUNTER =INVOICE_COUNTER+1
		key := INVOICE+strconv.FormatInt(INVOICE_COUNTER, 10)
		ccLogger.Infof("The key formed for saving the state: %s", key)
		stub.PutState(key,[]byte(invoiceID))
```

### Iterating over a map type
Iteration over a map type can lead to non-determinism, because order is not deterministic in the Go programming language. The following is an example of iteration over the map named `columnTypes`:

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

-->


<!-- ## Using the Node.js SDK
{: #nodesdk}

Use the [Hyperledger fabric client SDK ](https://github.com/IBM-Blockchain/ibm-blockchain-js/blob/master/README.md) library for easier interaction with an IBM Blockchain network.  The SDK, through importing packages and libraries, allows for an application developer to build Node.js applications that can invoke functionality on the blockchain network from the client side.  Member services and asset management are now pluggable components on client side applications.  See the [Enhanced Node.js SDK](etn_sdk.html) section for full documentation and application examples. -->
