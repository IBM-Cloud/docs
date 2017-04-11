---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# 適用於應用程式開發人員的 Node.js
{: #nodejs}

前次更新：2016 年 7 月 29 日
{: .last-updated}

您可以調整 Node.js 中的用戶端程式庫及範例，來建置及自訂應用程式，在 {{site.data.keyword.iot_full}} 上與組織互動。
{:shortdesc}

請使用所提供的資訊及範例，利用 Node.js 開始開發您的應用程式。

## 下載 Node.js 用戶端及資源
{: #nodejs_client_download}

若要存取適用於 {{site.data.keyword.iot_short_notm}} 的 Node.js 用戶端程式庫及其他可用的資源，請移至 GitHub 中的 [iot-nodejs ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-watson-iot/iot-nodejs){: new_window} 儲存庫，並完成安裝指示。


如需相關資訊，請參閱下列資源：
- GitHub 中的[應用程式範例 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-watson-iot/iot-nodejs/tree/master/samples){: new_window}。
- NPM 上的 [ibmiotf ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.npmjs.com/package/ibmiotf){: new_window}。
- 本文件的[參考資料](#reference_nodejs)小節。


## 建構子
{: #constructor}

建構子會建置應用程式用戶端實例，並接受包含下列內容的 JSON 配置檔：

| 內容     |說明     |
|----------------|----------------|
|`org` |您的組織 ID。這是必要值。|
|`id`  |組織內應用程式的唯一 ID。|
|`auth-key`   |將應用程式安全地連接至 Watson IoT Platform 的 API 金鑰。|
|`auth-token`   |將裝置安全地連接至 Watson IoT Platform 的 API 金鑰記號。|
|`type`  |訂閱的類型。指定 `shared`，以啟用共用訂閱。|


若要使用 Quickstart，只需要前兩個內容。

```
  var Client = require("ibmiotf");
	var appClientConfig = {
		"org" : orgId,
		"id" : appId,
		"auth-key" : apiKey,
		"auth-token" : apiToken
	}

	var appClient = new Client.IotfApplication(appClientConfig);
```


### 使用配置檔


您也可以使用配置檔，而非直接傳遞 JSON 內容，如下列程式碼範例所概述：

```

  var Client = require("ibmiotf");
	var appClientConfig = require("./application.json");
	var appClient = new Client.IotfApplication(appClientConfig);
```

請確定 JSON 配置檔的格式如下：

```
    {
	  "org": 'xxxxx',
	  "id": 'myapp',
	  "auth-key": 'a-xxxxxxx-zenkqyfiea',
	  "auth-token": 'xxxxxxxxxx'
    }
```


## 連接至 {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

若要連接至 {{site.data.keyword.iot_short_notm}}，請提交*連接* 要求，如下所示：

```
  var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

	//Add your code here
	});
```

順利連接至 {{site.data.keyword.iot_short_notm}} 服務之後，應用程式用戶端會傳送 `connect` 事件，因此可以在此回呼函數內實作任何邏輯。



應用程式用戶端會在中斷連線時自動嘗試重新連接。重新連線成功時，用戶端會傳送 `reconnect` 事件。



## 記載
{: #logging}

預設只會記錄類型 `warn` 的日誌事件。如果您要提高或降低記載層次，請使用 `log.setLevel` 函數。支援下列記載層次：
- trace
- debug
- info
- warn
- error

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//setting the log level to 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Add your code here
	});
```

## 共用訂閱
{: #shared_subscriptions}

請使用共用訂閱特性建置可擴充應用程式，來平衡多個應用程式實例之間的訊息負載。若要啟用負載平衡，請將 `type` 欄位設為 `shared`，如下列範例所示：

```

	var appClientConfig = {
	  org: 'xxxxx',
	  id: 'myapp',
	  "auth-key": 'a-xxxxxx-xxxxxxxxx',
	  "auth-token": 'xxxxx!xxxxxxxx',
	  "type" : "shared" // make this connection as shared subscription
	};
	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//setting the log level to 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Add your code here
	});
```

## 處理錯誤
{: #handling_errors}

應用程式用戶端發生錯誤時，會產生 `error` 事件。

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//setting the log level to 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Add your code here
	});
	appClient.on("error", function (err) {
		console.log("Error : "+err);
	});
```

## 訂閱裝置事件
{: #subscribing_device_events}

事件是裝置用來將資料發佈至 {{site.data.keyword.iot_short_notm}} 實例的機制。裝置會控制事件的內容，並指派名稱給它傳送的每個事件。

{{site.data.keyword.iot_short_notm}} 實例收到事件時，所收到事件的認證可識別傳送端裝置，這表示，裝置無法假冒另一個裝置。


應用程式預設會訂閱所有已連接裝置的所有事件。請使用裝置類型、裝置 ID、事件及訊息格式參數，以控制訂閱的範圍。下列程式碼範例顯示如何使用這些參數來定義訂閱的範圍：

### 訂閱所有裝置的所有事件


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents();
	});
