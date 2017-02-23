---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-07-28"

---

  {:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 適用於應用程式開發人員的 C#
{: #c_sharp}


您可以使用 C# 來建置及自訂應用程式，在 {{site.data.keyword.iot_full}} 上與組織互動。請使用所提供的資訊及範例，利用 C# 開始開發您的應用程式。
{:shortdesc}

## 下載 C# 用戶端及資源
{: #csharp_client_download}

若要存取適用於 {{site.data.keyword.iot_short_notm}} 的 C# 用戶端程式庫及範例，請移至 GitHub 中的 [iot-csharp](https://github.com/ibm-watson-iot/iot-csharp) 儲存庫，並完成安裝指示。


## 建構子
{: #constructor}

建構子會建置用戶端實例，並接受包含下列定義的引數：

|定義 |說明 |
|:---|:---|
|`orgId`   |您的組織 ID。|
|`appId`   |組織中應用程式的唯一 ID。|
|`auth-key`   |將應用程式安全地連接至 Watson IoT Platform 的 API 金鑰。|
|`auth-token`   |將應用程式安全地連接至 Watson IoT Platform 的 API 金鑰記號。|

如果 `appId` 是唯一提供的引數，用戶端會連接至 {{site.data.keyword.iot_short_notm}} 的 Quickstart 服務，作為已取消登錄的裝置。引數清單定義用戶端如何連接至 {{site.data.keyword.iot_short_notm}} 模組。

```
ApplicationClient applicationClient = new ApplicationClient(orgId, appId, apiKey, authToken);  
applicationClient.connect();
```


## 訂閱裝置事件
{: #subscribe_device_events}

裝置會使用事件來將資料發佈至 {{site.data.keyword.iot_short_notm}} 實例。裝置會控制事件的內容，並指派名稱給它傳送的每個事件。

{{site.data.keyword.iot_short_notm}} 實例收到事件時，所收到事件的認證可識別傳送端裝置，這表示，裝置無法假冒另一個裝置。

應用程式預設會訂閱所有已連接裝置的所有事件。請使用裝置類型、裝置 ID、事件及訊息格式參數，以控制訂閱的範圍。下列程式碼範例顯示如何使用這些參數來定義訂閱的範圍：

### 訂閱所有裝置的所有事件

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents();
```

### 訂閱特定類型之所有裝置的所有事件

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType);
```

### 訂閱所有裝置的特定事件

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(evt);
```

###  訂閱兩個以上不同裝置的特定事件

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt);
```

### 訂閱以 JSON 格式發佈的所有事件

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt, "json", 0);
```

**附註：**單一用戶端實例可以支援多個訂閱。

### 處理裝置的事件

若要處理訂閱所收到的事件，請登錄事件回呼方法，如下列範例所示：

```
public static void processEvent(String eventName, string eventFormat, string eventData) {
// Do something
}
applicationClient.connect();
applicationClient.eventCallback += processEvent;
applicationClient.subscribeToDeviceEvents();
```
下表說明事件回呼方法的參數：

|參數|資料類型|說明|
|:---|:---|
|`eventName`|字串|識別事件。 |
|`eventFormat`|字串| 格式可以是任何字串（例如，JSON）。|
|`eventData`|字典| 訊息有效負載的資料。長度上限是 131072 個位元組。|


## 訂閱裝置狀態
{: #subscribe_device_status}

訂閱預設為接收所有已連接裝置的狀態更新。請使用裝置類型及裝置 ID 參數，以控制訂閱的範圍。下列程式碼範例顯示如何使用這些參數來定義訂閱的範圍：

### 訂閱所有裝置的狀態更新

```
applicationClient.connect();
applicationClient.subscribeToDeviceStatus += processDeviceStatus;
applicationClient.subscribeToDeviceStatus();
```

### 訂閱兩個不同裝置的狀態更新

```
applicationClient.connect();
applicationClient.subscribeToDeviceStatus += processDeviceStatus;
applicationClient.subscribeToDeviceStatus(deviceType, deviceId);
```

**附註：**單一用戶端實例可以支援多個訂閱。

### 處理裝置的狀態更新

若要處理訂閱所收到的狀態更新，請登錄事件回呼方法，如下列範例所示：

```
public static void processDeviceStatus(String deviceType, string deviceId, string data)
        {
           //
        }
applicationClient.connect();
applicationClient.appStatusCallback += processAppStatus;
applicationClient.subscribeToApplicationStatus();
```

## 發佈裝置的事件
{: #publish_events_devices}

應用程式可以發佈事件，就彷彿事件是源自裝置一樣。

```
applicationClient.connect();
applicationClient.publishEvent(deviceType, deviceId, evt, data, 0);

```

下表說明 `publishEvent()` 方法中指定的參數：

|參數|資料類型|說明|
|:---|:---|
|`deviceType`|字串| 裝置類型。一般而言，deviceType 是執行特定作業的裝置分組，例如，"weatherballoon"。|
|`deviceId`|字串| 裝置的 ID。一般而言，針對給定的裝置類型，deviceId 是該裝置的唯一 ID（例如，序號或 MAC 位址）。|
|`evt`|字串| 事件的名稱。|
|`format`|字串| 格式可以是任何字串（例如，JSON）。|
|`data`|字典| 訊息有效負載的資料。長度上限是 131072 個位元組。|
|`QoS`|整數| 服務品質。有效值包含 `0`、`1`、`2`。 |


## 將指令發佈至裝置
{: #publish_commands_devices}

應用程式可對連接的裝置發佈指令。

```
applicationClient.connect();
applicationClient.publishCommand(deviceType, deviceId, "testcmd", "json", data, 0);
```
下表說明 `publishCommand()` 方法中指定的參數：

|參數|資料類型|說明|
|:---|:---|
|`deviceType`|字串| 裝置類型。一般而言，deviceType 是執行特定作業的裝置分組，例如，"weatherballoon"。|
|`deviceId`|字串| 裝置的 ID。一般而言，針對給定的裝置類型，deviceId 是該裝置的唯一 ID（例如，序號或 MAC 位址）。|
|`command`|字串| 指令的名稱。|
|`format`|字串| 格式可以是任何字串（例如，JSON）。|
|`data`|字典| 訊息有效負載的資料。長度上限是 131072 個位元組。|
|`QoS`|整數| 服務品質。有效值包含 `0`、`1`、`2`。 |
