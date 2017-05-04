---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# 在 Bluemix 上開始使用 Liberty

* {: download} 恭喜，您已在 {{site.data.keyword.Bluemix}} 上部署 Hello World 範例應用程式！若要開始使用，請遵循本逐步手冊。或者，<a class="xref" href="http://bluemix.net" target="_blank" title="（下載範例程式碼）"><img class="hidden" src="../../images/btn_starter-code.svg" alt="下載應用程式碼" />下載範例程式碼</a>，並自行探索。

遵循本手冊，您將設定開發環境、在本端及 {{site.data.keyword.Bluemix}} 上部署應用程式，以及在應用程式中整合 {{site.data.keyword.Bluemix}} 資料庫服務。

## 必要條件
{: #prereqs}

您需要下列帳戶及工具：
* [{{site.data.keyword.Bluemix_notm}} 帳戶](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Eclipse IDE for Java EE Developers ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}
* [Git ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://git-scm.com/downloads){: new_window}
* [Maven ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://maven.apache.org/download.cgi){: new_window}

若要在 Eclipse 中使用 {{site.data.keyword.eclipsetoolsfull}} 開發，您也需要[下載工具。![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix){: new_window}

## 1. 複製範例應用程式
{: #clone}

請先複製範例應用程式 GitHub 儲存庫。
  ```bash
git clone https://github.com/IBM-Bluemix/get-started-java
  ```
  {: pre}


## 2. 使用指令行，在本端執行應用程式
{: #run_locally}

使用 Maven 來建置原始碼，並執行產生的應用程式。

1. 在指令行上，將目錄切換至範例應用程式所在的目錄。

  ```
cd get-started-java
  ```
  {: pre}

1. 使用 Maven 來安裝相依關係，並建置 .war 檔。

  ```
mvn clean install
  ```
  {: pre}

1. 在 Liberty 本端執行應用程式。
  ```
mvn install liberty:run-server
  ```
  {: pre}

當您看到訊息*伺服器 defaultServer 已準備好執行 Smarter Planet。* 時，請在 http://localhost:9080/GetStartedJava 檢視應用程式。

若要停止應用程式，請在您啟動應用程式的指令行視窗中按 *Ctrl-C*。

## 3. 準備應用程式以進行部署
{: #prepare}

若要部署至 {{site.data.keyword.Bluemix_notm}}，它有助於設定 manifest.yml 檔案。manifest.yml 包括應用程式的基本資訊（例如名稱、配置給每一個實例的記憶體數量，以及路徑）。我們已在 `get-started-java` 目錄中提供範例 manifest.yml 檔案。

開啟 manifest.yml 檔案，然後將 `name` 從 `GetStartedJava` 變更為您的應用程式名稱 <var class="keyword varname" data-hd-keyref="app_name">app_name</var>。
{: download}

  ```
  applications:
   - name: GetStartedJava
     random-route: true
     path: target/GetStartedJava.war
     memory: 512M
     instances: 1
  ```
  {: codeblock}

在此 manifest.yml 檔案中，**random-route: true** 會為應用程式產生隨機路徑，以防止您的路徑與其他人發生衝突。如果您選擇這樣做，則可以將 **random-route: true** 取代為 **host: myChosenHostName**，並提供您選擇的主機名稱。[進一步瞭解...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. 部署至 {{site.data.keyword.Bluemix_notm}}
{: #deploy}

將您的應用程式部署至下列其中一個 Bluemix 地區。為取得最佳延遲，請選擇最接近使用者的地區。

|地區          |API 端點                             |
|:---------------|:-------------------------------|
| 美國南部       |https://api.ng.bluemix.net     |
| 英國 | https://api.eu-gb.bluemix.net  |
| 雪梨         | https://api.au-syd.bluemix.net |

1. 將 `<API-endpoint>` 取代為您地區的端點，以設定 API 端點。
  ```
cf api <API-endpoint>
  ```
  {: pre}

1. 登入 {{site.data.keyword.Bluemix_notm}} 帳戶。
  ```
cf login
```
  {: pre}

1. 從 `get-started-java` 目錄中，將應用程式推送至 {{site.data.keyword.Bluemix_notm}}。
  ```
cf push
```
  {: pre}

部署應用程式可能需要一些時間。部署完成之後，您會看到一則訊息，指出應用程式正在執行。檢視 push 指令輸出中所列 URL 的應用程式，或執行下列指令來檢視應用程式部署狀態及 URL：
  ```
cf apps
  ```
  {: pre}

您可以使用 `cf logs <Your-App-Name> --recent` 指令，來對部署處理程序中的錯誤進行疑難排解。
{: tip}  

## 5. 使用 Eclipse 進行開發
{: #eclipse}

{{site.data.keyword.eclipsetoolsfull}} 提供可安裝至現有 Eclipse 環境的外掛程式，以協助將整合開發環境 (IDE) 與 {{site.data.keyword.Bluemix_notm}} 整合。

1. 確定您具有 [IBM Eclipse Tools for Bluemix](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix)。

2. 移至**檔案 > 匯入 > Maven > 現有 Maven 專案**，以將 `get-started-java` 範例匯入至 Eclipse。

3. 建立 Liberty 伺服器定義。下列步驟將會下載新的 Liberty 伺服器。
  - 在**視窗 > 顯示視圖 > 伺服器**視圖中，按一下滑鼠右鍵選取**新建 > 伺服器**。
  - 選取 **IBM > WebSphere Application Server Liberty**。
  - 選取**從保存檔或儲存庫安裝**。
  - 系統提示時，請輸入您要安裝 Liberty 之新資料夾的目的地路徑 (/Users/username/liberty)。
  - 選取**從 ibm.com 下載及安裝新的運行環境**。
  - 選取**含 Java EE 7 Web 設定檔的 WAS Liberty**。
  - 繼續使用預設選項來執行精靈，直到完成。

4. 在 Liberty 本端執行應用程式：
  - 移至**視窗 > Web 瀏覽器 > 預設系統 Web 瀏覽器**，以將 Web 瀏覽器變更為系統預設值。
  - 用滑鼠右鍵按一下 `GetStartedJava` 範例，然後選取**執行身分 > 在伺服器中執行**。
  - 尋找並選取 localhost Liberty 伺服器，然後按一下**完成**。

  只要幾秒鐘，應用程式就會在 http://localhost:9080/GetStartedJava 執行。

5. 更新程式碼：
  - 開啟 `src/main/webapp/index.html`，並將標題從 `<h1>Welcome.</h1>` 更新為 `<h1>Welcome Jane.</h1>`。
  - 儲存變更。Liberty 會自動反映變更。
  - 重新整理瀏覽器 (`http://localhost:9080/GetStartedJava`)，以查看變更。

6. 將變更推送至 {{site.data.keyword.Bluemix_notm}}：
  - 在指令行上，從 `get-started-java` 目錄中，重建 .war 檔。
    ```
mvn clean install
    ```
    {: pre}
  - 將應用程式推送至 {{site.data.keyword.Bluemix_notm}}。
    ```
cf push
```
    {: pre}

現在，您已在本端及雲端上執行程式碼！

## 6. 新增資料庫
{: #add_database}

接下來，我們會將 NoSQL 資料庫新增至此應用程式並設定應用程式，因此，它可以在本端及 {{site.data.keyword.Bluemix_notm}} 上執行。

1. 在瀏覽器中，登入 {{site.data.keyword.Bluemix_notm}}，並移至「儀表板」。按一下**名稱**直欄中的應用程式名稱，以選取該應用程式。
2. 依序按一下**連線**及**連接新服務**。
3. 在**資料與分析**區段中，選取 **Cloudant NoSQL DB**，然後建立服務。
4. 系統提示時，請選取**重新編譯打包**。{{site.data.keyword.Bluemix_notm}} 會使用 `VCAP_SERVICES` 環境變數來重新啟動應用程式，並將資料庫認證提供給應用程式。只有在應用程式於 {{site.data.keyword.Bluemix_notm}} 上執行時，才能使用此環境變數。

環境變數可讓您分開部署設定與原始碼。例如，您可以將資料庫密碼儲存在原始碼中所參考的環境變數內，而不要將資料庫密碼寫在程式中。[進一步瞭解...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 7. 使用資料庫
{: #use_database}
我們現在即將更新本端程式碼，使其指向此資料庫。我們會將服務的認證儲存在內容檔中。只有在應用程式於本端執行時，才會使用此檔案。在 {{site.data.keyword.Bluemix_notm}} 中執行時，將會從 `VCAP_SERVICES` 環境變數中讀取認證。

1. 在 Eclipse 中，開啟 src/main/resources/cloudant.properties 檔案：
  ```
  cloudant_url=
  ```
  {: pre}

2. 在瀏覽器中，移至 {{site.data.keyword.Bluemix_notm}}，然後選取**應用程式 > _您的應用程式_ > 連線 > Cloudant > 檢視認證**。

3. 只要將 `url` 從認證複製並貼入 `cloudant.properties` 檔案的 `url` 欄位中，並儲存變更。
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:pre}

4. 在 Eclipse 中，從「伺服器」視圖重新啟動 Liberty 伺服器。

  重新整理位於下列網址的瀏覽器視圖：http://localhost:9080/GetStartedJava/ 任何您輸入至應用程式的名稱，現在都會新增至資料庫。

  本端應用程式及 {{site.data.keyword.Bluemix_notm}} 應用程式將會共用資料庫。當您重新整理瀏覽器時，從任一應用程式新增的名稱就會出現在這兩個應用程式中。


請記住，如果您不需要 {{site.data.keyword.Bluemix_notm}} 上有應用程式，請停止應用程式，如此就不會產生任何非預期的費用。
{: tip}  
