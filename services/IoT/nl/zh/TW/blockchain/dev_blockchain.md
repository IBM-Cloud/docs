---

copyright:
  years: 2016, 2017
lastupdated: "2017-2-6"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 開發 {{site.data.keyword.iot_short_notm}} 區塊鏈整合的智慧型合約
{: #iotblockchain_link}

使用 {{site.data.keyword.blockchainfull}} 及 Hyperledger 開發環境，以建立及測試您衍生自 IBM 所提供範例合約的專屬智慧型合約。
{:shortdesc}

開發及部署 Golang 鏈碼執行檔形式的智慧型合約。使用 {{site.data.keyword.iot_short_notm}} 區塊鏈整合，針對每個交易利用裝置事件資料來觸發合約更新及商業邏輯執行，並且將新的分類帳狀態寫入區塊鏈。

{{site.data.keyword.iot_short_notm}} 區塊鏈整合開發環境包含下列元件：

- {{site.data.keyword.Bluemix_notm}} 組織：
  - 已啟用 IoT 區塊鏈整合的 {{site.data.keyword.iot_short_notm}} 服務。
  - {{site.data.keyword.blockchainfull_notm}} 網狀架構
  - 執行 IoT 裝置模擬器的 Node-RED 應用程式。
   

**附註：**您也可以使用本端部署的 Node-RED 環境來執行模擬器。

- 本端環境：
  - 開發及測試智慧型合約鏈碼的 Hyperledger 開發環境。環境包含 GoLang。
  - 區塊鏈監視使用者介面
- GitHub 環境：
  - IBM 所提供之範例智慧型合約的 GitHub 儲存庫
  - 將智慧型合約部署至 {{site.data.keyword.blockchainfull_notm}} 網狀架構的 GitHub 儲存庫

下圖說明 {{site.data.keyword.iot_short_notm}} 區塊鏈整合開發環境：
![IoT 區塊鏈 {{site.data.keyword.iot_short_notm}} 整合架構。](images/architecture_contracts.svg "IoT 區塊鏈 {{site.data.keyword.iot_short_notm}} 整合架構")

## 開始之前

{: #byb}

取得 {{site.data.keyword.blockchainfull_notm}} 的概觀、其與一般區塊鏈概念的關聯，以及它的作用：
- IBM.com 上的 [{{site.data.keyword.blockchainfull_notm}}](http://www.ibm.com/blockchain/)。
- [{{site.data.keyword.blockchainfull_notm}} DOCS](https://console.ng.bluemix.net/docs/services/blockchain/index.html) - 開始使用 {{site.data.keyword.blockchainfull_notm}} 服務
- [{{site.data.keyword.blockchainfull_notm}} API](https://ibmblockchainapi.mybluemix.net/swagger/ui.html?scheme=http&host=127.0.0.1:3000&basepath=/) - {{site.data.keyword.blockchainfull_notm}} API 的概觀。
- [{{site.data.keyword.blockchainfull_notm}} for Developers](http://www.ibm.com/blockchain/for_developers.html) - 區塊鏈如何融入您開發環境的概觀，包括即時展示以及可部署以在 {{site.data.keyword.Bluemix_notm}} 上執行之程式碼的逐步演練。

## 範例智慧型合約

{: #samples}

您可以從 [https://github.com/ibm-watson-iot/blockchain-samples](https://github.com/ibm-watson-iot/blockchain-samples) 下載許多範例合約。您可以使用範例合約作為基礎，以將您自己的使用案例開發為可部署的鏈碼：

|範例合約 |說明 |
|:---|:---|
|[基本：簡單合約](https://github.com/ibm-watson-iot/blockchain-samples/tree/master/contracts/basic/simple_contract) | 簡化版的進階合約可讓您在區塊鏈上追蹤及儲存裝置資產資料
|[進階：IoT 一般範例合約](https://github.com/ibm-watson-iot/blockchain-samples/tree/master/contracts/advanced/iot_sample_contract) | 具有許多特性及**貿易航線**特色的資料模型和行為的進階範例合約|


## 配置 {{site.data.keyword.blockchainfull_notm}} 環境

{: #configure_environment}
您必須先設定自己的區塊鏈環境，才能開始部署及測試智慧型合約。

**附註：**{{site.data.keyword.iot_short_notm}} 區塊鏈整合支援連接至 {{site.data.keyword.blockchainfull_notm}} 網狀架構及 Hyperledger 網狀架構。下列範例係根據 {{site.data.keyword.blockchainfull_notm}} 的使用情形。

1. 建立及配置 {{site.data.keyword.blockchainfull_notm}} 網狀架構。
{{site.data.keyword.iot_short_notm}} 區塊鏈整合需要 {{site.data.keyword.blockchainfull_notm}} 網狀架構來管理區塊鏈分類帳、智慧型合約及一般區塊鏈基礎架構。{{site.data.keyword.Bluemix_notm}} 區塊鏈整合使用 {{site.data.keyword.blockchainfull_notm}} 來管理鏈結。如果您可以存取現有 {{site.data.keyword.blockchainfull_notm}} 環境，即可使用它。否則，您必須從 {{site.data.keyword.Bluemix_notm}} [型錄](https://console.ng.bluemix.net/catalog/services/blockchain/)中建立 {{site.data.keyword.blockchainfull_notm}} 實例。

  1. 從 {{site.data.keyword.Bluemix_notm}} 帳戶儀表板中，按一下**使用服務或 API**。
  2. 找到服務型錄的「應用程式服務」區段，然後選取 **Blockchain**。  
   **提示：**按一下[這裡](https://console.ng.bluemix.net/catalog/services/blockchain/)，直接移至 {{site.data.keyword.blockchainfull_notm}} 服務頁面。
  3. 在 {{site.data.keyword.blockchainfull_notm}} 服務頁面上，驗證「新增服務」選項：  
    - 空間 - 如果您不只有預設 `dev` 空間，請驗證您是在預期空間中部署服務。
    - 應用程式 - 維持不連結。
    - 服務名稱 - 選擇性地將服務名稱變更為容易記住的名稱。此名稱會顯示在 {{site.data.keyword.Bluemix_notm}} 儀表板的 {{site.data.keyword.blockchainfull_notm}} 磚中。
    - 選取的方案 - 選取免費方案。免費方案提供兩個驗證對等節點及一個憑證管理中心。
  4. 按一下**建立**，以將 {{site.data.keyword.blockchainfull_notm}} 部署至 {{site.data.keyword.Bluemix_notm}}。  
區塊鏈一開始會部署兩個對等節點。您可以視需要新增其他節點。

4. 將 {{site.data.keyword.iot_short_notm}} 鏈結至 {{site.data.keyword.blockchainfull_notm}} 服務  
    若要從 {{site.data.keyword.iot_short_notm}} 寫入至區塊鏈，您必須先鏈結服務。
     1. 在 {{site.data.keyword.Bluemix_notm}} 中，移至「儀表板」
     2. 選取已在其中部署 {{site.data.keyword.blockchainfull_notm}} 的空間。
     3. 按一下**服務**下的 **Blockchain** 鏈結。
     4. 按一下**服務認證**標籤。
     5. 選取一組服務認證，或按一下**新建認證**，以建立一組新的服務認證，並指定其敘述性名稱（例如 "IoT-Platform-integration"）。
     6. 在 JSON 格式化服務認證中，記下下列參數：  
      - 對等節點資訊：`api_host` 及 `api_port_tls`
      - 類型 1（用戶端）資訊的使用者：`username` 及 `secret`  

      服務認證範例：
     ```json
     {
      "peers": [
      {
       "discovery_host": "fa68cbcbfcec4726932e53e2fa4f3afc-vp0.us.blockchain.ibm.com",
        "discovery_port": 30003,
        "api_host": "fa68cbcbfcec4726932e53e2fa4f3afc-vp0.us.blockchain.ibm.com",
        "api_port_tls": 5003,
        "api_port": 5003,
        "event_host": "fa68cbcbfcec4726932e53e2fa4f3afc-vp0.us.blockchain.ibm.com",
        "event_port": 31003,
        "type": "peer",
        "network_id": "fa68cbcbfcec4726932e53e2fa4f3afc",
        "container_id": "e33f08f85988bf57ccfcf34ccdb80d72489e5bfb46786b570e1a74a6679f804e",
        "id": "fa68cbcbfcec4726932e53e2fa4f3afc-vp0",
        "api_url": "http://fa68cbcbfcec4726932e53e2fa4f3afc-vp0.us.blockchain.ibm.com:5003"
    },
       ...
      ],
      "users": [
      {
       "enrollId": "user_type1_0",
        "enrollSecret": "63c58806d6",
        "affiliation": "group1",
        "username": "user_type1_0",
        "secret": "63c58806d6"
      },
       ...
       ]
      }
     }
     ```  
     **重要事項：**您選取的使用者先前不得已向所選取對等節點之外的對等節點進行登錄。
     7. 按一下**回到儀表板**，以回到 {{site.data.keyword.Bluemix_notm}} 儀表板。
     8. 選取已在其中部署 {{site.data.keyword.iot_short_notm}} 的空間。
     9. 按一下**服務**下的 **{{site.data.keyword.iot_short_notm}}** 鏈結。
     10. 按一下**啟動**，以開啟 {{site.data.keyword.iot_short_notm}} 儀表板。
     11. 從 {{site.data.keyword.iot_short_notm}} 儀表板中，選取功能表資訊看板中的**延伸規格**。
     12. 在**延伸規格**頁面的 Blockchain 磚中，按一下**設定**，或者，如果您已鏈結網狀架構，請按一下 ![齒輪圖示](../images/gear.png "配置")。
     13. 在「配置區塊鏈」區段中，按一下**新增網狀架構**，然後輸入網狀架構資訊。
    **附註：**必須啟用區塊鏈整合，才會新增網狀架構。如需相關資訊，請參閱「外部服務整合」主題中的 [Blockchain](../reference/extensions/index.html#blockchain)。
    1. 在**網狀架構**標籤中，輸入名稱以識別 {{site.data.keyword.iot_short_notm}} 中的網狀架構，然後按**下一步**。   
    2. 在**對等節點**標籤中，輸入對等節點資訊：  
   <table>
   <thead>
   <tr>
   <th>參數</th>
   <th>值</th>
   </tr>
   </thead>
   <tbody>
   <tr>
   <td>名稱</td>
   <td>輸入名稱以識別 {{site.data.keyword.iot_short_notm}} 中的對等節點。</td>
   </tr>
   <tr>
   <td>主機</td>
   <td>「驗證對等節點 1」伺服器的 `api_host` 位址</td>
   </tr>
   <tr>
   <td>埠</td>
   <td>`api_port_tls` 號碼</td>
   </tr>
   <tr>
   <td>使用者 ID</td>
   <td>用來向區塊鏈登錄智慧型合約之使用者的 `username` 字串。稍後配置「簡式使用者介面」時，也可以使用此使用者 ID。</td>
   </tr>
   <tr>
   <td>秘密金鑰</td>
   <td>使用者的 `secret` 字串</td>
   </tr>
   <tr>
   <td>使用 TLS</td>
   <td>開啟或關閉</br>使用「傳輸層安全 (TLS)」來加密 {{site.data.keyword.iot_short_notm}} 與網狀架構中合約之間的通訊。連接至 {{site.data.keyword.blockchainfull_notm}} 網狀架構時，必須啟用 TLS。</td>
   </tr></tbody>
   </table>  
    3. 按一下**完成**。
     3. 在「配置區塊鏈」區段中，按一下**完成**，以儲存網狀架構資訊。    

網狀架構表格中即會移入新的網狀架構連線。  

## 建立、測試及部署智慧型合約
{: #test_contracts}

您現在可以在 GoLang 中建立自己的智慧型合約、在沙盤推演環境中進行測試，然後在自己的 {{site.data.keyword.blockchainfull_notm}} 網狀架構上進行部署與測試。

1. 建立 GitHub 專案，以儲存智慧型合約鏈碼。
  
您要部署的智慧型合約必須在公用 GitHub 儲存庫中。如需相關資訊，請參閱 https://github.com/
2.  設定本端 Hyperledger 開發及測試環境。
  
若要先開發及測試您自己的鏈碼，再將它部署至 {{site.data.keyword.blockchainfull_notm}}，您必須設定本端開發環境。此環境包含 GoLang，以用來撰寫合約的鏈碼。
 1. 設定開發環境。
   
開發環境包含在 GoLang 中使用鏈碼建置來開發智慧型合約所需的工具。如需相關資訊，請參閱 Hyperledger 文件中的 [Setting up the development environment](https://github.com/hyperledger/fabric/blob/master/docs/dev-setup/devenv.md)。
 2. 安裝鏈碼除錯環境。
    
除錯環境提供智慧型合約在部署至 {{site.data.keyword.blockchainfull_notm}} 之前進行測試及除錯所需的工具。如需相關資訊，請參閱 Hyperledger 文件中的 [Writing, Building, and Running Chaincode in a Development Environment](https://github.com/hyperledger/fabric/blob/master/docs/Setup/Chaincode-setup.md)。
 3. 設定進行開發的網路。
    
進行開發的網路提供更嚴格的正式作業類似環境，用來進行智慧型合約的最終測試。使用此環境來進行已測試及已除錯合約的最終測試，再將它們部署至 {{site.data.keyword.blockchainfull_notm}}。如需相關資訊，請參閱 Hyperledger 文件中的 [Setting Up a Network](https://github.com/hyperledger/fabric/blob/master/docs/Setup/Network-setup.md)。

3. 選用項目：下載 IBM 所提供的範例智慧型合約。  
IBM 提供許多智慧型合約，您可以下載且直接依現狀使用，或進行修改以符合您的組織目標。  
若要下載範例合約，請執行下列動作：
 1. 移至 Blockchain Samples GitHub 儲存庫，網址為：https://github.com/ibm-watson-iot/blockchain-samples/  
 basic_contract_hyperledger 及 trade_lane_contract_hyperledger 資料夾分別包含基本及貿易航線合約。
 3. 在終端機中使用 `git clone`，以複製 https://github.com/ibm-watson-iot/blockchain-samples 專案。  
   
 **提示：**您也可以按一下專案頁面中的**下載 ZIP**，來下載專案的壓縮檔。

6. 建立及測試智慧型合約。   
您可以使用 {{site.data.keyword.iot_short_notm}} 區塊鏈整合，將鏈碼執行檔形式的智慧型合約上傳至 {{site.data.keyword.blockchainfull_notm}}，以在寫入至區塊鏈的裝置資料上執行商業邏輯。智慧型合約鏈碼是使用 GoLang 開發的。  
範例合約著重在將感興趣事件的 IoT 裝置資料寫入區塊鏈以便與協力廠商共用，或建立防竄改日誌項目。
2. 建立合約執行檔。  
合約程式碼必須先轉換為執行檔，才能將它部署在區塊鏈上。  
    
  **附註：**已產生並且可以依現狀部署範例合約 (sample_contract_hyperledger)。  
請完成下列步驟：
   1. 開啟指令行，然後導覽至合約資料夾。
   2. 執行 `go generate` 指令。  
此指令會執行任何存在於程式碼中的 'go generate' 指令。go generate 是容許預先建置產生程式碼的 go 程式工具。在 IBM 提供的範例合約中，使用 go generate 來建立概述合約綱目的 schemas.go 檔案以及 sample.go 合約檔案。  
     
   **重要事項：**schemas.go 檔案是 {{site.data.keyword.iot_short_notm}} 區塊鏈整合的重要元件。此檔案可讓平台確認合約符合整合規格，並且可讓對映程式看到裝置事件可對映到的合約 API。
   2. 執行 `go build` 指令。  
此指令會建立與資料夾同名的執行檔。此檔案是將部署在區塊鏈上的合約執行檔。

6. 在 Hyperledger 沙盤推演中，測試智慧型合約。  
在您將已完成的智慧型合約部署至 {{site.data.keyword.blockchainfull_notm}} 之前，可以在安裝為開發環境一部分的 Hyperledger 沙盤推演中，進行鏈碼的測試和除錯。  

6. 將智慧型合約鏈碼部署至 {{site.data.keyword.blockchainfull_notm}}。  
在您於本端測試及驗證合約之後，可以將它部署至 {{site.data.keyword.blockchainfull_notm}} 網狀架構來進行測試。
  1. 將合約上傳至公用 GitHub 儲存庫。  
  例如，將 sample.go 檔案上傳至：  
  `http://github.com/{my organization}/{my project}/`
  2. 向您先前連接的對等節點登錄合約。  
使用 REST 用戶端（例如 CURL 或 Postman），以提交登錄呼叫。如需登錄呼叫的相關資訊，請參閱 [POST 登記員 API 文件](https://ibmblockchainapi.mybluemix.net/swagger/ui.html?scheme=http&host=127.0.0.1:3000&basepath=/#!/Registrar/registerUser)。登錄時，請使用下列資訊：
  <ul>
  <li>URL：`http://api_host:api_port_tls/registrar`
  <li>類型：POST
  <li>標頭：`Content type: application/json`
  <li>有效負載：  
  ```json
   {  
        "enrollId": "{username}",      
        "enrollSecret": "{secret}"    
   }
   ```

  </ul>
  3. 將合約部署至對等節點。  
如需部署呼叫的相關資訊，請參閱 [POST 開發/部署 API 文件](https://ibmblockchainapi.mybluemix.net/swagger/ui.html?scheme=http&host=127.0.0.1:3000&basepath=/#!/Devops/chaincodeDeploy)。  
部署時，請使用下列資訊：  
  <ul>
  <li>URL：`http://api_host:api_port_tls/chaincode`
  <li>類型：POST
  <li>標頭：`Accept: application/json`
  <li>標頭：`Content type: application/json`
  <li>有效負載：  
  ```
  {
    "jsonrpc": "2.0",
    "method": "deploy",
    "params": {
        "type": 1,
        "chaincodeID":{
              "path": "http://github.com/{my organization}/{my project}/sample.go"
        },
        "ctorMsg": {
            "function":"init",
            "args":["{\"version\":\"1.0\",\"nickname\":\"sample_contract\"}"]
        },
        "secureContext": "username"
    },
    "id":1234
}
  ```  
  </ul>  
  您的合約已部署至網狀架構。  
  **重要事項：**請記下傳回的合約 ID，其形式為 128 個字元的英數字串。您需要合約 ID，才能將裝置對映至合約。  

10. 將裝置資料對映至新的智慧型合約。  
若要開始將裝置資料寫入至新的區塊鏈智慧型合約，您必須先將裝置資料對映至合約。  
   1. 在 {{site.data.keyword.Bluemix_notm}} 中，移至「儀表板」
   2. 選取已在其中部署 {{site.data.keyword.iot_short_notm}} 的空間。
   3. 按一下 **{{site.data.keyword.iot_short_notm}}** 服務。
   4. 按一下**啟動**，以開啟 {{site.data.keyword.iot_short_notm}} 儀表板。
   5. 按一下功能表資訊看板中的![區塊鏈](images/platform_blockchain.png "區塊鏈")，以選取**區塊鏈**。
   6. 按一下**對映裝置資料**。
   7. 選取您要在區塊鏈中儲存其裝置資料的裝置類型，以及您要儲存之事件的事件名稱。按**下一步**。
   8. 選取先前所建立網狀架構的網狀架構名稱。按**下一步**。
   9. 輸入下列資訊，然後按**下一步**：
     - 合約 ID - 貼入在部署合約時所儲存的 128 個字元的合約 ID。
     - 合約名稱 - 輸入名稱以識別 {{site.data.keyword.iot_short_notm}} 中的合約。
     
     **提示：**若要尋找裝置的事件類型，請移至**裝置**頁面，然後按一下裝置名稱以開啟裝置詳細資料頁面。向下捲動至**感應器資訊**區段，以查看裝置的可用事件及資料點清單。

   11. 將可用的裝置內容對映至合約參數。  
      
   **重要事項：**請驗證每一個所對映資料點的資料類型，都對應到其所對映合約參數需要的資料類型。  
例如，合約內容（例如 string 類型的「資產 ID」）必須對映至 string 類型的內容。合約參數需求定義於合約 go-code 的 `type` 定義中。  
例如，基本 IBM 所提供的合約具有下列合約參數需求：
      
    <ul>
    <li>  資產 ID - string
    <li>  位置 - Geolocation  
    <ul>
    <li> 緯度 - float64
    <li>  經度 - float64
    </ul>
    <li>  溫度 - float64  
    <li>  載波 - string   
    </ul>  
    如需如何將裝置資料對映至合約的相關資訊，請參閱 GitHub 之 IoT Blockchain Samples Wiki 中的 [Data mapping example](https://github.com/ibm-watson-iot/blockchain-samples/wiki/Data-mapping-example)。
   12. 在摘要頁面中，驗證資訊正確無誤。
   13. 區塊鏈頁面中會顯示裝置資料與合約的對映。

7. 在 {{site.data.keyword.blockchainfull_notm}} 中測試智慧型合約。  
若要測試智慧型合約，請執行完整測試，方法是在 {{site.data.keyword.iot_short_notm}} 中建立裝置、將裝置連接至 {{site.data.keyword.iot_short_notm}}、將 IoT 區塊鏈配置成連接至區塊鏈網狀架構，以及將 {{site.data.keyword.iot_short_notm}} 配置成在區塊鏈中對映及儲存裝置訊息。您可以使用 {{site.data.keyword.blockchainfull_notm}} 主控台來檢視區塊鏈，以查看分類帳中的裝置資料。如果您的合約支援 readAsset() 函數，則可以使用監視使用者介面來檢視區塊鏈，以及查看區塊鏈中持續儲存的自有情境中的裝置資料。

5. 將「監視使用者介面」配置成連接至 {{site.data.keyword.blockchainfull_notm}}。  
 **提示：**如果您尚未在本端環境中安裝「監視使用者介面」，則可以立即安裝。請遵循[區塊鏈監視使用者介面](https://github.com/ibm-watson-iot/blockchain-samples/tree/master/applications/monitoring_ui) GitHub 目錄內可用「監視使用者介面」ReadMe 文件中的指示。  
按一下**配置**按鈕，以存取配置設定。   
使用下列資訊來連接至合約：
<table>
<thead>
<tr>
<th>參數</th>
<th>值</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr>
<td>API 主機及埠</td>
<td>`http://peer_URL:port`</td>
<td>前面附加 `https://` 的 {{site.data.keyword.blockchainfull_notm}} REST API 的主機及埠。使用 `api_host` 位址及 `api_port_tls` 號碼。</td>
</tr>
<tr>
<td>鏈碼 ID</td>
<td>登錄合約時所傳回的合約 ID。</td>
<td>合約 ID 是對應至「合約 ID」項目的 128 個字元的英數字串。  
**重要事項：**當您剪下並貼上合約 ID 時，請確定 ID 中不包含任何空格。如果未正確地輸入 ID，則會顯示區塊鏈分類帳項目，但資產搜尋功能不會運作。
</td>
</tr>
<tr>
<td>安全環境定義</td>
<td>您的網狀架構使用者</td>
<td>需要有此參數，才能連接至 {{site.data.keyword.Bluemix_notm}} 上的 {{site.data.keyword.blockchainfull_notm}} 實例。使用 `secureContext` 項目。  
**重要事項：**secureContext 應該是用來配置網狀架構的 `username`。
</td>
</tr>
<tr>
<td>要顯示的區塊數目</td>
<td>正整數。預設值：10</td>
<td>要顯示的區塊鏈區塊數目。
</td>
</tr>
</tbody>
</table>

3. 在「監視使用者介面」中，驗證設定如預期運作。  
使用「監視使用者介面」元件，以與區塊鏈合約互動：  
 - 鏈碼作業  
 驗證合約特有鏈碼作業可以如預期執行。例如，針對「基本合約」，驗證執行 `createAsset` 函數會將資產新增至區塊鏈。
 - 回應有效負載  
 驗證當您從「鏈碼作業」標籤提交 REST 要求時，對等節點要求回應會如預期顯示。
 - 區塊鏈  
驗證當您從鏈結的裝置中注入資料時，或當您使用「鏈碼作業」元件時，會將區塊新增至鏈結。    

## 後續步驟
{: #next_steps}

您現在已部署及瀏覽範例 IBM 所提供的智慧型合約。不過，設計良好的智慧型合約鏈碼開啟了許多可能性，而基本及貿易航線合約只提供其中有限的範例。現在已經可以實驗商業情境，並將其對應至 {{site.data.keyword.blockchainfull_notm}} 中的鏈碼合約。然後，您可以搭配使用 {{site.data.keyword.iot_short_notm}} 與 IoT 區塊鏈整合，以將裝置資料寫入區塊鏈分類帳，並且執行儲存為智慧型合約的商業邏輯，來回應資料。     


盡情使用區塊鏈吧！
