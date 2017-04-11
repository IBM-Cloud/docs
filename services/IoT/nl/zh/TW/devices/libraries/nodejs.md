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


# 適用於裝置開發人員的 Node.js
{: #nodejs}

您可以用 Node.js 調整用戶端程式庫及範例，來建置及開發裝置程式碼，在 {{site.data.keyword.iot_full}} 上與組織互動。
{:shortdesc}

請使用所提供的資訊及範例，利用 Node.js 開始開發您的裝置。

## 下載 Node.js 用戶端及資源
{: #node.js_client_downloads}

若要存取適用於 {{site.data.keyword.iot_short_notm}} 的 Node.js 用戶端程式庫及其他可用的資源，請移至 GitHub 中的 [iot-nodejs ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-watson-iot/iot-nodejs){: new_window} 儲存庫，並完成安裝指示。


如需相關資訊，請參閱下列資源：

- Github 中的[裝置的範例 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-watson-iot/iot-nodejs/tree/master/samples){: new_window}
- NPM 上的 [ibmiotf ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.npmjs.com/package/ibmiotf){: new_window} 儲存庫

## 建構子
{: #constructor}

建構子會建置裝置用戶端實例。其接受包含下列定義的配置 JSON：

|定義 |說明 |
|:---|:---|
|`org` |您的組織 ID。|
|`type`  |您的裝置類型。一般而言，deviceType 是執行特定作業的裝置分組，例如，"weatherballoon"。|
|`id`  |您的裝置 ID。一般而言，針對給定的裝置類型，deviceId 是該裝置的唯一 ID（例如，序號或 MAC 位址）。|
|`auth-method`   |要使用的鑑別方法。目前唯一支援的值是 `token`。|
|`auth-token`   |將裝置安全地連接至 Watson IoT Platform 的鑑別記號。如果 `auth-method` 為 `token`，則這是必要欄位。|

**附註：**如果您想要使用 Quickstart 服務，則只需要提交前三個內容。

```
    var iotf = require("ibmiotf");
    var config = {
		"org" : "organization",
		"id" : "deviceId",
		"type" : "deviceType",
		"auth-method" : "token",
		"auth-token" : "authToken"
    };


    var deviceClient = new iotf.IotfDevice(config);
```

### 使用配置檔

您可以使用 JSON 配置檔來提供必要配置內容，而非直接傳遞配置，如下列範例所示：


```  
    var iotf = require("ibmiotf");
    var config = require("./device.json");
    var deviceClient = new iotf.IotfDevice(config);  
```
`device.json` 配置檔必須為下列格式：

```
	{
	  "org": "xxxxx",
	  "type": "raspi",
	  "id": "pi1",
	  "auth-method" : "token",
	  "auth-token" : "xxxxxxxxxxxxxxxx"
	}

```  

## 連接至 {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

您可以呼叫 `connect` 函數來連接至 {{site.data.keyword.iot_short_notm}}。

```
	var iotf = require("ibmiotf");
	var config = require("./device.json");

	var deviceClient = new iotf.IotfDevice(config);

	//setting the log level to debug. By default its 'warn'
	deviceClient.log.setLevel('debug');

	deviceClient.connect();

	deviceClient.on('connect', function(){
		var i=0;
		console.log("connected");
		setInterval(function function_name () {
			i++;
			deviceClient.publish('myevt', 'json', '{"value":'+i+'}', 2);
		},2000);
	});

```

在順利連線至 {{site.data.keyword.iot_short_notm}} 服務之後，裝置用戶端會傳送 `connect` 事件。此程序表示，可在此回呼函數內實作所有裝置邏輯。

裝置用戶端會在中斷連線時自動嘗試重新連接。重新連線成功時，用戶端會傳送 `reconnect` 事件。

## 記載
{: #logging}

預設只會記錄類型 *warn* 的日誌事件。如果您要提高或降低記載層次，請使用 log.setLevel 函數。支援下列記載層次：
- trace
- debug
- info
- warn
- error

```
	var iotf = require("ibmiotf");
	var config = require("./device.json");

	var deviceClient = new iotf.IotfDevice(config);

	//setting the log level to debug. By default its 'warn'
	deviceClient.log.setLevel('debug');

```


## 發佈事件
{: #publishing_events}

事件是裝置用來將資料發佈至 {{site.data.keyword.iot_short_notm}} 的機制。裝置會控制事件的內容，並指派名稱給它傳送的每個事件。

{{site.data.keyword.iot_short_notm}} 實例收到事件時，所收到事件的認證可識別傳送端裝置，這表示，裝置無法假冒另一個裝置。

您可以為發佈的事件提高服務品質 (QoS) 水準。QoS 水準高於 `0` 的事件可能需要較長的發佈時間，因為包含額外的確認接收資訊。

**附註：**Quickstart 流程模式僅支援 QoS 水準 `0`。


事件可以搭配下列內容發佈：

|內容 |說明|
|:---|:---|
|`eventType`  | 發佈的事件類型，例如，status 或 GPS。 |  
|`eventFormat`  |事件的格式，例如，JSON。 |
|`data`  | 事件的有效負載，必須是緩衝區字串。 |
|`QoS`  | 發佈事件的 MQTT 服務品質。支援的值為 0、1 及 2。|


```
    var deviceClient = new Client.IotfDevice(config);

    deviceClient.connect();

    deviceClient.on("connect", function () {
       //publish an event at the default quality of service
       deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

       //publish an event at the user-defined quality of service
       var myQosLevel=2
       deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}', myQosLevel);
  });

```

## 處理指令
{: #handling_commands}

當裝置用戶端連接時，它會自動訂閱此裝置的任何指令。若要處理特定指令，您必須登錄指令回呼函數。收到指令時，裝置用戶端會呼叫指令回呼函數。回呼函數具有下列內容：

|內容 |說明|
|:---|:---|
|`commandName`  | 字串，指定呼叫的指令名稱。 |  
|`format`  | 字串，指定事件的格式，例如，JSON。 |
|`payload`  | 字串，指定指令有效負載的資料。  |
|`topic`  | 發佈為裝置時，主題字串不包含裝置類型或裝置 ID；這些是取自用戶端 ID。例如，`iot-2/evt/event_id/fmt/format_string`。代表裝置發佈為應用程式或閘道時，主題必須包含裝置類型及裝置 ID。例如，`iot-2/type/device_type/id/device_id/evt/event_id/fmt/format_string`。|


```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	deviceClient.on("connect", function () {
		//publish an event at the default quality of service
		deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

	});

	deviceClient.on("command", function (commandName,format,payload,topic) {
		if(commandName === "blink") {
			console.log(blink);
			//function to be performed for this command
			blink(payload);
		} else {
			console.log("Command not supported.. " + commandName);
		}
	});

```

## 處理錯誤
{: #handling_errors}

裝置用戶端發生錯誤時，會傳送 *error* 事件。

```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	deviceClient.on("connect", function () {
		//publish an event at the default quality of service
		deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

	});

	deviceClient.on("error", function (err) {
		console.log("Error : "+err);
	});
	....

```

## 中斷用戶端連線
{: #disconnecting_client}

下列範例顯示您如何中斷用戶端連線及釋出連線：

```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	client.on("connect", function () {
		//publish an event at the default quality of service
		client.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

		//publishing event at the user-defined quality of service
		var myQosLevel=2
		client.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}', myQosLevel);

		//disconnect the client
		client.disconnect();
	});

	....
```