```

### 訂閱特定類型之所有裝置的所有事件

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("mydeviceType");
	});
```

### 訂閱所有裝置的特定事件


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("+","+","myevent");
	});
```

### 訂閱兩個以上不同裝置的特定事件

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","myevent");
		appClient.subscribeToDeviceEvents("myOtherDeviceType","device02","myevent");
	});
```

### 訂閱以 JSON 格式發佈的所有事件


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","+","json");

	});
```

**附註**：單一用戶端可以支援多個訂閱。

### 處理裝置的事件


若要處理訂閱所收到的事件，請實作裝置事件回呼方法。{{site.data.keyword.iot_short_notm}} 應用程式用戶端會傳送事件 `deviceEvent`。這個函數具有下列內容：

- deviceType
- deviceId
- eventType
- format
- payload
- topic

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","+","json");

	});
	appClient.on("deviceEvent", function (deviceType, deviceId, eventType, format, payload) {

		console.log("Device Event from :: "+deviceType+" : "+deviceId+" of event "+eventType+" with payload : "+payload);

	});
```


## 訂閱裝置狀態
{: #subscribing_device_status}

依預設，當您訂閱裝置狀態時，會收到所有已連接裝置的狀態更新。請使用 type 及 ID 參數，以控制訂閱的範圍。單一用戶端可支援多個訂閱。

### 訂閱所有裝置的狀態更新

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus();

	});
```

### 訂閱特定類型之所有裝置的狀態更新


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType");

	});
```

### 訂閱兩個不同裝置的狀態更新

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType","device01");
		appClient.subscribeToDeviceStatus("myOtherDeviceType","device02");

	});
```

### 處理裝置的狀態更新

若要處理訂閱所收到的狀態更新，請實作裝置狀態回呼方法。{{site.data.keyword.iot_short_notm}} 應用程式用戶端會傳送事件 `deviceStatus`。這個函數具有下列內容：

-   deviceType
-   deviceId
-   payload
-   topic

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType","device01");
		appClient.subscribeToDeviceStatus("myOtherDeviceType","device02");

	});
	appClient.on("deviceStatus", function (deviceType, deviceId, payload, topic) {

		console.log("Device status from :: "+deviceType+" : "+deviceId+" with payload : "+payload);

	});
```


## 發佈裝置的事件
{: #publishing_device_events}


應用程式可以發佈事件，就彷彿事件是源自裝置一樣。此函數需要下列內容：

-   deviceType
-   deviceId
-   eventType
-   format
-   data


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50};
		myData = JSON.stringify(myData);
		appClient.publishDeviceEvent("myDeviceType","device01", "myEvent", "json", myData);

	});
```


## 將指令發佈至裝置
{: #publishing_commands_devices}

應用程式可對連接的裝置發佈指令。此函數需要下列內容：

-   deviceType
-   deviceId
-   eventType
-   format
-   data

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'DelaySeconds' : 10};
		myData = JSON.stringify(myData);
		appClient.publishDeviceCommand("myDeviceType","device01", "reboot", "json", myData);

	});
```


## 中斷用戶端連線
{: #disconnect_client}

下列範例會中斷用戶端連線，也會釋放連線：

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'DelaySeconds' : 10}
		appClient.publishDeviceCommand("myDeviceType","device01", "reboot", "json", myData);

		appClient.disconnect();
	});
```


## 參考資料
{: #reference_nodejs}

下表說明用於此 Node.js 文件中所述函數的參數：

|參數|資料類型|說明|
|:---|:---|
|`deviceType`|字串|裝置類型。一般而言，deviceType 是執行特定作業的裝置分組，例如，"weatherballoon"。|
|`deviceId`|字串|裝置的 ID。一般而言，針對給定的裝置類型，deviceId 是該裝置的唯一 ID（例如，序號或 MAC 位址）。|
|`eventType`|字串|特定事件群組，例如 "status"、"warning" 及 "data"。|
|`format`|字串|格式可以是任何字串，例如 JSON。  |
|`data`|字典|訊息有效負載的資料。長度上限是 131072 個位元組。|
|`payload`|字串|訊息有效負載的資料。長度上限是 131072 個位元組。|
|`topic`|字串|發佈為裝置時，主題字串不包含裝置類型或裝置 ID；這些是取自用戶端 ID。例如，`iot-2/evt/event_id/fmt/format_string`。代表裝置發佈為應用程式或閘道時，主題必須包含裝置類型及裝置 ID。例如，`iot-2/type/device_type/id/device_id/evt/event_id/fmt/format_string`。|
