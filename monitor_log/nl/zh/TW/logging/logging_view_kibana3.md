---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 在 Kibana 中分析日誌
{: #analyzing_logs_Kibana3}

在 {{site.data.keyword.Bluemix}} 中，您可以使用 Kibana（一種開放程式碼分析與視覺化平台）在各種圖形（例如圖表和表格）中監視、搜尋、分析及視覺化您的資料。使用 Kibana 來執行進階分析作業。
{:shortdesc}

您可以使用下列任何方式來啟動 Kibana：

* 從 Cloud Foundary 應用程式儀表板

    在 Kibana 中，您可以在特定 CF 應用程式的環境定義下，啟動至該特定應用程式的日誌。
    
    用來過濾儀表板顯示資料的查詢，會擷取 Cloud Foundry 應用程式的日誌項目。Kibana 儀表板預設顯示的日誌資訊，全都與單一 Cloud Foundry 應用程式及其所有實例相關。如需相關資訊，請參閱[從 {{site.data.keyword.Bluemix}} 儀表板進入 Kibana 儀表板](logging_view_kibana3.html#launch_Kibana_from_bluemix)。

* 從直接瀏覽器鏈結

    您可能會想要啟動至自訂 Kibana 儀表板，它會聚集來自所提供 {{site.data.keyword.Bluemix}} 空間內之服務的資料。
    
    用來過濾儀表板顯示資料的查詢，會擷取 {{site.data.keyword.Bluemix}} 組織中某個空間的日誌項目。Kibana 儀表板顯示的日誌資訊，包括部署在您登入之 {{site.data.keyword.Bluemix}} 組織的空間內的所有資源記錄。如需相關資訊，請參閱[從 Web 瀏覽器進入 Kibana 儀表板](logging_view_kibana3.html#launch_Kibana_from_browser)。
    
    您也可以變更或移除起始查詢，然後新增更多查詢。如需相關資訊，請參閱[在 Kibana 中以查詢來過濾 Cloud Foundry 應用程式日誌](kibana3/logging_kibana_query.html#logging_kibana_query)。


Kibana 是一種以瀏覽器為基礎的介面，您可以在這裡自訂儀表板，然後用來分析日誌資料，以及執行進階管理作業。 

在 {{site.data.keyword.Bluemix}} 中，您可以使用每個 Cloud Foundry 應用程式和組織的每個空間都可用的預設 Kibana 儀表板來分析資料。依預設，這些儀表板會透過包括直方圖列和事件表格列的畫面，顯示過去 24 小時可用的所有資料。 

若要限制透過任何預設儀表板顯示的資訊，您可以在預設儀表板中新增查詢和過濾器。然後，您可以儲存儀表板，以供日後重複使用。 

Kibana 儀表板顯示的資料是由查詢所控制。若要修改儀表板中顯示的資訊，您可以變更查詢、新增多個查詢，然後儲存儀表板。您可以同步自訂、儲存及共用多個儀表板。例如，這就是 Kibana 顯示空間中單一應用程式相關資訊的方式。

您也可以從日誌欄位（例如 message_type 和 instance_ID）配置過濾器。如需相關資訊，請參閱 [Kibana 日誌格式](logging_view_kibana3.html#kibana_log_format_cf)。您可以動態啟用或停用此過濾器。儀表板將會顯示符合您啟用之查詢和過濾準則的日誌項目。如需相關資訊，請參閱[在 Kibana 儀表板中過濾資料](logging_view_kibana3.html#filter_data_kibana_dashboard)。

若要將資料視覺化，您可以配置畫面。Kibana 包括可以用來分析資訊的各種畫面，例如表格、趨勢和直方圖。您可以新增、移除及重新排列儀表板中的畫面。每一個畫面的目標都不同。部分畫面會分組成數列，以提供一個以上查詢的結果。其他畫面則會顯示文件或自訂資訊。如需相關資訊，請參閱[自訂 Kibana 儀表板](logging_view_kibana3.html#customize_kibana_dashboard)。

自訂儀表板之後，您可以選擇下列任何動作：

* 您可以儲存儀表板，以供日後重複使用。如需相關資訊，請參閱[儲存 Kibana 儀表板](logging_view_kibana3.html#save_Kibana_dashboard)。

* 您可以匯出 Kibana 儀表板的直接鏈結或與其他使用者共用。如需相關資訊，請參閱[匯出及共用 Kibana 儀表板](kibana3/logging_kibana_export_share_dashboard.html#sexporting_sharing_kibana_dash)。

* 您可以將儀表板內嵌在網頁中。若要讓使用者看到內嵌的儀表板，該使用者必須要有存取 Kibana 的許可權。

如需相關資訊，請參閱 [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) 文件。

**附註：**支援 Kibana 4 和 Kibana 3。Kibana 3 已淘汰。


##  從 Bluemix 儀表板進入 Kibana 儀表板
{: #launch_Kibana_from_bluemix}

用來過濾儀表板顯示資料的查詢，會擷取 Cloud Foundry 應用程式的日誌項目。Kibana 儀表板預設顯示的日誌資訊，全都與單一 Cloud Foundry 應用程式及其所有實例相關。

若要在 Kibana 中查看 Cloud Foundry 應用程式的日誌，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}}，然後在 {{site.data.keyword.Bluemix_notm}} **應用程式**儀表板上按一下應用程式名稱。即會開啟應用程式詳細資料頁面。
    
2. 在導覽列中，按一下**日誌**。即會開啟「日誌」標籤。 
    
3. 按一下**進階視圖**。即會開啟 **Kibana 3** 儀表板。

如果沒有看到任何日誌，請調整標頭中的時間選取器。

如需自訂 Kibana 儀表板的相關資訊，請參閱[此部落格文章](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/)或 [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) 文件。

##  從 Web 瀏覽器進入 Kibana 儀表板
{: #launch_Kibana_from_browser}

用來過濾儀表板顯示資料的查詢，會擷取 {{site.data.keyword.Bluemix}} 組織中某個空間的日誌項目。Kibana 儀表板顯示的日誌資訊，包括部署在您登入之 {{site.data.keyword.Bluemix}} 組織的空間內的所有資源記錄。

完成下列步驟，以從瀏覽器開啟 Kibana 儀表板：

1. 開啟 [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName})，以登入 Kibana 使用者介面。

2. 選取 **Kibana 3** 標籤，以使用 Kibana 3。選取 **Kibana 4** 標籤，以使用 Kibana 4。預設會開啟 Kibana 儀表板。 

如果沒有看到任何日誌，請調整標頭中的時間選取器。

如需自訂 Kibana 儀表板的相關資訊，請參閱[此部落格文章](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/)或 [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) 文件。



## 在 Kibana 儀表板中過濾資料
{: #filter_data_kibana_dashboard}

在 {{site.data.keyword.Bluemix}} 中，您可以使用根據每項資源或由 {{site.data.keyword.Bluemix}} 空間所提供的預設 Kibana 儀表板來分析資料。依預設，這些儀表板會顯示過去 24 小時可用的所有資料。不過，您可以限制透過儀表板顯示的資訊。您可以在預設儀表板中新增查詢和過濾器，然後儲存儀表板，以供日後重複使用。

您可以在一個儀表板中新增多個查詢和過濾器。查詢會定義一個日誌項目子集，而過濾器可以透過包含或排除資訊的方式來修正資料選取項目。 

對於 Cloud Foundry 應用程式，下列清單概述如何過濾資料的範例：
* 如果您要在日誌中尋找包括重要詞彙的資訊，您可以建立查詢，以依據那些詞彙進行過濾。Kibana 可讓您在儀表板上以視覺化方式比較查詢。如需相關資訊，請參閱[在 Kibana 中以查詢來過濾 Cloud Foundry 應用程式日誌](kibana3/logging_kibana_query.html#logging_kibana_query)。

* 如果您要尋找特定時段內的資訊，您可以過濾某個時間範圍內的資料。如需相關資訊，請參閱[在 Kibana 中依時間過濾 Cloud Foundry 應用程式日誌](kibana3/logging_kibana_filter_by_time_period.html#logging_kibana_time_filter)。

* 如果您要尋找特定實例 ID 的資訊，您可以依實例 ID 過濾資料。如需相關資訊，請參閱[在 Kibana 中依實例 ID 過濾 Cloud Foundry 應用程式日誌](kibana3/logging_kibana_filter_by_instance_id.html#logging_kibana_instance_id)，以及[在 Kibana 中依已知的應用程式 ID 過濾 Cloud Foundry 應用程式日誌](kibana3/logging_kibana_filter_by_known_application_id.html#logging_kibana_known_application_id)。

* 如果您要尋找特定元件的資訊，您可以依元件（日誌類型）過濾資料。如需相關資訊，請參閱[在 Kibana 中依日誌類型過濾 Cloud Foundry 應用程式日誌](kibana3/logging_kibana_filter_by_component.html#logging_kibana_component_filter)。

* 如果您要尋找資訊，例如錯誤訊息，您可以依訊息類型過濾資料。如需相關資訊，請參閱[在 Kibana 中依訊息類型過濾 Cloud Foundry 應用程式日誌](kibana3/logging_kibana_filter_by_message_type.html#logging_kibana_message_type_filter)。

## 自訂 Kibana 儀表板
{: #customize_kibana_dashboard}

您可以自訂不同類型的儀表板，以視覺化及分析資料，例如：
* Single-cf-app 儀表板：此儀表板會顯示單一 Cloud Foundry 應用程式的資訊。  
* Multi-cf-app 儀表板：此儀表板會顯示部署在相同 {{site.data.keyword.Bluemix}} 空間中的所有 Cloud Foundry 應用程式的資訊。 

自訂儀表板時，您可以配置查詢和過濾器，以選取要透過儀表板來顯示的日誌資料子集。

若要將資料視覺化，您可以配置畫面。Kibana 包括可以用來分析資訊的各種畫面，例如表格、趨勢和直方圖。您可以新增、移除及重新排列儀表板中的畫面。每一個畫面的目標都不同。部分畫面會分組成數列，以提供一個以上查詢的結果。其他畫面則會顯示文件或自訂資訊。例如，您可以配置長條圖、圓餅圖或表格，以將資料視覺化，並進行分析。  


## 儲存 Kibana 儀表板
{: #save_Kibana_dashboard}

完成下列步驟，以在自訂 Kibana 儀表板之後予以儲存：

1. 在工具列中，按一下**儲存**圖示。

2. 輸入儀表板的名稱。

    **附註：**如果您嘗試用來儲存儀表板的名稱包含空格，將不會進行儲存。

3. 按一下名稱欄位旁邊的**儲存**圖示。



## 透過 Kibana 儀表板來分析日誌
{: #analyze_kibana_logs}

自訂 Kibana 儀表板之後，您可以透過其畫面來將資料視覺化並進行分析。 

若要搜尋資訊，您可以將查詢固定或取消固定。 

* 您可以將查詢固定至儀表板，以自動啟動搜尋。
* 若要移除儀表板中的內容，您可以取消啟動查詢。

若要過濾資訊，您可以啟用或停用過濾器。 

* 您可以選取過濾器中的**切換**勾選框 ![包含過濾器用的「切換」方框](images/logging_toggle_include_filter.jpg)，以進行啟用。   
* 您可以取消選取過濾器中的**切換**勾選框 ![包含過濾器用的「切換」方框](images/logging_toggle_exclude_filter.jpg)，以進行停用。 

儀表板中的圖形和圖表會顯示資料。您可以使用儀表板中的圖形和圖表來監視資料。 

例如，若為 single-cf-app 儀表板，儀表板中會包括某一個 Cloud Foundry 應用程式的相關資訊。您可以視覺化及分析的資料僅限於該應用程式。您可以使用儀表板來為應用程式的所有實例分析資料。您可以比較實例。您可以依實例 ID 來過濾資訊。 

您可以為每一個實例 ID 定義查詢，並將查詢固定至儀表板。 

![已固定查詢的儀表板](images/logging_kibana_dash_activate_query.jpg)

然後，您可以根據您想要在儀表板中看到的實例資訊，啟動或取消啟動個別查詢。 

下圖顯示一個啟動的查詢，和另一個取消啟動的查詢：

![已固定查詢的儀表板](images/logging_kibana_dash_deactivate_query.jpg)

如果您要在直方圖中比較 2 個實例，則可以在相同的儀表板中定義兩個查詢，每一個實例 ID 有一個查詢。您可以為其提供別名和唯一的顏色，以方便識別。Kibana 處理多個查詢時會使用邏輯 OR 來結合它們。 

下圖顯示用來為查詢配置別名和顏色、將查詢固定至儀表板，以及取消啟動查詢的畫面：

![用來配置查詢的儀表板精靈](images/logging_kibana_query_def.jpg)



## Cloud Foundry 應用程式的 Kibana 日誌格式
{: #kibana_log_format_cf}

您可以配置 Kibana 儀表板，以顯示每一個日誌項目的下列欄位：

<dl>
<dt><strong>@timestamp</strong></dt>
<dd>
<pre class="pre screen"><code>yyyy-MM-ddTHH:mm:ss:SS-0500</code></pre>
<p>記載事件的時間。時間戳記最多定義到毫秒。</p>
</dd>

<dt><strong>@version</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>ALCH_TENANT_ID</strong></dt>
<dd>
<p>{{site.data.keyword.Bluemix_notm}} 資源的 ID。</p>
</dd>

<dt><strong>_id</strong></dt>
<dd>
<p>日誌文件的唯一 ID。</p>
</dd>

<dt><strong>_index</strong></dt>
<dd>
<p>日誌項目的索引。</p>
</dd>

<dt><strong>_type</strong></dt>
<dd>
<p>日誌類型；例如 <samp>syslog</samp>。</p>
</dd>

<dt><strong>app_name</strong></dt>
<dd>
<p>{{site.data.keyword.Bluemix_notm}} 應用程式的名稱。</p>
</dd>

<dt><strong>application_id</strong></dt>
<dd>
<p>{{site.data.keyword.Bluemix_notm}} 應用程式的唯一 ID。</p>
</dd>

<dt><strong>host</strong></dt>
<dd>
<p>產生日誌資料的應用程式名稱。</p>
</dd>

<dt><strong>instance_id</strong></dt>
<dd>
<p>產生日誌資料之應用程式實例的實例 ID。</p>
</dd>

<dt><strong>module</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>loglevel</strong></dt>
<dd>
<p>所記載事件的嚴重性。</p>
</dd>

<dt><strong>message</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Message</var>&gt;</code></pre>
<p>元件所發出的訊息。訊息根據環境定義而不同。</p>
</dd>

<dt><strong>message_type</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>將日誌訊息寫入其中的串流。<samp class="ph codeph">OUT</samp> 指的是 <samp class="ph codeph">stdout</samp> 串流，而 <samp class="ph codeph">ERR</samp> 指的是 <samp class="ph codeph">stderr</samp> 串流。</p>
</dd>

<dt><strong>org_id</strong></dt>
<dd>
<p>{{site.data.keyword.Bluemix_notm}} 組織的唯一 ID。</p>
</dd>

<dt><strong>org_name</strong></dt>
<dd>
<p>在其中編譯打包應用程式之 {{site.data.keyword.Bluemix_notm}} 組織的名稱。</p>
</dd>

<dt><strong>origin</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>source_id</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>產生日誌的元件。下列清單說明來自各元件的日誌：</p>

<dl>
<dt><strong>API</strong></dt>
<dd>針對要求變更應用程式狀態之 API 呼叫所記載的回應。</dd>

<dt><strong>APP</strong></dt>
<dd>已記載的應用程式回應。</dd>

<dt><strong>CELL</strong></dt>
<dd>已記載的 Diego Cell 回應，指出應用程式開始、停止或當機的時間。</dd>

<dt><strong>LGR</strong></dt>
<dd>已記載的日誌聚集器回應，指出記載程序的問題。</dd>

<dt><strong>RTR</strong></dt>
<dd>當路由器將 HTTP 要求遞送至應用程式時，已記載的路由器回應。</dd>

<dt><strong>SSH</strong></dt>
<dd>當使用者使用 **cf ssh** 指令來存取應用程式容器時，已記載的 Diego Cell 回應。</dd>

<dt><strong>STG</strong></dt>
<dd>將應用程式編譯打包或重新編譯打包時，已記載的 Diego Cell 或 Droplet Execution Agent 回應。</dd>
</dl>
</dd>

<dt><strong>space_name</strong></dt>
<dd>
<p>在其中編譯打包應用程式之 {{site.data.keyword.Bluemix_notm}} 空間的名稱。</p>
</dd>

<dt><strong>timestamp</strong></dt>
<dd>
<p>記載事件的時間。時間戳記最多定義到毫秒。</p>
</dd>

<dt><strong>_type</strong></dt>
<dd>
<p>日誌類型，例如 <samp>syslog</samp>。</p>
</dd>
</dl>




