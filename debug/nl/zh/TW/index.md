---

copyright:
  years: 2015, 2016

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}


# 除錯
{: #debugging}

*前次更新：2016 年 3 月 3 日*

如果您遇到 {{site.data.keyword.Bluemix}} 問題，則可以檢視日誌檔來調查問題，並且進行除錯。
{:shortdesc}

日誌提供如工作是順利執行還是失敗這類的資訊。它們也會提供可用來除錯並判定問題原因的相關資訊。

日誌是固定格式。對於詳細日誌，您可以過濾日誌，或使用外部記載主機來儲存及處理日誌。如需日誌格式、檢視及過濾日誌，以及配置外部記載的相關資訊，請參閱 [Cloud Foundry 上執行之應用程式的記載](../monitor_log/monitoringandlogging.html#logging_for_bluemix_apps){: new_window}。


## 針對編譯打包錯誤進行除錯
{: #debugging-staging-errors}
您在 {{site.data.keyword.Bluemix_notm}} 上編譯打包應用程式時可能會遇到問題。如果無法編譯打包您的應用程式，您可以檢視日誌來查看錯誤原因，以及從問題中回復。

若要瞭解應用程式在 {{site.data.keyword.Bluemix_notm}} 上失敗的原因，您需要知道如何將應用程式部署至 {{site.data.keyword.Bluemix_notm}}，並在其上執行。如需詳細資訊，請參閱[應用程式部署](../manageapps/depapps.html#appdeploy){: new_window}。

下列程序顯示如何使用 `cf logs` 指令來針對編譯打包錯誤進行除錯。採取下列步驟之前，請確定已安裝 cf 指令行介面。如需安裝 cf 指令行介面的相關資訊，請參閱[安裝 cf 指令行介面](../starters/install_cli.html){: new_window}。

  1. 在 cf 指令行介面中輸入下列程式碼，以連接至 {{site.data.keyword.Bluemix_notm}}：
     ```
	 cf api https://api.ng.bluemix.net
	 ```
	 
  2. 輸入 `cf login`，以登入 {{site.data.keyword.Bluemix_notm}}。
  
  3. 輸入 `cf logs appname --recent`，以擷取最近日誌。如果您要過濾詳細日誌，請使用 `grep` 選項。例如，您可以輸入下列程式碼，只顯示 [STG] 日誌：
```
	cf logs appname --recent | grep '\[STG\]'
	```
  4. 檢視日誌中顯示的第一個錯誤。
  
如果您使用 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 外掛程式來部署應用程式，則會在 Eclipse 工具的**主控台**標籤中，看到類似 cf logs 輸出的日誌。當您部署應用程式時，也可以開啟不同的 Eclipse 視窗來追蹤日誌。``

除了 `cf logs` 指令之外，在 {{site.data.keyword.Bluemix_notm}} 中，您也可以使用 Monitoring and
Analytics 服務來收集日誌詳細資料。此外，Monitoring and Analytics 服務還會監視應用程式的效能、性能及可用性。它也提供 Node.js 及 Liberty 執行時期應用程式的日誌分析。  

### 針對 Node.js 應用程式的編譯打包錯誤進行除錯

下列範例顯示在您輸入 `cf logs appname --recent` 之後所顯示的日誌。此範例假設 Node.js 應用程式發生編譯打包錯誤：
```
2014-08-11T14:19:36.17+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({name"=>"SampleExpressApp"}
2014-08-11T14:20:44.17+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({"state"=>"STOPPED"})
2014-08-11T14:20:44.19+0100 [App/0]   ERR
2014-08-11T14:20:44.43+0100 [DEA]     OUT Stopping app instance (index 0) with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:44.44+0100 [DEA]     OUT Stopped app instance (index 0) with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:48.97+0100 [DEA]     OUT Got staging request for app with id 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:50.94+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({"state"=>"STARTED"})
2014-08-11T14:20:51.66+0100 [STG]     OUT -----> Download app package (4.1M)
2014-08-11T14:20:51.90+0100 [STG]     OUT -----> Download app buildpack cache (1.1M)
2014-08-11T14:20:52.78+0100 [STG]     OUT -----> Buildpack Version: v1.1-20140717-1447
2014-08-11T14:20:52.78+0100 [STG]     ERR parse error: Expected another key-value pair at line 18, column 3
2014-08-11T14:20:52.79+0100 [STG]     OUT 0 info it worked if it ends with ok
```
{: screen}


日誌中的第一個錯誤顯示編譯打包失敗的原因。在此範例中，第一個錯誤是 DEA 元件在編譯打包階段期間的輸出。
```
2014-08-11T14:20:52.78+0100 [STG]   ERR parse error: expected another key-value pair at line 18, column 3
```
{: screen}


針對 Node.js 應用程式，DEA 使用 `package.json` 檔案中的資訊來下載模組。從此錯誤中，您可以看到模組發生該錯誤。因此，您可能需要檢閱 `package.json` 檔案的第 18 行。 

```
15   "jade": "~1.3.0",
16   "mongodb": "*",
17   "monk":"*",
18   }
```
{: screen}


您可以看到在第 17 行結尾放置了逗點，因此，預期第 18 行會有鍵值組。若要修正問題，請移除逗點：

```
15   "jade": "~1.3.0",
16   "mongodb": "*",
17   "monk":"*"
18   }
```
{: screen}


## 針對執行時期錯誤進行除錯
{: #debugging-runtime-errors}
如果您的應用程式在執行時期遇到問題，應用程式日誌可以協助您精確找出發生此錯誤的原因，並從該問題中回復。 

具體而言，您可以啟用記載至 stdout 及 stderr。如需如何針對使用 {{site.data.keyword.Bluemix_notm}} 內建建置套件部署的應用程式，配置其日誌檔的相關資訊，請參閱下列清單：

  * 若為 Liberty for Java™ 應用程式，請參閱 [Liberty Profile: Logging and Trace](http://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html){: new_window}。
  * 若為 Node.js 應用程式，請參閱 [How to log in node.js](http://docs.nodejitsu.com/articles/intermediate/how-to-log){: new_window}。 
  * 若為 PHP 應用程式，請參閱 [error_log](http://php.net/manual/en/function.error-log.php){: new_window}。
  * 若為 Python 應用程式，請參閱 [logging HOWTO](https://docs.python.org/2/howto/logging.html){: new_window}。
  * 若為 Ruby on Rails 應用程式，請參閱 [The Logger](http://guides.rubyonrails.org/debugging_rails_applications.html#the-logger){: new_window}。
  * 若為 Ruby Sinatra 應用程式，請參閱 [Logging](http://www.sinatrarb.com/intro.html#Logging){: new_window}。
  
當您在 cf 指令行介面中輸入 `cf logs appname --recent` 時，只會顯示最新的日誌。若要檢視之前發生的錯誤日誌，您必須擷取所有的日誌，然後搜尋錯誤。若要擷取應用程式的所有日誌，請使用下列其中一種方法：
<dl> 
<dt><strong>{{site.data.keyword.Bluemix_notm}} Monitoring and Analytics 服務</strong></dt> 
<dd>Monitoring and Analytics 服務具有整合性的日誌檔搜尋及分析功能，可協助您快速地識別錯誤。如需相關資訊，請參閱 <a href="../services/monana/index.html#gettingstartedtemplate" target="_blank">Monitoring and Analytics</a>。</dd> 
<dt><strong>協力廠商工具</strong></dt> 
<dd>您可以收集應用程式的日誌，並將其匯出至外部日誌主機。如需相關資訊，請參閱<a href="../monitor_log/monitoringandlogging.html#thirdparty_logging" target="_blank">配置外部記載</a>。</dd> 
<dt><strong>收集並匯出日誌的 Script</strong></dt> 
<dd>若要使用 Script 來自動收集並匯出日誌到外部檔案，您必須從您的電腦連接至 {{site.data.keyword.Bluemix_notm}} 伺服器，而且您的電腦上必須具有足夠的空間可下載日誌。如需相關資訊，請參閱<a href="../support/index.html#collecting-diagnostic-information" target="_blank">收集診斷資訊</a>。</dd>
</dl>

依預設，之前可透過 {{site.data.keyword.Bluemix_notm}}「儀表板」中的應用程式視圖，在**檔案** > **日誌**下存取 `stdout.log` 及 `stderr.log` 檔案。然而，{{site.data.keyword.Bluemix_notm}} 管理所在的 Cloud Foundry 現行版本無法再使用該應用程式記載。若要持續可以透過 {{site.data.keyword.Bluemix_notm}}「儀表板」在**檔案** > **日誌**下存取 stdout 及 stderr 應用程式記載，您可以將記載重新導向至 {{site.data.keyword.Bluemix_notm}} 檔案系統中的其他檔案（視您使用的執行時期而定）。 

  * 若為 Liberty for Java 應用程式，導向到 stdout 及 stderr 的輸出已包含在 logs 目錄中的 `messages.log` 檔案中。請分別尋找字首為 SystemOut 及 SystemErr 的項目。
  * 若為 Node.js 應用程式，您可以置換 console.log 函數，以明確地寫入 logs 目錄中的檔案。
  * 若為 PHP 應用程式，您可以使用 error_log 函數來寫入 logs 目錄中的檔案。
  * 若為 Python 應用程式，您可以讓日誌程式寫入 logs 目錄中的檔案：logging.basicConfig(filename='../../logs/example.log',level=logging.DEBUG)
  * 若為 Ruby 應用程式，您可以讓日誌程式寫入 logs 目錄中的檔案。
 

# 相關鏈結
{: #rellinks}

## 一般
{: #general}

  * [Droplet Execution Agent (DEA)](http://docs.cloudfoundry.org/concepts/architecture/execution-agent.html){: new_window}
  * [開始使用 IBM Monitoring and Analytics for Bluemix 服務](../services/monana/index.html#gettingstartedtemplate){: new_window}
  * [Bluemix 運作方式](../public/index.html#howwork){: new_window}
  * [安裝 cf 指令工具](../starters/install_cli.html){: new_window}
  * [檢視日誌](../monitor_log/monitoringandlogging.html#viewing_logs){: new_window}
  
  
 














