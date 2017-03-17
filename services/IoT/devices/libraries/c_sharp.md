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


# ﻿C# for device developers
{: #c_sharp}

You can use C# to build and customize devices that interact with your organization on {{site.data.keyword.iot_full}}. Use the information and examples that are provided to start developing your devices by using C#.
{:shortdesc}

## Downloading the C# client and resources
{: #csharp_client_download}

To access the C# client and resources for {{site.data.keyword.iot_short_notm}}, go to the [iot-csharp ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-csharp){: new_window} repository in GitHub and complete the installation instructions.


## Constructor
{: #constructor}

The constructor builds the client instance and accepts arguments that contain the following definitions:

|Definition |Description |
|:---|:---|
|`orgId`|Your organization ID.|
|`deviceType`|The type of your device.|
|`deviceId` |The ID of your device.|
|`auth-method`   |The method of authentication to be used. The only value that is currently supported is `token`.|
|`auth-token`   |An authentication token to securely connect your device to Watson IoT Platform.|


If `deviceId` and `deviceType` are the only arguments that are provided, the client connects to the {{site.data.keyword.iot_short_notm}} Quickstart service as an unregistered device. The arguments list defines how the client connects to the {{site.data.keyword.iot_short_notm}} module.


```
namespace com.ibm.iotf.client

public DeviceClient(string orgId, string deviceType, string deviceID, string auth-method, string auth-token)
        : base(orgId, "d" + CLIENT_ID_DELIMITER + orgId + CLIENT_ID_DELIMITER + deviceType + CLIENT_ID_DELIMITER + deviceID, "use-token-auth", auth-token)
    {

    }
```

## Publishing events
{: #publishing-events}

Devices use events to publish data to the {{site.data.keyword.iot_short_notm}} instance. The device controls the content of the event and assigns a name to each event that it sends.

When an event is received by the {{site.data.keyword.iot_short_notm}} instance, the credentials of the incoming event identify the sending device, which means that a device cannot impersonate another device.

Events can be published at any of the three [quality of service (QoS) levels](../mqtt.html#managed-devices), which are defined by the MQTT protocol. By default, events are published at QoS 0.


## Publishing an event by using the default quality of service level
{: #publish_event_default_qos}

```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}");
```


## Publishing an event by using a user-defined quality of service level
{: #publish_event_user_qos}

Events that are published at an MQTT QoS level that is greater than `0` include extra receipt confirmation information and might take longer to publish than events that have a QoS level of `0`.


```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}", 2);
```

## Handling commands
{: #handling_commands}

When a device client connects, it automatically subscribes to any commands for this device. To process specific commands, you must register a command callback method as shown in the following example:

```
public static void processCommand(string cmdName, string cmdFormat, string cmdData) {
...
 }
```

```
deviceClient.connect();
deviceClient.commandCallback += processCommand;
```
The following table describes the parameters of the commandCallback method:

|Parameter|Data type|Description|
|:---|:---|
|`cmdName`|String|Identifies the command. |
|`cmdFormat`|String|The format can be any string, for example JSON.|
|`cmdData`|Dictionary|The data for the payload. Maximum length is 131072 bytes.|
