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

# 範例應用程式及指導教學
{: #1stanchor}


下列範例示範應用程式和 chaincode 如何在測試 IBM Blockchain 網路上運作。若要進一步瞭解加強 IBM Blockchain 網路的 Hyperledger Fabric 0.6 版程式碼，請造訪 Linux Foundation 之 Hyperledger Project 的 [Fabric Docs](https://github.com/hyperledger/fabric/tree/v0.6/docs)。  
{:shortdesc}

若要動態體驗鏈碼應用程式，您可以立即部署底下的「大理石」、「商業票據」或「租車」展示（按一下「部署至 Bluemix」按鈕）。或繼續閱讀以探索 Hello Chaincode 指導教學。

- [![部署至 Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  **大理石**
- [![部署至 Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  **商業票據**
- [![部署至 Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  **租車**  

<br>
## 了解 chaincode 指導教學
{: #hellocc}
本指導教學可指引您完成使用基本構成要素來撰寫基礎鏈碼應用程式的程式碼。您將漸進式地建置可運作的鏈碼，建立一般資產以在網路上交換。接著您會透過網路 API 與鏈碼互動。完成本指導教學之後，您將可以回答下列問題：
- 何謂鏈碼？
- 如何實作鏈碼？
- 有什麼相依關係存在？
- 主要函數有哪些？
- 如何將不同值傳遞至我的引數？
- 如何在我的網路上安全地登記使用者？
- 如何編譯鏈碼？
- 如何透過 REST API 與我的鏈碼互動？

### 何謂鏈碼？
chaincode 是 Go (Golang) 或 Java 程式碼，可讓使用者與區塊鏈網路互動。每當您在網路上「呼叫」(invoke) 交易時，都會呼叫鏈碼中的函數，讀取及寫入分類帳中的值。  

<br>
## 設定開發環境
若要開始開發 chaincode，首先安裝下列相依關係及建議工具：

### Git

- [Git 下載頁面](https://git-scm.com/downloads)
- [Pro Git 書籍](https://git-scm.com/book/en/v2)
- [Git Desktop（Git CLI 的替代方案）](https://desktop.github.com/)

Git 是快速且功能強大的版本控制工具，用於 chaincode 開發，而且通常用於軟體開發。與 Git for Windows 一起安裝的 Git Bash 是建議的指令行終端機。

在完成 Git 安裝之後，請驗證是否已安裝 Git：

```
$ git version
git version 2.9.0.windows.1
```

一旦安裝了 Git，即可在 [GitHub](https://github.com/) 建立自己的帳戶。Bluemix 上的 IBM Blockchain 服務需要 chaincode 位於 GitHub 儲存庫，才能透過 REST API 進行部署。  

## Go

Go 是目前可在 Bluemix 上撰寫 chaincode 的唯一支援語言。Go 安裝包括一組用於撰寫 chaincode 的有用 CLI 工具。例如，`go build` 指令可讓您先編譯 chaincode，然後再嘗試將它部署至網路。請安裝 Go 1.6 版，這是用來開發 Hyperledger Fabric 0.6 版的版本：  

- [Go 1.6 安裝](https://golang.org/dl/#go1.6.3)
- [Go 安裝指示](https://golang.org/doc/install)
- [Go 文件及指導教學](https://golang.org/doc/)

執行下列指令，驗證是否已適當地安裝 Go。`go version` 指令的輸出可能有所不同，視作業系統而定：

```
$ go version
go version go1.6.3 windows/amd64

$ echo $GOPATH
C:\gopath
```

您的 `GOPATH` 環境變數不必符合先前範例，但是您必須在檔案系統上使用有效的目錄。當您執行 `go build` 以驗證 chaincode 是否編譯時，Go 會在 `$GOPATH/src` 目錄中尋找您在 chaincode 的 `import` 區塊中列出的任何非標準相依關係。[Go 安裝指示](https://golang.org/doc/install)會引導您進行 GOPATH 環境變數設定。  

<br>
## Hyperledger Fabric

Blockchain on Bluemix 支援兩種 Hyperledger Fabric 版本：0.5 版與 0.6 版。如下述，您的 chaincode 版本必須與 Bluemix 網路上的 Hyperledger 版本匹配。

注意：
1. 若要在分類帳上啟用讀取及寫入功能，您的 chaincode 必須從 Hyperledger Fabric 匯入 chaincode shim。
2. 若要在本端編譯您的 chaincode，您必須在 `GOPATH` 環境變數中指定 Hyperledger Fabric 程式碼位置。

若要判定您的 Bluemix 實例正在執行哪個版本的 Hyperledger Fabric，請按一下「儀表板版本」上的**服務狀態**標籤。向下捲動至**版本注意事項**區段；`您的網路正在使用此版本`畫面將顯示您正在執行的 **Hyperledger 確定層次**：

![Bluemix 後端版本](images/fabricversion.png "Bluemix 後端版本")
圖 1. Hyperledger Fabric 版本

您的 chaincode 版本必須與將部署您的 chaincode 的 Hyperledger Fabric 版本匹配。例如，圖 1 中描述的網路需要複製 Hyperledger Fabric 0.6 版預覽程式碼庫。任一版本的網狀架構程式碼庫均須儲存在 `$GOPATH/hyperledger/fabric` 路徑中：

- [0.5 版 Hyperledger Fabric](https://github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview)
- [0.6 版 HHyperledger Fabric](https://gerrit.hyperledger.org/r/gitweb?p=fabric.git;a=shortlog;h=refs/heads/v0.6)

若要安裝 Hyperledger Fabric 0.5 版程式碼庫，請使用下列 git clone 指令：

```
# Create the parent directories on your GOPATH
mkdir -p $GOPATH/src/github.com/hyperledger
cd $GOAPTH/src/github.com/hyperledger

# Clone the appropriate release codebase into $GOPATH/src/github.com/hyperledger/fabric
# Note that the v0.5 release is a branch of the repository.  It is defined below after the -b argument
git clone -b v0.5-developer-preview https://github.com/hyperledger-archives/fabric.git
```

若要安裝 Hyperledger Fabric 0.6 版程式碼庫，請使用下列 git clone 指令：

```
# The v0.6 release exists as a branch inside the Gerrit fabric repository
git clone -b v0.6 http://gerrit.hyperledger.org/r/fabric
```

如果網狀架構未適當地安裝在您的 `GOPATH` 中，則建置您的 chaincode 時將傳回與下列範例類似的錯誤：
```
$ go build .
chaincode_example02.go:27:2: cannot find package "github.com/hyperledger/fabric/core/chaincode/shim" in any of:
        C:\Go\src\github.com\hyperledger\fabric\core\chaincode\shim (from $GOROOT)
        C:\gopath\src\github.com\hyperledger\fabric\core\chaincode\shim (from $GOPATH)
```

### 設定您的開發管線

請使用下列步驟，設定用於撰寫、建置並測試 chaincode 的管線。您將在本端機器上撰寫 chaincode、驗證它是否編譯，並將它上傳至 GitHub。然後，將使用網狀架構 REST API，在 Bluemix 網路上部署並測試您的 chaincode：

1. 將您網路版本適用的 [learn chaincode](https://github.com/IBM-Blockchain/learn-chaincode) 儲存庫版本分出至您的 GitHub 帳戶。對 0.5 版網狀架構網路分出 1.0 版，或對 0.6 版網狀架構網路分出 2.0 版。其中一個選項為使用頁面右上角的**分出**按鈕。分出會將整個儲存庫複製至您的本端機器，包括按一下頁面左上角的**分支：**按鈕所顯示的所有分支。若要使用 CLI 進行分出，請將下列指令輸入至您的 Git Bash Shell：

2. 將您的分出複製至您的 $GOPATH：

  ```bash
  cd $GOPATH
  mkdir -p src/github.com/<YOUR_GITHUB_ID_HERE>/
  cd src/github.com/<YOUR_GITHUB_ID_HERE>/
  git clone -b v1.0 https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode.git
  OR
  git clone -b v2.0 https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode.git
  ```

  現在您在本端機器上具有分出的副本。若要撰寫 chaincode，請變更或新增本端檔案、將它們推送至您在 GitHub 上的分出，然後在網路對等節點上使用 REST API，將您的 chaincode 部署至您的區塊鏈網路。

3. 在本指導教學中使用的 chaincode 提供有兩個版本：**start** 是您將從中開始的架構 chaincode，而 **finished* 是您備妥要建置的已完成 chaincode。首先，確定 **start** 建置在您的本端環境中：

  ```bash
  cd $GOPATH/src/github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/start
  go build ./
  ```

learn-chaincode 的 **start** 版本應該編譯，而且沒有顯示任何錯誤或訊息。若非如此，請檢閱先前指示以正確地安裝 Go。

5. 將變更寫入至您的本端 chaincode 檔案，然後將更新的檔案推送至您的 GitHub 分出：

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

#### 實作 chaincode 介面
下一步是在您的 Go 程式碼中實作 chaincode shim 介面。三個主要函數為 **Init**、**Invoke** 及 **Query**。這三個函數全都採用一個函數名稱及一連串字串作為輸入，但在不同點呼叫。您的開發路徑會以工作中 chaincode 結束，而此 chaincode 會建立一般資產以在區塊鏈網路上交換。

### 相依關係
`import` 陳述式列出用於建置 chaincode 的相依關係：
1. `fmt` - 包含 `Println` 以進行除錯/記載。
2. `errors` - 標準的 Go 錯誤格式。
3. `github.com/hyperledger/fabric/core/chaincode/shim` - 讓 Golang 程式碼與網路對等節點互動的程式碼。

#### Init()
第一次部署 chaincode 時，會呼叫 `Init` 函數。顧名思義，使用此函數即可起始設定 chaincode。在此範例中，`Init` 會在分類帳上配置單一索引鍵/值配對的起始狀態。

在您的 `chaincode_start.go` 檔中，變更 `Init` 函數，使其將第一個 `args` 元素儲存至索引鍵 "hello_world"：

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

作法為使用 stub 函數 `stub.PutState`。此函數會將部署要求中傳送的第一個引數解譯為要在索引鍵 'hello_world' 下儲存的值。如果發生錯誤的原因是傳入的引數數目錯誤，或寫入至分類帳時出錯，則此函數會傳回錯誤。否則，它會乾淨地結束，不傳回任何訊息。  

#### Invoke()
使用 `Invoke` 函數，呼叫 chaincode 函數以在區塊鏈網路上執行「實際工作」。Invoke 函數會被當成交易來擷取，以分組成各種區塊來寫入至分類帳。更新分類帳的方式為呼叫您的 chaincode。`Invoke` 的結構很簡單；它會接收一個函數及一連串引數。根據呼叫要求中函數參數所傳入的函數，`Invoke` 將呼叫 helper 函數或傳回錯誤。

在您的 `chaincode_start.go` 檔案中，將 `Invoke` 函數變更為呼叫一般 write 函數：

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

程式碼現在會尋找 `write`，因此請將 write 函數新增至您的 `chaincode_start.go` 檔案：

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

這個 `write` 函數應該看起來類似您先前的 `Init` 變更。您現在可以設定 `PutState` 的索引鍵和值，它允許您在區塊鏈分類帳上儲存任何索引鍵/值配對。

#### Query()
呼叫 `Query` 函數是為了查詢您的 chaincode 狀態，而且不會將區塊新增至鏈（分類帳）。只有 deploy 和 invoke 函數會新增區塊。請使用 `Query` 來讀取鏈碼狀態的索引鍵/值配對的值。

在您的 `chaincode_start.go` 檔中，變更 `Query` 函數，使其呼叫一般的 read 函數：

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

程式碼現在會尋找 `read`，因此請將 'read' 函數新增至您的 `chaincode_start.go` 檔案：

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

這個 `read` 函數會使用 `GetState`，它是 `PutState` 的互補。這個 shim 函數只採用一個字串引數：要擷取的索引鍵名稱。接下來，這個函數會將位元組陣列形式的值，傳回給 `Query`，後者則將它傳送給 REST 處理程式。

#### Main()
`main` 函數會在每個對等節點部署其鏈碼實例時執行。它會啟動鏈碼並向對等節點登錄。'main' 不需要程式碼更新；chaincode_start.go 和 chaincode_finished.go 都在每個檔案的頂端包含了 `main` 函數：

```go
func main() {
	err := shim.Start(new(SimpleChaincode))
	if err != nil {
		fmt.Printf("Error starting Simple chaincode: %s", err)
	}
}
```

### 與鏈碼互動
測試鏈碼最快的方法是在對等節點使用 REST 介面。Bluemix 儀表板監視器上的 Swagger 使用者介面，可讓您實驗鏈碼的部署，而不必撰寫任何其他程式碼。  

#### Swagger API
完成下列步驟，以使用 Swagger API：

1. 登入 [Bluemix](https://console.ng.bluemix.net/login) 並確定您在**儀表板**標籤上。
1. 檢查您是否在包含 IBM Blockchain 服務的相同 Bluemix 空間中。空間導覽在左邊。
1. 接近底端有一個**服務**畫面；按一下 IBM Blockchain 服務。
1. 您應該看到「歡迎使用 IBM Blockchain...」訊息；按一下右邊的**啟動**按鈕。
1. 在監視器頁面上，您應該看到兩個表格；底端表格可能是空的。
	- **網路標籤：**
		- **對等節點日誌**在頂端表格。在**對等節點 1** 的列，按一下檔案圖示，以檢視日誌。除了這個靜態視圖，在接近頁面頂端的**檢視日誌**標籤有即時的**串流對等節點日誌**。
		- **鏈碼日誌**在底端表格。每個鏈碼會標示鏈碼雜湊，這是在它部署時所傳回。選取任何鏈碼列中的對等節點，然後按一下檔案圖示，以檢視日誌。
	- **API 標籤**：顯示 Swagger API 文件頁面。
1. 繼續下列步驟，以實作安全的登記。在 REST 介面呼叫 `/chaincode` 端點需要安全環境定義 ID。為了讓大部分 REST 呼叫被接受，您必須傳遞來自服務認證清單的已登錄 *enrollID*：
  - 按一下 **+ 網路的登記 ID**，以展開 *enrollID* 值及其密碼的清單。
  - 將認證集複製到文字檔，以便之後使用。
  - 展開**登記員** API 區段。
  - 展開 `POST /registrar` 區段。
  - 用 JSON 移入 `Value` 欄位，該 JSON 指定來自您的認證的 `enrollID` 和 `enrollSecret`：

  ![Register 範例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/registrar.PNG "Register 範例")

  *回應內文* 應該類似下列範例：

  ![Register 範例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/register_response.PNG "Register 範例回應內文")

既然您已設定 `enrollID`，便可以在接下來的步驟裡部署、呼叫及查詢鏈碼時使用此 ID。
### 部署鏈碼
為了要透過 REST 介面部署鏈碼，您的鏈碼必須儲存在公用 GitHub 儲存庫。傳送 deploy 要求到對等節點時，請指定鏈碼儲存庫的 URL，以及起始設定鏈碼用的參數。

**在部署鏈碼之前**，請驗證它是在本端環境建置：
1. 開啟命令提示字元，然後瀏覽至包含 `chaincode_start.go` 的目錄。輸入下列指令：
	```
	go build ./
	```
1. 展開 **Chaincode** API 區段。
1. 展開 `POST /chaincode` 區段。
1. 使用以下的程式碼範例設定 `DeploySpec` 文字欄位（讓其他欄位空白），並指定您的鏈碼儲存庫路徑，以及先前 `/registrar` 步驟中的 `enrollID`。`"path":` 應該看似：`"https://github.com/johndoe/learn-chaincode/finished"`。這是儲存庫分出項的路徑，加上您 chaincode_finished.go 檔案的路徑：

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

  *回應內文* 應該類似下列範例：

  ![Deploy 範例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/deploy_response.PNG "Deploy 範例回應內文")

  部署的回應將包含此鏈碼的 ID。ID 是一個 128 個字元的英數雜湊，您可以將其用於未來的 invoke 或 query 要求。請將這個 ID 複製到文字編輯器。

#### Query()
查詢鏈碼的 `hello_world` 索引鍵值，這是您使用 `Init` 函數所設定：
1. 展開 **Chaincode** API 區段。
1. 展開 `POST /chaincode` 區段。
1. 使用下列範例移入 `QuerySpec` 文字欄位（讓其他欄位空白），並指定先前部署步驟的鏈碼 ID，以及先前 `/registrar` 步驟中的 `enrollID`。

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
 「回應內文」應該類似下列範例：

  ![Query 範例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query_response.PNG "Query 範例回應內文")

  `hello_world` 的值是 "hi there"，這是由您先前 deploy 呼叫的內文所設定。

#### Invoke()
使用 `invoke` 呼叫您的一般 write 函數。將 `hello_world` 的值變更為 "go away"：
1. 展開 **Chaincode** API 區段。
1. 展開 `POST /chaincode` 區段。
1. 使用下列範例移入 `InvokeSpec` 文字欄位（讓其他欄位空白），並指定先前部署步驟的鏈碼 ID，以及先前 `/registrar` 步驟中的 `enrollID`。

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
 「回應內文」應該類似下列範例：

  ![Invoke 範例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/invoke_response.PNG "Invoke 範例回應內文")

  重新執行上述查詢，您應該得到下列回應：

  ![Query2 範例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query2_response.PNG "Invoke 範例回應")

您剛剛已完成撰寫某個基本 chaincode。  

<br>
## 展示需求
{: #requirements}

若要執行 Marbles、Commercial Paper 及 Car Lease 展示應用程式，需要 Bluemix 服務隨附的下列必備項目。您的 Bluemix 環境會複製 Hyperledger Fabric 以提供下列相依關係：

- Bluemix ID https://console.ng.bluemix.net/（建立 IBM Blockchain 網路及提供服務認證給對等節點和憑證管理中心時需要）
- Node.js 0.12.0+ 及 npm v2+
- Golang 環境（僅自行建置鏈碼時需要）

展示也需要您精通 Node.js 和 express 模組。您也必須對於區塊鏈環境定義的「鏈碼」、「分類帳」和「對等節點」有概念上的瞭解；請參閱 [Hyperledger Fabric  Glossary](https://github.com/hyperledger/fabric/blob/v0.6/docs/glossary.md)。  

<br>
## 大理石展示
{: #marbles}

「大理石」應用程式示範兩方之間簡單的資產轉移。應用程式的設計是要測試 JavaScript SDK、指引其開發，以及協助開發人員熟悉 SDK 和 chaincode。

探索 [Marbles Tutorials](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md) 以瞭解 Web 應用程式、SDK 及鏈碼如何一起運作。如果您已經熟悉鏈碼和 IBM Blockchain，可以將展示[手動部署](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md#)至 Bluemix，或按一下「部署至 Bluemix」按鈕以使用 Web 應用程式：
  
[![部署至 Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  

<br>
## 商業票據展示
{: #commercialpaper}

「商業票據」應用程式示範如何使用 IBM Blockchain 實作商業票據交易網路。「商業票據」展示會探索具有許可權的區塊鏈網路，在這個網路上，參與者會被指派角色以及相對應的存取層次。請造訪 [Commercial Paper README](https://github.com/IBM-Blockchain/cp-web#readme) 以進一步瞭解這份展示的元件，或立即將它部署至 Bluemix，查看運作中的交易網路：
  
[![部署至 Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  

<br>
## 租車展示
{: #carlease}

「租車」應用程式示範車輛的生命週期，從製造、經過一系列擁有者，最後到車輛報廢。展示使用 Node.js 進行伺服器端程式設計，針對在 IBM Blockchain 網路上執行的鏈碼則使用 Golang。展示包含兩個鏈碼實例：一個定義車輛交易的規則，另一個則記載生命週期內的所有車輛交易。兩個鏈碼程式都使用 JSON 物件來儲存資料。請造訪 [Car Lease README](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md) 以進一步瞭解與這份展示相關聯的應用程式架構和車輛屬性，或將展示立即部署至 Bluemix：
  
[![部署至 Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  

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
