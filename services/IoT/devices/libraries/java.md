---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-21"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Java for device developers
{: #java}

You can build and customize devices that interact with your organization on {{site.data.keyword.iot_full}} by using Java™. A Java client library for {{site.data.keyword.iot_short_notm}}, documentation, and examples are provided to help you get started with device development.
{:shortdesc}

## Downloading the Java client and resources
{: #java_client_download}

To access the Java client libraries and samples for {{site.data.keyword.iot_short_notm}}, go to the [iot-java ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-java){: new_window} repository in GitHub and complete the installation instructions.

## Constructor
{: #constructor}

The constructor builds the client instance and accepts the `Properties` object, which contains the following definitions:

|Definition |Description |
|:----|:----|
|`org` |A required value that must be set to your organization ID. If you are using a Quickstart flow, specify `quickstart`.|
|`type`  |A required value that specifies the type of the device.|
|`id`  |A required value that specifies the unique ID of the device.|
|`auth-method`  |The method of authentication to be used. The only method that is supported is `token`.|
|`auth-token`   |An authentication token to securely connect your device to {{site.data.keyword.iot_short_notm}}.|
|`clean-session`|A true or false value that is required only if you want to connect the application in durable subscription mode. By default, `clean-session` is set to true.|
|`Port`|The port number to connect to. Specify either 8883 or 443. If you do not specify a port number, the client connects to {{site.data.keyword.iot_short_notm}} on port number 8883 by default.|
|`MaxInflightMessages`  |Sets the maximum number of in-flight messages for the connection. The default value is 100.|
|`Automatic-Reconnect`  |A true or false value that is required when you want to automatically reconnect the device to {{site.data.keyword.iot_short_notm}} while it is in a disconnected state. The default value is false.|
|`Disconnected-Buffer-Size`|The maximum number of messages that can be stored in memory while the client is disconnected. The default value is 5000.|
|`WebSocket`|A true or false value that is required when you want to use websocket connections with {{site.data.keyword.iot_short_notm}}. The default value is false.|

**Note:** To connect the device in durable subscription mode, set `clean-session` to `false`. For more information about clean session, see the 'Subscription Buffers and Clean Session' section of the [MQTT documentation](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

The `Properties` object creates definitions that are used to interact with the {{site.data.keyword.iot_short_notm}} module.

The following code sample shows how devices can publish events in Quickstart mode.

```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class QuickstartDeviceEventPublish {

    public static void main(String[] args) {

        //Provide the device specific data using Properties class
        Properties options = new Properties();
        options.setProperty("org", "quickstart");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generate a JSON object of the event to be published
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Quickstart flow allows only QoS = 0
        myClient.publishEvent("status", event, 0);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

The following code sample shows how devices can publish events in a registered flow.


```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class RegisteredDeviceEventPublish {

    public static void main(String[] args) {

        //Provide the device specific data, as well as Auth-key and token using Properties class
        Properties options = new Properties();

        options.setProperty("org", "uguhsp");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");
        options.setProperty("auth-method", "token");
        options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generate a JSON object of the event to be published
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Registered flow allows 0, 1 and 2 QoS
        myClient.publishEvent("status", event);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

### Using a configuration file

Instead of using the `Properties` object directly, you can use a configuration file that contains the name-value pairs for the properties. If you are using a configuration file that contains the `Properties` object, use the following code format:

```
package com.ibm.iotf.sample.client.device;

import java.io.File;
import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class RegisteredDeviceEventPublishPropertiesFile {

    public static void main(String[] args) {
        //Provide the device specific data, as well as Auth-key and token using Properties class
        Properties options = DeviceClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generate a JSON object of the event to be published
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Registered flow allows 0, 1 and 2 QoS
        myClient.publishEvent("status", event, 1);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

The content of the configuration file must be in the following format:

```
    [device]
    org=$orgId
    typ=$myDeviceType
    id=$myDeviceId
    auth-method=token
    auth-token=$token
```

## Connecting to {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}


To connect to {{site.data.keyword.iot_short_notm}}, use the `connect()` function. The `connect()` function includes an optional boolean parameter called `autoRetry`, which determines whether the library tries to reconnect when there is an MqttException connection failure. By default, `autoRetry` is set to true. If an MqttSecurityException connection fails because incorrect device registration details are passed, the library does not attempt to reconnect, even if `autoRetry` is set to true.

To set the 'keep alive' interval for MQTT, you can optionally use the `setKeepAliveInterval(int)` method before you call the `connect()` function. The `setKeepAliveInterval(int)` value is  measured in seconds, and defines the maximum time interval between messages that are sent or received. When used, the client can detect when the server is no longer available without waiting for the end of the TCP/IP timeout period to be reached. The client ensures that at least one message travels across the network within each 'keep alive' interval period. If zero data-related messages are received during the timeout period, the client sends a small `ping` message, which the server acknowledges. The `setKeepAliveInterval(int)` is set to 60 seconds by default. To disable the 'keep alive' processing feature on the client, set the `setKeepAliveInterval(int)` value to 0.


```
DeviceClient myClient = new DeviceClient(options);
myClient.setKeepAliveInterval(120);
myClient.connect(true);
```

To control the number of retries that occur when there is a connection failure, use the overloaded connect(int numberOfTimesToRetry) function.


```
DeviceClient myClient = new DeviceClient(options);
myClient.setKeepAliveInterval(120);
myClient.connect(10);
```

After your devices successfully connect to {{site.data.keyword.iot_short_notm}}, they can publish events and subscribe to device commands from an application.


## Publishing events
{: #publishing_events}

Events are the mechanism by which devices publish data to the {{site.data.keyword.iot_short_notm}}. The device controls the content of the event and assigns a name for each event that it sends.

When an event is received by the {{site.data.keyword.iot_short_notm}} instance, the credentials of the received event identify the sending device, which means that a device cannot impersonate another device.

Events can be published at any of the three [quality of service (QoS) levels](../../reference/mqtt/index.html#qos-levels) that are defined by the MQTT protocol.  By default, events are published at QoS=0.

### Publish events at the default QoS level

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

myClient.publishEvent("status", event);
```


### Increasing the QoS level for an event

You can increase the [QoS levels](../../reference/mqtt/index.html#qos-levels) for events that are published. Events with a QoS level that is greater than zero might take longer to publish because of the extra confirmation receipt information that is included.

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

//Registered flow allows 0, 1 and 2 QoS
myClient.publishEvent("status", event, 2);
```

### Publishing events in custom formats

Events can be published in different formats, for example, JSON, string, binary, and more. By default, the library publishes events in JSON format, but you can specify the data in different formats if you prefer. For example, to publish data in string format use the following code snippet.

```
myClient.connect();

String data = "cpu:"+getProcessCpuLoad();
status = myClient.publishEvent("load", data, "text", 2);
```

**Note:** In the previous code example, the payload of the event must be in string format.

Any XML data can be converted to string format and published as follows,

```
status = myClient.publishEvent("load", xmlConvertedString, "xml", 2);
```

Similarly, to publish events in binary format, use the byte array that is outlined in the following example:

```
myClient.connect();

byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = myClient.publishEvent("blink", cpuLoad , "binary", 1);
```

### Publish events by using HTTP
{: #publishing_events_http}


In addition to using MQTT, you can also configure your devices to publish events to {{site.data.keyword.iot_short_notm}} through HTTP. The following steps outline the sequence for publishing events through HTTP:

1. Construct a `DeviceClient` instance by using the properties file.
2. Construct an event that needs to be published.
3. Specify the event name, and then publish the event by using the `publishEventOverHTTP()` method, as shown in the following code sample:

``` 
DeviceClient myClient = new DeviceClient(deviceProps);

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

boolean response  = myClient.api().publishDeviceEventOverHTTP("blink", event, ContentType.json);
```

To view the entire code, see the [HttpDeviceEventPublish ![External link icon](../../../../icons/launch-glyph.svg "External link icon")] device example.{: new_window}

Based on the settings in the properties file, the ``publishEventOverHTTP()`` method publishes the event in either Quickstart mode or in registered flow mode. When the organization ID in the properties file is set to `quickstart`, the ``publishEventOverHTTP()`` method publishes the event to the device example quickstart service and publishes the event in plain HTTP format. When a valid registered organization is specified in the properties file, events are securely published through HTTPS.

The HTTP protocol provides 'at most once' delivery, which is similar to the 'at most once' (QoS 0) quality of service level of the MQTT protocol. When you use 'at most once' delivery to publish events, the application must implement retry logic whenever there is an error.

[HttpDeviceEventPublish]: https://github.com/ibm-messaging/iot-device-samples/blob/master/java/device-samples/src/main/java/com/ibm/iotf/sample/client/device/HttpDeviceEventPublish.java

## Handling commands
{: #handling_commands}

When the device client connects, it automatically subscribes to any commands for this device. To process specific commands, you need to register a command callback method.
The messages are returned as an instance of the `Command` class, which contains the following properties:

| Property     |Data type     | Description|
|----------------|----------------|
|`payload` |java.lang.String| The data for the message payload.|
|`format`  |java.lang.String| The format can be any string, for example JSON.|
|`command`   |java.lang.String|Identifies the command.|
|`timestamp`   |org.joda.time.DateTime|The date and time of the event.|


```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.LinkedBlockingQueue;


import com.ibm.iotf.client.device.Command;
import com.ibm.iotf.client.device.CommandCallback;
import com.ibm.iotf.client.device.DeviceClient;


//Implement the CommandCallback class to provide the way in which you want the command to be handled
class MyNewCommandCallback implements CommandCallback, Runnable {

    // A queue to hold & process the commands for smooth handling of MQTT messages
    private BlockingQueue<Command> queue = new LinkedBlockingQueue<Command>();

    /**
    * This method is invoked by the library whenever there is command matching the subscription criteria
    */
    @Override
    public void processCommand(Command cmd) {
        try {
            queue.put(cmd);
            } catch (InterruptedException e) {
        }
    }

    @Override
    public void run() {
        while(true) {
            Command cmd = null;
            try {
                //In this sample, we just display the command
                cmd = queue.take();
                System.out.println("COMMAND RECEIVED = '" + cmd.getCommand() + "'\twith Payload = '" + cmd.getPayload() + "'");
            } catch (InterruptedException e) {}
        }
    }
}

public class RegisteredDeviceCommandSubscribe {


    public static void main(String[] args) {

        //Provide the device specific data, as well as Auth-key and token using Properties class
        Properties options = new Properties();

        options.setProperty("org", "uguhsp");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");
        options.setProperty("auth-method", "token");
        options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Pass the above implemented CommandCallback as an argument to this device client
        myClient.setCommandCallback(new MyNewCommandCallback());

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();
    }
}
```

## Samples
{: #samples}

For a list of device and device management samples that are developed by using the {{site.data.keyword.iot_short_notm}} Java client library, see the [iot-device-samples GitHub repository ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/iot-device-samples/tree/master/java){: new_window}.
