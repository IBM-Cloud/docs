---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# ﻿C# for device developers
{: #c_sharp}

For more information, see [iot-csharp](https://github.com/IoT-Analytics/iot-csharp) in GitHub.





## Constructor
{: #constructor}

The constructor builds the client instance, and accepts arguments that contain the following definitions:

| Definition     |Description     |
|----------------|----------------|
|``orgId``|Your organization ID
|``deviceType``|The type of your device|
|``deviceId`` |The ID of your device|
|``auth-method`` |Method of authentication whereby the only value that is currently supported is 'token')|
|``auth-token``|API key token, which is required only if ``auth-method`` is set to 'token'|

If ``deviceId`` and ``deviceType`` are provided, the client connects to the {{site.data.keyword.iot_full}} Quickstart service, and defaults to an unregistered device. The argument lists create definitions that are used to interact with the {{site.data.keyword.iot_short_notm}} module.





```
namespace com.ibm.iotf.client

public DeviceClient(string orgId, string deviceType, string deviceID, string authmethod, string authtoken)
        : base(orgId, "d" + CLIENT_ID_DELIMITER + orgId + CLIENT_ID_DELIMITER + deviceType + CLIENT_ID_DELIMITER + deviceID, "use-token-auth", authtoken)
    {

    }
```

## Publishing events
{: #publishing-events}

Devices use events to publish data to the {{site.data.keyword.iot_short_notm}} instance. The device controls the content of the event and assigns a name to each event that it sends.

When an event is received by the {{site.data.keyword.iot_short_notm}} instance, the credentials of the incoming event identify the sending device, making it impossible for a device to impersonate another device.

Events can be published at any of the three [quality of service (QoS) levels](../mqtt.html#managed-devices), as defined by the MQTT protocol. By default, events are published as QoS level zero.


## Publishing an event by using the default quality of service level
{: #publish_event_default_qos}

```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}");
```


## Publishing an event by using a user-defined quality of service level
{: #publish_event_user_qos}

Events that are published with an MQTT QoS level greater than zero include extra receipt confirmation information, and therefore might take longer to publish than events with a QoS level of zero.


```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}", 2);
```

## Handling commands
{: #handling_commands}

When a device client connects, it automatically subscribes to any commands for this device. To process specific commands, you must register a command callback method.

```
public static void processCommand(string cmdName, string format, string data) {
...
 }
```

```
deviceClient.connect();
deviceClient.commandCallback += processCommand;
```
