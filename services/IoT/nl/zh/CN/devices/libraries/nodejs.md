---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-09-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 针对设备开发者的 Node.js
{: #nodejs}

您可以调整 Node.js 中的客户机库和样本来构建和开发设备代码，以用于在 {{site.data.keyword.iot_full}} 上与您的组织进行交互。
{:shortdesc}

使用提供的信息和示例通过 Node.js 开始开发设备。

## 下载 Node.js 客户机和资源
{: #node.js_client_downloads}

要访问 {{site.data.keyword.iot_short_notm}} 的 Node.js 客户机库和其他可用资源，请转至 GitHub 中的 [iot-nodejs](https://github.com/ibm-watson-iot/iot-nodejs) 存储库，并完成安装指示信息。


有关更多信息，请参阅以下资源：

- Github 中的[用于设备的样本](https://github.com/ibm-watson-iot/iot-nodejs/tree/master/samples)
- NPM 上的 [ibmiotf](https://www.npmjs.com/package/ibmiotf) 存储库

## 构造方法
{: #constructor}

构造方法用于构建设备客户机实例。它接受包含以下定义的配置 JSON：

|定义 |描述 |
|:---|:---|
|`org` |组织标识。|
|`type`  |设备类型。通常，deviceType 是对执行特定任务的设备的一种分组，例如“weatherballoon”。|
|`id`  |设备的标识。通常，对于给定设备类型，deviceId 是该设备的唯一标识，例如序列号或 MAC 地址。|
|`auth-method`   |要使用的认证方法。当前支持的唯一值是 `token`。|
|`auth-token`   |用于将设备安全连接到 Watson IoT Platform 的认证令牌。如果 `auth-method` 为 `token`，那么此字段是必填的。|

**注：**如果要使用 Quickstart 服务，那么需要仅提交前三个属性。

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

### 使用配置文件

您可以使用 JSON 配置文件来提供必需的配置属性，而不直接传递配置，如以下示例中所示：


```  
    var iotf = require("ibmiotf");
    var config = require("./device.json");
    var deviceClient = new iotf.IotfDevice(config);  
```
`device.json` 配置文件必须为以下格式：

```
	{
	  "org": "xxxxx",
	  "type": "raspi",
	  "id": "pi1",
	  "auth-method" : "token",
	  "auth-token" : "xxxxxxxxxxxxxxxx"
	}

```  

## 连接到 {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

可以通过调用 `connect` 函数来连接到 {{site.data.keyword.iot_short_notm}}。

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

成功连接到 {{site.data.keyword.iot_short_notm}} 服务后，设备客户机会发送 `connect` 事件。此过程意味着可以在此回调函数内部实现所有设备逻辑。

设备客户机在连接断开后会自动尝试重新连接。重新连接成功后，客户机将发送 `reconnect` 事件。

## 日志记录
{: #logging}

缺省情况下，只记录类型为 *warn* 的日志事件。如果要提高或降低日志记录级别，请使用 log.setLevel 函数。支持以下日志级别：
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


## 发布事件
{: #publishing_events}

事件是设备将数据发布到 {{site.data.keyword.iot_short_notm}} 时所采用的机制。设备控制事件内容，并为其发送的每个事件指定名称。

{{site.data.keyword.iot_short_notm}} 实例接收到事件时，所接收事件的凭证会识别发送设备，这意味着一台设备无法冒充其他设备。

可以提高已发布事件的服务质量 (QoS) 级别。QoS 级别大于 `0` 的事件发布所用时间可能更长，因为包含额外的接收确认信息。

**注：**Quickstart 流方式仅支持 QoS 级别 `0`。


可以使用以下属性来发布事件：

|属性 |描述|
|:---|:---|
|`eventType`  | 要发布的事件的类型，例如 status 或 GPS。 |  
|`eventFormat`  |事件的格式，例如 JSON。 |
|`data`  | 事件的有效内容，必须为缓冲区字符串。 |
|`QoS`  | 发布事件的 MQTT 服务质量。支持的值为 0、1 和 2。|


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

## 处理命令
{: #handling_commands}

设备客户机进行连接时，会自动预订此设备的任何命令。要处理特定命令，必须注册命令回调函数。收到命令时，设备客户机会调用命令回调函数。回调函数具有以下属性：

|属性 |描述|
|:---|:---|
|`commandName`  | 字符串，指定调用的命令的名称。 |  
|`format`  | 字符串，指定事件的格式，例如 JSON。 |
|`payload`  | 字符串，指定命令有效内容的数据。  |
|`topic`  | 发布为设备时，topic 字符串不包含设备类型或设备标识；这两个值取自客户机标识。例如，`iot-2/evt/event_id/fmt/format_string`。代表设备发布为应用程序或网关时，topic 必须包含设备类型和设备标识。例如，`iot-2/type/device_type/id/device_id/evt/event_id/fmt/format_string`。|


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

## 处理错误
{: #handling_errors}

设备客户机遇到错误时，会发送 *error* 事件。

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

## 断开客户机连接
{: #disconnecting_client}

以下样本显示了可以如何断开客户机连接并释放连接：

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
