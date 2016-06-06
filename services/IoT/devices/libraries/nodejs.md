---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Node.js for device developers
{: #nodejs}

For more information, see the following resources:

- The [iot-nodejs](https://github.com/ibm-messaging/iot-nodejs) repository in GitHub
- [Samples for device](https://github.com/ibm-messaging/iot-nodejs/tree/master/samples) in Github
- The [ibmiotf](https://www.npmjs.com/package/ibmiotf) repository on NPM

## Constructor
{: #constructor}

The constructor builds the device client instance. It accepts a configuration json containing the following definitions:

- ``org`` - Your organization ID
- ``type`` - The type of your device
- ``id`` - The ID of your device
- ``auth-method`` - Method of authentication (the only value currently supported is ``token``)
- ``auth-token`` - API key token (required if auth-method is ``token``)

If you want to use Quickstart, then send only the first three properties.

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

Instead of passing the configuration directly, you can use a JSON configuration file to provide the required configuration properties, as outlined in the following example:


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

You can connect to the {{site.data.keyword.iot_full}} by calling the *connect* function.

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

After the successful connection to the {{site.data.keyword.iot_short_notm}} service, the device client sends a *connect* event. This means that all of the device logic can be implemented inside this callback function.

The device client automatically tries to reconnect when it loses connection. When the reconnection is successful, the client emits a *reconnect* event.

## Logging
{: #logging}

By default, only log events of type ```warn``` are recorded. If you want to increase or decrease the  logging level, use the *log.setLevel* function. The supported log levels are:
- *trace
- debug
- info
- warn
- error*


```
	var iotf = require("ibmiotf");
	var config = require("./device.json");

	var deviceClient = new iotf.IotfDevice(config);

	//setting the log level to debug. By default its 'warn'
	deviceClient.log.setLevel('debug');

```


## Publishing events
{: #publishing_events}

Events are the mechanism by which devices publish data to the {{site.data.keyword.iot_short_notm}}. The device controls the content of the event and assigns a name for each event it sends.

When an event is received by the {{site.data.keyword.iot_short_notm}} instance, the credentials of the received event identify the sending device, making it impossible for a device to impersonate another device.

You can increase the quality of service(QoS) level for events that are published. Events with a higher QoS level than zero can take longer to publish due to the extra confirmation receipt information that is included.

**Note:** The Quickstart flow mode supports only a QoS level of zero.


Events can be published by using the following properties:

- eventType - Type of event to be published, for example, status or GPS.
- eventFormat - Format of the event, for example JSON.
- data - Payload of the event, which must be a buffer string
- QoS - MQTT quality of service for the publish event. Supported values are 0,1, and 2.

```
    var deviceClient = new Client.IotfDevice(config);

    deviceClient.connect();

    deviceClient.on("connect", function () {
       //publishing event using the default quality of service
       deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

       //publishing event using the user-defined quality of service
       var myQosLevel=2
       deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}', myQosLevel);
  });

```

## Handling commands
{: #handling_commands}

When the device client connects, it automatically subscribes to any command for this device. To process specific commands you need to register a command callback function. The device client sends *command* when a command is received. The callback function has the following properties.

-   commandName - Name of the command that was invoked
-   format - For example, JSON or XML
-   payload - Payload for the command
-   topic - Actual topic where the command was received

```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	deviceClient.on("connect", function () {
		//publishing event using the default quality of service
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

When the device clients encounters an error, it emits an *error* event.

```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	deviceClient.on("connect", function () {
		//publishing event using the default quality of service
		deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

	});

	deviceClient.on("error", function (err) {
		console.log("Error : "+err);
	});
	....

```

## Disconnecting the client
{: #disconnecting_client}

The following sample outlines how you can disconnect the client and release the connection:

```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	client.on("connect", function () {
		//publishing event using the default quality of service
		client.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

		//publishing event using the user-defined quality of service
		var myQosLevel=2
		client.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}', myQosLevel);

		//disconnect the client
		client.disconnect();
	});

	....
```
