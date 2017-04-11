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


# Node.js for device developers
{: #nodejs}

You can adapt the client libraries and samples in Node.js to build and develop device code that interacts with your organization on {{site.data.keyword.iot_full}}.
{:shortdesc}

Use the information and examples that are provided to start developing your devices by using Node.js.

## Downloading the Node.js client and resources
{: #node.js_client_downloads}

To access the Node.js client libraries for {{site.data.keyword.iot_short_notm}} and other available resources, go to the [iot-nodejs ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-nodejs){: new_window} repository in GitHub and complete the installation instructions.


For more information, see the following resources:

- [Samples for devices ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-nodejs/tree/master/samples){: new_window} in Github
- The [ibmiotf ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://www.npmjs.com/package/ibmiotf){: new_window} repository on NPM

## Constructor
{: #constructor}

The constructor builds the device client instance. It accepts a configuration JSON that contains the following definitions:

|Definition |Description |
|:---|:---|
|`org` |Your organization ID.|
|`type`  |The type of your device. Typically, the deviceType is a grouping for devices that perform a specific task, for example "weatherballoon".|
|`id`  |The ID of your device. Typically, for a given device type, the deviceId is a unique identifier of that device, for example a serial number or MAC address.|
|`auth-method`   |The method of authentication to be used. The only value that is currently supported is `token`.|
|`auth-token`   |An authentication token to securely connect your device to Watson IoT Platform. This field is required if `auth-method` is `token`.|

**Note:** If you would like to use the Quickstart service, then you need to submit only the first three properties.

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

### Using a configuration file

Instead of passing the configuration directly, you can use a JSON configuration file to provide the required configuration properties, as shown in the following example:


```  
    var iotf = require("ibmiotf");
    var config = require("./device.json");
    var deviceClient = new iotf.IotfDevice(config);  
```
The `device.json` configuration file must be in the following format:

```
	{
	  "org": "xxxxx",
	  "type": "raspi",
	  "id": "pi1",
	  "auth-method" : "token",
	  "auth-token" : "xxxxxxxxxxxxxxxx"
	}

```  

## Connecting to the {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

You can connect to the {{site.data.keyword.iot_short_notm}} by calling the `connect` function.

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

After the successful connection to the {{site.data.keyword.iot_short_notm}} service, the device client sends a `connect` event. This process means that all of the device logic can be implemented inside this callback function.

The device client automatically tries to reconnect when it loses connection. When the reconnection is successful, the client sends a `reconnect` event.

## Logging
{: #logging}

By default, only log events of type *warn* are recorded. If you want to increase or decrease the logging level, use the log.setLevel function. The following log levels are supported:
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


## Publishing events
{: #publishing_events}

Events are the mechanism by which devices publish data to the {{site.data.keyword.iot_short_notm}}. The device controls the content of the event and assigns a name for each event that it sends.

When an event is received by the {{site.data.keyword.iot_short_notm}} instance, the credentials of the received event identify the sending device, which means that a device cannot impersonate another device.

You can increase the quality of service (QoS) level for events that are published. Events with a QoS level that is higher than `0` can take longer to be published because of the extra confirmation receipt information that is included.

**Note:** The Quickstart flow mode supports only a QoS level of `0`.


Events can be published with the following properties:

|Property |Description|
|:---|:---|
|`eventType`  | The type of event to be published, for example, status or GPS. |  
|`eventFormat`  |The format of the event, for example, JSON. |
|`data`  | The payload of the event, which must be a buffer string. |
|`QoS`  | The MQTT quality of service for the publish event. Supported values are 0, 1, and 2.|


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

## Handling commands
{: #handling_commands}

When the device client connects, it automatically subscribes to any command for this device. To process specific commands, you must register a command callback function. The device client invokes the command callback function when a command is received. The callback function has the following properties:

|Property |Description|
|:---|:---|
|`commandName`  | A string, specifying the name of the command that was invoked. |  
|`format`  | A string, specifying the format of the event, for example, JSON. |
|`payload`  | A string, specifying the data for the command payload.  |
|`topic`  | When publishing as a device, the topic string does not include the device type or device ID; these are taken from the client ID.  For example, `iot-2/evt/event_id/fmt/format_string`.  When publishing as an application or gateway on behalf of a device, the topic must include the device type and device ID.  For example `iot-2/type/device_type/id/device_id/evt/event_id/fmt/format_string`.|


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

## Handling errors
{: #handling_errors}

When the device client encounters an error, it sends an *error* event.

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

## Disconnecting the client
{: #disconnecting_client}

The following sample shows how you can disconnect the client and release the connection:

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
