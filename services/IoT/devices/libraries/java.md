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

For more information about Java for device developers, see [iot-java](https://github.com/ibm-messaging/iot-java) in GitHub.

## Constructor
{: #constructor}

The constructor builds the client instance and accepts a properties object that contains the following definitions:

| Definition     |Description     |
|----------------|----------------|
|``org`` |Your organization ID. This is a required field. If you are using a Quickstart flow, specify ``quickstart``.
|``type``  |The type of your device. This is a required field.|
|``id``  |The ID of your device. This is a required field.|
|``auth-method``   |Method of authentication. The only value that is currently supported is ``apikey``).|
|``auth-token``   |An API key token, which is required when auth-method is set to ``apikey``.|
|``clean-session``|A true or false value that is required only if you want to connect the application in durable subscription mode. By default, ``clean-session`` is set to 'true'.|

**Note:** To connect the device in durable subscription, set `clean-session` to false. For more information about clean session, see [Subscription Buffers and Clean Session](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

The properties object creates definitions that are used to interact with the {{site.data.keyword.iot_full}} module.

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

The following code sample outlines how devices can publish events in a registered flow.


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

Instead of including a properties object directly, you can use a configuration file that contains the name-value pairs for the properties. If you are using a configuration file containing a Properties object, use the following code format:

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

Connect to the {{site.data.keyword.iot_short_notm}} by calling the connect function. The connect function takes an optional boolean parameter autoRetry (by default autoRetry is true), which allows the library to retry the connection when there is an MqttException. Note that the library doesn't retry when there is a MqttSecurityException due to incorrect device registration details passed, even if the autoRetry is set to true.

```
DeviceClient myClient = new DeviceClient(options);

myClient.connect(true);
```

After the successful connection to the {{site.data.keyword.iot_short_notm}} service, the device client can perform the following operations, like publishing events and
subscribe to device commands from application.


## Publishing events
{: #publishing_events}

Events are the mechanism by which devices publish data to the {{site.data.keyword.iot_short_notm}}. The device controls the content of the event and assigns a name for each event it sends.

When an event is received by the {{site.data.keyword.iot_short_notm}} instance, the credentials of the received event identify the sending device, making it impossible for a device to impersonate another device.

Events can be published at any of the three [quality of service (QoS) levels](../../reference/mqtt/index.html#qos-levels) that are defined by the MQTT protocol.  By default events will be published as QoS level 0.

### Publish events with the default QoS level

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

myClient.publishEvent("status", event);
```


### Increasing the QoS level for an event

You can increase the [QoS levels](../../reference/mqtt/index.html#qos-levels) for events that are published. Events with a higher QoS level than zero might take longer to publish, due to the extra confirmation receipt information that is included.

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

//Registered flow allows 0, 1 and 2 QoS
myClient.publishEvent("status", event, 2);
```

### Publish event using HTTP(s)

Apart from MQTT, the devices can publish events to the {{site.data.keyword.iot_short_notm}} by using HTTP(s) and by also following three simple steps,

* Construct a DeviceClient instance using the properties file.
* Construct an event that needs to be published.
* Specify the event name and publish the event using publishEventOverHTTP() method as follows:

``` sourceCode
DeviceClient myClient = new DeviceClient(deviceProps);

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

int httpCode = myClient.publishEventOverHTTP("blink", event);
```

You can find the entire code in the [HttpDeviceEventPublish] device example.

Based on the settings in the properties file, the publishEventOverHTTP() method either publishes the event in Quickstart mode or in registered flow mode. When the Organization ID mentioned in the properties file is quickstart, the publishEventOverHTTP() method publishes the event to the device example quickstart service and publishes the event in plain HTTP format. But when valid registered organization is mentioned in the properties file, this method always publishes the event in HTTPS (HTTP over SSL), so all the communication is secured.

The event in HTTP(s) is published at most once QoS, so the device needs to implement the retry logic when there is an error.

[HttpDeviceEventPublish]: https://github.com/ibm-messaging/iot-device-samples/blob/master/java/device-samples/src/main/java/com/ibm/iotf/sample/client/device/HttpDeviceEventPublish.java

## Handling commands
{: #handling_commands}

When the device client connects it automatically subscribes to any commands for this device. To process specific commands you need to register a command callback method.
The messages are returned as an instance of the Command class which has the following properties:

* payload - java.lang.String
* format - java.lang.String
* command - java.lang.String
* timestamp - org.joda.time.DateTime

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
