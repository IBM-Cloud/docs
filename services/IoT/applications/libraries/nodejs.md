---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-07-29"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# Node.js for application developers
{: #nodejs}

Last updated: 29 July 2016
{: .last-updated}

You can adapt the client libraries and samples in Node.js to build and customize applications that interact with your organization on {{site.data.keyword.iot_full}}.
{:shortdesc}

Use the information and examples that are provided to start developing your applications by using Node.js.

## Downloading the Node.js client and resources
{: #nodejs_client_download}

To access the Node.js client libraries for {{site.data.keyword.iot_short_notm}} and other available resources, go to the [iot-nodejs](https://github.com/ibm-watson-iot/iot-nodejs) repository in GitHub and complete the installation instructions.


For more information, see the following resources:
- [Application samples](https://github.com/ibm-watson-iot/iot-nodejs/tree/master/samples) in GitHub.
- [ibmiotf](https://www.npmjs.com/package/ibmiotf) on NPM.
- [Reference](#reference_nodejs) section of this document.


## Constructor
{: #constructor}

The constructor builds the application client instance and accepts a JSON configuration file that contains the following properties:

| Property     |Description     |
|----------------|----------------|
|`org` |Your organization ID. This is a required value.|
|`id`  |The unique ID of your application within your organization.|
|`auth-key`   |An API key to securely connect your application to Watson IoT Platform.|
|`auth-token`   |An API key token to securely connect your device to Watson IoT Platform.|
|`type`  |The type of subscription. Specify `shared` to enable shared subscription.|


To use Quickstart, only the first two properties are required.

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


### Using a configuration file


Instead of passing the JSON properties directly, you can also use a configuration file which is outlined in the following code sample:

```

  var Client = require("ibmiotf");
	var appClientConfig = require("./application.json");
	var appClient = new Client.IotfApplication(appClientConfig);
```

Ensure that the JSON configuration file is in the following format:

```
    {
	  "org": 'xxxxx',
	  "id": 'myapp',
	  "auth-key": 'a-xxxxxxx-zenkqyfiea',
	  "auth-token": 'xxxxxxxxxx'
    }
```


## Connecting to {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

To connect to {{site.data.keyword.iot_short_notm}}, submit a *connect* request, as follows:

```
  var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

	//Add your code here
	});
```

After successfully connecting to the {{site.data.keyword.iot_short_notm}} service, the application client sends a `connect` event, so any logic can be implemented inside this callback function.



The application client automatically tries to reconnect when it loses connection. When the reconnection is successful, the client sends a `reconnect` event.



## Logging
{: #logging}

By default, only log events of type ``warn`` are recorded. If you want to increase or decrease the  logging level, use the `log.setLevel` function. The following log levels are supported:
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

## Shared subscriptions
{: #shared_subscriptions}

Use the shared subscription feature to build scalable applications that balance the load of messages across multiple instances of the application. To enable load balancing, set the `type` field to `shared`, which is shown in the following example:

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

## Handling errors
{: #handling_errors}

When the application client encounters an error, an `error` event is generated.

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

## Subscribing to device events
{: #subscribing_device_events}

Events are the mechanism by which devices publish data to the {{site.data.keyword.iot_short_notm}} instance. The device controls the content of the event and assigns a name for each event that it sends.

When an event is received by the {{site.data.keyword.iot_short_notm}} instance, the credentials of the received event identify the sending device, which means that a device cannot impersonate another device.


By default, applications subscribe to all events from all connected devices. Use the device type, device ID, event, and message format parameters to control the scope of the subscription. The following code samples show how you can use these parameters to define the scope of a subscription:

### Subscribing to all events from all devices


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents();
	});
```

### Subscribing to all events from all devices of a specific type

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("mydeviceType");
	});
```

### Subscribing to a specific event from all devices


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("+","+","myevent");
	});
```

### Subscribing to a specific event from two or more different devices

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","myevent");
		appClient.subscribeToDeviceEvents("myOtherDeviceType","device02","myevent");
	});
```

### Subscribing to all events that are published in JSON format


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","+","json");

	});
```

**Note**: A single client can support multiple subscriptions.

### Handling events from devices


To process the events that are received by your subscriptions, implement a device event callback method. The {{site.data.keyword.iot_short_notm}} application client sends the event ``deviceEvent``. This function has the following properties:

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


## Subscribing to device status
{: #subscribing_device_status}

By default, when you subscribe to device status, status updates are received for all connected devices. Use the type and ID parameters to control the scope of the subscription. A single client can support multiple subscriptions.

### Subscribing to status updates for all devices

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus();

	});
```

### Subscribing to status updates for all devices of a specific type


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType");

	});
```

### Subscribing to status updates for two different devices

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType","device01");
		appClient.subscribeToDeviceStatus("myOtherDeviceType","device02");

	});
```

### Handling status updates from devices

To process the status updates that are received by your subscriptions, implement a device status callback method. The {{site.data.keyword.iot_short_notm}} application client sends the event `deviceStatus`. This function has the following properties:

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


## Publishing events from devices
{: #publishing_device_events}


Applications can publish events as if they originated from a device. The function requires the following properties:

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


## Publishing commands to devices
{: #publishing_commands_devices}

Applications can publish commands to connected devices. The function requires the following properties:

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


## Disconnecting the client
{: #disconnect_client}

The following sample disconnects the client and also releases the connections:

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'DelaySeconds' : 10}
		appClient.publishDeviceCommand("myDeviceType","device01", "reboot", "json", myData);

		appClient.disconnect();
	});
```


## Reference
{: #reference_nodejs}

The following table describes the parameters that are used in the functions that are described in this Node.js documentation:

|Parameter|Data type|Description|
|:---|:---|
|`deviceType`|String|The device type. Typically, the deviceType is a grouping for devices that perform a specific task, for example "weatherballoon".|
|`deviceId`|String|The ID of the device. Typically, for a given device type, the deviceId is a unique identifier of that device, for example a serial number or MAC address.|
|`eventType`|String|A group of specific events, for example "status", "warning" and "data".|
|`format`|String|The format can be any string, for example JSON.  |
|`data`|Dictionary|The data for the message payload. Maximum length is 131072 bytes.|
|`payload`|String|The data for the message payload. Maximum length is 131072 bytes.|
|`topic`|String|When publishing as a device, the topic string does not include the device type or device ID; these are taken from the client ID.  For example, `iot-2/evt/event_id/fmt/format_string`.  When publishing as an application or gateway on behalf of a device, the topic must include the device type and device ID.  For example `iot-2/type/device_type/id/device_id/evt/event_id/fmt/format_string`.|
