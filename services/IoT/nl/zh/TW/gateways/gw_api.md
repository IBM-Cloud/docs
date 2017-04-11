---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-07"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 閘道裝置的 HTTP REST API
{: #api_link}


若要存取 {{site.data.keyword.iot_short_notm}} HTTP REST API 文件，以及尋找有關建立、更新、刪除及列出裝置的詳細資訊，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html)。

唯一支援的 {{site.data.keyword.iot_short_notm}} HTTP REST API 版本是第 2 版。請確定您的 {{site.data.keyword.iot_short_notm}} 解決方案使用的是第 2 版。

## 用戶端連線
{: #client_connections}

如需用戶端安全以及如何將用戶端連接至 {{site.data.keyword.iot_short_notm}} 中閘道裝置的相關資訊，請參閱[將應用程式、裝置及閘道連接至 {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html)。


### 鑑別

所有要求都必須包含授權標頭。基本鑑別是唯一支援的方法。當裝置使用 {{site.data.keyword.iot_short_notm}} HTTP REST API 提出 HTTP 要求時，需要下列認證：

|認證|必要輸入|
|:---|:---|
|使用者名稱| `g/{orgId}/{gwType}/{gwDevId}`
|密碼| 在登錄閘道裝置時，自動產生或手動指定的鑑別記號。


其中：

**_orgId_**   
- 組織名稱，必須符合主機標頭中指定的名稱。

**_gwType_**
- 閘道的類型。

**_gwDevId_**

- 閘道的裝置 ID。

### Content-Type 要求標頭

`Content-Type` 要求標頭必須隨要求提供。下表顯示支援的類型如何對映至 {{site.data.keyword.iot_short_notm}} 內部格式：

|Content-Type 標頭|{{site.data.keyword.iot_short_notm}} 中的格式|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

## 前次事件快取
{: #last-event-cache}

您可以使用 {{site.data.keyword.iot_short_notm}} 的「前次事件快取 API」，擷取裝置前次傳送的事件。不論裝置是連線還是離線，此 API 皆可運作，而不管裝置的實體位置或使用狀態為何，都可讓您擷取裝置狀態。您可以針對特定裝置擷取事件 ID 的前次記錄值，也可以針對特定裝置所報告的每一個事件 ID，擷取前次記錄值。可針對最多 365 天之前發生的任何特定事件，擷取裝置的前次事件資料。

若要要求特定事件 ID 的最新值，請使用下列 API 要求，它會傳回 "power" 事件 ID 的前次記錄值：

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events/power
```

傳回的回應具有下列 JSON 格式：

```
{
    "deviceId": "<device-id>",
    "eventId": "power",
    "format": "json",
    "payload": "eyJzdGF0ZSI6Im9uIn0=",
    "timestamp": "2016-03-14T14:12:06.527+0000",
    "typeId": "<device-type>"
}
```

**附註：**API 回應為 JSON 格式時，可以使用任何格式來撰寫事件有效負載。「前次事件快取 API」所傳回的有效負載會使用 base64 進行編碼。

若要要求裝置所報告之每個事件 ID 的最新值，請使用下列 API 要求：

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events
```

回應包括裝置所傳送的所有事件 ID。在下列範例中，會傳回 "power" 及 "temperature" 事件的值。

```
[
    {
        "deviceId": "<device-id>",
        "eventId": "power",
        "format": "json",
        "payload": "eyJzdGF0ZSI6Im9uIn0=",
        "timestamp": "2016-03-14T14:12:06.527+0000",
        "typeId": "<device-type>"
    },
    {
        "deviceId": "<device-id>",
        "eventId": "temperature",
        "format": "json",
        "payload": "eyJpbnRlcm5hbCI6MjIsICJleHRlcm5hbCI6MTZ9",
        "timestamp": "2016-03-14T14:17:44.891+0000",
        "typeId": "<device-type>"
    }
]
```
