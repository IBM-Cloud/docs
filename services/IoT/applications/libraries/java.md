---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Java for application developers
{: #java}


You can build and customize applications that interact with your organization on {{site.data.keyword.iot_full}} by using Java™. A Java client library for {{site.data.keyword.iot_short_notm}}, documentation, and examples are provided to help you get started with application development.

{:shortdesc}

## Downloading the Java client and resources
{: #java_client_download}

Last updated: 25 October 2016
{: .last-updated}

To access the Java client libraries and samples for {{site.data.keyword.iot_short_notm}}, go to the [iot-java](https://github.com/ibm-watson-iot/iot-java) repository in GitHub and complete the installation instructions.


## Constructor
{: #constructor}

The constructor builds the client instance and accepts the `Properties` object, which contains the following definitions:

| Definition     |Description     |
|----------------|----------------|
|`org` |A required value that must be set to your organization ID. If you are using a Quickstart flow, specify `quickstart`.|
|`id` |The unique ID of the application in your organization.|
|`auth-method`  |The method of authentication. The only method that is supported is `apikey`.|
|`auth-key`   |An optional API key, which you must specify when you set the value of auth-method to `apikey`.|
|`auth-token`   |An API key token, which is also required when you set the value of auth-method to `apikey`. |
|`clean-session`|A true or false value that is required only if you want to connect the application in durable subscription mode. By default, `clean-session` is set to `true`.|
|`Port`|The port number to connect to. Specify either 8883 or 443. If you do not specify a port number, the client connects to {{site.data.keyword.iot_short_notm}} on port number 8883 by default.|
|`MaxInflightMessages`  |Sets the maximum number of in-flight messages for the connection. The default value is 100.|
|`Automatic-Reconnect`  |A true or false value that is required when you want to automatically reconnect the device to {{site.data.keyword.iot_short_notm}} while it is in a disconnected state. The default value is false.|
|`Disconnected-Buffer-Size`|The maximum number of messages that can be stored in memory while the client is disconnected. The default value is 5000.|
|`shared-subscription`|A boolean value that must be set to true if you would like to build scalable applications that balance the load of messages across multiple instances of the application. For more information, see [Scalable applications](../mqtt.html#scalable_apps).

The `Properties` object creates definitions that are used to interact with the {{site.data.keyword.iot_short_notm}} module. If you do not specify the properties for this object, or if you specify `quickstart`, the client connects to the {{site.data.keyword.iot_short_notm}} Quickstart service as an unregistered device.

The following code sample shows how you can construct the application client (`ApplicationClient`) instance in `quickstart` mode:

```
    import com.ibm.iotf.client.app.ApplicationClient;
    import java.util.Properties;

    Properties options = new Properties();
    options.put("org", "quickstart");

    ApplicationClient myClient = new ApplicationClient(options);
```

The following code sample shows how you can construct the application client (`ApplicationClient`) instance in registered flow mode:

```
    Properties options = new Properties();
    options.put("org", "uguhsp");
    options.put("id", "app" + (Math.random() * 10000));
    options.put("Authentication-Method","apikey");
    options.put("API-Key", "<API-Key>");
    options.put("Authentication-Token", "<Authentication-Token>");

    ApplicationClient myClient = new ApplicationClient(options);
```

### Using a configuration file

Instead of including the `Properties` object directly, you can use a configuration file that contains the name-value pairs for the `Properties` object, as outlined in the following code sample:

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    ...
```
The specified application configuration file must be in the following format:

```
    [application]
    org=$orgId
    id=$myApplication
    auth-method=apikey
    auth-key=$key
    auth-token=$token
    enable-shared-subscription=true|false
```

## Connecting to the {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

To connect to the {{site.data.keyword.iot_short_notm}}, use the `connect()` function. The `connect()` function includes an optional boolean parameter called `autoRetry`, which determines whether the library tries to reconnect when there is an MqttException connection failure. By default, `autoRetry` is set to true. If an MqttSecurityException connection fails because incorrect device registration details are passed, the library does not attempt to reconnect, even if `autoRetry` is set to true.

To set the 'keep alive' interval for MQTT, you can optionally use the `setKeepAliveInterval(int)` method before you call the `connect()` function. The `setKeepAliveInterval(int)` value is  measured in seconds, and defines the maximum time interval between messages that are sent or received. When used, the client can detect when the server is no longer available without waiting for the end of the TCP/IP timeout period to be reached. The client ensures that at least one message travels across the network within each 'keep alive' interval period. If zero data-related messages are received during the timeout period, the client sends a small `ping` message, which the server acknowledges. The `setKeepAliveInterval(int)` is set to 60 seconds by default. To disable the 'keep alive' processing feature on the client, set the `setKeepAliveInterval(int)` value to 0.

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    myClient.setKeepAliveInterval(120);
    myClient.connect();
```

To control the number of retries that occur when there is a connection failure, specify an integer in the myClient.connect() function, as outlined in the following code snippet:

```
    DeviceClient myClient = new DeviceClient(options);
    myClient.setKeepAliveInterval(120);
    myClient.connect(10);
```

After your application clients successfully connect to the {{site.data.keyword.iot_short_notm}} service, they can subscribe to device events and statuses, and they can also publish device events and commands.

## Subscribing to device events
{: #subscribing_device_events}

Events are the mechanism by which devices publish data to {{site.data.keyword.iot_short_notm}}. The device controls the content of the event and assigns a name for each event that it sends.

When an event is received by the {{site.data.keyword.iot_short_notm}} instance, the credentials of the received event identify the sending device, which means that a device cannot impersonate another device.


By default, applications subscribe to all events from all connected devices. Use the device type, device ID, event, and message-format parameters to control the scope of the subscription. The following code samples show how you can use these parameters to define the scope of a subscription:

### Subscribing to all events from all devices


```
    myClient.connect();
    myClient.subscribeToDeviceEvents();
```
### Subscribing to all events from all devices of a specific type


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino");
```

### Subscribing to all events from a specific device


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee");
```
### Subscribing to a specific event from two or more different devices

```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee", "myEvent");
    myClient.subscribeToDeviceEvents("iotsample-arduino", "10aabbccddee", "myEvent");
```
### Subscribing to events that are published in JSON format


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee", "myEvent", "json", 0);
```

**Note**: A single client can support multiple subscriptions.

## Handling events from devices
{: #handling_device_events}

To process the events that are received by your subscriptions, register an event callback method. The messages are returned as an instance of the Event class, which has the following parameters:

|Parameter|Data type|Description|
|:---|:---|
|`event.device`|String|Uniquely identifies the device across all types of devices in the organization.|
|`event.deviceType`|String|Identifies the device type. Typically, the deviceType is a grouping for devices that do a specific task, for example, "weatherballoon" could be a device type.|
|`event.deviceId`|String|Represents the ID of the device. Typically, for a specific device type, the deviceId is a unique identifier of that device, for example a serial number or MAC address.|
|`event.event`|String|Typically used to group specific events, for example "status", "warning" and "data".|
|`event.format`|String|The format can be any string, for example JSON.  |
|`event.data`|Dictionary|The data for the message payload. Maximum length is 131072 bytes.|
|`event.timestamp`|Date and time|The date and time of the event|


The following code provides a sample implementation of the event callback:

```
  import com.ibm.iotf.client.app.Event;
  import com.ibm.iotf.client.app.EventCallback;
  import com.ibm.iotf.client.app.Command;

  import java.util.concurrent.BlockingQueue;
  import java.util.concurrent.LinkedBlockingQueue;

  /**
    * A sample Event callback class that processes the device events in a separate thread.
    *
    */
   class MyEventCallback implements EventCallback, Runnable {

	// A queue to hold and process the Events for smooth handling of MQTT messages
	private BlockingQueue<Event> evtQueue = new LinkedBlockingQueue<Event>();

	public void processEvent(Event e) {
		try {
			evtQueue.put(e);
		} catch (InterruptedException e1) {
			e1.printStackTrace();
		}
	}

	@Override
	public void processCommand(Command cmd) {
		System.out.println("Command received:: " + cmd);
	}

	@Override
	public void run() {
		while(true) {
			Event e = null;
			try {
				e = evtQueue.take();
				// In this example, the only output is the event
				System.out.println("Event:: " + e.getDeviceId() + ":" + e.getEvent() + ":" + e.getPayload());
			} catch (InterruptedException e1) {
				// Ignore the Interuppted exception, retry
				continue;
			}
		}
	}
    }
```

When the event callback is added to the ApplicationClient, the `processEvent()` method is invoked whenever an event is published that matches the subscription. The following snippet shows how to add the event callback into ApplicationClient instance:



```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToDeviceEvents();
```

Similar to subscribing to device events, the application can subscribe to commands that are sent to the devices. The following code sample shows how to subscribe to all commands for all of the devices in the organization:

```

    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToDeviceCommands();
```

Overloaded methods are available to control the command subscription. The `processCommand()` method is called when a command is sent to the device that matches the command subscription.


## Subscribing to device status
{: #subscribing_device_status}

Similar to subscribing to device events, applications can subscribe to device status, such as device connect and disconnect to {{site.data.keyword.iot_short_notm}}. By default, this subscription subscribes to status updates for all connected devices. Use the device type and device ID parameters to control the scope of the subscription. The following code samples show how you can use these parameters to define the scope of a subscription:

### Subscribe to status updates for all devices

```
    myClient.connect();
    myClient.subscribeToDeviceStatus();
```

### Subscribe to status updates for all devices of a specific type


```

    myClient.connect();
    myClient.subscribeToDeviceStatus("iotsample-arduino");
```

### Subscribe to status updates for two different devices


```

    myClient.connect();
    myClient.subscribeToDeviceStatus("iotsample-arduino", "00aabbccddee");
    myClient.subscribeToDeviceStatus("iotsample-arduino", "10aabbccddee");
```

**Note**: A single client can support multiple subscriptions.

## Handling status updates from devices
{: #handling_device_status_updates}

To process the status updates that are received by your subscriptions, you need to register a status event callback method. For `Connect` and `Disconnect` status events, the messages are returned as an instance of the Status class, which contains the following parameters:


| Parameter     |Data type     |
|----------------|----------------|
|`status.clientAddr` |string|
|`status.protocol`  |string|
|`status.clientId`   |string|
|`status.user`   |string|
|`status.time`   |java.util.Date|
|`status.action` |string|
|`status.connectTime`   |java.util.Date|
|`status.port`|integer|

The following properties are only set when the status event is ``Disconnect``:

| Property     |Data type     |
|----------------|----------------|
|`status.writeMsg` |integer|
|`status.readMsg`  |integer|
|`status.reason`   |string|
|`status.readBytes`   |integer|
|`status.writeBytes`   |integer|


The following code sample provides an example implementation of the Status callback:

```

  private static class MyStatusCallback implements StatusCallback {

      public void processApplicationStatus(ApplicationStatus status) {
          System.out.println("Application Status = " + status.getPayload());
      }

      public void processDeviceStatus(DeviceStatus status) {
          if(status.getAction() == "Disconnect") {
              System.out.println("device: "+status.getDeviceId()
                                  + "  time: "+ status.getTime()
                                  + "  action: " + status.getAction()
                                  + "  reason: " + status.getReason());
          } else {
              System.out.println("device: "+status.getDeviceId()
                                  + "  time: "+ status.getTime()
                                  + "  action: " + status.getAction());
          }
      }
  }
```

When the status callback is added to the application client, the ``processDeviceStatus()`` method is invoked whenever a device that matches the criteria is connected or disconnected from the {{site.data.keyword.iot_short_notm}}. The following code sample shows how you can add the status callback instance to the application client:

```

    myClient.connect()
    myClient.setStatusCallback(new MyStatusCallback());
    myClient.subscribeToDeviceStatus();
```
Applications can subscribe to any other application status, such as application connect and disconnect to {{site.data.keyword.iot_short_notm}}. The following code snippet shows how to subscribe to the application status of a {{site.data.keyword.iot_short_notm}} organization:

```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToApplicationStatus();
```
The overloaded method is available to control the status subscription to a particular application. The ``processApplicationStatus()`` method is called whenever an application that matches the criteria is connected or disconnected from {{site.data.keyword.iot_short_notm}}.


## Publishing events from devices
{: #publishing_events_devices}

The following code sample shows how applications can publish events as if they originated from a device.

```

    myClient.connect()

    //Generate the event to be published
    JsonObject event = new JsonObject();
    event.addProperty("name", "foo");
    event.addProperty("cpu",  60);
    event.addProperty("mem",  40);

    // publish the event on behalf of device
    myClient.publishEvent(deviceType, deviceId, "blink", event);
```


Events can be published in different formats, for example, JSON, string, binary, and more. By default, the library publishes events in JSON format, but you can specify the data in different formats if you prefer. For example, to publish data in string format use the following code snippet.

```
    myClient.connect();
    String data = "cpu:"+60;
    status = myClient.publishEvent("load", data, "text", 2);
```
**Note:** In the previous code example, the payload of the event must be in string format.

Any XML data can be converted to string and published as follows:

```
    status = myClient.publishEvent("load", xmlConvertedString, "xml", 2);
```

Similarly, to publish events in binary format, use the byte array, as outlined in the following example:

```
    myClient.connect();
    byte[] cpuLoad = new byte[] {60, 35, 30, 25};
    status = myClient.publishEvent("blink", cpuLoad , "binary", 1);
```

### Publish events by using HTTP
{: #publishing_events_http}

In addition to using MQTT, you can also configure your applications to publish device events to {{site.data.keyword.iot_short_notm}} through HTTP. The following steps outline the sequence for publishing device events through HTTP:

1. Construct the ApplicationClient instance by using the properties file.
2. Construct the event that needs to be published.
3. Specify the event name, device type, and device ID.
4. Publish the event by using the `publishEventOverHTTP`() method, as shown in the following code example:

```
    	ApplicationClient myClient = new ApplicationClient(props);

    	JsonObject event = new JsonObject();
    	event.addProperty("name", "foo");
    	event.addProperty("cpu",  90);
    	event.addProperty("mem",  70);

    	boolean status = myClient.publishApplicationEventforDeviceOverHTTP(deviceId, deviceType, "blink", event, ContentType.json);
```

For the complete code sample, see the [HttpApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpApplicationDeviceEventPublish.java) application example.

Based on the settings in the properties file, the `publishEventOverHTTP()` method publishes the event in either Quickstart or in Registered flow. When  `quickstart` is specified as the organization ID in the properties file, the `publishEventOverHTTP()` method publishes the event to the {{site.data.keyword.iot_short_notm}} Quickstart service in plain HTTP format. When a valid registered organization is specified in the properties file, the event is always published by using HTTPS so that all of the communication is secure.

The HTTP protocol provides 'at most once' delivery, which is similar to the 'at most once' (QoS 0) quality of service level of the MQTT protocol. When you use 'at most once' delivery to publish events, the application must implement retry logic when there is an error.


## Publishing commands to devices
{: #publishing_commands_devices}

Applications can publish commands to connected devices, as shown in the following example:

```

    myClient.connect()

    //Generate the event to be published
    JsonObject data = new JsonObject();
    data.addProperty("name", "stop-rotation");
    data.addProperty("delay",  0);

    //Registered flow allows 0, 1 and 2 QoS
    myAppClient.publishCommand(deviceType, deviceId, "stop", data);
```

### Publish commands by using HTTP
{: #publishing_commands_http}

In addition to using MQTT, you can also configure your applications to publish commands to the connected device through HTTP. The following steps outline the sequence for publishing device events by using HTTP:

1. Construct the ApplicationClient instance by using the properties file
2. Construct the command that needs to be published
3. Specify the command name, device type, and device ID
4. Publish the command by using the `publishCommandOverHTTP`() method, as shown in the following code:

```

    	ApplicationClient myClient = new ApplicationClient(props);

    	// Generate a JSON object of the event to be published
	JsonObject event = new JsonObject();
	event.addProperty("reboot", 5);

	boolean response = myClient.publishCommandOverHTTP("execute", event);
```

To view the complete code sample, see the [HttpCommandPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpCommandPublish.java) application example.

The HTTP protocol provides 'at most once' delivery, which is similar to the 'at most once' (QoS 0) quality of service level of the MQTT protocol. When you use 'at most once' delivery to publish commands, the application must implement retry logic when there is an error. For more information, see [HTTP REST API for applications](../api.html).


## Samples
{: #samples}

-  [MQTTApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/MQTTApplicationDeviceEventPublish.java) - A sample application that shows how you can  publish device events.
-   [RegisteredApplicationCommandPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationCommandPublish.java) - A sample application that shows how you can publish a command to a device.
-  [RegisteredApplicationSubscribeSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationSubscribeSample.java) - A sample application that shows how you can subscribe to different events such as device events, device commands, device status, and application status.
-   [SharedSubscriptionSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/SharedSubscriptionSample.java) - A sample application that shows how you can build a scalable application that balances the load of messages across multiple instances of the application.
-  [Backup-restore-sample](https://github.com/ibm-messaging/iot-backup-restore-sample) - A sample that shows how you can back up and restore the device configuration in {{site.data.keyword.cloudant}}.
