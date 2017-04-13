---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-31"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# HFC SDK for Node.js
{: #etn_sdk}


Hyperledger Fabric Client (HFC) SDK 可讓應用程式開發人員建置與區塊鏈網路互動的 Node.js 應用程式。運用 HFC SDK 的 Node.js 應用程式可以用來執行下列網路作業：
{:shortdesc}

* 安全地登錄及登記使用者。具有 `registrar` 權限的 Web 應用程式管理者可以動態登錄及登記已向 Web 應用程式鑑別的使用者。
* 將交易（deploy、invoke 及 query）提交至區塊鏈網路。在沒有 'auditor' 權限的情況下，所有交易都是匿名、機密且可解除鏈結的。
* 將機密私密金鑰及憑證儲存至任何位置（例如不在區塊鏈上的資料庫）。這需要實作一個簡單的金鑰值儲存庫介面。

HFC SDK 提供 API，而應用程式透過此 API 與 Hyperledger Fabric 區塊鏈網路互動。這些 API 的設計是要支援兩種可外掛元件：

1. 可外掛金鑰值儲存庫，用來擷取及儲存與成員相關聯的金鑰。`chain.setKeyValStore()` 方法會置換預設的檔案型金鑰值儲存庫實作。鏈結金鑰值儲存庫是用來將機密私密金鑰存入倉儲中，因此必須適當地保護存取權。
2. 可外掛成員服務，用來登錄及登記成員。`chain.setMemberServices()` 方法會置換 `MemberServices` 中的預設實作。成員服務會將 Hyperledger Fabric 實作為具有許可權的區塊鏈網路，以提供匿名、交易不可鏈結性及機密性。

您可以使用離線方法或 npm 方法，以在 Node.js 應用程式中包含 HFC SDK：
*  離線方法：先將檔案從 Hyperledger Fabric 來源樹狀結構 (https://github.com/hyperledger/fabric/tree/v0.6/sdk/node/lib) 複製到 Node.js 應用程式 `/lib` 目錄。然後，新增下列程式碼 Snippet，以在應用程式中包含 HFC SDK：

```js
var hfc = require("./lib/hfc");
```

* npm 方法：從指令行中，先使用下列 Snippet，從 npm 安裝 HFC SDK：

```
npm install hfc@0.6.5
```

然後，使用下列程式碼 Snippet，在應用程式中包含 HFC SDK：

```js
var hfc = require('hfc');
```  
<br>
## HFC 物件
{: #objects}

高階說明下列 HFC 物件（類別及介面），以協助引導您瞭解物件階層：

* 最上層類別是 `Chain`，即區塊鏈網路的用戶端呈現。HFC 可讓您與多個網路互動，以及視需要與多個 `Chain` 物件共用單一 `KeyValStore` 及 `MemberServices` 物件。對於每一個區塊鏈網路，您將會新增一個以上的 `Peer` 物件，這代表 HFC 所連接以提交交易的端點。
* HFC 使用 `KeyValStore` 介面來儲存及擷取所有持續性資料。此資料包括必須保持安全的私密金鑰。預設實作是位於 `FileKeyValStore` 類別中的檔案型版本。
* `MemberServices` 介面是透過 `MemberServicesImpl` 類別所實作，並提供安全及身分相關特性（例如隱私權、不可鏈結性及機密性）。此實作會發出 *eCerts*（成員登記憑證）及 *tCerts*（每一個成員的交易憑證）。
* `Member` 類別代表在網路上進行交易的一般使用者，以及其他類型的成員，例如對等節點（peer，也就是節點、node）。使用與 `MemberServices` 物件互動的 `Member` 類別，以*登錄* 及*登記* 成員和使用者。您也可以與 `Peer` 物件進行交易，以直接從 'Member' 類別部署、查詢及呼叫鏈碼；此實作只是將工作委派給暫時性的 `TransactionContext` 物件。
* `TransactionContext` 類別會實作大多數的 deploy、invoke 及 query 邏輯。每個 `TransactionContext` 實例會從 `MemberServices` 收到唯一 tCert，並且一律用它來提交交易。若要使用相同的 tCert 來發出多個交易，請直接從 Member 物件中擷取 `TransactionContext` 物件，以及發出多個 deploy、invoke 及 query 作業。不過，針對多個交易使用單一 tCert 時會鏈結交易，因此，可以將它們識別為牽涉同一個匿名使用者。若要避免交易鏈結，請在 `User` 或 `Member` 物件上呼叫 deploy、invoke 及 query。  

<br>

## 範例 Node.js 應用程式
{: #nodesample}

下列範例 Node.js 應用程式運用 HFC SDK API，以與 Bluemix 區塊鏈網路互動。此程式使用兩種區塊鏈網路方案（入門範本及 HSBN）運作，並且可以搭配任何用戶端作業系統。

目標是使用 JavaScript 應用程式 ([helloblockchain.js](https://github.com/IBM-Blockchain/SDK-Demo/blob/master/helloblockchain.js)) 將一段 chaincode ([chaincode_example02](https://github.com/IBM-Blockchain/SDK-Demo/blob/master/src/chaincode/chaincode_example02.go)) 順利部署至 Bluemix 網路，後面接著呼叫及查詢。  

1. 此程式需要 Node.js 及 npm JavaScript 套件管理程式。安裝最新版本的 [Node.js](https://nodejs.org/en/) 將自動包括 npm。  

1. 開啟終端機並建立目錄（工作區），您想要在其中放置此示範的原始碼。例如：

    ```
    mkdir -p $HOME/workspace
    ```

1. 移至新建的目錄，並複製 [SDK-Demo](https://github.com/IBM-Blockchain/SDK-Demo) 儲存庫。確定您對安裝的作業系統具有適當的 [Git](https://git-scm.com/downloads) 版本，然後再執行 `git clone` 指令：

     ```
     cd $HOME/workspace
     git clone https://github.com/IBM-Blockchain/SDK-Demo.git
     ```
 如果您的網路正在執行 Hyperledger Fabric 0.5 版，請在完成複製之後移出 0.5 版分支：

     ```
     cd $HOME/workspace/SDK-Demo
     git checkout v0.5
     ```

1. 現在您需要使用來自區塊鏈實例的「服務認證」。

1. 如果您尚未這麼做，請存取 Bluemix 中的 [Blockchain](https://console.ng.bluemix.net/catalog/services/blockchain/) 磚，以及建立該服務的實例。選取**入門範本開發人員**方案或**高安全性商業網路**方案。在策劃了網路之後，請按一下**建立**按鈕。這將開啟「服務儀表板」。按一下頁面上半部的**服務認證**標籤，為您的網路存取對等節點及使用者登記資料。**附註**：若為 HSBN 網路，可能不會自動產生「服務認證」。只需按一下**新建認證**按鈕，即會開啟新視窗。然後，按一下視窗底端的**新增**。這將移入包含「服務認證」的 JSON 有效負載。

1. 使用新認證更新您在複製 SDK-Demo 儲存庫時收到的 ServiceCredentials.json 檔案。

1. 程式執行時，HFC SDK 會在 $HOME/workspace/SDK-Demo 內建立 `keyValStore-<network-id>` 目錄。此 `keyValStore-<network-id>` 目錄包含每一個已登記使用者的加密金鑰。連接至新 Bluemix 網路時，您不需要刪除 `keyValStore` 目錄，而是會針對每個 Bluemix 實例建立唯一的 `keyValStore-<network-id>` 目錄。**請勿**刪除此加密資料，直到網路遭到刪除或重設為止。若沒有此資料，您的用戶端無法與 Bluemix CA 伺服器通訊，而且登記將會失敗。

1. 從 SDK-Demo 資料夾中，執行 node 程式：

	```
	node helloblockchain.js
	```
	啟用除錯日誌：
	```
	DEBUG=hfc node helloblockchain.js
	```

	啟用 gRPC 追蹤：
	```
	GRPC_TRACE=all DEBUG=hfc node helloblockchain.js
	```

如果 `deploy`、`invoke` 及 `query` 交易成功，您將會在終端機中看到下列訊息：

```
Successfully deployed chaincode: request={"fcn":"init","args":["a","100","b","200"],"certificatePath":"/certs/blockchain-cert.pem","chaincodePath":"github.com/chaincode_example02/"}, response={"uuid":"2d6ad8d6-1390-4c60-a01b-f4c301175eb7","chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","result":"TODO: get actual results; waited 120 seconds and assumed deploy was successful"}

Successfully submitted chaincode invoke transaction: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"invoke","args":["a","b","1"]}, response={"uuid":"f9a902d2-44d8-4b68-b43d-419470ba73ae"}

Successfully completed chaincode invoke transaction: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"invoke","args":["a","b","1"]}, response={"result":"waited 20 seconds and assumed invoke was successful"}

Successfully queried  chaincode function: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"query","args":["a"]}, value=99
```

**附註**：chaincode 原始碼保存在 SDK-Demo 儲存庫的 **src/chaincode** 資料夾下。此資料夾 **ALSO** 包含 **/vendor** 資料夾，其中包含來自 Hyperledger Fabric 程式碼庫的程式庫及相依關係。如果您將現行 chaincode 檔案 (chaincode_example02.go) 取代為您自己的 chaincode，請確保您保留了 **/vendor** 資料夾。對等節點需要這些相依關係，才能順利編譯您的 chaincode 並建立容器。此外，如果您有任何相依程式庫，請確定在 **/vendor** 資料夾下新增它們。

請注意，在「入門範本開發人員」網路上執行時，有時可能需要延長時間，部署才能成功且 chaincode 容器才能啟動。不過，啟動之後，後續部署及呼叫將立即執行，因為必要檔案已經儲存在區塊鏈實例的主機上。  

從**網路主控台**中，導覽至 **Blockchain** 標籤。此視圖會顯示正在將區塊附加至區塊鏈分類帳，因為 helloblockchain.js 程式發出 deploy 及 invoke 交易。下列擷取畫面顯示 helloblockchain.js 使用預設引數 "a" 及 "b" 執行兩次的結果：

   ![Node 工作區 3](images/nodeworkspace3.PNG "Node 工作區 3")  

<br>

## 疑難排解
從 **/workspace** 目錄發出下列一個指令，確保您是執行 **hfc@0.5.4** 或 **hfc@0.6.5**：
  * npm list | grep hfc
  * npm list -g | grep hfc（如果已使用廣域 `-g` 旗標安裝的話）

使用 0.5 版分支的網路將需要更早的 hfc 版本 - 0.5.4

如果您收到查詢訊息，請使用下列程序：

  ```
Failed to query chaincode, function: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"query","args":["a"]}, error={"error":{"status":"FAILURE","msg":{"type":"Buffer","data":[69,114,114,111,114,58,70,97,105,108,101,100,32,116,111,32,108,97,117,110,99,104,32,99,104,97,105,110,99,111,100,101,32,115,112,101,99,40,112,114,101,109,97,116,117,114,101,32,101,120,101,99,117,116,105,111,110,32,45,32,99,104,97,105,110,99,111,100,101,32,40,57,98,101,48,97,48,101,100,51,102,49,55,56,56,101,56,55,50,56,99,56,57,49,49,99,55,52,55,100,50,102,54,100,48,101,50,48,53,102,97,54,51,52,50,50,100,99,53,57,56,100,52,57,56,102,101,55,48,57,98,57,98,56,100,41,32,105,115,32,98,101,105,110,103,32,108,97,117,110,99,104,101,100,41]}},"msg":"Error:Failed to launch chaincode spec(premature execution - chaincode (9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d) is being launched)"}
  ```

在 Node.js 應用程式中，增加部署等待時間。預設值設為 60 秒，但可能需要較長的時間，才能適當地部署程式碼、編譯程式碼，以及開始在 Docker 容器中執行。請嘗試將部署等待時間增加為 120 秒。因為在管理區塊鏈實例的機器上共用運算資源，所以這項特性只會在「入門範本開發人員」方案上觀察到：

  ```js
chain.setDeployWaitTime(120);
  ```

在網路上順利部署鏈碼之後，即可將部署等待時間減少為額定量（例如幾秒鐘）。

如果您收到信號交換錯誤，請嘗試不同的 `grpc` 版本。您可以使用下列任一指令來存取 grpc 版本：
    - `npm list | grep grpc`
    - `npm list -g | grep grpc`  



<br>
## 公開和私密金鑰
{: #keys}

Hyperledger Fabric 使用憑證管理中心及其基礎公開和私密金鑰，以符合透過共用區塊鏈營運之企業的安全需求。成員身分管理、角色管理及交易隱私全都可以透過 HFC SDK 控制。

共用區塊鏈上的使用者及交易隱私是透過實作 PKI（公開金鑰基礎架構）架構來進行管理。PKI 透過憑證管理中心管理金鑰及數位憑證的產生、配送及撤銷。Hyperledger Fabric 0.6 版 [通訊協定規格](http://hyperledger-fabric.readthedocs.io/en/v0.6/protocol-spec/)的安全小節中說明 PKI 及「成員資格服務」的完整技術規格。Hyperledger Fabric PKI 的基本宗旨說明如下：

1. 「登錄管理中心 (RA)」會驗證要求存取區塊鏈網路的使用者的身分。這可以透過具有 `registrar` 權限的使用者動態完成，或透過編輯 membersrvc.yaml 檔案手動完成。登錄程序是在頻外發生，並透過 `RegisterUser` 函數執行。RA 會將登記認證（`<enrollID>` 及 `<enrollPWD>`）指派給使用者。

2. 使用者接著會使用 `CreateCertificatePair` 函數，將登記要求傳送給「登記憑證管理中心 (ECA)」。此有效負載包含使用者的一次性 `<enrollPWD>`、「公開簽章驗證金鑰」及「公開加密金鑰」，並且透過使用者的「私密簽章驗證金鑰」進行簽署。<br><br>收到登記要求時，ECA 會發出已加密的盤查給使用者，這項盤查只能利用使用者的「私密加密金鑰」進行解密。解密盤查之後，使用者就可以重新傳送憑證要求。ECA（視正確解密的回應而定）會傳回使用其數位簽章簽署的已鑑別憑證配對。<br><br>數位簽章的產生方式是使用 SHA-2 演算法加密雜湊憑證要求（訊息）來產生「摘要」。此「訊息摘要」接著會使用 ECA 的私密簽章金鑰進行加密。網路成員接著可以使用 ECA 的公開簽章金鑰將數位簽章解密，以進行鑑別。傳回的登記憑證 (eCert) 配對包含一個憑證進行資料簽署（私密）以及一個憑證進行資料加密（公開）。此 eCert 配對是靜態且長期的，而且可讓交易看到或看不到。

3. 若要在任何區塊鏈網路上進行交易，每一位使用者也必須具有交易憑證 (tCert)。成功登記時，使用者會提交要求給「交易憑證管理中心 (TCA)」以取得一批 tCert。tCert 是短期且某個交易特有的，用戶端可以使用 API 進行修改。驗證使用者的 eCert 之後，TCA 會指派一批 tCert 以及一個 KeyDF_Key（金鑰衍生功能金鑰），以容許使用者將其私密金鑰解密。雖然單一 KeyDF_Key 用於批次中的每個 tCert，但後續產生的私密金鑰則是每個 tCert 所獨有。若要進行交易，用戶端必須可以使用已解密的私密金鑰來簽署交易有效負載。如此才會將交易轉遞給網路驗證對等節點以取得共識。
