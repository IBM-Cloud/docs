---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 範例應用程式及指導教學
{: #1stanchor}
前次更新：2016 年 10 月 5 日
{: .last-updated}

下列範例示範 IBM Blockchain 網路中的應用程式和鏈碼如何運作。若要進一步瞭解加強您的區塊鏈網路的 Hyperledger Fabric 0.5 版程式碼，請造訪 Linux Foundation 之 Hyperledger Project 的 [Fabric Docs](https://github.com/hyperledger/fabric/tree/master/docs) 小節。  
{:shortdesc}

若要動態體驗鏈碼應用程式，您可以立即部署底下的「大理石」、「商業票據」或「租車」展示（按一下「部署至 Bluemix」按鈕）。或繼續閱讀以探索 Hello 鏈碼指導教學。

- [![部署至 Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  **大理石**
- [![部署至 Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  **商業票據**
- [![部署至 Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  **租車**  

<br>
## 使用 Hello 鏈碼指導教學
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
鏈碼是可讓使用者與區塊鏈網路互動的 Go (GoLang) 或 Java 程式碼。每當您在網路上「呼叫」(invoke) 交易時，都會呼叫鏈碼中的函數，讀取及寫入分類帳中的值。

### 實作您的第一個鏈碼
請完成下列主題，以在 IBM Blockchain on Bluemix 網路上實作鏈碼：
#### 設定環境
1. 下載並安裝您作業系統的 Golang：[GoLang](https://golang.org/dl/)。
2. 設定 GOPATH：
	- $GOPATH 是您的 Go 程式碼及專案的**環境變數**路徑。必須設定 $GOPATH 才能在標準 Go 樹狀結構之外取得、建置及安裝套件。因此，$GOPATH 必須是從 $GOROOT 路徑（您的原始 Go 樹狀結構所在之處）起唯一的路徑徑。您只要建立目錄，然後將 $GOPATH 指向該處。
	- 在 Windows 上設定 $GOPATH：
		- 建立專案的工作區目錄，例如 C:\Users\ADMIN\Documents\GoProjects。
		- 按一下 Windows **開始**功能表，並搜尋「系統環境變數」。
		- 按一下**編輯系統環境變數**。
		- 從**進階**標籤，按一下**環境變數**。
		- 尋找您的系統環境變數 GOPATH 和 GOROOT。如果需要建立 GOPATH，請按一下**新建**。  
		- GOROOT 及 GOPATH 值必須是唯一的。當您安裝 Go 時會自動產生 GOROOT，且應該是 C:\Go\。
		- 將 GOPATH 設定成您建立的工作區目錄。在此範例中，**GOPATH** 是 **C:\Users\ADMIN\Documents\GoProjects**。  
		- 如需詳細資料，請執行指令 `go help gopath` 或造訪 [Go 文件](https://golang.org/doc/install)。
3. 執行下列指令，將 Hyperledger Faric 0.5 版 shim 程式碼新增至 Go 路徑：

	```
	go get github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview/core/chaincode/shim
	```

4. **附註**：請務必遵循上述鏈結來匯入 0.5 版 hyperledger-archives shim 程式碼。Bluemix 後端會使用這個相同的版本來建置；因此，請務必使 shim 版本和 Bluemix 版本一致。

#### 設定 GitHub
Blockchain on Bluemix 方案要求您的鏈碼位於 [GitHub](https://Github.com/) 儲存庫。建立 GitHub 帳戶並如 [Set Up Git](https://help.github.com/articles/set-up-git/) 中所述地設定 Git。設定 GitHub 之後，請完成下列步驟：
1. 前往 [learn chaincode](https://github.com/IBM-Blockchain/learn-chaincode) 並分出儲存庫。  
2. 將分出項複製到 $GOPATH 中指定的目錄。  
3. 儲存庫包含兩個鏈碼目錄：[Start](https://github.com/IBM-Blockchain/learn-chaincode/blob/master/start/chaincode_start.go) 是您要從該處開始建置的鏈碼。[Finished](https://github.com/IBM-Blockchain/learn-chaincode/blob/master/finished/chaincode_finished.go) 是您最終會建置的鏈碼。
4. 確定鏈碼建置在您的本端環境中。開啟命令提示字元，然後導覽至包含 `chaincode_start.go` 的資料夾。輸入下列指令：

	```
	go build ./
	```
指令應該傳回且沒有錯誤或訊息。


#### 實作鏈碼介面
下一步是在您的 Golang 程式碼中實作鏈碼 shim 介面。三個主要的函數是 **Init**、**Invoke** 和 **Query**。這三個函數都需要一個函數名稱和一個字串陣列作為輸入，但會隨著它們呼叫的時機而變。您將建置可運作的鏈碼，建立一般資產以在區塊鏈網路上交換。

### 相依關係
The `import` 陳述式會列出建置鏈碼所需要的相依關係：
1. `fmt` - 包含 `Println` 以進行除錯/記載。
2. `errors` - 標準的 Go 錯誤格式。
3. `github.com/hyperledger/fabric/core/chaincode/shim` - 讓 Golang 程式碼與網路對等節點互動的程式碼。

### 傳遞值

會傳遞下列鏈碼值：
#### Init()
在您第一次將鏈碼部署至網路時，會呼叫 Init 以起始設定您的鏈碼。在本例中，您使用 `Init` 來配置分類帳上一個變數的起始狀態。

在您的 `chaincode_start.go` 檔中，變更 `Init` 函數，使其將第一個 `args` 元素儲存至索引鍵 "hello_world"：

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

這是使用 shim 函數 `stub.PutState` 來完成。第一個引數以字串形式採用索引鍵，第二個引數則是位元組陣列形式的值。此函數可能傳回錯誤，如果有錯誤的話您的程式碼會檢查並傳回它。

#### Invoke()
會呼叫 `Invoke` 以新增交易要求給鏈結。`Invoke` 的結構很簡單；它收到 `function` 引數，並根據這個引數在鏈碼中呼叫 Go 函數。

在您的 `chaincode_start.go` 檔中，變更 `Invoke` 函數，使其呼叫一般的 write 函數。

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

程式碼現在會尋找 `write`，因此請將該函數新增至您的 `chaincode_start.go` 檔案：

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

這個 `write` 函數應該看起來類似您先前的 `Init` 變更。您現在可以設定 `PutState` 的索引鍵和值，它允許您在區塊鏈分類帳上儲存任何索引鍵/值配對。

#### Query()
會呼叫 `Query` 來查詢您的鏈碼狀態，且不會新增區塊至鏈結。只有 deploy 和 invoke 函數會新增區塊。請使用 `Query` 來讀取鏈碼狀態的索引鍵/值配對的值。

在您的 `chaincode_start.go` 檔中，變更 `Query` 函數，使其呼叫一般的 read 函數：

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

程式碼現在會尋找 `read`，因此請將該函數新增至您的 `chaincode_start.go` 檔案：

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

這個 `read` 函數會使用 `GetState`，它是 `PutState` 的互補。這個 shim 函數只採用一個字串引數，也就是要擷取的索引鍵名稱。接下來，這個函數會將位元組陣列形式的值，傳回給 `Query`，後者則將它傳送給 REST 處理程式。

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

<br>
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
  - 用 JSON 移入 ``Value`` 欄位，該 JSON 指定來自您的認證的 ``enrollID` 和 `enrollSecret`：

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
1. 展開**鏈碼** API 區段。
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
1. 展開**鏈碼** API 區段。
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
1. 展開**鏈碼** API 區段。
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

您剛剛已完成撰寫某個基本鏈碼。  

<br>
## 大理石、商業票據和租車展示的需求
{: #requirements}

下列必要條件包含在您的 Bluemix 服務，以便在本端執行「大理石」、「商業票據」及「租車」應用程式。您的 Bluemix 環境會複製 Hyperledger Fabric 以提供下列相依關係：

- Bluemix ID https://console.ng.bluemix.net/（建立 IBM Blockchain 網路及提供服務認證給對等節點和憑證管理中心時需要）
- Node.js 0.12.0+ 及 npm v2+
- Golang 環境（僅自行建置鏈碼時需要）

展示需要您精通 Node.js 和 express 模組。您也必須對於區塊鏈環境定義的「鏈碼」、「分類帳」和「對等節點」有概念上的瞭解；請參閱 [Hyperledger Fabric  Glossary](https://github.com/hyperledger/fabric/blob/master/docs/glossary.md)。  

<br>
## 使用大理石展示
{: #marbles}

「大理石」應用程式示範兩方之間簡單的資產轉移。應用程式的設計是要測試 JavaScript SDK、指引其開發，以及協助開發人員熟悉 SDK 和鏈碼。

探索 [Marbles Tutorials](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md) 以瞭解 Web 應用程式、SDK 及鏈碼如何一起運作。如果您已經熟悉鏈碼和 IBM Blockchain，可以將展示[手動部署](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md#)至 Bluemix，或按一下「部署至 Bluemix」按鈕以使用 Web 應用程式：
  
[![部署至 Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  

<br>
## 使用商業票據展示
{: #commercialpaper}

「商業票據」應用程式示範如何使用 IBM Blockchain 實作商業票據交易網路。「商業票據」展示會探索具有許可權的區塊鏈網路，在這個網路上，參與者會被指派角色以及相對應的存取層次。請造訪 [Commercial Paper README](https://github.com/IBM-Blockchain/cp-web#readme) 以進一步瞭解這份展示的元件，或立即將它部署至 Bluemix，查看運作中的交易網路：
  
[![部署至 Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  

<br>
## 使用租車展示
{: #carlease}

「租車」應用程式示範車輛的生命週期，從製造、經過一系列擁有者，最後到車輛報廢。展示使用 Node.js 進行伺服器端程式設計，針對在 IBM Blockchain 網路上執行的鏈碼則使用 Golang。展示包含兩個鏈碼實例：一個定義車輛交易的規則，另一個則記載生命週期內的所有車輛交易。兩個鏈碼程式都使用 JSON 物件來儲存資料。請造訪 [Car Lease README](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md) 以進一步瞭解與這份展示相關聯的應用程式架構和車輛屬性，或將展示立即部署至 Bluemix：
  
[![部署至 Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  

<br>
## 非唯一性鏈碼
{: #ndcc}

IBM Blockchain 網路只支援唯一性鏈碼。在任何區塊鏈網路上都不支援使用非唯一性鏈碼，且會導致重大錯誤。

**非唯一性鏈碼** 是指跨越時間和節點，**不會**在區塊鏈分類帳上導致相同附加值的任何鏈碼。相反地，**唯一性鏈碼** 則會在區塊鏈分類帳上，跨越時間和節點，一律產生相同的附加值。

### 唯一性鏈碼範例
一律將變數值加一的 **invoke** 交易是唯一性的，因為結果在每個節點上都一律相同，不會有變化。例如，每當對固定值五執行這個交易時，附加的值在每個節點上、每次都一律是六。唯一性鏈碼的網路結果不會在區塊鏈中造成分歧；每個節點上的分類帳副本一律會指出（在同步化之後）值比前一次呼叫多一。

### 非唯一性鏈碼範例
根據當日開始 (00:00) 之後經歷的秒數來增加區塊鏈變數值的 **invoke** 交易，則是非唯一性的，因為值會隨著時間不同而在各節點之間變化。例如，每次對固定值「五」執行這個交易時，附加的值會在各節點不同（罕有例外），因為自 00:00 起經歷的秒數勢必會變化。這個非唯一性鏈碼的網路結果就是分歧的區塊鏈；所有節點無法針對「五 + 自 00:00 起經歷秒數」的值達成一致。

### 隨機性
鏈碼跨越時間和節點，對於附加的值都不能有任何隨機性。任何隨機性都會在各節點之間造成分歧的區塊鏈，然後就必須由網路來解決此現象。為了避免隨機性，您必須確保不會有任何平行鏈碼影響來自呼叫鏈碼的輸入值。例如，請勿同時執行任何 **query** 交易和 **invoke** 交易，因為平行查詢可能會在各節點之間的呼叫值產生變化。

### 使用廣域變數
使用廣域變數或實例變數來儲存從分類帳中擷取的值或在分類帳上設定值，可能會導致非唯一性。鏈碼不應該根據在重新啟動鏈碼容器時不會保留其狀態的廣域變數或實例變數。以下是使用廣域變數的範例；透過 `stub.PutState` 函數寫入分類帳的 `key` 值，是衍生自廣域變數：

```go
//declare global variable
var INVOICE_COUNTER int64

//increment the counter and save the state
		INVOICE_COUNTER =INVOICE_COUNTER+1
		key := INVOICE+strconv.FormatInt(INVOICE_COUNTER, 10)
		ccLogger.Infof("The key formed for saving the state: %s", key)
		stub.PutState(key,[]byte(invoiceID))
```

### 反覆運算對映類型
反覆運算對映類型可能導致非唯一性，因為順序在 Go 程式設計語言中不具唯一性。下列範例說明如何反覆運算名為 `columnTypes` 的對映：

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
