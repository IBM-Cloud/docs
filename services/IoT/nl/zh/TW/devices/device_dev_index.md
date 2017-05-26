---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-03"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 在 {{site.data.keyword.iot_short_notm}} 上開發裝置
{: #device_dev_index}

裝置具有網際網路連線，並且可將資料傳送至雲端或接收來自雲端的資料。您可以使用裝置將感應器讀數這類事件資訊傳送至雲端，以及接受來自雲端中應用程式的指令。

裝置會使用事件將資料發佈至 {{site.data.keyword.iot_short_notm}}。裝置會控制事件的內容，並指派所傳送的每一個事件的名稱。{{site.data.keyword.iot_short_notm}} 接收來自裝置的事件時，會使用收到事件之連線的認證來判定傳送事件的裝置。此架構可防止裝置假冒另一個裝置。

如需主要概念（包括裝置）的相關資訊，請參閱[關於 Watson IoT Platform](https://console.ng.bluemix.net/docs/services/IoT/iotplatform_overview.html#watsoniotplatform_importantconcepts)。


## 將裝置連接至 {{site.data.keyword.iot_short_notm}}
{: #device_connect}
您可以使用 HTTP 或 MQTT 通訊協定，將裝置連接至 {{site.data.keyword.iot_short_notm}}。如果您要配置要求/回應情境（例如，有人進行採購並收到認可），請使用 HTTP。如果您要配置事件情境（例如，有人按門鈴而觸發行動裝置的警示時），請使用 MQTT。

必須先向組織登錄裝置，裝置才能連接至 {{site.data.keyword.iot_full}}。若要安全地連接至 {{site.data.keyword.iot_short_notm}}，您必須登錄 Bluemix 帳戶，並建立自己的 {{site.data.keyword.iot_short_notm}} 組織。您接著可以使用此組織的 ID 來登錄裝置。已登錄裝置會透過唯一裝置 ID（例如 MAC 位址）以及僅針對該裝置所接受的鑑別記號，向 {{site.data.keyword.iot_short_notm}} 識別它們。安全地連接之後，請使用 Bluemix 來建置自己的應用程式。請嘗試使用 Node-RED 將應用程式連結在一起。

如果您要連接裝置，而不登錄裝置（例如，執行概念驗證），則可以使用特殊組織 ID `QuickStart` 來執行。`QuickStart` 是在雲端中執行的 {{site.data.keyword.iot_short_notm}} 的公用沙盤推演實例。如果您不需要安全地連接，則可以使用 `QuickStart` 來測試裝置連線功能，並實驗 {{site.data.keyword.iot_short_notm}}。完成實驗時，請使用傳輸層安全 (TLS) 及鑑別記號，將裝置安全地重新連接至專屬特定組織 ID 實例。

如需使用 HTTP 通訊協定將裝置連接至 {{site.data.keyword.iot_short_notm}} 的相關資訊，請參閱[裝置的 HTTP REST API](https://console.ng.bluemix.net/docs/services/IoT/devices/api.html)。
如需使用 MQTT 通訊協定將裝置連接至 {{site.data.keyword.iot_short_notm}} 的相關資訊，請參閱[裝置的 MQTT 連線功能](https://console.ng.bluemix.net/docs/services/IoT/devices/mqtt.html)。

## 開始使用開發裝置
{: #get_started}
如果已針對 {{site.data.keyword.iot_short_notm}} 啟用您的裝置，您就可以開始使用它。

如果裝置尚未啟用，請參閱 [developerWorks](https://developer.ibm.com/recipes/) 上可用的秘訣。請瀏覽現有秘訣，以查看是否有您裝置適用的秘訣，並使用秘訣協助您開始開發。如果想要的話，您甚至可以發佈自己的秘訣。

如果找不到您的特定裝置適用的秘訣，則 IBM 提供一些可用來開始使用的程式設計手冊及 API。這些手冊包含用戶端程式庫、範例及資訊，可協助您建置及開發程式碼，以將裝置與應用程式整合及連接至 {{site.data.keyword.iot_short_notm}}。下列是目前可用的程式設計手冊：

- Java
- Node.js
- 嵌入式 C
- ARM mBed C++
- Python
- C#
- Node-RED

如需相關資訊以及可用程式設計手冊的鏈結，請參閱[適用於 {{site.data.keyword.iot_short_notm}} 開發的用戶端程式庫](../iot_platform_client_lib.html)。

如果您找不到適合的 {{site.data.keyword.iot_short_notm}} 程式設計手冊，則可以撰寫自己的程式，並使用 MQTT 或 HTTP 通訊協定將裝置連接至 {{site.data.keyword.iot_short_notm}}。

MQTT 是由 ISO 認可的 OASIS 國際標準組織所管理的開放式標準。如需相關資訊，請參閱 [OASIS 訊息佇列作業遙測傳輸 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=mqtt){: new_window}。

許多不同的系統會有各種 MQTT 用戶端程式庫，包括下列環境：
- http://www.eclipse.org/paho/
- https://github.com/mqtt/mqtt.github.io/wiki/software?id=software

如需 MQTT 的相關資訊，請參閱 [MQTT 傳訊](https://console.ng.bluemix.net/docs/services/IoT/reference/mqtt/index.html?pos=3)。
