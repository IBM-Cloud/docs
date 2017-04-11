---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

  {:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# ﻿C# for application developers
{: #c_sharp}


You can use C# to build and customize applications that interact with your organization on {{site.data.keyword.iot_full}}. Use the information and examples that are provided to start developing your applications by using C#.
{:shortdesc}

## Downloading the C# client and resources
{: #csharp_client_download}

To access the C# client libraries and samples for {{site.data.keyword.iot_short_notm}}, go to the [iot-csharp ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-csharp){: new_window} repository in GitHub and complete the installation instructions.


## Constructor
{: #constructor}

The constructor builds the client instance and accepts arguments that contain the following definitions:

|Definition |Description |
|:---|:---|
|`orgId`   |Your organization ID.|
|`appId`   |The unique ID of an application in your organization.|
|`auth-key`   |An API key to securely connect your application to Watson IoT Platform|
|`auth-token`   |An API key token to securely connect your application to Watson IoT Platform.|

If `appId` is the only argument that is provided, the client connects to the {{site.data.keyword.iot_short_notm}} Quickstart service as an unregistered device. The arguments list defines how the client connects to the  {{site.data.keyword.iot_short_notm}} module.

```
ApplicationClient applicationClient = new ApplicationClient(orgId, appId, apiKey, authToken);  
applicationClient.connect();
```


## Subscribing to device events
{: #subscribe_device_events}

Devices use events to publish data to the {{site.data.keyword.iot_short_notm}} instance. The device controls the content of the event and assigns a name to each event that it sends.

When an event is received by the {{site.data.keyword.iot_short_notm}} instance, the credentials of the received event identify the sending device, which means that a device cannot impersonate another device.

By default, applications subscribe to all events from all connected devices. Use the device type, device ID, event, and message format parameters to control the scope of the subscription. The following code samples show how you can define the scope of a subscription by using these parameters:

### Subscribing to all events from all devices

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents();
```

### Subscribing to all events from all devices of a specific type

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType);
```

### Subscribing to a specific event from all devices

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(evt);
```

###  Subscribing to a specific event from two or more different devices:

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt);
```

### Subscribing to all events that are published in JSON format

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt, "json", 0);
```

**Note**: A single client instance can support multiple subscriptions.

### Handling events from devices

To process events that are received by your subscriptions, register an Event callback method as shown in the following example:

```
public static void processEvent(String eventName, string eventFormat, string eventData) {
// Do something
}
applicationClient.connect();
applicationClient.eventCallback += processEvent;
applicationClient.subscribeToDeviceEvents();
```
The following table describes the parameters of the Event callback method:

|Parameter|Data type|Description|
|:---|:---|
|`eventName`|String|Identifies the event. |
|`eventFormat`|String| The format can be any string, for example JSON.|
|`eventData`|Dictionary| The data for the message payload. Maximum length is 131072 bytes.|


## Subscribing to device status
{: #subscribe_device_status}

By default, the subscription is set to receive status updates for all connected devices. Use the device type and device ID parameters to control the scope of the subscription. The following code samples show how you can define the scope of a subscription by using these parameters:

### Subscribing to status updates for all devices

```
applicationClient.connect();
applicationClient.subscribeToDeviceStatus += processDeviceStatus;
applicationClient.subscribeToDeviceStatus();
```

### Subscribing to status updates for two different devices

```
applicationClient.connect();
applicationClient.subscribeToDeviceStatus += processDeviceStatus;
applicationClient.subscribeToDeviceStatus(deviceType, deviceId);
```

**Note**: A single client instance can support multiple subscriptions.

### Handling status updates from devices

To process the status updates that are received by your subscriptions, register an Event callback method as shown in the following example:

```
public static void processDeviceStatus(String deviceType, string deviceId, string data)
        {
           //
        }
applicationClient.connect();
applicationClient.appStatusCallback += processAppStatus;
applicationClient.subscribeToApplicationStatus();
```

## Publishing events from devices
{: #publish_events_devices}

Applications can publish events as if they originated from a device.

```
applicationClient.connect();
applicationClient.publishEvent(deviceType, deviceId, evt, data, 0);

```

The following table describes the parameters that are specified in the `publishEvent()` method:

|Parameter|Data type|Description|
|:---|:---|
|`deviceType`|String| The device type. Typically, the deviceType is a grouping for devices that perform a specific task, for example "weatherballoon".|
|`deviceId`|String| The ID of the device. Typically, for a given device type, the deviceId is a unique identifier of that device, for example a serial number or MAC address.|
|`evt`|String| The name of the event.|
|`format`|String| The format can be any string, for example JSON.|
|`data`|Dictionary| The data for the message payload. Maximum length is 131072 bytes.|
|`QoS`|Integer| The Quality of Service. Valid values are `0`, `1`, `2`. |


## Publishing commands to devices
{: #publish_commands_devices}

Applications can publish commands to connected devices.

```
applicationClient.connect();
applicationClient.publishCommand(deviceType, deviceId, "testcmd", "json", data, 0);
```
The following table describes the parameters that are specified in the `publishCommand()` method:

|Parameter|Data type|Description|
|:---|:---|
|`deviceType`|String| The device type. Typically, the deviceType is a grouping for devices that perform a specific task, for example "weatherballoon".|
|`deviceId`|String| The ID of the device. Typically, for a given device type, the deviceId is a unique identifier of that device, for example a serial number or MAC address.|
|`command`|String| The name of the command.|
|`format`|String| The format can be any string, for example JSON.|
|`data`|Dictionary| The data for the message payload. Maximum length is 131072 bytes.|
|`QoS`|Integer| The Quality of Service. Valid values are `0`, `1`, `2`. |
