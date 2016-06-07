---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# ﻿Java for application developers
{: #java}

For more information, see [iot-java](https://github.com/ibm-messaging/iot-java) in GitHub.

## Constructor
{: #constructor}

The constructor builds the client instance, and accepts a Properties object that contains the following definitions:

| Definition     |Description     |
|----------------|----------------|
|``org`` |Your organization ID. This is a required value. If you are using a Quickstart flow, specify ``quickstart``.|
|``id``  |The unique ID of the application within your organization.|
|``auth-method``   |Method of authentication whereby the only value that is currently supported is ``apikey``).|
|``auth-key``   |An API key, which is required when auth-method is set to ``apikey``.|
|``auth-token``   |An API key token, which is required when auth-method is set to ``apikey``.|
|``clean-session``|A true or false value that is required only if you want to connect the application in durable subscription mode. By default, ``clean-session`` is set to 'true'.|
|``shared-subscription``|A boolean value. Set to true if you would like to build scalable applications that balance the load of messages across multiple instances of the application. For more information, see [Scalable applications](https://docs.internetofthings.ibmcloud.com/applications/mqtt.html#/scalable-applications#scalable-applications).

The Properties object creates definitions which are used to interact with the {{site.data.keyword.iot_full}} module. If you do not specify the properties for this object, or if you specify ``quickstart``, the client connects to the {{site.data.keyword.iot_short_notm}} Quickstart service, and defaults to an unregistered device.

The following code sample shows how you can construct the ApplicationClient instance in Quickstart mode:

```
    import com.ibm.iotf.client.app.ApplicationClient;
    import java.util.Properties;

    Properties options = new Properties();
    options.put("org", "quickstart");

    ApplicationClient myClient = new ApplicationClient(options);
```

The following code sample shows how you can construct the ApplicationClient instance in registered flow mode:

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

Instead of including a Properties object directly, you can use a configuration file containing the name-value pairs for the Properties object with the following format:

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    ...
```
The application configuration file must be in the following format:

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

To connect to the {{site.data.keyword.iot_short_notm}} use the ``connect()`` function. The ``connect()`` function includes an optional boolean parameter called ``autoRetry`` that determines whether the library attempts to reconnect in the event of a ``MqttException`` connection failure. By default, ``autoRetry`` is set to true. In the event of a ``MqttSecurityException`` connection failure as a result of incorrect device registration details being passed, the library does not attempt to reconnect, even if ``autoRetry`` is set to true.

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);

    myClient.connect();
```

After successfully connecting to the {{site.data.keyword.iot_short_notm}} service, your  application clients can subscribe to device events, subscribe to device statuses, and  publish device events and commands.

## Subscribing to device events
{: #subscribing_device_events}

Events are the mechanism by which devices publish data to {{site.data.keyword.iot_short_notm}}. The device controls the content of the event and assigns a name for each event that it sends.

When an event is received by the {{site.data.keyword.iot_short_notm}} instance, the credentials of the received event identify the sending device, making it impossible for a device to impersonate another device.



By default, applications subscribe to all events from all connected devices. Use the type, ID, event, and msgFormat parameters to control the scope of the subscription. A single client can support multiple subscriptions. The following code samples provide examples of how you can subscribe to devices that are dependent on device type, ID, event, and msgFormat parameters.

### Subscribing to all events from all devices


```
    myClient.connect();
    myClient.subscribeToDeviceEvents();
```
### Subscribing to all events from all devices of a specific type


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-ardunio");
```

### Subscribing to all events from a specific device


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-ardunio", "00aabbccddee");
```
### Subscribing to a specific event from two or more different devices

```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-ardunio", "00aabbccddee", "myEvent");
    myClient.subscribeToDeviceEvents("iotsample-ardunio", "10aabbccddee", "myEvent");
```
### Subscribing to events published by a device in JSON format


```

    client.connect()
    myClient.subscribeToDeviceEvents("iotsample-ardunio", "00aabbccddee", "myEvent", "json", 0);
```

## Handling events from devices
{: #handling_device_events}

To process the events received by your subscriptions, register an event callback method. The messages are returned as an instance of the Event class, which has the following properties:

* event.device - string (uniquely identifies the device across all types of devices in the organization)
* event.deviceType - string
* event.deviceId - string
* event.event - string
* event.format - string
* event.data - dict
* event.timestamp - datetime

The following code provides a sample implementation of the Event callback:

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

	// A queue to hold & process the Events for smooth handling of MQTT messages
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
				// In this example, we just output the event
				System.out.println("Event:: " + e.getDeviceId() + ":" + e.getEvent() + ":" + e.getPayload());
			} catch (InterruptedException e1) {
				// Ignore the Interuppted exception, retry
				continue;
			}
		}
	}
    }
```

When the event callback is added to the ApplicationClient, the processEvent() method is invoked whenever any event is published on the subscribed criteria, The following snippet shows how to add the Event call back into ApplicationClient instance,





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

Overloaded methods are available to control the command subscription. The processCommand() method is called when a command is sent to the device that matches the command subscription.


## Subscribing to device status
{: #subscribing_device_status}

Similar to subscribing to device events, applications can subscribe to device status, like device connect and disconnect to {{site.data.keyword.iot_short_notm}}. By default, this will subscribe to status updates for all connected devices. Use the Device Type and Device ID parameters to control the scope of the subscription. A single ApplicationClient can support multiple subscriptions.

### Subscribe to status updates for all devices

```
    myClient.connect();
    myClient.subscribeToDeviceStatus();
```

### Subscribe to status updates for all devices of a specific type


```

    myClient.connect();
    myClient.subscribeToDeviceStatus("iotsample-ardunio");
```

### Subscribe to status updates for two different devices


```

    myClient.connect();
    myClient.subscribeToDeviceStatus("iotsample-ardunio", "00aabbccddee");
    myClient.subscribeToDeviceStatus("iotsample-ardunio", "10aabbccddee");
```

## Handling status updates from devices
{: #handling_device_status_updates}

To process the status updates that are received by your subscriptions, you need to register a status event callback method. The messages are returned as an instance of the Status class, which contains the following properties:

The following properties are set for both "Connect" and "Disconnect" status events:

* status.clientAddr - string
* status.protocol - string
* status.clientId - string
* status.user - string
* status.time - java.util.Date
* status.action - string
* status.connectTime - java.util.Date
* status.port - integer

The following properties are only set when the action is "Disconnect":

* status.writeMsg - integer
* status.readMsg - integer
* status.reason - string
* status.readBytes - integer
* status.writeBytes - integer

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

When the status callback is added to the ApplicationClient, the processDeviceStatus() method is invoked whenever any device is connected or disconnected from the {{site.data.keyword.iot_short_notm}} that matches the criteria. The following code sample shows how you can add the status call back instance into ApplicationClient:

```

    myClient.connect()
    myClient.setStatusCallback(new MyStatusCallback());
    myClient.subscribeToDeviceStatus();
```
As with device status, the application can also subscribe to any other application connect or disconnect status. The following code snippet shows how to subscribe to the application status in the organization:

```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToApplicationStatus();
```
Overloaded method is available to control the status subscription to a particular application. The processApplicationStatus() method is called whenever any application is connected or disconnected from the {{site.data.keyword.iot_short_notm}} that matches the criteria.


## Publishing events from devices
{: #publishing_events_devices}

[Backup and restore sample](https://github.com/ibm-messaging/iot-backup-restore-sample)

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

### Publish events using HTTP(s)
{: #publishing_events_http}

In addition to MQTT, you can configure your applications to publish device events to {{site.data.keyword.iot_short_notm}} through HTTP(s) by completing the following steps:

* Construct the ApplicationClient instance by using the properties file
* Construct the event that needs to be published
* Specify the event name, device type, and device ID
* Publish the event using the publishEventOverHTTP() method, as follows:

```

    	ApplicationClient myClient = new ApplicationClient(props);

    	JsonObject event = new JsonObject();
    	event.addProperty("name", "foo");
    	event.addProperty("cpu",  90);
    	event.addProperty("mem",  70);

    	code = myClient.publishEventOverHTTP(deviceType, deviceId, "blink", event);
```

For the complete code sample, go to the following application example:

[HttpApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdeviceclient/src/com/ibm/iotf/sample/client/application/HttpApplicationDeviceEventPublish.java)

Based on the settings in the properties file, the publishEventOverHTTP() method publishes the event in either Quickstart or in Registered flow. When  `quickstart` is the Organization ID that is specified in the properties file, the publishEventOverHTTP() method publishes the event to the  {{site.data.keyword.iot_short_notm}} Quickstart service in plain HTTP format. When a valid registered organization is specified in the properties file, the event is always published through HTTPS, so that all of the communication is secure.

The event in HTTP(s) is published at most once Quality of Service, so the application needs to implement the retry logic when there is an error.

## Publishing commands to devices
{: #publishing_commands_devices}

Applications can publish commands to connected devices, as outlined in the following example:

```

    myClient.connect()

    //Generate the event to be published
    JsonObject data = new JsonObject();
    data.addProperty("name", "stop-rotation");
    data.addProperty("delay",  0);

    //Registered flow allows 0, 1 and 2 QoS
    myAppClient.publishCommand(deviceType, deviceId, "stop", data);
```


## Examples
{: #examples}


-  [MQTTApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/MQTTApplicationDeviceEventPublish.java) - A sample application that shows how you can  publish device events.
-   [RegisteredApplicationCommandPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationCommandPublish.java) - A sample application that shows how you can publish a command to a device.
-  [RegisteredApplicationSubscribeSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationSubscribeSample.java) - A sample application that shows how you can subscribe to different events such as, device events, device commands, device status, and application status.
-   [SharedSubscriptionSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/SharedSubscriptionSample.java) - A sample application that shows how you can build a scalable application, which balances the load of messages across multiple instances of the application.
-  [Backup and restore sample](https://github.com/ibm-messaging/iot-backup-restore-sample) - A sample that shows how you can backup and restore the device configuration in a Cloudant NoSQL database.
