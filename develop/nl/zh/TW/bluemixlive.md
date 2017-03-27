---



copyright:
  years: 2015，2017
lastupdated: "2017-3-10"

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}

#{{site.data.keyword.Bluemix_notm}} Live Sync 
{: #live-sync}

 
如果您要建置 Node.js 應用程式，可以使用 {{site.data.keyword.Bluemix}} Live Sync 快速更新 {{site.data.keyword.Bluemix_notm}} 上的應用程式實例，而且不需手動重新部署即可開發。   
{: shortdesc}

當您進行變更時，可以立即在執行中的 {{site.data.keyword.Bluemix_notm}} 應用程式看到該變更。{{site.data.keyword.Bluemix_notm}} Live Sync 會 
<!--from both the command line and -->
在 Eclipse Orion Web IDE (Web IDE) 中運作。您可以使用 {{site.data.keyword.Bluemix_notm}} Live Sync，針對以 Node.js 撰寫的應用程式進行除錯。  

{{site.data.keyword.Bluemix_notm}} Live Sync 包含兩個特性。
<!-- three -->

<!--
**Desktop Sync**  

You can synchronize any desktop directory tree with a cloud-based project workspace similar to the way Dropbox works. The Web IDE directly edits the same cloud-based workspace, so both stay in sync. Desktop Sync works for any kind of application. To use Desktop Sync, you need to download and install the BL command line interface.  
-->

**即時編輯**

您可以對在 {{site.data.keyword.Bluemix_notm}} 中執行的 Node.js 應用程式進行變更，並立刻在瀏覽器中加以測試。您在 Web IDE 中進行的任何變更，都會立即延伸到應用程式的檔案系統。  

**除錯**  

當 Node.js 應用程式處於「即時編輯」模式時，您可以使用 Shell 方式連入並進行除錯。您可以使用 Node Inspector 除錯器，以動態編輯程式碼、插入岔斷點、逐步執行程式碼、重新啟動運行環境等等。  

<!-- You can use Desktop Sync to keep your desktop workspace in sync with the cloud-based project workspace that you edit directly with the Web IDE. -->

您可以使用「即時編輯」，將雲端型專案工作區中的變更延伸到執行中的應用程式。 
<!-- You can use one or both of these features. And if you use Desktop Sync or -->
如果您使用「即時編輯」將應用程式置於「即時編輯」模式，就可以對執行中的應用程式進行除錯。下圖說明 Bluemix Live Sync 處理程序。    

圖 1. Bluemix Live Sync 處理程序
    

![Bluemix Live Sync 處理程序的影像](images/bluemix-live-sync.png)

如果您要開發在 Liberty 上執行的 Java 應用程式，可以使用 [Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools) 進行遠端除錯。


##即時編輯 {: #live-edit}

如果您要建置 Node.js 應用程式，則使用 Web IDE 來變更專案時，{{site.data.keyword.Bluemix_notm}} Live Sync 的「即時編輯」特性能夠快速更新在 {{site.data.keyword.Bluemix_notm}} 上執行的應用程式實例。「即時編輯」可讓您就像在桌面上開發一樣，而無需重新部署。

「即時編輯」支援僅適用於 Node.js 應用程式。

在 Eclipse Orion Web IDE (Web IDE) 的執行列中，按一下**即時編輯**。

![含有即時編輯之執行列的影像](images/bluemix-live-sync-light.png)

「即時編輯」可讓您快速預覽在 {{site.data.keyword.Bluemix_notm}} 上執行之 Node.js 應用程式的變更。當您開啟「即時編輯」來更新程式碼時，可以重新整理 Web 應用程式的瀏覽器視窗，就能看到在進行變更幾秒後所反映的變更。

<!--
For a tutorial on using the Live Edit feature of {{site.data.keyword.Bluemix_notm}} Live Sync, see the tutorial [Test and debug a Node.js app with Bluemix Live Sync![External link icon](../icons/launch-glyph.svg "External link icon")](https://hub.jazz.net/tutorials/livesync){:new_window}.
-->

當您變更 Web IDE 中的檔案時，會自動將其重新部署至在 {{site.data.keyword.Bluemix_notm}} 上執行的應用程式。如果您需要重新啟動 Node 應用程式，可以使用執行列中的**重新啟動**按鈕。

**附註：**為達到使用 {{site.data.keyword.Bluemix_notm}} Live Sync 的「即時編輯」特性時更一致的體驗，需要且將會新增 256MB 的額外記憶體。

##{{site.data.keyword.Bluemix_notm}} 即時除錯 {: #live-debug}

如果已針對 Node.js 應用程式啟用 {{site.data.keyword.Bluemix_notm}} Live Sync，則您可以存取 {{site.data.keyword.Bluemix_notm}} Live Sync 的「除錯」特性。

您可以使用除錯來動態編輯程式碼、插入岔斷點、逐步執行程式碼、重新啟動運行環境等等，這些全都可以在由 {{site.data.keyword.Bluemix_notm}} 為您的應用程式提供服務時執行。您可以靈活地以漸進方式開發應用程式，同時從龐大的 {{site.data.keyword.Bluemix_notm}} 服務清單進行選擇。

「{{site.data.keyword.Bluemix_notm}} 即時除錯」包含下列特性：

* 應用程式運行環境控制
* 使用 [node-inspector ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/node-inspector/node-inspector){:new_window} 進行除錯
* Shell 存取

###應用程式運行環境控制 {: #app-runtime}

使用應用程式運行環境控制，您可以用「除錯」來檢查應用程式在啟動時的狀態。當您對於在啟動時當機的應用程式進行疑難排解時，此功能很有用。

開發應用程式時，可以從下列動作選取：

* 執行應用程式的快速重新啟動
* 在任何應用程式程式碼執行之前先暫停應用程式

###除錯 {: #debug}

「除錯」包含下列功能：

**限制：**需要使用 Google Chrome。

* 在應用程式碼中設定岔斷點，以在特定行暫停執行。
* 編輯岔斷點條件，只在符合特定準則時暫停執行。
* 檢查區域變數及欄位的狀態。
* 立即檢視來自 `console.log()` 呼叫的除錯輸出。此動作的速度比監視 cf logs 還要快。
* 使用內建原始碼編輯器，對執行中的應用程式碼進行立即但暫時的變更。

###Shell {: #shell}

此工具可讓您對應用程式執行所在的容器進行 Shell 存取。您可以使用此終端機，在遠端執行診斷 Shell 指令來管理應用程式。

監視使用標準 Linux 指令（例如 **top**、**ps** 及 **kill**）之實例內的記憶體及 CPU 用量。

###配置應用程式，以啟用 {{site.data.keyword.Bluemix_notm}} 即時除錯 {: #configure_app_debug}

應用程式必須使用 IBM SDK for Node.js 建置套件。不支援自訂建置套件。

1. 容許建置套件偵測應用程式啟動指令。啟動指令必須由建置套件自動偵測，而不是設定在 `manifest.yml` 檔案中。  

    a. 確保 `package.json` 檔案包含一個包括應用程式啟動指令的啟動 Script。  
    b. 如果應用程式 `manifest.yml` 檔案包含指令，請將它設為 null。  

2. 設定環境變數。  

    a. 在 `manifest.yml` 檔案中，新增下列變數：
	
	```
	env:
      ENABLE_BLUEMIX_DEV_MODE: "true" 
	```

3. 增加記憶體。  

    a. 在應用程式 `manifest.yml` 檔案中，在為記憶體屬性指定的值加上 128M 以上。

安裝「{{site.data.keyword.Bluemix_notm}} 即時除錯」之後，您可以使用除錯工具。

推送應用程式，然後瀏覽至 `https://app-host.mybluemix.net/bluemix-debug/manage`，以存取 {{site.data.keyword.Bluemix_notm}} 除錯使用者介面。當系統提示您進行鑑別時，請輸入您的使用者 ID 及個人存取記號或 IBM ID 密碼。    

<!--
   **Note**: Your user ID for DevOps Services can be either an IBMid or a federated ID (corporate ID). If you use federated authentication, to log in to your Bluemix Live Sync command-line client, you must use a personal access token instead of a password. If you don't use federated authentication, your IBMid and password work with all clients. For more information about creating a personal access token, see [What's federated authentication and how does it affect me?![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/devops-services/2016/06/23/whats-federated-authentication-and-how-does-it-affect-me/){:new_window}
   -->

###還原應用程式配置並停用 Bluemix 即時除錯 {: #restore_live_debug}

1. 從應用程式 `manifest.yml` 檔案移除 ENABLE_BLUEMIX_DEV_MODE 環境變數。

2. 還原應用程式的原始啟動指令及記憶體值。

3. 推送應用程式。


## 相關鏈結
{: #general}

* [Eclipse Tools for Bluemix ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ng.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html){:new_window}
