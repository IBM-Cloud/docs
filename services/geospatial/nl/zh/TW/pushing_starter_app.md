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

#將入門範本應用程式推送至 {{site.data.keyword.Bluemix_short}}
{: #pushing_starter_app}


 
部署入門範本應用程式，並快速瞭解如何使用 {{site.data.keyword.geospatialshort_Geospatial}} 服務：
{:shortdesc}

1. 如果尚未進行，請[安裝 cf 指令行工具](docs/starters/install_cli.html)。
2. [取得 {{site.data.keyword.geospatialshort_Geospatial}} 入門範本應用程式的程式碼](https://hub.jazz.net/project/streamscloud/geo-starter/overview)。 
3. 重新命名包含應用程式檔案的目錄，以符合您在 {{site.data.keyword.Bluemix_short}} 中提供給應用程式的名稱。例如，如果應用程式命名為 myapp，請將目錄重新命名為 myapp。
4. 在指令行上，切換至已重新命名的目錄。
<pre><code>cd myapp</code></pre>
5. 連接至 {{site.data.keyword.Bluemix_short}}：
<pre><code>cf api https://api.DomainName</code></pre>
6. 登入 {{site.data.keyword.Bluemix_short}}，並在提示時設定目標組織，然後部署應用程式。
<pre><code>
cf login
cf push myapp
</code></pre>

##下一步

* 移至您的應用程式概觀頁面（可從 {{site.data.keyword.Bluemix_short}} 儀表板存取），以驗證您的應用程式已順利啟動。

* 啟動應用程式以在瀏覽器中看到它。您可以在應用程式概觀頁面上找到應用程式的 URL（或「路徑」）。範例應用程式的網頁會顯示應用程式碼中
REST API 呼叫狀態的相關資訊，以及 {{site.data.keyword.geospatialshort_Geospatial}} 偵測到的事件。
