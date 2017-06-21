---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-10"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 


# 運行環境疑難排解
{: #runtimes}

您在使用 {{site.data.keyword.Bluemix}} 運行環境時可能會遇到問題。在許多情況下，您可以遵照一些簡單的步驟，從這些問題回復。
{:shortdesc}


## 推送應用程式時，使用已作廢的建置套件
{: #ts_loading_bp}

您推送應用程式時可能無法使用最新的建置套件元件。您可以使用具有內建機制的建置套件，以避免載入已作廢的元件，或者您可以刪除應用程式快取目錄中的內容，然後才推送或重新編譯打包應用程式。 

當您在建置套件更新之後，推送或重新編譯打包應用程式時，不會自動載入最新的建置套件元件。因此，您的應用程式會使用快取中已作廢的建置套件元件。自您上次推送應用程式之後，套用至建置套件的更新都不會實作。
{: tsSymptoms}

部分建置套件未配置為自動從網際網路下載所有更新的元件，來確保您隨時使用最新的版本。
{: tsCauses} 

您可以使用具有內建機制的建置套件來避免載入已作廢的元件，例如下列建置套件：
{: tsResolve}

  * [Cloud Foundry Java 建置套件 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/cloudfoundry/java-buildpack){: new_window}。這個建置套件具有內建的機制，可以確保使用最新版本的建置套件。如需此機制運作方式的相關資訊，請參閱 [extending-caches.md ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window}。 
  * [Cloud Foundry Node.js 建置套件 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}。此建置套件的功能與使用環境變數類似。為了讓 Node.js 建置套件能每次從網際網路下載 node 模組，請在 cf 指令行介面中，鍵入下列指令： 	
  ```
  set NODE_MODULES_CACHE=false
  ```

如果您使用的建置套件未提供自動載入最新元件的機制，您可以手動刪除快取目錄中的內容，然後重新推送應用程式。請使用下列步驟：

 1. 移出空值建置套件的分支，例如 https://github.com/ryandotsmith/null-buildpack。如需如何移出分支的相關資訊，請參閱 [Git Basics - Getting a Git Repository ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window}。  
 2. 將下行新增到 `null-buildpack/bin/compile` 檔案並確定變更。如需如何確定變更的相關資訊，請參閱 [Git Basics - Recording Changes to the Repository ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window}。
  ```
  rm -rfv $2/*
  ```
 3. 使用下列指令，用已修改的空值建置套件推送應用程式，以刪除快取。完成此步驟之後，應用程式快取目錄中的所有內容都會刪除。
  ```
  cf push appname -p app_path -b <modified_null_buildpack>
  ```
 4. 使用下列指令，用您想要使用的最新建置套件來推送應用程式： 
  ```
  cf push appname -p app_path -b <latest_buildpack>
  ```
 
## PHP 建置套件產生的 NOTICE 訊息
{: #ts_phplog}

您可能會在日誌中看到包含 NOTICE 的訊息。您可以變更記載層次，以停止記載這些訊息。	

當您使用 PHP 建置套件將應用程式推送至 {{site.data.keyword.Bluemix_notm}} 時，可能會看到包含 `NOTICE` 的訊息：
{: tsSymptoms}

```
• 2015-01-26T15:00:59.70+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: fpm is running, pid 93
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: ready to handle connections
```
在 PHP 建置套件中，error_log 參數會定義記載層次。依預設，`error_log` 參數的值為 **stderr notice**。下列範例顯示 Cloud Foundry 提供之 PHP 建置套件的 `nginx-defaults.conf` 檔案中的預設記載層次配置。如需相關資訊，請參閱 [cloudfoundry/php-buildpack ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window}。
{: tsCauses} 

```
daemon off;
error_log stderr notice;
pid @{HOME}/nginx/logs/nginx.pid;
```
	
`NOTICE` 訊息僅提供資訊，不一定表示有問題。若要停止記載這些訊息，您可以在建置套件的 nginx-defaults.conf 檔案中，將記載層次從 `stderr notice` 變更為 `stderr error`。例如：
{: tsResolve}

```
daemon off;
error_log stderr error;
pid @{HOME}/nginx/logs/nginx.pid;
```
如需如何變更預設記載配置的相關資訊，請參閱 [error_log ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window}。
	

## 無法將協力廠商的 Python 檔案庫匯入 {{site.data.keyword.Bluemix_notm}}
{: #ts_importpylib}

您可能無法將協力廠商的 Python 檔案庫匯入 {{site.data.keyword.Bluemix_notm}}。若要解決此問題，請在 Python 應用程式的根目錄中新增配置檔。

當您嘗試匯入協力廠商的 Python 檔案庫（例如 `web.py` 檔案庫）時，`cf push` 指令會失敗。
{: tsSymptoms}

Python 應用程式的配置資訊遺失。
{: tsCauses}

在 Python 應用程式的根目錄中，新增 `requirements.txt` 檔案和 `Procfile` 檔案。下列資訊是假設您要匯入 `web.py` 檔案庫：
{: tsResolve}

 1. 在 Python 應用程式的根目錄中，新增 `requirements.txt` 檔案。
 
 `requirements.txt` 檔案可指定 Python 應用程式所需的檔案庫套件，以及套件的版本。下列範例顯示 `requirements.txt` 檔案的內容，其中 `web.py==0.37` 表示將要下載的 `web.py` 檔案庫版本為 0.37，而 `wsgiref==0.1.2` 表示 web.py 檔案庫所需的 Web 伺服器閘道介面版本為 0.1.2。
	 ```
	 web.py==0.37
     wsgiref==0.1.2
```
	 如需如何配置 `requirements.txt` 檔案的相關資訊，請參閱[需求檔案](https://pip.readthedocs.org/en/1.1/requirements.html)。
 2. 在 Python 應用程式的根目錄中，新增 `Procfile` 檔案。`Procfile` 檔案必須包含 Python 應用程式的啟動指令。在下列指令中，*yourappname* 是 Python 應用程式的名稱，而 *PORT* 是 Python 應用程式必須用來接收應用程式使用者要求的埠號。*$PORT* 是選用項目。如果您未在啟動指令中指定 PORT，則會使用應用程式內 `VCAP_APP_PORT` 環境變數下的埠號。 
	```
	web: python <yourappname>.py $PORT
```

您現在可以將協力廠商的 Python 檔案庫匯入 {{site.data.keyword.Bluemix_notm}}。	


## 已停用「實例詳細資料」頁面上的「動作」按鈕
{: #ts_actionsbutton}

已停用「實例詳細資料」頁面上的「動作」按鈕。
{: tsSymptoms} 

發生此問題的原因如下：
{: tsCauses}

 * 應用程式不是 Java&trade; Web 應用程式。Runtime Management Utilities (RMU) 只支援使用 Liberty 建置套件所部署的 Web 應用程式。
 * 應用程式不是使用內嵌的 Liberty 建置套件所部署。
 * 應用程式是使用舊版 Liberty 建置套件所部署。

如果問題是舊版 Liberty 建置套件所造成，請在 {{site.data.keyword.Bluemix_notm}} 中重新部署應用程式。否則，您可以將下列用戶端應用程式日誌檔提供給支援團隊：
{: tsResolve} 

  * logs/messages.log
  * logs/stdout.log
  * logs/stderr.log
 
  
## 需要有認證才能開啟追蹤或傾出視窗
{: #ts_username}

需要有使用者名稱和密碼，才能開啟追蹤或傾出視窗。
{: tsSymptoms}

此問題的發生原因是登入階段作業逾時。
{: tsCauses}

請重新輸入使用者名稱和密碼。
{: tsResolve}


## 追蹤或傾出作業執行時發生錯誤
{: #ts_target}

當追蹤或傾出作業在執行時顯示錯誤訊息。訊息指出應用程式的目標實例不是處於執行中狀態：
{: tsSymptoms}

```
實例 0：已順利設定追蹤規格
實例 2：已順利設定追蹤規格
實例 1：應用程式 abcd 的目標實例 1 未處於執行中狀態。
實例 3：已順利設定追蹤規格
實例 4：已順利設定追蹤規格
```

發生此問題的原因如下：
{: tsCauses} 

  * 追蹤或傾出管理功能僅適用於執行中的應用程式實例。在已停止、啟動中或已損毀的應用程式實例上，無法執行追蹤或傾出作業。
  * 當追蹤或傾出對話框開啟時，應用程式實例的狀態為變更中。 

請關閉視窗，然後再重新開啟。
{: tsResolve} 


## 實例的 traceSpecification 配置各不相同
{: #ts_different_config}

對於某個應用程式的不同實例，您可能會看到不同的 traceSpecification 配置。
{: tsSymptoms}

發生此行為的原因如下：
{: tsCauses}

  * 您先前已變更一個以上實例的配置。如果您變更某個實例的 traceSpecification 配置，該變更並不適用於相同應用程式的其他實例。例如，您的應用程式使用 log4j，而這個應用程式有兩個實例。您可以將實例 0 的記載層次從 info 變更為 debug，但實例 1 的記載層次仍為 info。
  
  * 應用程式橫向擴充，並且有新的實例。RMU 不會將現有實例的 traceSpecification 配置套用至新的橫向擴充實例。新的實例會使用預設配置。例如，您的應用程式使用 log4j，而其具有一個實例。您可以將此實例的記載層次從 info 變更為 debug。進行這項變更之後，如果您將應用程式橫向擴充為兩個實例，則新實例的記載層次是 info，而非 debug。

不需要執行任何動作。這是預期的行為。
{: tsResolve} 


## 已超出磁碟限額
{: #ts_diskquota}

您可能會在應用程式日誌中看到已超出磁碟限額。

您在應用程式的日誌中看到`已超出磁碟限額`訊息。
{: tsSymptoms}

發生此問題的原因為下列其中一項：
{: tsCauses} 

  * 傾出檔案是由執行中的應用程式實例所產生，而這些檔案耗盡配置的磁碟限額。依預設，一個應用程式實例的磁碟限額為 1 GB。您可以按一下**儀表板 > 應用程式 > 應用程式運行環境**，來檢查您的磁碟用量。下列範例顯示一個應用程式的兩個實例的運行環境資訊，包括磁碟用量：
    ```
    Instance	State	CPU	Memory Usage	Disk Usage

	0		Running	1.0%	344.8MB/512MB	236.8MB/1GB
	2		Running	2.3%	361.2MB/512MB	235.7MB/1GB
    ```
  * 磁碟限額受限於現行組織配額。

請使用下列其中一種方法：
{: tsResolve} 

  * 在下載傾出檔案之後刪除它們。
  * 在部署資訊清單中包含下列項目，以較大的磁碟限額來重新部署應用程式：
    ```
	disk_quota: 2048
	```
	
