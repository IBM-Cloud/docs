---

著作權：

  年份：2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 開始使用 Cloudant
{: #getting-started-with-cloudant}
前次更新：2016 年 8 月 12 日
{: .last-updated}

{{site.data.keyword.cloudant}} 是以 JSON 儲存資料的文件資料庫即服務 (DBaaS)。
它在建置時謹記可擴充性、高可用性和延續性。
並且具有各種檢索選項，包括 map-reduce、Cloudant Query、全文檢索及地理空間。
抄寫功能讓它能輕鬆保持資料庫叢集、桌上型電腦和行動裝置之間的資料同步。
{:shortdesc}

您可以從 Bluemix 儀表板的服務啟動頁面啟動 {{site.data.keyword.cloudant}} 主控台。

若要使用該服務，請遵循下列步驟：
<ol>
<li>使用 Bluemix 儀表板或 CloudFoundry 指令行介面，來建立服務實例。
<p>若要使用儀表板來建立實例，請遵循下列步驟：
<ol>
<li>登入 Bluemix。</li>
<li>在儀表板上，按一下「資料及分析」畫面上的「<code>使用資料</code>」鏈結。</li>
<li>按一下「<code>新建服務</code>」按鈕。</li>
<li>在服務清單中，按一下 {{site.data.keyword.cloudant}} 按鈕。</li>
<li>在 {{site.data.keyword.cloudant}} 資訊頁面上，按一下「<code>選擇 {{site.data.keyword.cloudant}}</code>」按鈕。</li>
<li>在 {{site.data.keyword.cloudant}} 型錄頁面上，填寫您所需服務的詳細資料。
當您準備好繼續時，請按一下「<code>建立</code>」按鈕。</li>
<li>建立 Cloudant 實例之後，系統會向您呈現該實例的儀表板。
按一下「<code>服務認證</code>」鏈結，來查看可存取您實例所需的所有詳細資料。</li>
</ol>
</p>
<p>若要使用 CloudFoundry 指令行介面來建立實例，請遵循下列步驟：
<ol>
<li>在您的系統上安裝 CloudFoundry <code>cf</code> 工具。
在 <a href="https://console.ng.bluemix.net/docs/cli/index.html">Bluemix CLI 及開發工具手冊</a>中可以找到如何執行該動作的指示。</li>
<li>使用下列指令，建立新的服務實例：<br/>
<pre><code>cf create-service</code></pre></li>
<li>系統會向您呈現一個可用的服務清單。
請選擇其中一個，然後輸入服務的唯一實例名稱和方案。建議針對實例使用隨機名稱，但您可以將它變更為您要的其他名稱。</li>
<li>建立服務之後，即可取得您已建立的所有服務的清單：<br/>
<pre><code>cf services</code></pre></li>
<li>在應用程式中使用服務之前，您必須將服務連結至應用程式。
請使用下列指令來執行這項動作：<br/>
<pre><code>cf bind-service</code></pre>
從產生的清單中，選取一個應用程式以及一個服務。<code>cf</code> 指令會在連結動作成功時通知您。</li>
</ol>
</p>
</li>
<li><p>建立服務實例之後，將會顯示類似如下的 JSON 資料，並且可在 Bluemix 儀表板中進行檢視：<br/>
<pre><code>{
"cloudantNoSQLDB": {"name": "Cloudant-3s",
    "label": "cloudantNoSQLDB",
    "plan": "shared",
    "credentials": {
      "username": "someusername",
      "password": "secret",
      "host": "myhost-bluemix.cloudant.com",
      "port": 443,
      "url": "https://someusername:secret@myhost-bluemix.cloudant.com"
    }
    }
}</code></pre></p>
{: screen}
<p>資料也會新增至服務已連結的任何 Bluemix 應用程式的 <code>VCAP_SERVICES</code> 環境變數。</p>
<p>服務認證儲存在包含下列欄位的 JSON 物件中：
<ul>
<li><code>key</code>：服務的名稱 (cloudantNoSQLDB)</li>
<li><code>name</code>：服務實例的使用者提供名稱</li>
<li><code>host</code>：伺服器的主機名稱</li>
<li><code>port</code>：服務執行所在的埠號，通常為 443</li>
<li><code>username</code>：鑑別用的使用者名稱</li>
<li><code>password</code>：鑑別用的密碼</li>
<li><code>url</code>：服務實例的 URL</li>
</ul></li>
<li><p>在您的 Bluemix 應用程式中，從 <code>VCAP_SERVICES</code> 環境變數讀取認證。</p>
<p>在 Bluemix 之外執行的應用程式中，或是在 Bluemix 內不同地理地區執行的應用程式中，您可以從 Bluemix 儀表板擷取認證，並將它們新增到應用程式的配置。</p>
</li>
<li>若要存取資料庫，基本機制是透過 HTTPS 將要求傳送到給定的主機及埠，並以使用者名稱及密碼進行鑑別。
您的要求可以使用各種應用程式語言及平台進行傳送，包括：
<ul>
<li><a href="https://github.com/cloudant/sync-android">Android</a></li>
<li><a href="https://github.com/cloudant/CDTDatastore">Apple iOS</a></li>
<li><a href="https://github.com/cloudant/java-cloudant">Java</a></li>
<li><a href="https://github.com/cloudant/objective-cloudant">Objective C 及 Swift</a></li>
<li><a href="https://github.com/cloudant/python-cloudant">Python</a></li>
</ul>
以及許多其他項目。
如需相關資訊，請參閱 <a href="https://cloudant.com/for-developers/">Cloudant Developer 首頁</a>及<a href="http://docs.cloudant.com/libraries.html">用戶端程式庫</a>清單。
</li>
<li>應用程式備妥時，即可將它部署至 Bluemix 環境來進行驗證。
若要部署應用程式，請使用下列指令：<br/>
<pre><code>cf push</code></pre></li>
<li>若要從應用程式中取消服務實例的連結，請使用下列指令：<br/>
<pre><code>cf unbind-service</code></pre></li>
<li>若要刪除服務實例，請使用下列指令：<br/>
<pre><code>cf delete-service</code></pre></li>
</ol>

向資料庫進行鑑別及提出要求的相關資訊，提供於 [API 參考資料](https://docs.cloudant.com/api.html)。

# 相關鏈結
{: #rellinks}

## 指導教學及範例
{: #samples}

* [Cloudant 用戶端程式庫](https://docs.cloudant.com/libraries.html)
* [在 Bluemix 上搭配使用 Cloudant 與 Liberty](https://developer.ibm.com/bluemix/2014/07/08/cloudant_on_bluemix/)
* [Cloudant 手冊](https://docs.cloudant.com/guides.html)

## API 參考資料
{: #api}

* [Cloudant API 參考資料](https://docs.cloudant.com/api.html)

## 相關鏈結
{: #general}

* [Cloudant 網站及儀表板](https://cloudant.com/)
* [Cloudant 部落格](https://cloudant.com/blog)
