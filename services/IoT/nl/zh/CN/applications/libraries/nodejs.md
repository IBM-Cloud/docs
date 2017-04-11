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



# 针对应用程序开发者的 Node.js
{: #nodejs}

上次更新时间：2016 年 7 月 29 日
{: .last-updated}

您可以调整 Node.js 中的客户机库和样本来构建和定制应用程序，以用于在 {{site.data.keyword.iot_full}} 上与您的组织进行交互。
{:shortdesc}

使用提供的信息和示例通过 Node.js 开始开发应用程序。

## 下载 Node.js 客户机和资源
{: #nodejs_client_download}

要访问 {{site.data.keyword.iot_short_notm}} 的 Node.js 客户机库和其他可用资源，请转至 GitHub 中的 [iot-nodejs ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-watson-iot/iot-nodejs){: new_window} 存储库，并完成安装指示信息。


有关更多信息，请参阅以下资源：
- GitHub 中的[应用程序样本 ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-watson-iot/iot-nodejs/tree/master/samples){: new_window}。
- NPM 中的 [ibmiotf ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://www.npmjs.com/package/ibmiotf){: new_window}。
- 本文档的[参考](#reference_nodejs)部分。


## 构造方法
{: #constructor}

构造方法用于构建应用程序客户机实例，并接受包含以下属性的 JSON 配置文件：

| 属性     |描述     |
|----------------|----------------|
|`org` |组织标识。这是必需值。|
|`id`  |组织中应用程序的唯一标识。|
|`auth-key`   |用于将应用程序安全连接到 Watson IoT Platform 的 API 密钥。|
|`auth-token`   |用于将设备安全连接到 Watson IoT Platform 的 API 密钥令牌。|
|`type`  |预订的类型。指定 `shared` 可启用共享的预订。|


要使用 Quickstart，只有前两个属性是必需的。

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


### 使用配置文件


您还可以使用以下代码样本中概述的配置文件，而不直接传递 JSON 属性：

```

  var Client = require("ibmiotf");
	var appClientConfig = require("./application.json");
	var appClient = new Client.IotfApplication(appClientConfig);
```

确保 JSON 配置文件为以下格式：

```
    {
	  "org": 'xxxxx',
	  "id": 'myapp',
	  "auth-key": 'a-xxxxxxx-zenkqyfiea',
	  "auth-token": 'xxxxxxxxxx'
    }
```


## 连接到 {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

要连接到 {{site.data.keyword.iot_short_notm}}，请提交 *connect* 请求，如下所示：

```
  var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

	//Add your code here
	});
```

成功连接到 {{site.data.keyword.iot_short_notm}} 服务后，应用程序客户机会发送 `connect` 事件，以便可以在此回调函数中实现任何逻辑。



应用程序客户机在连接断开后会自动尝试重新连接。重新连接成功后，客户机将发送 `reconnect` 事件。



## 日志记录
{: #logging}

缺省情况下，只记录类型为 `warn` 的日志事件。如果要提高或降低日志记录级别，请使用 `log.setLevel` 函数。支持以下日志级别：
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

## 共享的预订
{: #shared_subscriptions}

使用共享的预订功能可构建可扩展应用程序，用于在应用程序的多个实例之间均衡消息负载。要启用负载均衡，请将 `type` 字段设置为 `shared`，如以下示例中所示：

```

	var appClientConfig = {
	  org: 'xxxxx',
	  id: 'myapp',
	  "auth-key": 'a-xxxxxx-xxxxxxxxx',
	  "auth-token": 'xxxxx!xxxxxxxx',
	  "type" : "shared" // 使此连接成为共享的预订
	};
	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//setting the log level to 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Add your code here
	});
```

## 处理错误
{: #handling_errors}

应用程序客户机遇到错误时，会生成 `error` 事件。

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

## 预订设备事件
{: #subscribing_device_events}

事件是设备用于将数据发布到 {{site.data.keyword.iot_short_notm}} 实例的机制。设备控制事件内容，并为其发送的每个事件指定名称。

{{site.data.keyword.iot_short_notm}} 实例接收到事件时，所接收事件的凭证会识别发送设备，这意味着一台设备无法冒充其他设备。


缺省情况下，应用程序会预订来自所有已连接设备的所有事件。使用设备类型、设备标识、事件和消息格式参数可控制预订的范围。以下代码样本显示了可以如何使用这些参数来定义预订范围：

### 预订来自所有设备的所有事件


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents();
	});
```

### 预订来自特定类型的所有设备的所有事件

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("mydeviceType");
	});
```

### 预订来自所有设备的特定事件


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("+","+","myevent");
	});
```

### 预订来自两个或更多不同设备的特定事件

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","myevent");
		appClient.subscribeToDeviceEvents("myOtherDeviceType","device02","myevent");
	});
```

### 预订以 JSON 格式发布的所有事件


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","+","json");

	});
```

**注**：单个客户机可支持多个预订。

### 处理来自设备的事件


要处理您的预订接收到的事件，请实现设备事件回调方法。{{site.data.keyword.iot_short_notm}} 应用程序客户机会发送事件 `deviceEvent`。此函数具有以下属性：

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


## 预订设备状态
{: #subscribing_device_status}

缺省情况下，预订设备状态时，会收到所有已连接设备的状态更新。使用类型和标识参数可控制预订范围。单个客户机可支持多个预订。

### 预订所有设备的状态更新

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus();

	});
```

### 预订特定类型的所有设备的状态更新


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType");

	});
```

### 预订两种不同设备的状态更新

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType","device01");
		appClient.subscribeToDeviceStatus("myOtherDeviceType","device02");

	});
```

### 处理来自设备的状态更新

要处理您的预订接收到的状态更新，请实现设备状态回调方法。{{site.data.keyword.iot_short_notm}} 应用程序客户机会发送事件 `deviceStatus`。此函数具有以下属性：

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


## 发布来自设备的事件
{: #publishing_device_events}


应用程序可以将事件当作源自设备的事件进行发布。此函数需要以下属性：

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


## 将命令发布到设备
{: #publishing_commands_devices}

应用程序可以将命令发布到已连接设备。此函数需要以下属性：

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


## 断开客户机连接
{: #disconnect_client}

以下样本断开客户机连接，同时释放连接：

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'DelaySeconds' : 10}
		appClient.publishDeviceCommand("myDeviceType","device01", "reboot", "json", myData);

		appClient.disconnect();
	});
```


## 参考
{: #reference_nodejs}

下表描述了此 Node.js 文档中所述函数中使用的参数：

|参数|数据类型|描述|
|:---|:---|
|`deviceType`|字符串|设备类型。通常，deviceType 是对执行特定任务的设备的一种分组，例如“weatherballoon”。|
|`deviceId`|字符串|设备的标识。通常，对于给定设备类型，deviceId 是该设备的唯一标识，例如序列号或 MAC 地址。|
|`eventType`|字符串|特定事件组，例如“status”、“warning”和“data”。|
|`format`|字符串|格式可以为任意字符串，例如 JSON。  |
|`data`|字典|消息有效内容的数据。最大长度为 131072 字节。|
|`payload`|字符串|消息有效内容的数据。最大长度为 131072 字节。|
|`topic`|字符串|发布为设备时，topic 字符串不包含设备类型或设备标识；这两个值取自客户机标识。例如，`iot-2/evt/event_id/fmt/format_string`。代表设备发布为应用程序或网关时，topic 必须包含设备类型和设备标识。例如，`iot-2/type/device_type/id/device_id/evt/event_id/fmt/format_string`。|
