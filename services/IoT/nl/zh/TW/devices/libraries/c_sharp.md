---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-08-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 適用於裝置開發人員的 C#
{: #c_sharp}

您可以使用 C# 來建置及自訂裝置，在 {{site.data.keyword.iot_full}} 上與組織互動。請使用所提供的資訊及範例，利用 C# 開始開發您的裝置。
{:shortdesc}

## 下載 C# 用戶端及資源
{: #csharp_client_download}

若要存取適用於 {{site.data.keyword.iot_short_notm}} 的 C# 用戶端及資源，請移至 GitHub 中的 [iot-csharp](https://github.com/ibm-watson-iot/iot-csharp) 儲存庫，並完成安裝指示。


## 建構子
{: #constructor}

建構子會建置用戶端實例，並接受包含下列定義的引數：

|定義 |說明 |
|:---|:---|
|`orgId`|您的組織 ID。|
|`deviceType`|您的裝置類型。|
|`deviceId` |您的裝置 ID。|
|`auth-method`   |要使用的鑑別方法。目前唯一支援的值是 `token`。|
|`auth-token`   |將裝置安全地連接至 Watson IoT Platform 的鑑別記號。|


如果 `deviceId` 及 `deviceType` 是唯一提供的引數，則用戶端會連接至 {{site.data.keyword.iot_short_notm}} 的 Quickstart 服務，作為已取消登錄的裝置。引數清單定義用戶端如何連接至 {{site.data.keyword.iot_short_notm}} 模組。


```
namespace com.ibm.iotf.client

public DeviceClient(string orgId, string deviceType, string deviceID, string auth-method, string auth-token)
        : base(orgId, "d" + CLIENT_ID_DELIMITER + orgId + CLIENT_ID_DELIMITER + deviceType + CLIENT_ID_DELIMITER + deviceID, "use-token-auth", auth-token)
    {

    }
```

## 發佈事件
{: #publishing-events}

裝置會使用事件來將資料發佈至 {{site.data.keyword.iot_short_notm}} 實例。裝置會控制事件的內容，並指派名稱給它傳送的每個事件。

{{site.data.keyword.iot_short_notm}} 實例收到事件時，送入事件的認證可識別傳送端裝置，這表示，裝置無法假冒另一個裝置。

可使用三種[服務品質 (QoS) 水準](../mqtt.html#managed-devices)的任一種發佈事件，這些水準由 MQTT 通訊協定定義。依預設，事件是以 QoS 0 來發佈。


## 使用預設服務品質水準發佈事件
{: #publish_event_default_qos}

```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}");
```


## 使用使用者定義的服務品質水準發佈事件
{: #publish_event_user_qos}

以 MQTT QoS 水準大於 `0` 發佈的事件，會包含額外的接收確認資訊，且所需的發佈時間可能會比 QoS 水準為 `0` 的事件還久。


```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}", 2);
```

## 處理指令
{: #handling_commands}

當裝置用戶端連接時，它會自動訂閱此裝置的任何指令。若要處理特定指令，您必須登錄指令回呼方法，如下列範例所示。

```
public static void processCommand(string cmdName, string cmdFormat, string cmdData) {
...
 }
```

```
deviceClient.connect();
deviceClient.commandCallback += processCommand;
```
下表說明 commandCallback 方法的參數：

|參數|資料類型|說明|
|:---|:---|
|`cmdName`|字串|識別指令。 |
|`cmdFormat`|字串|格式可以是任何字串（例如，JSON）。|
|`cmdData`|字典|有效負載的資料。長度上限是 131072 個位元組。|
