---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# ﻿C# for application developers
{: #c_sharp}

For more information, see [iot-csharp](https://github.com/IoT-Analytics/iot-csharp) in GitHub.


## Constructor
{: #constructor}

The constructor builds the client instance, and accepts arguments that contain the following definitions:

| Definition     |Description     |
|----------------|----------------|
|``orgId``   |Your organization ID
|``appId``   |The unique ID of an application within your organization|
|``auth-key``   |An optional API key, which is required when auth-method is ``apikey``|
|``auth-token``   |API key token, which is required when auth-method is ``apikey``|

If ``appId`` is the only argument that is provided, the client connects to the {{site.data.keyword.iot_full}} Quickstart service and defaults to an unregistered device. The argument lists create definitions that are used to interact with the {{site.data.keyword.iot_short_notm}} module.



```
ApplciationClient applicationClient = new ApplciationClient(orgId, appId, apiKey, authToken);  
applicationClient.connect();
```

## Subscribing to device events
{: #subscribe_device_events}

Devices use events to publish data to the {{site.data.keyword.iot_short_notm}} instance. The device controls the content of the event and assigns a name to each event that it sends.

When an event is received by the {{site.data.keyword.iot_short_notm}} instance, the credentials of the received event identify the sending device, making it impossible for a device to impersonate another device.

By default, applications can subscribe to all events from all connected devices. Use the ``type``, ``id``, ``event``, and ``msgFormat`` parameters to control the scope of the subscription. A single client instance can support multiple subscriptions. The following code samples outline how you can subscribe to devices that depend on ``device type``, ``id``, ``event``, and ``msgFormat`` parameters.

### Subscribing to all events from all devices:

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents();
```

### Subscribing to all events from all devices of a specific type:

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType);
```

### Subscribing to a specific event from all devices:

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(evt);
```

###  Subscribing to a specific event from two or more different devices

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt);
```

### Subscribing to all events published by a device in JSON format

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt, "json", 0);
```

### Handling events from devices

To process events that are received by your subscriptions, register an event callback method as outlined in the following example:

```
public static void processEvent(String eventName, string format, string data) {
// Do something
}
applicationClient.connect();
applicationClient.eventCallback += processEvent;
applicationClient.subscribeToDeviceEvents();
```
Where:

- ``event.device`` is a string that uniquely identifies the device across all types of devices in the organization
- ``eventName`` is a string
- ``eventFormat`` is a string
- ``eventData`` is a string

## Subscribing to device status
{: #subscribe_device_status}

By default, the subscription is set to receive status updates for all connected devices. Use the device type and ID parameters to control the scope of the subscription. A single client can support multiple subscriptions.

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

### Handling status updates from devices

To process the status updates that are received by your subscriptions, register an event callback method, as outlined in the following example:

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

## Publishing commands to devices
{: #publish_commands_devices}

Applications can publish commands to connected devices.

```
applicationClient.connect();
applicationClient.publishCommand(deviceType, deviceId, "testcmd", "json", data, 0);
```
