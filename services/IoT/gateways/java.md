---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Java for gateway developers
{: #IoT_JavaGateway}
*Last updated: 13 May 2016*

This topic explains how you can use Java to develop gateways in {{site.data.keyword.iot_full}}. For more information, see [iot-java](https://github.com/ibm-messaging/iot-java) in GitHub
{:shortdesc}

## Constructor
{: #IoT_constructor}

The constructor builds the Gateway client instance, and accepts a Properties object containing the following definitions:

-   ``org`` - Your organization ID.
-   ``type`` - The type of your Gateway device.
-   ``id`` - The ID of your Gateway.
-   ``auth-method`` - Method of authentication (The only value currently
    supported is "token").
-   ``auth-token`` - API key token.

The Properties object creates definitions which are used to interact with the {{site.data.keyword.iot_short}} module.

The following code sample shows how to construct the GatewayClient instance:

```

Properties options = new Properties();
options.setProperty("org", "<Your Organization ID>");
options.setProperty("type", "<The Gateway Device Type>");
options.setProperty("id", "The Gateway Device ID");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "API token");

GatewayClient gwClient = new GatewayClient(options);
```

### Using a configuration file
{: #IoT_usingConfigFile}

Instead of including a Properties object directly, you can use a configuration file containing the name-value pairs for Properties. If you are using a configuration file containing a Properties object, use
the following code format.

```   
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
...
```

The Gateway device configuration file must be in the following format:

```
    [Gateway]
    org=$orgId
    typ=$myGatewayDeviceType
    id=$myGatewayDeviceId
    auth-method=token
    auth-token=$token

```

## Connecting to the {{site.data.keyword.iot_short}}
{: #IoT_connectPlatform}

Connect to the {{site.data.keyword.iot_short}} by calling the *connect* function.

```   
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);

gwClient.connect();
```

After you successfully connect to the {{site.data.keyword.iot_short}}, the gateway client can perform the following operations:

-   Publish events for itself and on behalf of devices connected behind the Gateway
-   Subscribe to commands for itself and on behalf of devices behind the Gateway


## Register devices using the {{site.data.keyword.iot_short}} API
{: #IoT_regdevices}

The following list outlineds the different ways that you can register devices that are behind the gateway in {{site.data.keyword.iot_short}}:

-   **Auto registration**: The device gets added automatically in {{site.data.keyword.iot_short}} when Gateway publishes any event/subscribes to any commands for the devices connected to it.
-   **API**: The {{site.data.keyword.iot_short}} API can be used to register the devices to the {{site.data.keyword.iot_short}}.

The {{site.data.keyword.iot_short}} API can be used to register the devices (that are connected to the Gateway) to the {{site.data.keyword.iot_short}}. The APIClient simplifies the interactions with {{site.data.keyword.iot_short}} API. Get the APIClient instance by invoking the api() method, as outlined in the following example:

```   
import com.ibm.iotf.client.api.APIClient;

....

GatewayClient gwClient = new GatewayClient(props);
gwClient.connect();

APIClient api = gwClient.api();
```

Once you get the handle of APIClient, you can add the devices. Following code snippet shows how to add a device to a Gateway in {{site.data.keyword.iot_short}},

```   
GatewayClient gwClient = new GatewayClient(props);
gwClient.connect();

String deviceToBeAdded = "{\"deviceId\": \"" + DEVICE_ID +
                    "\",\"authToken\": \"qwer123\"}";

JsonParser parser = new JsonParser();
JsonElement input = parser.parse(deviceToBeAdded);
JsonObject response = this.gwClient.api().registerDeviceUnderGateway(DEVICE_TYPE, gwDeviceId, gwDeviceType, input);
```

The ``gwDeviceId`` and ``gwDeviceType`` are the gateway properties to which this device will be attached to when its registered.



## Publishing events
{: #IoT_pubevents}

Events are the mechanism by which Gateways/devices publish data to the {{site.data.keyword.iot_short}}. The Gateway/device controls the content of the event and assigns a name for each event it sends.

**The Gateway can publish events from itself and on behalf of any device connected via the Gateway**.

When an event is received by the {{site.data.keyword.iot_short}}, the credentials of the connection on which the event was received are used to determine which Gateway sent the event. With this architecture it is impossible for a Gateway to impersonate another device.

Events can be published at any of the three [quality of service levels](../messaging/mqtt.html#/) thay are defined by the MQTT protocol. By default events are published as qos level 0.

### Publish gateway event using default quality of service


```   
gwClient.connect();
JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event);
```

### Increasing the QoS level for a gateway event

You can increase the [quality of service(QoS) level](../messaging/mqtt.html#/) for gateway events that are published. Gateway events with a higher QoS level than zero might take longer to publish, due to the extra confirmation receipt information that is included.

**Note:** The Quickstart flow mode only supports a QoS level of zero.



```   
gwClient.connect();
JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event, 2);
```

## Publishing events from devices
{: #IoT_pubeventdevices}

The Gateway can publish events on behalf of any device connected via the Gateway by passing the appropriate ``typeId`` and ``deviceId`` based on the origin of the event:

```   
gwClient.connect()

//Generate the event to be published
JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  60);
event.addProperty("mem",  40);

// publish the event on behalf of device
 gwClient.publishDeviceEvent(deviceType, deviceId, eventName, event);
```

You can use the overloaded ``publishDeviceEvent()`` method to publish the device event in the desired quality of service. For more information about the topic structure, see the [MQTT connectivity for  Gateways](https://docs.internetofthings.ibmcloud.com/gateways/mqtt.html) documentation.


## Handling commands
{: #IoT_handlingCommands}

The gateway can subscribe to commands directed at the gateway itself and to any device connected via the gateway. When the gateway client connects, it automatically subscribes to any commands for this Gateway.
To subscribe to any commands for the devices connected via the gateway, use one of the overloaded ``subscribeToDeviceCommands()`` methods, as outlined in the following example:

```   
gwClient.connect()

// subscribe to commands on behalf of device
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

To process specific commands you need to register a command callback method. The messages are returned as an instance of the Command class, which contains the following properties:

-   deviceType - The device type for which the command is received.
-   deviceId - The device id for which the command is received, Could be the Gateway or any device connected via the Gateway.
-   payload - The command payload.
-   format - The format of the command payload, currently only JSON format is supported in the Java Client Library.
-   command - The name of the command.
-   timestamp - The org.joda.time.DateTime when the command is sent.

A sample implementation of the Command callback is shown below,

```   
import com.ibm.iotf.client.gateway.Command;
import com.ibm.iotf.client.gateway.GatewayCallback;

public class GatewayCommandCallback implements GatewayCallback, Runnable {
    // A queue to hold & process the commands
    private BlockingQueue<Command> queue = new LinkedBlockingQueue<Command>();

    public void processCommand(Command cmd) {
        queue.put(cmd);
    }

    public void run() {
        while(true) {
            Command cmd = queue.take();
            System.out.println("Command " + cmd.getPayload());

            // code to process the command
        }
    }

    /**
     * If a gateway subscribes to a topic of a device or sends data on behalf of a device
 * where the gateway does not have permission for, the message or the subscription is being ignored.
 * This behavior is different compared to applications where the connection will be terminated.
 * The Gateway will be notified on the notification topic:
 */
    @Override
public void processNotification(Notification notification) {

}
}
```

Once the Command callback is added to the GatewayClient, the processCommand() method is invoked whenever any command is published on the subscribed criteria, The following snippet shows how to add the command call back into GatewayClient instance,

```   
gwClient.connect()
GatewayCommandCallback callback = new GatewayCommandCallback();
gwClient.setGatewayCallback(callback);
//Subscribe to device connected to the Gateway
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

Overloaded methods are available to control the command subscription.

## List devices connected through the gateway
{: #IoT_listDevices}

Invoke the method getDevicesConnectedThroughGateway() to retrieve all devices that are connected through the specified gateway(typeId, deviceId) to {{site.data.keyword.iot_short}}:

```   
gwClient.connect()
gwClient.api().getDevicesConnectedThroughGateway(gatewayType, gatewayId);
```

## Examples
{: #IoT_examples}

-   [SampleRasPiGateway](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples) -
    This Java project contains 3 samples, which can help you to connect your own Gateway and devices behind the Gateway to {{site.data.keyword.iot_short}}. All of the samples use the Java Client Library for {{site.data.keyword.iot_short}} to simplify the gateway interactions with the platform.

## Recipes
{: #IoT_recipes}

Refer to [the recipe](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-gateway-to-watson-iot-platform/) that explains how to connect your Gateway and devices behind the Gateway
to {{site.data.keyword.iot_short}} with the sample present in this github project.

Refer to [the recipe](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/) that explains how to connect your Gateway as managed device in {{site.data.keyword.iot_short}} and perform one or more device management operations.
