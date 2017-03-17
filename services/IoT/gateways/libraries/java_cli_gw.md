---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

#Developing gateways on {{site.data.keyword.iot_short_notm}} by using Java
{: #java_cli_gw}

If your devices cannot directly connect to your organization on {{site.data.keyword.iot_full}}, you can build and customize gateways by using Java™. A Java client library for {{site.data.keyword.iot_short_notm}}, documentation, and examples are provided to help you get started with gateway development.
{:shortdesc}

## Downloading the Java client and resources
{: #java_client_download}

To access the Java client libraries and samples for {{site.data.keyword.iot_short_notm}}, go to the [iot-java](https://github.com/ibm-watson-iot/iot-java) repository in GitHub and complete the installation instructions.

## Constructor
{: #constructor}

The constructor builds the gateway client instance and accepts the `Properties` object, which contains the following definitions:

|Definition |Description |
|:----|:----|
|`org`|A required value that must be set to your organization ID. If you are using a Quickstart flow, specify `quickstart`.|
|`domain`|The messaging endpoint URL, which is optional. If you do not specify a value for a domain, the URL defaults to `internetofthings.ibmcloud.com`, which is the {{site.data.keyword.iot_short_notm}} production server.|
|`type`|A required value that specifies the type of the gateway.|
|`id` |A required value that specifies the unique ID of the gateway.|
|`auth-method`|The method of authentication to be used. The only method that is supported is `token`.|
|`auth-token`|An API key authentication token to securely connect your gateway to {{site.data.keyword.iot_short_notm}}.|
|`clean-session`|A true or false value that is required only if you want to connect the gateway in durable subscription mode. By default, `clean-session` is set to true.|
|`WebSocket`|A true or false value that is required only if you want to connect the gateway by using websockets.|
|`Port`|The port number to connect to. Specify either 8883 or 443. If you do not specify a port number, the client connects to {{site.data.keyword.iot_short_notm}} on port number 8883 by default.|
|`MaxInflightMessages`|Sets the maximum number of in-flight messages for the connection. The default value is 100.|
|`Automatic-Reconnect`|A true or false value that is required when you want to automatically reconnect the gateway to {{site.data.keyword.iot_short_notm}} while it is in a disconnected state. The default value is false.|
|`Disconnected-Buffer-Size`|The maximum number of messages that can be stored in memory while the client is disconnected. The default value is 5000.|

**Note:** To connect the gateway in durable subscription mode, set `clean-session` to `false`. For more information about clean session, see the 'Subscription Buffers and Clean Session' section of the [MQTT documentation](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

The `Properties` object creates definitions that are used to interact with the {{site.data.keyword.iot_short_notm}} module.

The following code sample shows how to construct a gateway client instance:

```java
Properties options = new Properties();
options.setProperty("org", "<Your organization ID>");
options.setProperty("type", "<The gateway device type>");
options.setProperty("id", "The gateway device ID");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "API token");
GatewayClient gwClient = new GatewayClient(options);

```


### Using a configuration file

Instead of using the `Properties` object directly to create a gateway instance, you can use a configuration file that contains the name-value pairs for the properties of the gateway. To use a configuration file to build the `Properties` object for the gateway, use the following code format:

```Java
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
...
```

The content of the configuration file must be in the following format:

```java
[Gateway]
org=$orgId
domain=$domain
typ=$myGatewayDeviceType
id=$myGatewayDeviceId
auth-method=token
auth-token=$token

```

## Connecting to {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

To connect to {{site.data.keyword.iot_short_notm}}, use the `connect()` function. The `connect()` function includes an optional boolean parameter that is called `autoRetry`, which determines whether the library tries to reconnect when an MQTT exception (MqttException) connection fails. By default, `autoRetry` is set to true. If an MqttSecurityException connection fails because incorrect device registration details are passed, the library does not attempt to reconnect, even if `autoRetry` is set to true.

To set the keep alive interval for MQTT, you can optionally use the `setKeepAliveInterval(int)` method before you call the `connect()` function. The `setKeepAliveInterval(int)` value is measured in seconds and defines the maximum time interval between messages that are sent or received. When a `setKeepAliveInterval(int)` value is specified, the client can detect that the server is no longer available without waiting for the end of the TCP/IP timeout period to be reached. The client ensures that at least one message travels across the network within each keep alive interval period. If zero data-related messages are received during the timeout period, the client sends a small `ping` message, which the server acknowledges. The `setKeepAliveInterval(int)` is set to 60 seconds by default. To disable the keep alive processing feature on the client, set the `setKeepAliveInterval(int)` value to 0.

```java
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
gwClient.setKeepAliveInterval(80);
gwClient.connect();
```

To control the number of retries that occur when a connection fails, use the overloaded connect(int numberOfTimesToRetry) function.

```java
GatewayClient gwClient = new GatewayClient(props);
gwClient.setKeepAliveInterval(80);
gwClient .connect(10);
```

After the gateway client successfully connects to {{site.data.keyword.iot_short_notm}}, the gateway can publish events and subscribe to commands for itself and also on behalf of the devices that are attached to the gateway.

## Registering devices that are behind the gateway
{: #register_device_gateway}

You can register devices that are behind the gateway that is connected to your {{site.data.keyword.iot_short_notm}} instance either automatically or by developing code by using the API.

### Automatic device registration
You can register your devices on {{site.data.keyword.iot_short_notm}} automatically whenever the gateway publishes any events or subscribes to any commands for the devices that are connected to it.

### API device registration
You can also use the {{site.data.keyword.iot_short_notm}} API to register devices that are behind a gateway to your {{site.data.keyword.iot_short_notm}} instance.

To simplify development with the {{site.data.keyword.iot_short_notm}} API, initiate an API client instance by invoking the api() method, which is outlined in the following code sample:

```java
import com.ibm.iotf.client.api.APIClient;
....

GatewayClient gwClient = new GatewayClient(props);
gwClient.connect();

APIClient api = gwClient.api();
```
When you receive the handle of the API client, you can start registering devices to a gateway, which is outlined in the following code sample:

```java
gwClient.connect();

  String deviceToBeAdded = "{\"deviceId\": \"" + DEVICE_ID +
					"\",\"authToken\": \"qwer123\"}";

    JsonParser parser = new JsonParser();
    JsonElement input = parser.parse(deviceToBeAdded);
    JsonObject response = this.gwClient.api().registerDeviceUnderGateway(DEVICE_TYPE, gwDeviceId, gwDeviceType, input);

```

When a device that is behind a gateway is registered, the device is associated with the gateway by the values of the `gwDeviceId`and `gwDeviceType` attributes.

## Publishing events
{: #publish_events}

Events are the mechanism by which gateways and devices publish data to {{site.data.keyword.iot_short_notm}}. The gateway or device controls the content of the event and assigns a name for each event that it sends. A gateway can publish events from itself and on behalf of any device that is connected through the gateway.

When an event is received by the {{site.data.keyword.iot_short_notm}} instance, the credentials of the received event identify the sending gateway, which means that a gateway cannot impersonate another device.

Events can be published at any of the three [quality of service (QoS) levels](../../reference/mqtt/index.html#qos-levels) that are defined by the MQTT protocol.  By default, events are published at QoS=0.

### Code for publishing gateway events at the default QoS level

```java
gwClient.connect();
  JsonObject event = new JsonObject();
  event.addProperty("name", "foo");
  event.addProperty("cpu",  90);
  event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event);
```

### Code for increasing the default QoS level for an event

You can increase the [QoS levels](../../reference/mqtt/index.html#qos-levels) for gateway events that are published. Events that have a QoS level that is greater than zero might take longer to publish because of the extra confirmation receipt information that is included.


```java
gwClient.connect();
  JsonObject event = new JsonObject();
  event.addProperty("name", "foo");
  event.addProperty("cpu",  90);
  event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event, 2);
```

### Code for publishing events in custom formats

Events can be published in different formats, for example, JSON, string, binary, and more. By default, the library publishes events in JSON format, but you can specify the data in different formats if you prefer. For example, to publish data in string format, use the following code snippet:

```java
gwClient.connect();
String data = "cpu:80";
boolean status = gwClient.publishGatewayEvent("load", data, "text", 2);
```

**Note:** In the previous code example, the payload of the event must be in string format.

XML data can be converted to string format and published as outlined in the following code sample:

```java
status = gwClient.publishGatewayEvent("load", xmlConvertedString, "xml", 2);
```

Similarly, to publish events in binary format, use the byte array that is outlined in the following example:

```java
gwClient.connect();
byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = gwClient.publishGatewayEvent("blink", cpuLoad , "binary", 1);
```

### Code for publishing events from devices
{: #publishing_events_devices}

A gateway can publish events on behalf of any device that is connected through the gateway by passing the appropriate type ID and device ID values of the original event, which is outlined in the following sample:

```java

gwClient.connect()

//Generate the event to be published
JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  60);
event.addProperty("mem",  40);

// publish the event on behalf of device
gwClient.publishDeviceEvent(deviceType, deviceId, eventName, event);
```

Use the overloaded `publishDeviceEvent()` method to publish the device event at a preferred quality of service level. For more information about the topic structure that is used, see [MQTT Connectivity for Gateways](../mqtt.html).

### Code for publishing device events that are in a custom format

Similar to gateway events, device events can also be published in different formats. By default, the library publishes device events in JSON format, but you can specify the data in different formats if you prefer. For example, to publish data in string format, use the following code sample:

```java
gwClient.connect();
String data = "cpu:80";
boolean status = gwClient.publishDeviceEvent(deviceType, deviceId, "load", data, "text", 2);
```

**Note:**  The payload of the event must be in string format.

Any XML data can be converted to string format and published as shown in the following example:

```java
status = gwClient.publishDeviceEvent(deviceType, deviceId, "load", xmlConvertedString, "xml", 2);
```

Similarly, to publish device events in binary format, use the byte array that is outlined in the following example:
```java
gwClient.connect();
byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = gwClient.publishDeviceEvent(deviceType, deviceId, "blink", cpuLoad , "binary", 1);
```

## Handling commands
{: #handling_commands}

The gateway can subscribe to commands that are directed at the gateway itself and to any device that is connected behind a gateway. When the gateway client connects, it automatically subscribes to any commands for this gateway. But to subscribe to any commands for the devices that are connected through the gateway, use the overloaded `subscribeToDeviceCommands()` method, which is outlined in the following example:

```java
gwClient.connect()

// subscribe to commands on behalf of device
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

To process specific commands, you need to register a `Command` callback method. The messages are returned as an instance of the `Command` class and contain the following properties:


| Property     |Data type     | Description|
|----------------|----------------|---------------
|`deviceType`|String| The device type for which the command is received.|
|`deviceId`|String| The device ID for which the command is received, which can be either the gateway or a device that is connected through the gateway.|
|`data`|Object| The command payload.|
|`format`|String| The format of the command payload, which can be any string, for example, JSON. binary, text, or other.|
|`command`|String|The name of the command.|
|`timestamp`|org.joda.time.DateTime|The date and time at the point when the command is sent.|

The following code sample outlines how you can implement the `Command` callback method:

```java
import com.ibm.iotf.client.gateway.Command;
import com.ibm.iotf.client.gateway.GatewayCallback;

public class GatewayCommandCallback implements GatewayCallback, Runnable {
	// A queue to hold and process the commands
	private BlockingQueue<Command> queue = new LinkedBlockingQueue<Command>();

	public void processCommand(Command cmd) {
  	    queue.put(cmd);
  	}

  	public void run() {
  	    while(true) {
  	        Command cmd = queue.take();
  	        System.out.println("Command " + cmd.getData());

  	        // code to process the command
  	    }
  	}

  	/**
	 * If a gateway subscribes to a topic of a device or sends data on behalf of a device
	 * that the gateway does not have permission to connect to, the message or the subscription is ignored.
	 * This behavior is different compared with the behavior of applications, where the connection is terminated.
	 * The Gateway is notified on the the notification topic:
	 */
  	@Override
public void processNotification(Notification notification) {

}
  }

```
When the `Command` callback is added to the gateway client, the `processCommand()` method is invoked whenever any command is published that has the subscribed criteria.

The following code sample outlines how to add the `Command`callback into the gateway client instance.

```java
gwClient.connect()
GatewayCommandCallback callback = new GatewayCommandCallback();
gwClient.setGatewayCallback(callback);
//Subscribe to a device that is connected to the gateway
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

Overloaded methods are available to control the command subscription.

### Listing devices that are connected through a gateway
{: #list_devices_gw}


To retrieve all devices that are connected through the specified gateway (typeId, deviceId) to {{site.data.keyword.iot_short_notm}}, invoke the method `getDevicesConnectedThroughGateway()`.

```java
gwClient.connect()
gwClient.api().getDevicesConnectedThroughGateway(gatewayType, gatewayId);
```

## Samples
{: #samples}

Several samples are available to help you to connect gateways and devices that are behind gateways to your {{site.data.keyword.iot_short_notm}} instance. The samples use the {{site.data.keyword.iot_short_notm}} Java client library and are located in the [Gateway Samples GitHub repository ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples){: new_window}.

## Recipes
{: #recipes}

| Recipe     | Description|
|----------------|----------------
|[Connecting your device as a gateway to {{site.data.keyword.iot_short_notm}} ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-gateway-to-watson-iot-platform/){: new_window}| A GitHub project and detailed instructions that explain how to connect a Raspberry Pi gateway and Arduino Uno devices behind the gateway to {{site.data.keyword.iot_short_notm}}.
|[Raspberry Pi as a managed gateway in {{site.data.keyword.iot_short_notm}} ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/){: new_window}|An extension of the previous gateway recipe that explains how to connect your Raspberry Pi gateway as a managed device in {{site.data.keyword.iot_short_notm}} and how to do device management operations.
