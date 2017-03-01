---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#在 {{site.data.keyword.Bluemix_short}} 上部署入門範本應用程式
{: #starterapps_deploy}

您可以將其中一個 {{site.data.keyword.streaminganalyticsshort}} 入門範本應用程式推送及部署至 {{site.data.keyword.Bluemix_short}} 雲端。
{:shortdesc}

開始之前，請準備好 {{site.data.keyword.Bluemix_short}} 來部署 {{site.data.keyword.streaminganalyticsshort}} 入門範本應用程式：

* [安裝 cf 指令行工具](https://github.com/cloudfoundry/cli/releases)。
* 在 {{site.data.keyword.Bluemix_short}} 中建立應用程式，並將 {{site.data.keyword.streaminganalyticsshort}} 服務新增至應用程式，然後重新編譯打包應用程式：
	* 若要部署 Event Detection 入門範本應用程式，請使用 {{site.data.keyword.sdk4node}} 運行環境來建立應用程式。
	* 若要部署 NYC Traffic 入門範本應用程式，請使用 Liberty for Java™ 運行環境來建立應用程式。

請記住您提供給應用程式的名稱，稍後您會需要用到它。

{{site.data.keyword.streaminganalyticsshort}} 提供兩個範例應用程式，來協助您開始使用服務。 

Event Detection 入門範本應用程式會透過即時串流分析氣候相關資料，並顯示分析的狀態和結果。此應用程式是以 {{site.data.keyword.sdk4node}} 撰寫。如需如何使用 Event Detection 入門範本應用程式的詳細資料，請參閱[透過即時資料串流偵測複式事件](https://www.ibm.com/developerworks/library/ba-bluemix-detect-complex-events-from-data-stream-trs/index.html)。

NYC Traffic 入門範本應用程式會讀取及分析公用網站中的交通資料。此應用程式是以 Liberty for Java™ 撰寫。如需如何使用 NYC Traffic 入門範本應用程式的詳細資料，請參閱 [{{site.data.keyword.streaminganalyticsfull}} 入門範本應用程式](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-starter-application/)。 

若要將入門範本應用程式下載並部署至 {{site.data.keyword.Bluemix_short}}，請執行下列動作：

1. 下載 [Event Detection](https://hub.jazz.net/project/streamscloud/EventDetection/overview) 或 [NYC Traffic](https://hub.jazz.net/project/streamscloud/NYCTraffic/overview) 入門範本應用程式。
2. 在指令行上，移至專案目錄。
  <pre><code>cd myapp</code></pre>
 
3. 在 {{site.data.keyword.Bluemix_short}} 中，重新命名專案目錄，使其符合您提供給應用程式的名稱。
4. 連接至 {{site.data.keyword.Bluemix_short}}：
  <pre><code>cf api https://api.DomainName</code></pre>
   
5. 登入 {{site.data.keyword.Bluemix_short}}，並在系統提示時設定目標組織：
   <pre><code>cf login</code></pre>
    
6. 部署應用程式：
  <pre><code>cf push myapp</code></pre>
   
7. 移至您的應用程式概觀頁面（可從 {{site.data.keyword.Bluemix_short}} 儀表板存取），以驗證您的應用程式已順利啟動。
8. 啟動應用程式以在瀏覽器中看到它。您可以在應用程式概觀頁面上找到應用程式的 URL（或「路徑」）。

現在，您的應用程式正在執行中，您可以移至服務儀表板來查看 {{site.data.keyword.streaminganalyticsshort}} 實例的狀態，以及取得疑難排解的資訊。若要存取服務儀表板，請移至 {{site.data.keyword.Bluemix_short}} 儀表板，然後按一下應用程式概觀頁面上的 {{site.data.keyword.streaminganalyticsshort}} 磚。
