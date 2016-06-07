---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 情境：端對端開發
{: #ee}

*前次更新：2016 年 4 月 18 日*

您可以使用 {{site.data.keyword.Bluemix}} 使用者介面、平台及工具選擇來建置、執行及部署應用程式。請遵循這份端對端開發情境以便開始使用。
{:shortdesc}

## 註冊
{: #ee_start}

開始之前，您必須先從 [https://console.ng.bluemix.net/](https://console.ng.bluemix.net/) 註冊 IBM ID。然後就可以登入 {{site.data.keyword.Bluemix_notm}}，並開始免費試用 30 天。{{site.data.keyword.Bluemix_notm}} 提供 2 GB 執行時期記憶體和 10 個服務實例的額度供您免費試用。

## 使用 {{site.data.keyword.Bluemix_notm}} 使用者介面建立 Web 應用程式
{: #ee_appui}

註冊之後，您會使用 {{site.data.keyword.Bluemix_notm}} 使用者介面開始建置第一個應用程式。

在 {{site.data.keyword.Bluemix_notm}} 中，應用程式與組織及空間相關聯。組織是由多個合作人員所擁有及使用。一開始，您會得到預設組織，它是以您的使用者名稱來命名，且您是唯一的合作人員。您也會在這個組織內得到一個空間。該空間是用來執行您應用程式的環境；例如，您可以有 dev 空間作為開發環境、test 空間作為測試環境，以及 production 空間作為正式作業環境。此外，每一個環境都屬於一個地區。使用 {{site.data.keyword.Bluemix_notm}}，您可以將應用程式部署至特定的地理區域，以獲得較低的網路延遲、資料隱私及更好的可用性。如需詳細資料，請參閱「地區」。

針對此情境，您想要使用 Node.js 開發 Web 應用程式。假設您位在美國，而您大部分的應用程式使用者也在美國。您決定在接近使用者族群的地方建置及執行應用程式，以便得到較低網路延遲的好處。登入 {{site.data.keyword.Bluemix_notm}} 之後，請按一下您位於右上方的帳戶名稱，然後選取**美國南部**地區。然後，您可以採取下列步驟來建立應用程式：

  1. 按一下加號按鈕。
  2. 選取**計算**>**CF 應用程式**>**SDK for Node.js**。
  3. 為您的應用程式鍵入唯一名稱（例如，TestNode），然後按一下**建立**。應用程式名稱在整個 {{site.data.keyword.Bluemix_notm}} 環境中必須是唯一的。
  
現在您會看到**開始撰寫程式碼**指示。您可以遵循指示來下載 TestNode 的入門範本程式碼，然後加以修改及部署。

依預設，應用程式會被指派 1 個實例及 512 MB 記憶體配額。您可以增加記憶體，或新增更多實例以取得應用程式的高可用性，例如 3 個實例且每個實例有 1 GB 記憶體。按一下**檢視應用程式概觀**可指定您的應用程式實例及記憶體配額。例如，針對實例鍵入 3，針對記憶體配額鍵入 1 GB，然後按一下**儲存**。您也可以查看檔案、日誌及環境變數來進行問題的疑難排解。

## 使用 {{site.data.keyword.Bluemix_notm}} 使用者介面連結服務
{: #ee_bindui}

建立應用程式之後，您想要使用應用程式連接至資料庫。如此，您可以使用資料庫查詢語言來儲存及觀察應用程式資料。在此情境中，您決定使用 {{site.data.keyword.Bluemix_notm}} 所提供的 {{site.data.keyword.cloudant}} 服務。

若要在應用程式內使用服務，您需要採取下列步驟，建立服務實例並將應用程式連結至服務實例：
  1. 在應用程式「概觀」頁面上，按一下**新增服務或 API**。
  2. 在 {{site.data.keyword.Bluemix_notm}}「型錄」中，選取 {{site.data.keyword.cloudant}} 服務。
  3. 鍵入服務實例的唯一名稱，或使用 {{site.data.keyword.Bluemix_notm}} 產生的預設名稱，然後按一下**建立**。
  4. 即會顯示「重新編譯打包應用程式」視窗。按一下**重新編譯打包**，以重新編譯打包您的應用程式。
  
現在您的應用程式已連結至 {{site.data.keyword.cloudant}} 服務。您可以在 VCAP_SERVICES 環境變數中，找到應用程式與服務實例通訊所需的全部資料。例如，因為 {{site.data.keyword.Bluemix_notm}} 在相同虛擬機器上管理數個應用程式，因此應用程式不能使用相同的 HTTP 埠號來接收送入的要求。為了避免衝突，會針對每個應用程式提供一個唯一的埠號。此埠號可在 VCAP_APP_PORT 變數下取得。

按一下應用程式「概觀」頁面上的**環境變數**，查看 VCAP_SERVICES 的整份清單以取得相關資訊：
```
{
   "cloudantNoSQLDB": [
      {
         "name": "Cloudant NoSQL DB-tx",
         "label": "cloudantNoSQLDB",
         "plan": "Shared",
         "credentials": {
            "username": "d72837bb-b341-4038-9c8e-7f7232916197-bluemix",
            "password": "b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424",
            "host": "d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com",
            "port": 443,
            "url": "https://d72837bb-b341-4038-9c8e-7f7232916197-bluemix:b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424@d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com"
         }
      }
   ]
}
```

**附註：**此環境變數是 JSON 物件的序列化，針對應用程式連結的每一個服務實例會有一個項目。每一個服務實例所提供資料的數量及類型都是服務所特有的。當您的應用程式未使用任何服務時，VCAP_SERVICES 是個空的 JSON 物件。此環境變數只適用於您將服務新增至應用程式時。


## 使用 cf CLI 建置應用程式
{: #ee_cf}

{{site.data.keyword.Bluemix_notm}} 提供數個工具讓您開始撰寫應用程式的程式碼，這些工具包括例如 cf 指令行介面及 Eclipse 工具。您可以選擇 cf 指令行介面開始撰寫應用程式 TestNode 的程式碼。

  1. 首先，下載並開發您應用程式的程式碼。
  
    1. 移至應用程式的「開始撰寫程式碼」頁面。按一下**下載入門範本程式碼**按鈕，以下載您的應用程式程式碼。
    2. 將下載的檔案解壓縮到目錄中，例如 `C:\test`。
    3. 使用本端整合開發環境來開發程式碼。
	
  2. 安裝 **cf** 指令行介面 (CLI)。
  
    1. 下載適用於您的作業系統的 cf 指令行工具安裝程式。
    2. 遵循工具精靈以完成安裝。
    3. 使用 **cf -v** 指令來驗證 cf 指令行介面的版本。例如：
	
	```
	cf -v
	```
	
    **需求：**請確定您隨時都使用最新版本的 cf 指令行工具。
  3. 安裝 **cf** 指令行介面之後，您必須使用 **cf api** 指令，來指定您工作時要使用的 {{site.data.keyword.Bluemix_notm}} 地區。**cf** 指令行介面使用 *https://api.Bluemix_URL*，其中 *Bluemix_URL* 是地區的 URL。「美國南部」地區 URL 是 {{Domain}}。請輸入下列指令，以連接至 {{site.data.keyword.Bluemix_notm}}：
  
  ```
  cf api https://api.ng.bluemix.net
	 ```
  
  如需連接至其他 {{site.data.keyword.Bluemix_notm}} 地區的相關資訊，請參閱 {{site.data.keyword.Bluemix_notm}} 地區。指定 {{site.data.keyword.Bluemix_notm}} 地區之後，會儲存您指定的位置資訊。
  
  4. 接下來，您可以使用 cf login 指令登入 {{site.data.keyword.Bluemix_notm}}。
  
  ```
  cf login -u your_user_ID -p ***** -o your_org_name -s your_space_name
  ```
  
  5. 登入 {{site.data.keyword.Bluemix_notm}} 之後，您便可以將應用程式部署回 {{site.data.keyword.Bluemix_notm}}。從您的應用程式目錄 `C:\test` 輸入下列指令：
  
  ```
  cf push TestNode
  ```
  
  如需 **cf push** 指令的相關資訊，請參閱「上傳應用程式」。
  
  6. 現在，您可以在瀏覽器裡輸入下列應用程式 URL，來存取應用程式：
```
  http://TestNode.mybluemix.net
  ```

您也可以選擇其他工具來建置您的應用程式，例如 Eclipse 工具。如需相關資訊，請參閱 {{site.data.keyword.Bluemix_notm}} 使用者介面上應用程式的「開始撰寫程式碼」頁面。

## 使用 cf CLI 連結服務
{: #ee_cfbind}

使用 {{site.data.keyword.Bluemix_notm}}，您可以使用 Bluemix 使用者介面來新增服務，如本情境稍早所述。但您也可以使用 **cf** 指令行介面來連結服務。假設您想要使用 cf 指令行介面將 {{site.data.keyword.cloudant}} 服務新增至應用程式 TestNode。

若要在應用程式內使用 {{site.data.keyword.cloudant}} 服務，您需要建立 Cloudant 服務實例、將應用程式連結至服務實例，然後使用該服務實例。相同的程序也適用於所有其他服務。

  1. 建立 Cloudant NoSQL DB 服務實例。
  
  使用 cf create-service 指令來建立新的服務實例。例如：
  
  ```
  cf create-service cloudantNoSQLDB Shared cloudant100
  ```
  
  還可以使用 cf services 指令來查看您所建立的服務實例清單。
  
  ```
  cf services
```
  
  建立服務實例之後，即可供您的任何應用程式連結和使用。
  
  2. 將服務實例連結至您的應用程式。
  
  若要使用服務實例，必須將它連結至您的應用程式。使用 cf bind-service 指令，透過指定應用程式名稱以及您所建立的服務實例，將服務實例連結至應用程式。
  
  ```
  cf bind-service TestNode cloudant100
  ```
  
  將服務實例連結至應用程式可讓 {{site.data.keyword.Bluemix_notm}} 與服務通訊，並可指定新的應用程式將與該服務實例通訊。對於不同服務，{{site.data.keyword.Bluemix_notm}} 在連結期間，可能以不同方式處理應用程式及服務實例。例如，部分服務可能會針對每一個與服務實例通訊的應用程式，建立新的承租戶。服務會使用認證之類的資訊回應 {{site.data.keyword.Bluemix_notm}}，必須將這些資訊傳遞給應用程式，才能在應用程式與服務之間進行通訊。

  **附註：**如果應用程式在連結至服務實例時正在執行，則在重新啟動應用程式之前，都不會更新 VCAP_SERVICES 環境變數。若要重新啟動應用程式，請使用 cf restart 指令。
  
  3. 使用服務實例。
  
  在此情況下，VCAP_SERVICES 環境變數包括應用程式可用來連接至此 {{site.data.keyword.cloudant}} 實例的資訊，例如下列項目：
  
  <dl><dt>username</dt>
  <dd>d72837bb-b341-4038-9c8e-7f7232916197-bluemix</dd>
  <dt>password</dt>
  <dd>b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424</dd>
  <dt>url</dt>
  <dd>https://d72837bb-b341-4038-9c8e-7f7232916197-bluemix:b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424@d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com</dd></dt></dl>
  
  例如，您的 Node.js 應用程式可能會存取此資訊，如下所示：
```
  if (process.env.VCAP_SERVICES) {
        var env = JSON.parse(process.env.VCAP_SERVICES);
        var cloudant = env['"cloudantNoSQLDB'][0].credentials;
  } else {
        var cloudant = {
                "username" : "user1",
                "password" : "secret",
                "url" : "https://user1:secret@localhost:25002"
                }
        };
  ```
  
  **附註：**如範例程式碼所示，若要連接至 {{site.data.keyword.cloudant}} 服務實例，您可以先檢查 VCAP_SERVICES 環境變數是否存在。如果存在，應用程式就可以使用 cloudant 變數的內容來存取資料庫。不過，如果 VCAP_SERVICES 環境變數不存在，則會以所提供的預設值來使用本端 {{site.data.keyword.cloudant}} 服務實例。
  
  4. 與服務實例互動。
  
  您可以使用認證資訊來與服務實例互動。您可以採取的動作包括讀取、寫入及更新。下列範例示範如何將 JSON 物件插入到 {{site.data.keyword.cloudant}} 服務實例：
```
  // create a new message
var create_message = function(req, res) {
  require('cloudantdb').connect(cloudant.url, function(err, conn) {
    var collection = conn.collection('messages');

    // create message record
    var parsedUrl = require('url').parse(req.url, true);
    var queryObject = parsedUrl.query;
    var name = (queryObject["name"] || 'Bluemix');
    var message = { 'message': 'Hello, ' + name, 'ts': new Date()
};
    collection.insert(message, {safe:true}, function(err){
      if (err) { console.log(err.stack); }
      res.writeHead(200, {'Content-Type': 'text/plain'});
      res.write(JSON.stringify(message));
      res.end('\n');
    });
  });
}
  ```
  
  5. **選用項目：**取消連結或刪除服務實例。
  
  當您不再使用服務實例或想要釋放一些空間時，可能會想要取消連結或刪除服務實例。若要取消應用程式與服務實例的連結，請使用 **cf unbind-service** 指令；若要刪除服務實例，請使用 **cf delete-service** 指令。

  如需服務的相關資訊，請參閱「服務」。如需可用來在 {{site.data.keyword.Bluemix_notm}} 環境中管理應用程式的 **cf** 選項相關資訊，請在 **cf** 指令行介面中發出 **cf --help**。

  **附註：**刪除服務實例之前，請先確定不再需要該服務實例。刪除服務實例會同時消除與該服務實例相關聯的所有資料。任何連結至已刪除之服務的應用程式，在重新啟動之前，都無法更新其 VCAP_SERVICES 環境變數。

## 計算應用程式成本
{: #ee_billing}

您的 30 天免費試用已過期，但還想要繼續使用 {{site.data.keyword.Bluemix_notm}}。您必須新增信用卡資訊，以成為「隨收隨付制」帳戶或「訂閱」帳戶，才能繼續使用 {{site.data.keyword.Bluemix_notm}}。不過，即使您轉換成付費帳戶，{{site.data.keyword.Bluemix_notm}} 還是會針對大部分的執行時期架構和服務提供免費額度。除非用量超過免費額度，否則 {{site.data.keyword.Bluemix_notm}} 不會向您收費。

{{site.data.keyword.Bluemix_notm}} 提供預估器和計算機，可讓您查看應用程式成本。您可以使用下列方式查看 TestNode 的成本：

  * 在儀表板中，按一下 TestNode。然後在「概觀」頁面中，按一下**預估此應用程式的成本**，以查看 **SDK for Node.js** 執行時期和支援的價格，並查看應用程式每月價格總計。
  
  * 或者，在「定價單」頁面中，鍵入應用程式的執行時期和服務的每月用量。例如，3 個 **SDK for Node.js** 實例且每個實例有 1 GB 的記憶體。即會計算並顯示每月價格。

您也可以手動計算應用程式成本，方法是將執行時期和服務的價格相加，再減掉免費額度。如需相關資訊，請參閱「手動計算您的成本」。

## 移除應用程式
{: #ee_removing}

隨著您建置更多的應用程式，可能會達到配額限制。不過，有些您可能不會再使用的應用程式仍會佔用配額。您隨時都可以輕鬆地刪除應用程式，以在 {{site.data.keyword.Bluemix_notm}} 中釋出一些空間。

在 {{site.data.keyword.Bluemix_notm}} 使用者介面中，移至應用程式「概觀」頁面，按一下**功能表**圖示，然後刪除您不再使用的應用程式。您也可以使用 **cf delete** 指令來刪除應用程式。
