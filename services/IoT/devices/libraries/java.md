---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Java for device developers
{: #java}

Last updated: 02 Aug 2016
{: .last-updated}


You can use Java to build and customize devices that interact with your organization on {{site.data.keyword.iot_full}}. Use the information and examples that are provided to start developing your devices by using Java.
{:shortdesc}

## Downloading the Java client and resources
{: #java_client_download}

To access the Java client libraries and samples for {{site.data.keyword.iot_short_notm}}, go to the [iot-java](https://github.com/ibm-watson-iot/iot-java) repository in GitHub and complete the installation instructions.


## Constructor
{: #constructor}

The constructor builds the client instance and accepts a properties object that contains the following definitions:

|Definition |Description |
|:---|:---|
|`org` |Your organization ID. This field is required. If you are using a Quickstart flow, specify ``quickstart``.|
|`type`  |The type of your device. This field is required.|
|`id`  |The ID of your device. This field is required.|
|`auth-method`   |The method of authentication to be used. The only value that is currently supported is `token`.|
|`auth-token`   |An authentication token to securely connect your device to Watson IoT Platform.|
|`clean-session`|A true or false value that is required only if you want to connect the application in durable subscription mode. By default, `clean-session` is set to `true`.|

**Note:** To connect the device in durable subscription mode, set `clean-session` to `false`. For more information about clean session, see the 'Subscription Buffers and Clean Session' section of the [MQTT documentation](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

The properties object creates definitions that are used to interact with the {{site.data.keyword.iot_short_notm}} module.

The following code shows a device publishing events in Quickstart mode.

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

Instead of using a properties object directly, you can use a configuration file that contains the name-value pairs for the properties. If you are using a configuration file that contains a properties object, use the following code format:

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

## Connecting to the {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

Connect to the {{site.data.keyword.iot_short_notm}} by calling the connect function. The connect function takes an optional boolean parameter `autoRetry`, which is `true` by default. The `autoRetry` parameter allows the library to reconnect when an MqttException error occurs. Note that the library doesn't try to reconnect when an MqttSecurityException errors because incorrect device registration details were used, even if the `autoRetry` parameter is set to `true`.

```
DeviceClient myClient = new DeviceClient(options);

myClient.connect(true);
```

After the successful connection to the {{site.data.keyword.iot_short_notm}} service, the device client can perform operations such as publishing events and subscribing to device commands from an application.


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

You can increase the [QoS levels](../../reference/mqtt/index.html#qos-levels) for events that are published. Events that have a QoS level that is greater than zero might take longer to publish, because of the extra confirmation receipt information that is included.

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

//Registered flow allows 0, 1 and 2 QoS
myClient.publishEvent("status", event, 2);
```

### Publish event by using HTTP

In addition to MQTT, the devices can publish events to the {{site.data.keyword.iot_short_notm}} by using HTTP and by using the following steps:

* Construct a DeviceClient instance by using the properties file.
* Construct an event that needs to be published.
* Specify the event name and publish the event by using the ``publishEventOverHTTP()`` method, as shown in the following code:

``` sourceCode
DeviceClient myClient = new DeviceClient(deviceProps);

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

int httpCode = myClient.publishEventOverHTTP("blink", event);
```

You can find the entire code in the [HttpDeviceEventPublish] device example.

Based on the settings in the properties file, the ``publishEventOverHTTP()`` method either publishes the event in Quickstart mode or in registered flow mode. When the Organization ID in the properties file is `quickstart`, the ``publishEventOverHTTP()`` method publishes the event to the device example quickstart service and publishes the event in plain HTTP format. When a valid registered organization is used in the properties file, this method always publishes the event in HTTPS, which is HTTP over SSL, so all the communication is secured.

The HTTP protocol provides 'at most once' delivery, which is similar to the 'at most once' (QoS 0) quality of service level of the MQTT protocol. When you use 'at most once' delivery to publish events, the application must implement retry logic when there is an error.

[HttpDeviceEventPublish]: https://github.com/ibm-messaging/iot-device-samples/blob/master/java/device-samples/src/main/java/com/ibm/iotf/sample/client/device/HttpDeviceEventPublish.java

## Handling commands
{: #handling_commands}

When the device client connects, it automatically subscribes to any commands for this device. To process specific commands, you need to register a command callback method.
The messages are returned as an instance of the Command class, which has the following properties:

| Property     |Data type     | Description|
|----------------|----------------|
|`payload` |java.lang.String| The data for the message payload.|
|`format`  |java.lang.String| The format can be any string, for example JSON.|
|`command`   |java.lang.String|Identifies the command.|
|`timestamp`   |org.joda.time.DateTime|The date and time of the event.|


``` sourceCode
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

For a list of device and device management samples that are developed by using the  {{site.data.keyword.iot_short_notm}} Java Client library, see the [GitHub  repository](https://github.com/ibm-messaging/iot-device-samples/tree/master/java).
