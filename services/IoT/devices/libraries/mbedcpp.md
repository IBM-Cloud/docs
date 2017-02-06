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


# mBed C++ for device developers
{: #mbedcpp}

Use the [mBed C++ client library](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/) to easily connect [mBed devices](https://www.mbed.com/en/), such as [LPC1768](https://developer.mbed.org/platforms/mbed-LPC1768/) or [FRDM-K64F](https://developer.mbed.org/platforms/FRDM-K64F/), to the {{site.data.keyword.iot_full}} service.
{:shortdesc}

For more information, see [ibmiotf](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/) on [developer.mbed.org](https://developer.mbed.org/).

Although the library uses C++, it still avoids dynamic memory allocations and the use of STL functions, because the mBed devices sometimes have idiosyncratic memory models that make porting difficult. In any case, the library allows you to make memory use as predictable as possible.

## Dependencies
{: #dependencies}

|Dependency |Description|
|:---|:---|
|[Eclipse Paho MQTT library](https://developer.mbed.org/teams/mqtt/code/MQTT/)|Provides an MQTT client library for mBed devices. For more information, see  [Embedded MQTT C/C++ client libraries](http://www.eclipse.org/paho/clients/c/embedded/)|
|[EthernetInterface library](https://developer.mbed.org/users/mbed_official/code/EthernetInterface/)|An mBed IP library over Ethernet.|

## How to use the library
{: #library_use}

Use the [mBed compiler](https://developer.mbed.org/compiler/) to create your applications when you use the mBed C++ IBMIoTF client library. The mBed compiler provides a lightweight online C/C++ IDE that is configured for writing, compiling, and downloading programs to run on your mBed microcontroller.

**Note:** You don't have to install or set up anything to get running with mBed.

For information on how to connect an ARM mBed NXP LPC 1768 microcontroller to the {{site.data.keyword.iot_short_notm}}, see the [mBed C++ client library for IBM Watson IoT Platform](https://developer.ibm.com/recipes/tutorials/mbed-c-client-library-for-ibm-iot-foundation/) recipe.

## Constructor
{: #constructor}

The constructor builds the client instance and accepts the following parameters:

|Parameter |Description |
|:---|:---|
|`org` |Your organization ID. This value is required. If you are using a Quickstart flow, specify `quickstart`.|
|`type`   |The type of your device. This field is required.|
|`id`   |The  ID of your device. This field is required.|
|`auth-method`   |The method of authentication, which is an optional field that is needed only for a registered flow. The only value that is currently supported is `token`.|
|`auth-token`   |An authentication token to securely connect your device to Watson IoT Platform. This is an optional field that is needed only for a registered flow.|

These parameters create definitions that are used to interact with the {{site.data.keyword.iot_short_notm}} service.

The following code sample outlines how a DeviceClient instance can interact with the {{site.data.keyword.iot_short_notm}} Quickstart service:

```
  #include "DeviceClient.h"
  ....
  ....

  // Set {{site.data.keyword.iot_short_notm}} connection parameters
  char organization[11] = "quickstart";     // For a registered connection, replace with your org
  char deviceType[8] = "LPC1768";           // For a registered connection, replace with your device type
  char deviceId[3] = "01";                  // For a registered connection, replace with your device id

  // Create DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId);

  // Get the DeviceID(MAC Address) if we are in quickstart mode and device ID is not specified
  if((strcmp(organization, QUICKSTART) == 0) && (strcmp("", deviceId) == 0))
  {
  	char tmpBuf[50];
  	client.getDeviceId(tmpBuf, sizeof(tmpBuf));
  }
  ....
```

As shown in the previous code sample, if the device ID is not specified, the DeviceClient uses the MAC address of the device as device ID to connect to the {{site.data.keyword.iot_short_notm}}. The device code can use `getDeviceId()` method to retrieve the device ID from the DeviceClient instance.

The following code block shows how to create a DeviceClient instance to interact with the {{site.data.keyword.iot_short_notm}} Registered organization.

```
  #include "DeviceClient.h"
  ....
  ....

  // Set {{site.data.keyword.iot_short_notm}} connection parameters
  char organization[11] = "hrcl78";
  char deviceType[8] = "LPC1768";
  char deviceId[3] = "LPC176801";
  char method[6] = "token";
  char token[9] = "password";

  // Create DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId, method, token);
  ....
```

## Connecting to the {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

The device can connect to the {{site.data.keyword.iot_short_notm}} by calling the connect function on the DeviceClient instance.

```
  #include "DeviceClient.h"
  ....
  ....

  // Create DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId, method, token);

  bool status = client.connect();

```
After the successful connection, the device can publish events to the {{site.data.keyword.iot_short_notm}} and can listen for commands.

Also, the device can query the status of the connection by using the `isConnected()` method, which is shown in the following example:

```
  #include "DeviceClient.h"
  ....
  ....

  client.isConnected();

```


## Publishing events
{: #publishing_events}

Events are the mechanism by which devices publish data to the {{site.data.keyword.iot_short_notm}}. The device controls the content of the event and assigns a name for each event that it sends.

When an event is received by the {{site.data.keyword.iot_short_notm}} instance, the credentials of the received event identify the sending device, which means that a device cannot impersonate another device.

Events can be published at any of the three [quality of service (QoS) levels](../../reference/mqtt/index.html#qos-levels) that are defined by the MQTT protocol. By default, events are published at QoS 0.

### Publish event by using the default quality of service

The following sample shows how to publish the following data points to {{site.data.keyword.iot_short_notm}} in JSON format:

- LPC1768, such as the x,y and z axis
- Joystick position
- Current temperature reading

```
	boolean status = client.connect();

	// Create buffer to hold the event
	char buf[250];

	// Construct an event message with desired datapoints in JSON format
	sprintf(buf,
            "{\"d\":{\"myName\":\"IoT mbed\",\"accelX\":%0.4f,\"accelY\":%0.4f,\"accelZ\":%0.4f,
            \"temp\":%0.4f,\"joystick\":\"%s\",\"potentiometer1\":%0.4f,\"potentiometer2\":%0.4f}}",
            MMA.x(), MMA.y(), MMA.z(), sensor.temp(), joystickPos, ain1.read(), ain2.read());

        status = client.publishEvent("blink", buf);
	....
```
For the complete sample, see [ IBMIoTClientLibrarySample](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/file/e58533b6bc6b/src/Main.cpp).

### Increasing the QoS level for an event

You can increase the [QoS levels](../../reference/mqtt/index.html#qos-levels) for events that are published. Events that have a QoS level that is greater than `0` might take longer to publish because of the extra confirmation receipt information that is included.

**Note:** The Quickstart flow mode only supports QoS 0.

```
	#include "MQTTClient.h"

	boolean status = client.connect();

	// Create buffer to hold the event
	char buf[250];

	// Construct an event message with desired datapoints in JSON format
	sprintf(buf,
            "{\"d\":{\"myName\":\"IoT mbed\",\"accelX\":%0.4f,\"accelY\":%0.4f,\"accelZ\":%0.4f,
            \"temp\":%0.4f,\"joystick\":\"%s\",\"potentiometer1\":%0.4f,\"potentiometer2\":%0.4f}}",
            MMA.x(), MMA.y(), MMA.z(), sensor.temp(), joystickPos, ain1.read(), ain2.read());

        status = client.publishEvent("blink", buf, MQTT::QOS2);
	....
```

### Handling the connection lost error during the event publish


When the `publishEvent()` method returns the false value, you can check the status of the connection and call `reConnect()` if the connection is lost.

```
	#include "MQTTClient.h"

	status = client.publishEvent("blink", buf, MQTT::QOS2);

	if(status == false) {
	    // Check if connection is lost and retry
	    while(!client.isConnected())
	    {
	        client.reConnect();
	        wait(5.0);
	    }
	}
	....
```
The library does not store the events that are published during the unconnected state, so the device needs to call the `publishEvent()` method again in order to send those events after the connection is reestablished.


## Handling commands
{: #handling_commands}

When the device client connects, it automatically subscribes to any commands for this device. To process specific commands you need to register a command callback method.
The messages are returned as an instance of the Command class, which has the following properties:

|Property |Description|
|:---|:---|
|`command` | The name of the command that was invoked.|  
|`format`  |The format of the event. The format can be any string, for example JSON. |
|`payload`  |The data for the command payload. Maximum length is 131072 bytes. |


The following code defines a sample command callback function that processes the LED blink interval command from the application and sets the function handle on the DeviceClient instance so that the callback method is run whenever the device receives the blink command.

```
    #include "DeviceClient.h"
    #include "Command.h"

    // Process the command and set the LED blink interval
    void processCommand(IoTF::Command &cmd)
    {
        if (strcmp(cmd.getCommand(), "blink") == 0)
    	{
    	    char *payload = cmd.getPayload();
    	    char* pos = strchr(payload, '}');
    	    if (pos != NULL) {
    	        *pos = '\0';
    	        char* ratepos = strstr(payload, "rate");
    	        if(ratepos == NULL)
    	            return;
    	        if ((pos = strchr(ratepos, ':')) != NULL)
    	        {
    	            int blink_rate = atoi(pos + 1);
    	            blink_interval = (blink_rate <= 0) ? 0 : (blink_rate > 50 ? 1 : 50/blink_rate);
    	        }
    	    }
    	} else {
            WARN("Unsupported command: %s\n", cmd.getCommand());
        }
    }

    client.setCommandCallback(processCommand);

    client.yield(1000);  // allow the MQTT client to receive messages
    ....
```
For the complete sample, see [ IBMIoTClientLibrarySample](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/file/e58533b6bc6b/src/Main.cpp).

**Note:** The `client.yield()` function must be called periodically to receive commands.
The `client.yield()` function enables the device to receive commands from the Watson IoT Platform and keeps the connection alive. If the `client.yield()` function is not called within the time frame that is specified by the keepAlive interval, then any commands that are sent from the platform will not be received by the device. The value that is assigned to the `client.yield()` function specifies length of time (in milliseconds) that data can be read from the socket before control is returned to the application.

## Disconnecting the client
{: #disconnect_client}

To disconnect the client and release the connections, run the following code snippet:

```
	...
	client.disconnect();
	....
```
## Samples
{: #samples}

[IBMIoTClientLibrarySample](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/) is a code sample that shows how to use the {{site.data.keyword.iot_short_notm}} client library to connect the mbed LPC1768 or FRDM-K64F devices to the service instance.
