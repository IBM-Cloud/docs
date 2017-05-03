---

copyright:
  years: 2017
lastupdated: "2017-04-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# 在 Bluemix 上開始使用 PHP
{: #getting_started}

* {: download} 恭喜，您已在 {{site.data.keyword.Bluemix}} 上部署 Hello World 範例應用程式！若要開始使用，請遵循本逐步手冊。或者，<a class="xref" href="http://bluemix.net" target="_blank" title="（下載範例程式碼）"><img class="hidden" src="../../images/btn_starter-code.svg" alt="下載應用程式碼" />下載範例程式碼</a>，並自行探索。

遵循本手冊，您將設定開發環境、在本端及 {{site.data.keyword.Bluemix}} 上部署應用程式，以及在應用程式中整合 {{site.data.keyword.Bluemix}} 資料庫服務。

## 必要條件
{: #prereqs}

您需要下列各項：
* [{{site.data.keyword.Bluemix_notm}} 帳戶](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://git-scm.com/downloads){: new_window}
* [PHP ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://php.net/downloads.php){: new_window}
* [Composer ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://getcomposer.org/download/){: new_window}

## 1. 複製範例應用程式
{: #clone}

現在您可以開始使用應用程式。請複製儲存庫，並將目錄變更為範例應用程式所在的目錄。
  ```
git clone https://github.com/IBM-Bluemix/get-started-php
  ```
  {: pre}
  ```
cd get-started-php
  ```
  {: pre}

## 2. 在本端執行應用程式

安裝相依關係
```
php composer.phar install
```
{: pre}

執行應用程式
  ```
php -S localhost:8000
  ```
  {: pre}

在下列網址檢視您的應用程式：http://localhost:8000

## 3. 準備應用程式以進行部署
{: #prepare}

若要部署至 {{site.data.keyword.Bluemix_notm}}，它有助於設定 manifest.yml 檔案。manifest.yml 包括應用程式的基本資訊（例如名稱、配置給每一個實例的記憶體數量，以及路徑）。我們已在 `get-started-php` 目錄中提供範例 manifest.yml 檔案。

開啟 manifest.yml 檔案，然後將 `name` 從 `GetStartedPHP` 變更為您的應用程式名稱 <var class="keyword varname" data-hd-keyref="app_name">app_name</var>。
{: download}

  ```
 applications:
 - name: GetStartedPHP
   random-route: true
   memory: 128M
  ```
  {: codeblock}

在此 manifest.yml 檔案中，**random-route: true** 會為應用程式產生隨機路徑，以防止您的路徑與其他人發生衝突。如果您選擇這樣做，則可以將 **random-route: true** 取代為 **host: myChosenHostName**，並提供您選擇的主機名稱。[進一步瞭解...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. 部署應用程式
 {: #deploy}

您可以使用 Cloud Foundry CLI 來部署應用程式。

選擇您的 API 端點
   ```
cf api <API-endpoint>
   ```
   {: pre}

將指令中的 *API-endpoint* 取代為下列清單中的 API 端點。

|URL                             |地區          |
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net     | 美國南部       |
| https://api.eu-gb.bluemix.net  | 英國 |
| https://api.au-syd.bluemix.net | 雪梨         |

登入 {{site.data.keyword.Bluemix_notm}} 帳戶

   ```
cf login
```
   {: pre}

 從 *get-started-php* 目錄中，將應用程式推送至 {{site.data.keyword.Bluemix_notm}}
   ```
cf push
```
   {: pre}

 這可能需要一分鐘。如果部署程序發生錯誤，則您可以使用指令 `cf logs <Your-App-Name> --recent` 進行疑難排解。

 部署完成之後，您應該會看到一則訊息，指出應用程式正在執行。檢視 push 指令輸出中所列 URL 的應用程式。您也可以發出 
  ```
cf apps
  ```
  {: pre}
  指令來檢視應用程式狀態，並且查看 URL。

## 5. 新增資料庫
{: #add_database}

接下來，我們會將 NoSQL 資料庫新增至此應用程式並設定應用程式，因此，它可以在本端及 {{site.data.keyword.Bluemix_notm}} 上執行。

1. 在「瀏覽器」中，登入 {{site.data.keyword.Bluemix_notm}}。瀏覽至「儀表板」。按一下「名稱」直欄中的應用程式名稱，以選取該應用程式。
2. 依序按一下「連線」及「連接新服務」。
3. 在「資料與分析」區段中，選取 `Cloudant NoSQL DB`，然後建立服務。
4. 系統提示時，請選取「重新編譯打包」。{{site.data.keyword.Bluemix_notm}} 會使用 `VCAP_SERVICES` 環境變數來重新啟動應用程式，並將資料庫認證提供給應用程式。只有在應用程式於 {{site.data.keyword.Bluemix_notm}} 上執行時，才能使用此環境變數。

環境變數可讓您分開部署設定與原始碼。例如，您可以將資料庫密碼儲存在原始碼中所參考的環境變數內，而不要將資料庫密碼寫在程式中。[進一步瞭解...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 6. 使用資料庫
{: #use_database}
我們現在即將更新本端程式碼，使其指向此資料庫。我們將建立可儲存服務之認證的 json 檔案，應用程式將使用這些服務。只有在應用程式於本端執行時，才會使用此檔案。在 {{site.data.keyword.Bluemix_notm}} 中執行時，將會從 VCAP_SERVICES 環境變數中讀取認證。

1. 在 `get-started-php` 目錄中，建立稱為 `.env` 且具有下列內容的檔案：
  ```
  CLOUDANT_HOST=
  CLOUDANT_USERNAME=
  CLOUDANT_PASSWORD=
  ```

2. 回到 {{site.data.keyword.Bluemix_notm}} 使用者介面，然後選取您的應用程式 ->「連線」-> Cloudant ->「檢視認證」

3. 將 `CLOUDANT_HOST`、`CLOUDANT_USERNAME` 及 `CLOUDANT_PASSWORD` 欄位的值複製並貼入 `.env` 檔案，並儲存變更。結果將如下：
  ```
  CLOUDANT_HOST=abc...yz.cloudant.com
  CLOUDANT_USERNAME=abc...yz
  CLOUDANT_PASSWORD=445d...d1a
  ```

4. 在本端執行應用程式。
  ```
php -S localhost:8000
  ```
  {: pre}

  在下列網址檢視您的應用程式：http://localhost:8000 任何您輸入至應用程式的名稱，現在都會新增至資料庫。

  本端應用程式及 {{site.data.keyword.Bluemix_notm}} 應用程式將會共用資料庫。檢視上述 push 指令輸出中所列 URL 的 {{site.data.keyword.Bluemix_notm}} 應用程式。當您重新整理瀏覽器時，從任一應用程式新增的名稱應該會出現在這兩個應用程式中。

請記住，如果您不需要有應用程式，請停止它，如此就不會產生任何非預期的費用。
{: tip}  
