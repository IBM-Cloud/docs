---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 使用 Cloud Foundry 監視及記載
{: #monitoringandlogging}


透過監視您的應用程式以及檢閱日誌，即可追蹤應用程式執行及資料流程，更深入地瞭解部署。此外，您還可以減少尋找及修復任何問題所需的時間及工作量。
{:shortdesc}

{{site.data.keyword.Bluemix}} 應用程式可以是廣泛分佈且多重實例的應用程式，而且應用程式的執行及其資料可以在多個服務之間共用。在此複雜環境中，對於管理應用程式而言，監視應用程式以及檢閱日誌十分重要。

## 監視及記載 Cloud Foundry 應用程式
{: #monitoring_logging_bluemix_apps}

{{site.data.keyword.Bluemix_notm}} 具有內建記載機制，可產生執行中應用程式的日誌檔。在日誌中，您可以檢視針對應用程式所產生的錯誤、警告及參考訊息。此外，您也可以配置應用程式將日誌訊息寫入日誌檔中。如需日誌格式及日誌檢視方式的相關資訊，請參閱 [Cloud Foundry 上執行之應用程式的記載](#logging_for_bluemix_apps)。

監視應用程式可讓您查看及控制應用程式部署。運用監視，您可以完成下列作業：

* 收集並監視應用程式實例的效能資訊，以及檢查它們是否正常運作。
* 瞭解應用程式作業（例如，偵測潛在瓶頸或需要升級的時機）。
* 估計資源用量與費用。

為了讓您的部署在 {{site.data.keyword.Bluemix_notm}} 平台上能穩定運作，您會想要迅速地偵測問題，並且有效率地判定原因。若要達成此目標，請在設計應用程式時隨時謹記疑難排解，並在將應用程式部署至 {{site.data.keyword.Bluemix_notm}} 時使用進行監視及記載的服務或工具。

### 監視 Cloud Foundry 上執行的應用程式
{: #monitoring_bluemix_apps}

當您使用 Cloud Foundry 基礎架構在 {{site.data.keyword.Bluemix_notm}} 上執行應用程式時，會想要保有最新效能資訊（例如性能狀態、資源用量及資料流量度量值）。運用此效能資訊，您接著可以進行決策，或相應地採取動作。


若要監視 {{site.data.keyword.Bluemix_notm}} 應用程式，請使用下列其中一種方法：

* {{site.data.keyword.Bluemix_notm}} 服務。Monitoring and Analytics 提供一種服務，可用來監視應用程式效能。此外，此服務也會提供分析特性（例如 Log Analysis）。如需相關資訊，請參閱 [Monitoring and Analytics](/docs/services/monana/index.html#gettingstartedtemplate)。
* 協力廠商選項。例如，[New Relic ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://newrelic.com/){:new_window}。

### Cloud Foundry 上執行之應用程式的記載功能
{: #logging_for_bluemix_apps}

當您使用 Cloud Foundry 基礎架構在 {{site.data.keyword.Bluemix_notm}} 上執行應用程式時，會自動建立日誌檔。若從部署到運行環境的任何階段中有發現錯誤，您可以檢查日誌以尋找有助於解決問題的線索。


<!-- 2016.1.27: original shortdes: Log files are automatically created when you are using the Cloud Foundry infrastructure to run your apps on {{site.data.keyword.Bluemix_notm}}. You can view logs from the {{site.data.keyword.Bluemix_notm}} Dashboard, the cf command line interface, or external hosts. You can also filter the logs to see the parts that you are interested in. -->



### 日誌格式及保留
{: #log_format}

在「{{site.data.keyword.Bluemix_notm}} 公用」的 Cloud Foundry 應用程式中，日誌資料依預設會儲存 7 天。您每天最多可以搜尋 1 GB 的資料。

{{site.data.keyword.Bluemix_notm}} 應用程式的日誌會以固定格式顯示，與下列型樣類似：

```
         1         2         3         4         5
12345678901234567890123456789012345678901234567890
--------------------------------------------------
yyyy-MM-ddTHH:mm:ss:SS-0500 [App/0]      OUT <message>
```
{:screen}

每個日誌項目都包含四個欄位。請參閱下列清單，以取得每一個欄位的簡要說明：

<dl>
<dt><strong>時間戳記</strong></dt>
<dd>
<pre class="pre screen"><code>yyyy-MM-ddTHH:mm:ss:SS-0500</code></pre>
<p>直欄：1 - 27</p>
<p>日誌陳述文字的時間。時間戳記最多定義到毫秒。</p>
</dd>

<dt><strong>元件</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>直欄：29 - 40</p>
<p>產生日誌的元件。</p>
<p>每一個元件類型後面都接著一個斜線和一個數字，用來指出應用程式實例。0 是配置給第一個實例的數字，1 是配置給第二個實例的數字，依此類推。</p>
<p>下列清單概述不同類型的元件：</p>

<dl>
<dt><strong>LGR</strong></dt>
<dd>日誌聚集器：LGR 元件提供記載服務的相關資訊。</dd>

<dt><strong>RTR</strong></dt>
<dd>路由器：RTR 元件會將 HTTP 要求的相關資訊提供給應用程式。</dd>

<dt><strong>STG</strong></dt>
<dd>編譯打包：STG 元件提供應用程式如何編譯打包或重新編譯打包的相關資訊。</dd>

<dt><strong>APP</strong></dt>
<dd>應用程式：APP 元件提供應用程式的相關資訊。</dd>

<dt><strong>API</strong></dt>
<dd>Cloud Foundry API：API 元件提供使用者要求變更應用程式狀態後，所產生之內部動作的相關資訊。</dd>

<dt><strong>DEA</strong></dt>
<dd>Droplet Execution Agent：DEA 元件提供應用程式開始、停止或當機的相關資訊。
<p>只有在應用程式部署在以 DEA 為基礎的 Cloud Foundry 架構中時，此元件才可供使用。</p></dd>

<dt><strong>CELL</strong></dt>
<dd>Diego Cell：CELL 元件提供應用程式開始、停止或當機的相關資訊。
<p>只有在應用程式部署在以 Diego 為基礎的 Cloud Foundry 架構中時，此元件才可供使用。</p></dd>

<dt><strong>SSH</strong></dt>
<dd>SSH：SSH 元件會在使用者每次使用 **cf ssh** 指令來存取應用程式時，提供資訊。
<p>只有在應用程式部署在以 Diego 為基礎的 Cloud Foundry 架構中時，此元件才可供使用。</p></dd>

</dl>
</dd>

<dt><strong>串流</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>直欄：42 - 44</p>
<p>將日誌訊息寫入其中的串流。<samp class="ph codeph">OUT</samp> 指的是 <samp class="ph codeph">stdout</samp> 串流，而 <samp class="ph codeph">ERR</samp> 指的是 <samp class="ph codeph">stderr</samp> 串流。</p>
</dd>

<dt><strong>訊息</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Message</var>&gt;</code></pre>
<p>直欄：46 - 行尾</p>
<p>元件所發出的訊息。訊息會視環境定義而改變。</p>
</dd>
</dl>

下圖顯示以 Droplet Execution Agent (DEA) 為基礎之 Cloud Foundry 架構中的不同元件（日誌類型）：![DEA 架構中的日誌類型。](images/logging_F1.png "以 Droplet Execution Agent (DEA) 為基礎之 Cloud Foundry 架構中的元件（日誌類型）。")


## 檢視日誌
{: #viewing_logs}

您可以在以下四個位置中檢視 Cloud Foundry 應用程式的日誌：

  * {{site.data.keyword.Bluemix_notm}} 儀表板
  * Kibana 儀表板
  * 指令行介面
  * 外部日誌主機

### 從 {{site.data.keyword.Bluemix_notm}} 儀表板檢視日誌
{: #viewing_logs_UI}

若要查看部署或運行環境日誌，請完成下列步驟：
1. 登入 {{site.data.keyword.Bluemix_notm}}，然後按一下應用程式的磚。即會顯示「應用程式詳細資料」頁面。
2. 在導覽列中，按一下**日誌**。

在**日誌**主控台中，您可以檢視應用程式的最新日誌，或即時讀取日誌尾端的內容。此外，您還可以依日誌類型及通道來過濾日誌。

**附註：**在應用程式損毀與部署之間不會持續保存日誌。


### 從 Kibana 儀表板檢視日誌
{: #viewing_logs_Kibana}

建立自訂儀表板，以透過簡單或創意方式顯示在空間中執行之應用程式的日誌。

1. 開啟 [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName})，以登入 Kibana 使用者介面。
2. 選取 **Kibana 3** 標籤。
3. 如果沒有看到任何日誌，請調整標頭中的時間選取器。
4. 將儀表板儲存為新的儀表板。
  1. 在工具列中，按一下**儲存**圖示。
  2. 輸入儀表板的名稱。
  3. 按一下名稱欄位旁邊的**儲存**圖示。

如需自訂 Kibana 儀表板的相關資訊，請參閱[此部落格文章](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/)或 [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) 文件。


### 從指令行介面檢視日誌
{: #viewing_logs_cli}

從下列選項進行選擇，以從指令行介面檢視日誌：

<ul>
<li>部署應用程式時讀取日誌尾端的內容。
<p>當您將應用程式部署至 {{site.data.keyword.Bluemix_notm}} 時，請使用 **cf logs** 指令來顯示來自應用程式以及來自與其互動之系統元件的日誌。您可以在 cf 指令行介面中鍵入下列指令。如需 cf 日誌的相關資訊，請參閱 <a href="http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html" target=" _blank">Log Types and Their Messages in Cloud Foundry <img src="../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></p>
<dl>
<dt><strong>cf logs <var class="keyword varname">appname</var> --recent</strong></dt>
<dd>從最新到最舊顯示日誌。</dd>

<dt><strong>cf logs <var class="keyword varname">appname</var></strong></dt>
<dd>顯示您執行此指令時所產生的日誌。</dd>
</dl>
<div class="note tip"><span class="tiptitle">提示：</span>當您在某個指令行視窗中執行 <span class="keyword cmdname">cf push</span> 或 <span class="keyword cmdname">cf start</span> 指令時，即可在另一個指令行視窗中輸入 <samp class="ph codeph">cf logs appname --recent</samp>，以即時查看日誌。</div>
</li>

<li>在部署應用程式之後檢視日誌。

<p>如果啟用應用程式記載，則應用程式在執行時發現問題時，您可以檢視下列應用程式日誌。應用程式日誌可以協助您判斷錯誤原因。</p>

<dl><dt><strong>buildpack.log</strong></dt>
<dd>
<p>此日誌檔會記錄精細的參考資訊事件，以進行除錯。您可以使用此日誌，對建置套件執行問題進行疑難排解。</p>
<p>若要在 <span class="ph filepath">buildpack.log</span> 檔案中產生資料，您必須使用下列指令來啟用建置套件追蹤：<pre class="pre">cf set-env <var class="keyword varname">appname</var> JBP_LOG_LEVEL DEBUG</pre></p>
<p>若要檢視此日誌，請輸入下列指令：<pre class="pre">cf files <var class="keyword varname">appname</var> app/.buildpack-diagnostics/buildpack.log</pre>
</p>
</dd>
<dt><strong>staging_task.log</strong></dt>
<dd><p>此日誌檔會記錄編譯打包作業的主要步驟之後的訊息。您可以使用此日誌，對編譯打包問題進行疑難排解。</p>
<p>若要檢視此日誌，請輸入下列指令：<pre class="pre">cf files <var class="keyword varname">appname</var> logs/staging_task.log</pre>
</p>
</dd>
</dl>
</li></ul>


**附註：**如需如何啟用應用程式記載的相關資訊，請參閱[針對運行環境錯誤進行除錯](/docs/debug/index.html#debugging-runtime-errors)。

### 從外部主機檢視日誌
{: #viewing_logs_external}


產生日誌時，在短暫延遲之後，您就可以檢視外部日誌主機中的訊息，而這些訊息與您從 {{site.data.keyword.Bluemix_notm}} 使用者介面或 cf 指令行介面檢視的訊息類似。如果您的應用程式有多個實例，則會產生日誌，而且您可以查看應用程式的所有日誌。此外，在應用程式損毀與部署之間會持續保存日誌。

**附註：**您在指令行介面中檢視的日誌不是 syslog 格式，而且可能未完全符合外部日誌主機中所顯示的訊息。




## 從指令行介面過濾日誌
{: #filtering_logs}

若要檢視感興趣的日誌，或排除不想要檢視的內容，您可以在 cf 指令行介面中搭配使用 **cf logs** 指令與過濾選項，例如 **cut** 及 **grep**。

* 若要檢視某個部分，而非完整詳細日誌，請使用 **cut** 選項。例如，若要顯示元件及訊息資訊，請使用下列指令：
```
cf logs appname --recent | cut -c 29-40,46-
```

如需 **grep** 選項的相關資訊，請鍵入 cut --help。
* 若要顯示包含特定關鍵字的日誌項目，請使用 **grep** 選項。例如，若要顯示包含關鍵字 `[APP` 的日誌項目，您可以使用下列指令：

```
cf logs appname --recent | grep '\[App'
```
如需 **grep** 選項的相關資訊，請鍵入 `grep --help`。



## 配置外部日誌主機
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} 在記憶體中保留了有限的日誌資訊量。在記載資訊時，舊資訊會取代為較新的資訊。若要保留所有日誌資訊，您可以將日誌儲存到外部日誌主機（例如協力廠商日誌管理服務或其他主機）。

若要將日誌從您的應用程式及系統串流到外部日誌主機，請完成下列步驟：

  1. 決定記載端點。

	 您可以將日誌傳送給協力廠商日誌聚集器（例如 Papertrail、Splunk 或 Sumologic）。您也可以將日誌傳送給 syslog 主機、使用 TLS（傳輸層安全）加密的 syslog 主機，或 HTTPS POST 端點。不同日誌主機取得記載端點的方法會不同。

  2. 建立使用者提供的服務實例。

	 使用 `cf create-user-provided-service` 指令（或 `cups`，這是此指令的簡短版本），以建立使用者提供的服務實例：
	 ```
	 cf create-user-provided-service <service_name> -l <logging_endpoint>
	 ```
	 &lt;service_name&gt;

	 使用者提供的服務實例的名稱。

	 &lt;logging_endpoint&gt;

	 {{site.data.keyword.Bluemix_notm}} 將日誌傳送至其中的記載端點。請參閱下表，以將 *logging_endpoint* 取代為您的值：

	 <table>
	 <caption>表 1. 記載端點值</caption>
     <thead>
     <tr>
     <th>記載端點</th>
     <th>指令</th>
	 <th>附註</th>
     </tr>
     </thead>
     <tbody>
     <tr>
     <td>syslog 主機</td>
     <td>`cf cups my-logs -l syslog://HOST:PORT`</td>
	 <td>例如，若要啟用記載至 Papertrail 的功能，請鍵入 `cf cups my-logs -l syslog://<papertrail-url>`。請將 `<papertrail-url>` 取代為來自 Papertrail 的記載端點的 URL。</td>
     </tr>
	 <tr>
     <td>syslog-tls 主機</td>
     <td>`cf cups my-logs -l syslog-tls://HOST:PORT`</td>
	 <td>憑證必須受憑證管理中心信任。請不要使用自簽憑證。</td>
     </tr>
	 <tr>
     <td>HTTPS POST</td>
     <td>`cf cups my-logs -l https://HOST:PORT`</td>
	 <td>此端點必須位在公用網際網路上，並且可供 {{site.data.keyword.Bluemix_notm}} 存取</td>
     </tr>
     </tbody>
     </table>
  3. 將服務實例連結至您的應用程式。

	 使用下列指令，將服務實例連結至您的應用程式：

	 ```
	 cf bind-service <appname> <service_name>
	 ```
	 &lt;appname&gt;
	 
	 應用程式的名稱。

	 &lt;service_name&gt;

	 使用者提供的服務實例的名稱。

  4. 重新編譯打包應用程式。
     鍵入 `cf restage appname`，讓變更生效。


### 範例：將 Cloud Foundry 應用程式日誌串流至 Splunk
{: #splunk}

在此範例中，名為 Jane 的開發人員會使用 IBM Virtual Servers 測試版及 Ubuntu 映像檔來建立虛擬伺服器。Jane 嘗試將 Cloud Foundry 應用程式日誌從 {{site.data.keyword.Bluemix_notm}} 串流至 Splunk。

  1. Jane 是從設定 Splunk 開始。

     a. Jane 從 [Download Splunk Light ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.splunk.com/en_us/download/splunk-light.html){:new_window} 網站下載 Splunk Light，然後使用下列指令進行安裝。軟體會安裝在 */opt/splunk* 上。

	    ```
        dpkg -i  ~/splunklight-6.3.0-aa7d4b1ccb80-linux-2.6-amd64.deb
        ```

     b. Jane 會安裝及修補 RFC5424 syslog 技術附加程式，以與 {{site.data.keyword.Bluemix_notm}} 整合。如需附加程式安裝指示的相關資訊，請參閱 [Cloud Foundry 準則 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.cloudfoundry.org/devguide/services/integrate-splunk.html){:new_window}。

	    Jane 使用下列指令來安裝附加程式：

	    ```
        cd /opt/splunk/etc/apps
        tar xvfz ~/rfc5424-syslog_11.tgz
        ```

        然後，Jane 會將 */opt/splunk/etc/apps/rfc5424/default/transforms.conf* 取代為包含下列文字的新 *transforms.conf* 檔案，以修補附加程式：

	    ```
        [rfc5424_host]
        DEST_KEY = MetaData:Host
        REGEX = <\d+>\d{1}\s{1}\S+\s{1}(\S+)
        FORMAT = host::$1

        [rfc5424_header]
        REGEX = <(\d+)>\d{1}\s{1}\S+\s{1}\S+\s{1}(\S+)\s{1}(\S+)\s{1}(\S+)
        FORMAT = prival::$1 appname::$2 procid::$3 msgid::$4
        MV_ADD = true
        ```
        {:screen}

     c. 設定 Splunk 之後，Jane 必須開啟 Ubuntu 機器上的一些埠來接受送入的 syslog 排除（埠 5140）及 Splunk Web 使用者介面（埠 8000），因為 {{site.data.keyword.Bluemix_notm}} 虛擬伺服器依預設會設定防火牆。

	    **附註：**在這裡完成 iptable 確認以供 Jane 進行評估，而且是暫時的。若要在正式作業環境中配置 Bluemix 虛擬伺服器中的防火牆設定，請參閱 [Network Security Groups ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://new-console.ng.bluemix.net/docs/services/networksecuritygroups/index.html){:new_window} 文件以取得詳細資料。

	   ```
	   iptables -A INPUT -p tcp --dport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --sport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
       iptables -A INPUT -p tcp --sport 8000 -j ACCEPT
	   ```
	   {:screen}

	   然後，Jane 會使用下列指令來執行 Splunk：

       ```
	   /opt/splunk/bin/splunk start --accept-license
       ```

  2. Jane 會配置 Splunk 設定，以接受來自 {{site.data.keyword.Bluemix_notm}} 的 syslog 排除。她必須為 syslog 排除建立一個資料輸入。

     a. 從 Splunk Web 介面中，Jane 按一下**資料 > 資料輸入**。即會顯示 Splunk 所支援的輸入類型清單。

     b. 她選取 **TCP**，因為 syslog 排除使用 TCP 通訊協定。

     c. 在 **TCP** 窗格中，她在**埠**欄位中輸入 **5140**，並將其餘欄位空白，然後按**下一步**。

     d. 從**來源類型**清單中，她選取**未分類 > rfc5424_syslog**。

     e. 對於**方法**類型，她選取 **IP**。

     f. 在**索引**欄位中，Jane 按一下**建立新索引**。她將新索引命名為 "bluemix"，然後按一下**儲存**。

     g. 最後，在**檢閱**視窗中，Jane 確認設定正確，然後按一下**提交**來啟用此資料輸入。

  3. 在 {{site.data.keyword.Bluemix_notm}} 中，Jane 建立 syslog 排除服務，並將服務連結至應用程式。

     a. Jane 從 cf cli 使用下列指令來建立 syslog 排除服務：

     ```
     cf cups splunk -l syslog://dummyhost:5140
     ```

     **附註：***dummyhost* 不是實際名稱。它用來隱藏實際主機名稱。

     b. Jane 會將 syslog 排除服務連結至她空間中的應用程式，然後重新編譯打包應用程式。

	 ```
     cf bind-service myapp splunk
     cf restage myapp
     ```


Jane 試用她的應用程式，然後在 Splunk Web 介面中鍵入下列查詢字串：

```
source="tcp:5140" index="bluemix" sourcetype="rfc5424_syslog"
```

Jane 在她的 Splunk Web 介面中看到日誌串流。雖然 Jane 所安裝的 Splunk 是 Splunk Light，但一天還是可以保留 500MB 日誌。

## {{site.data.keyword.Bluemix_dedicated_notm}} 及 {{site.data.keyword.Bluemix_local_notm}} 中 Cloud Foundry 應用程式的記載功能
{: #hybrid_apps_logs_ov}


在 {{site.data.keyword.Bluemix_dedicated_notm}} 及 {{site.data.keyword.Bluemix_local_notm}} 中，Cloud Foundry 應用程式有內建的記載。您可以在 {{site.data.keyword.Bluemix_notm}} 主控台上檢閱從您的應用程式收集到的資料。
{:shortdesc}

Cloud Foundry 應用程式會使用 Cloud Foundry 日誌聚集器，從應用程式之外監視並轉遞日誌。您不需要在應用程式內安裝代理程式。

### 硬體需求


| **需求** |    **1 個節點**     | **3 個節點（針對高可用性）** |
|-----------------|-------------------|-------------------|
| vCPU | 19 | 57 |
| 記憶體 | 80 GB | 240 GB |
| 本端儲存空間 | 2.98 TB | 8.94 TB |
{: caption="表 2. {{site.data.keyword.Bluemix_local_notm}} 的記載硬體需求" caption-side="top"}

### 設定

在 {{site.data.keyword.Bluemix_dedicated_notm}} 及 {{site.data.keyword.Bluemix_local_notm}} 中，對於所有應用程式，日誌依預設為作用中。若要檢視讀取標準日誌的相關資訊，請參閱 [Cloud Foundry 上執行之應用程式的記載](#logging_for_bluemix_apps)。此外，也可在 {{site.data.keyword.Bluemix_dedicated_notm}} 及 {{site.data.keyword.Bluemix_local_notm}} 環境中啟用進階記載。

* 若要確認在 {{site.data.keyword.Bluemix_dedicated_notm}} 及 {{site.data.keyword.Bluemix_local_notm}} 環境中啟用進階記載，請遵循[檢視日誌](#hybrid_apps_logs_dash)中的步驟。如果沒有**進階視圖**按鈕，則表示未啟用此特性。

* 若要將進階記載新增至您的環境，請遵循 [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) 或 [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) 文件中的步驟。

### 日誌保留

在 {{site.data.keyword.Bluemix_dedicated_notm}} 及 {{site.data.keyword.Bluemix_local_notm}} 的 Cloud Foundry 應用程式中，日誌資料依預設會儲存 30 天。

## 檢視 {{site.data.keyword.Bluemix_dedicated_notm}} 及 {{site.data.keyword.Bluemix_local_notm}} 中 Cloud Foundry 應用程式的日誌
{: #hybrid_apps_logs_dash}

您可以檢閱正在 {{site.data.keyword.Bluemix_dedicated_notm}} 及 {{site.data.keyword.Bluemix_local_notm}} 上執行之應用程式的日誌。
{:shortdesc}

若要檢視您的應用程式日誌，請遵循下列步驟。
1. 選取執行中應用程式。
2. 按一下**日誌**。在**日誌**視圖中，您可以檢視來自執行中應用程式的日誌。
4. 按一下**進階視圖**按鈕。**進階視圖**會使用 Kibana 顯示更詳細的日誌視圖。Kibana 是一種視覺化工具，其會使用日誌及時間戳記資料來建立自訂視覺化。如需使用進階視圖的相關資訊，請參閱 [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) 文件。

接下來，您可以自訂 Kibana 儀表板。如需相關資訊，請參閱[自訂 Kibana 儀表板中的日誌顯示方式](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_dash_logs_custom)。
