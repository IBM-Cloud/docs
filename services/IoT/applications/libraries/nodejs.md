---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# Node.js for application developers
{: #nodejs}


For more information, see:
- [Client libraries and samples](https://github.com/ibm-messaging/iot-nodejs) in GitHub.
- [Device samples](https://github.com/ibm-messaging/iot-nodejs/tree/master/samples) in GitHub.
- [ibmiotf](https://www.npmjs.com/package/ibmiotf) on NPM.


## Application client
{: #app_client}

*ApplicationClient* is an application client for the {{site.data.keyword.iot_full}} service. This section contains information on how {{site.data.keyword.iot_short_notm}} applications interact with devices.

## Constructor
{: #constructor}

The constructor builds the application client instance, and accepts a JSON configuration file that contains the following properties:

| Definition     |Description     |
|----------------|----------------|
|``org`` |Your organization ID|
|``id`` |The unique ID of your application within your organization|
|``auth-key``|API key|
|`auth-token``|API key token|
|`type``|Specify `shared` to enable shared subscription|

To use Quickstart, the first two properties are required only.


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


Instead of passing the JSON properties directly, you can also use a configuration file, as outlined in the following code sample:

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

After successfully connecting to the {{site.data.keyword.iot_short_notm}} service, the application client sends a *connect* event. So all the logic can be implemented inside this callback function.



The application client automatically tries to reconnect when it loses connection. When the reconnection is successful, the client emits a *reconnect* event.



## Logging
{: #logging}

By default, only log events of type ```warn``` are recorded. If you want to increase or decrease the  logging level, use the *log.setLevel* function. The supported log levels are:
- *trace
- debug
- info
- warn
- error*.

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

Use the shared subscription feature to build scalable applications that balance the load of messages across multiple instances of the application. To enable load balancing, set the 'type' field to 'shared', as outlined in the following example:

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

When the application client encounters an error, an *error* event is generated.

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

When an event is received by the {{site.data.keyword.iot_short_notm}} instance, the credentials of the received event identify the sending device, making it impossible for a device to impersonate another device.




By default, applications subscribe to all events from all connected devices. Use the type, ID, event, and msgFormat parameters to control the scope of the subscription. A single client can support multiple subscriptions. The following code samples provide examples of how to subscribe to devices that are dependent on device type, ID, event, and msgFormat parameters.

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

### Subscribing to all events published by a device in JSON format


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","+","json");

	});
```

### Handling events from devices


To process the events that are received by your subscriptions, implement a device event callback method. The {{site.data.keyword.iot_short_notm}} application client emits the event *deviceEvent*. This function has the following properties:

- deviceType
- deviceId
- eventType
- format
- payload - Device event payload
- topic - Original topic

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

To process the status updates received by your subscriptions, implement a device status callback method. The {{site.data.keyword.iot_short_notm}} application client emits the event *deviceStatus*. This function has the following properties:

-   deviceType
-   deviceId
-   payload - Device status payload
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


Applications can publish events as if they originated from a device. The function requires:

-   DeviceType
-   Device ID
-   Event Type
-   Format
-   Data

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

Applications can publish commands to connected devices. The function requires:



-   DeviceType
-   Device ID
-   Command Type
-   Format
-   Data

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
