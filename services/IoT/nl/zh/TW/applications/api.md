---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-02-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 應用程式的 HTTP REST API
{: #api}

您可以使用 {{site.data.keyword.iot_full}} HTTP REST API 來建置及自訂應用程式，在 {{site.data.keyword.iot_short_notm}} 上與組織互動。
{:shortdesc}

## 功能
{: #capabilities}

{{site.data.keyword.iot_short_notm}} HTTP REST API 支援應用程式的下列功能：

- 擷取組織資訊
- 大量裝置作業（列出、新增及移除）
- 裝置類型作業（列出、建立、刪除、檢視詳細資料，以及更新）
- 裝置作業（列出、新增、移除、檢視詳細資料、更新、檢視位置，以及檢視管理資訊）
- 裝置診斷作業（清除日誌、擷取日誌、新增日誌資訊、刪除日誌、取得特定日誌、清除錯誤碼、取得裝置錯誤碼，以及新增錯誤碼）
- 連線問題判斷（列出裝置連線日誌事件）
- 前次事件快取（檢視特定裝置的前次事件）
- 裝置管理要求作業（列出裝置管理要求、起始要求、清除要求狀態、取得要求的詳細資料、依裝置列出所有要求狀態，以及取得特定裝置的要求狀態）
- 用量管理作業（擷取資料的總使用量）
- 裝置事件發佈（測試版）
- 服務狀態查詢（依組織擷取服務狀態）

## 存取 HTTP REST API 文件
{: #api_link}

若要存取 {{site.data.keyword.iot_short_notm}} HTTP REST API 文件，以及取得如何建置及自訂應用程式的相關資訊，請移至下列 URL：[https://docs.internetofthings.ibmcloud.com/swagger/v0002.html](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html)

唯一支援的 {{site.data.keyword.iot_short_notm}} HTTP REST API 版本是第 2 版。請確定您的 {{site.data.keyword.iot_short_notm}} 解決方案使用的是第 2 版。

# 應用程式的 HTTP REST 傳訊 API
{: #rest_messaging_api}

## 發佈事件及指令
{: #event_command_publication}

除了使用 MQTT 傳訊通訊協定之外，您還可以使用下列其中一個 HTTP REST API 指令來配置應用程式，讓它透過 HTTP 將事件及指令發佈至 {{site.data.keyword.iot_short_notm}}。

### 未受保護的事件 POST 要求
<pre class="pre">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### 安全的事件 POST 要求
<pre class="pre">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

**附註：**您也可以指定埠 443（預設 SSL 埠）來進行安全 HTTP API 呼叫。

### 未受保護的指令 POST 要求
<pre class="pre">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/commands/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### 安全的指令 POST 要求
<pre class="pre">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/commands/<var class="keyword varname">eventId</var></pre>
{: codeblock}

如果您要將裝置或應用程式連接至 Quickstart 服務，請將 **orgId** 取代為字串 'quickstart'。

**附註：**
- 雖然應用程式可以重複使用 HTTP 連線，將事件或指令張貼至不同的裝置，但是無法變更授權 HTTP 標頭。
- 您也可以指定埠 443（預設 SSL 埠）來進行安全 HTTP API 呼叫。

### 鑑別

所有要求都必須包含授權標頭。基本鑑別是唯一支援的方法。應用程式是使用 API 金鑰進行鑑別。應用程式透過 {{site.data.keyword.iot_short_notm}} HTTP REST API 提出要求時，需要下列認證：

```
username = API key (for example, a-orgId-a84ps90Ajs)
password = Authentication token
```

### Content-Type 要求標頭

`Content-Type` 要求標頭必須隨要求提供。下表顯示支援的類型如何對映至 {{site.data.keyword.iot_short_notm}} 內部格式。

|Content-Type 標頭|{{site.data.keyword.iot_short_notm}} 中的格式|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

### 服務品質

與 MQTT 服務品質「最多一次」遞送服務水準 0 類似，HTTP REST 傳訊提供非持續訊息遞送，但會驗證要求正確無誤，並驗證要求會先遞送至伺服器，再傳送 HTTP 回應。包含 HTTP 狀態碼 200 的回覆會確認已將訊息遞送至伺服器。當您使用「最多一次」的 MQTT 服務品質水準或 HTTP 對等項目來遞送事件訊息時，裝置或應用程式必須實作重試邏輯以保證遞送。


如需 {{site.data.keyword.iot_short_notm}} 的 MQTT 通訊協定及服務品質水準的相關資訊，請參閱 [MQTT 傳訊](../reference/mqtt/index.html)。
