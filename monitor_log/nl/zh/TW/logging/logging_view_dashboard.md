---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 從 Bluemix 主控台分析日誌
{: #analyzing_logs_bmx_ui}

在 {{site.data.keyword.Bluemix}} 中，您可以透過每一個 Cloud Foundry 應用程式或 Docker 容器都有的日誌標籤，來檢視、過濾及分析日誌。
{:shortdesc}

「{{site.data.keyword.Bluemix_notm}} 公用」提供整合式記載功能。例如，在 Cloud Foundry (CF) 中執行應用程式時，會擷取與應用程式互動之系統元件的日誌資料、關於應用程式的日誌資料，甚至是當您使用 stdout 和 stderr 時應用程式內所產生的日誌資料。

請考慮分析及日誌保留的日誌資料可用性的下列資訊：

* 在「{{site.data.keyword.Bluemix_notm}} 公用」中，日誌資料預設會儲存 7 天。 
* 您每天最多可以儲存 1 GB 的資料。 
* 根據預設值，來自 {{site.data.keyword.Bluemix_notm}} 主控台可供分析的日誌包含過去 24 小時的資料。

**提示：**若要分析超過過去 24 小時之自訂期間的資料，請參閱[使用 Kibana 進行進階日誌分析](logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana)。 

##  取得 Cloud Foundry 應用程式的日誌
{: #launch_logs_tab_bmx_ui_cf}

若要查看 Cloud Foundry 應用程式的部署或運行環境日誌，請完成下列步驟：

1. 從「應用程式」儀表板，按一下 Cloud Foundry 應用程式的名稱。 
    
2. 從應用程式詳細資料頁面，按一下**日誌**。
    
    從**日誌**標籤，您可以檢視應用程式的最新日誌，或即時讀取日誌尾端的內容。此外，您還可以依元件（日誌類型）、依應用程式實例 ID 以及依錯誤來過濾日誌。
    

##  取得 Docker 容器的日誌
{: #launch_logs_tab_bmx_ui_containers}

若要查看 Docker 容器的部署或運行環境日誌，請完成下列步驟：

1. 從「應用程式」儀表板，按一下單一容器或容器群組。 
    
2. 從應用程式詳細資料頁面，按一下**監視及記載**。

3. 選取**記載**標籤。
    
    從**記載**標籤，您可以檢視容器的最新日誌，或即時讀取日誌尾端的內容。 

## CF 應用程式日誌的日誌格式
{: #log_format_cf}

{{site.data.keyword.Bluemix_notm}} 應用程式的日誌會以固定格式顯示，與下列型樣類似：

<code><var class="keyword varname">Component</var>/<var class="keyword varname">instanceID</var>/<var class="keyword varname">message</var>/<var class="keyword varname">timestamp</var></code>

每個日誌項目都包含下列欄位：

| 欄位 | 說明 |
|-------|-------------|
| 時間戳記 | 日誌陳述文字的時間。時間戳記最多定義到毫秒。 |
| 元件 | 產生日誌的元件。如需不同元件的清單，請參閱 [CF 應用程式的日誌來源](logging_cf_apps.html#logging_bluemix_cf_apps_log_sources)。<br> 每一個元件類型後面都接著一個斜線和一個數字，用來指出應用程式實例。0 是配置給第一個實例的數字，1 是配置給第二個實例的數字，依此類推。 |
| 訊息 | 元件所發出的訊息。訊息根據環境定義而不同。 |



## 容器日誌的日誌格式
{: #log_format_containers}

容器的日誌會以固定格式顯示，與下列型樣類似：

<code><var class="keyword varname">timestamp</var>/<var class="keyword varname">machine</var>/<var class="keyword varname">message</var>  </code>

每個日誌項目都包含下列欄位：

| 欄位 | 說明 |
|-------|-------------|
| 日期/時間 | 日誌陳述文字的時間。時間戳記最多定義到毫秒。 |
| 機器 | 容器執行所在的主機名稱。 |
| 訊息 | 發出的訊息。訊息根據環境定義而不同。 |


