---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 裝置的 HTTP REST API
{: #api}
前次更新：2016 年 9 月 9 日
{: .last-updated}

**重要事項：**裝置的 {{site.data.keyword.iot_full}} HTTP REST API 特性僅是有限測試版程式的一部分。未來更新可能包括與此特性的目前版本不相容的變更。請試用，並且[讓我們知道您的想法](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html)。

## 存取 HTTP REST API
{: #api_link}

若要存取 {{site.data.keyword.iot_short_notm}} HTTP REST API，以及取得如何將裝置整合至組織的相關資訊，請移至 https://docs.internetofthings.ibmcloud.com/swagger/v0002.html。

唯一支援的 {{site.data.keyword.iot_short_notm}} HTTP REST API 版本是第 2 版。請確定您的 {{site.data.keyword.iot_short_notm}} 解決方案使用的是第 2 版。

# 裝置的 HTTP REST 傳訊 API
{: #rest_messaging_api}

## 發佈事件
{: #event_publication}

除了使用 MQTT 傳訊通訊協定之外，您還可以使用 HTTP REST API 指令來配置裝置，讓它透過 HTTP 將事件發佈至 {{site.data.keyword.iot_short_notm}}。

請使用下列其中一個 URL，來提交來自連接至 {{site.data.keyword.iot_short_notm}} 之裝置的 `POST` 要求：

### 未受保護的 POST 要求
<pre class="pre">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### 安全的 POST 要求
<pre class="pre">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

如果您要將裝置或應用程式連接至「快速入門」服務，請改用下列其中一個 URL：

### 連接至快速入門的未受保護 POST 要求
<pre class="pre">http://quickstart.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### 連接至快速入門的安全 POST 要求
<pre class="pre">https://quickstart.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

**重要注意事項：**
- 在現行 HTTP REST API 版本中，您只能使用 HTTP 傳訊來提交裝置事件。使用 MQTT 傳訊通訊協定，以提交其他裝置管理及控制特性的要求。
- 因為無法變更授權 HTTP 標頭，所以只能重複使用 HTTP 連線來發佈相同裝置的事件。

### 鑑別

所有要求都必須包括授權標頭。基本鑑別是唯一支援的方法。裝置透過 {{site.data.keyword.iot_short_notm}} HTTP REST API 提出 HTTP 要求時，需要下列認證：

```
username = "use-token-auth"
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

與 MQTT 服務品質「最多一次」遞送服務水準 0 類似，HTTP REST 傳訊提供非持續訊息遞送，但會驗證要求正確無誤，並驗證要求會先遞送至伺服器，再傳送 HTTP 回應。包含 HTTP 狀態碼 200 的回覆確認已將訊息遞送至伺服器。當您使用「最多一次」MQTT 服務品質水準或 HTTP 對等項目來遞送事件訊息時，裝置或應用程式必須實作重試邏輯來保證遞送。

如需 {{site.data.keyword.iot_short_notm}} 的 MQTT 通訊協定及服務品質水準的相關資訊，請參閱 [MQTT 傳訊](../reference/mqtt/index.html)。
