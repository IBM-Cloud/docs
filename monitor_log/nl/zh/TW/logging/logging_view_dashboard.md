---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 從 Bluemix 儀表板分析 CF 應用程式日誌
{: #analyzing_logs_bmx_ui}

在 {{site.data.keyword.Bluemix}} 中，您可以透過每一個 Cloud Foundry 應用程式都有的**日誌**標籤，來檢視、過濾及分析日誌。使用 {{site.data.keyword.Bluemix}} 儀表板，以檢視應用程式的最新活動。
{:shortdesc}

「{{site.data.keyword.Bluemix_notm}} 公用」提供整合式記載服務。在 Cloud Foundry 中執行應用程式時，記載服務會擷取與應用程式互動之系統元件的日誌資料、關於應用程式的日誌資料，甚至是當您使用 stdout 和 stderr 時應用程式內所產生的日誌資料。

{{site.data.keyword.Bluemix_notm}} 應用程式的日誌會以固定格式顯示，與下列型樣類似：

<code><var class="keyword varname">Component</var>/<var class="keyword varname">instanceID</var>     <var class="keyword varname">message</var>     <var class="keyword varname">timestamp</var></code>
   
如需日誌格式的相關資訊，請參閱 [Cloud Foundry 應用程式日誌的日誌格式](logging_view_dashboard.html#log_format_cf)。

**附註：**在「{{site.data.keyword.Bluemix_notm}} 公用」中，日誌資料預設會儲存 7 天。您每天最多可以搜尋 1 GB 的資料。



##  進入 Bluemix 日誌標籤
{: #launch_logs_tab_bmx_ui}

若要查看 Cloud Foundry 應用程式的部署或運行環境日誌，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}}，然後在 {{site.data.keyword.Bluemix_notm}} **應用程式**儀表板上按一下應用程式名稱。 

    即會顯示「應用程式詳細資料」頁面。
    
2. 在導覽列中，按一下**日誌**。

    即會開啟「日誌」標籤。 
    
    在**日誌**標籤中，您可以檢視應用程式的最新日誌，或即時讀取日誌尾端的內容。此外，您還可以依元件（日誌類型）、依應用程式實例 ID 以及依錯誤來過濾日誌。



## Cloud Foundry 應用程式日誌的日誌格式
{: #log_format_cf}

每個日誌項目都包含下列欄位：

<dl>
<dt><strong>時間戳記</strong></dt>
<dd>
<p>日誌陳述文字的時間。時間戳記最多定義到毫秒。</p>
</dd>

<dt><strong>元件</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>產生日誌的元件。</p>
<p>每一個元件類型後面都接著一個斜線和一個數字，用來指出應用程式實例。0 是配置給第一個實例的數字，1 是配置給第二個實例的數字，依此類推。請注意，您可以過濾為只查看儀表板中的某個應用程式實例。</p>
<p>下列清單概述不同類型的元件：</p>

<dl>
<dt><strong>LGR</strong></dt>
<dd>日誌聚集器：LGR 元件提供 Cloud Foundry 日誌聚集器的相關資訊，它可轉遞 Cloud Foundry 中的日誌。</dd>

<dt><strong>RTR</strong></dt>
<dd>路由器：RTR 元件會將 HTTP 要求的相關資訊提供給應用程式。</dd>

<dt><strong>STG</strong></dt>
<dd>編譯打包：STG 元件提供應用程式如何編譯打包或重新編譯打包的相關資訊。</dd>

<dt><strong>APP</strong></dt>
<dd>應用程式：APP 元件提供來自應用程式的日誌。這是您的程式碼中會出現 stderr 和 stdout 的地方。</dd>

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

<dt><strong>訊息</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Message</var>&gt;</code></pre>
<p>元件所發出的訊息。訊息根據環境定義而不同。</p>
</dd>
</dl>

下圖顯示以 Droplet Execution Agent (DEA) 為基礎之 Cloud Foundry 架構中的不同元件（日誌類型）：
![DEA 架構中的日誌類型。](images/logging_F1.png "以 Droplet Execution Agent (DEA) 為基礎之 Cloud Foundry 架構中的元件（日誌類型）。")



