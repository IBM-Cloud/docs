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


# Python for device developers
{: #python}

You can use Python to build and develop device code to interact with your organization on {{site.data.keyword.iot_full}}. The Python client for {{site.data.keyword.iot_short_notm}} provides an API to facilitate simple interaction with {{site.data.keyword.iot_short_notm}} features by abstracting away the underlying protocols such as MQTT and HTTP.
{:shortdesc}

Use the information and examples that are provided to start developing your devices by using Python.

## Downloading the Python client and resources
{: #python_client_download}

To access the Python client for {{site.data.keyword.iot_short_notm}} and other available resources, go to the [iot-python ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-python){: new_window} repository in GitHub and complete the installation instructions.

## Constructor
{: #constructor}

The options dictionary creates definitions that are used to interact with the {{site.data.keyword.iot_short_notm}} module. The constructor builds the client instance and accepts an options dictionary that contains the following definitions:

|Definition|Description |
|:---|:---|
|`orgId`|Your organization ID.|
|`type`|The type of the device. The device type is a grouping for devices that perform a specific task, for example, "weatherballoon".|
|`id`|A unique ID to identify a device. Typically, for a given device type, the device ID is a unique identifier of that device, for example, a serial number or MAC address.|
|`auth-method`|The method of authentication. The only method that is supported is `token`.|
|`auth-token`|An API key token, which is also required when you set the value of auth-method to `token`.|
|`clean-session`|A true or false value that is required only if you want to connect the application in durable subscription mode. By default, `clean-session` is set to true.|

If no options dictionary is provided, the client connects to the {{site.data.keyword.iot_short_notm}} Quickstart service as an unregistered device.

```python

import ibmiotf.device
try:
  options = {
    "org": orgId,
    "type": deviceType,
    "id": deviceId,
    "auth-method": authMethod,
    "auth-token": authToken,
    "clean-session": true
  }
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

### Using a configuration file

Instead of defining an options dictionary directly, you can also define an options dictionary separately in a configuration file, as outlined in the following code sample:

```python

import ibmiotf.device
try:
  options = ibmiotf.device.ParseConfigFile(configFilePath)
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

The configuration file that contains the options dictionary must be in the following format:

```python

[device]
org=orgID
type=deviceType
id=deviceId
auth-method=token
auth-token=token
clean-session=true/false
```

## Publishing events
{: #publishing_events}

Events are the mechanism by which devices publish data to the {{site.data.keyword.iot_short_notm}}. The device controls the content of the event and assigns a name for each event that it sends.

When an event is received by the {{site.data.keyword.iot_short_notm}} instance, the credentials of the received event identify the sending device, which means that a device cannot impersonate another device.

Events can be published with any of the three quality of service (QoS) levels that are defined by the MQTT protocol.  By default, events are published with a QoS level of `0`.

### Publish an event by using the default quality of service

```
client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData)
```

### Increasing the QoS level for an event

You can increase the [quality of service(QoS) level](../../reference/mqtt/index.html#qos-levels) for events that are published. Events that have a higher QoS level than `0` can take longer to publish because of the extra confirmation receipt information that is included.

**Note:** The Quickstart flow mode supports only a QoS level of `0`.

```
client.connect()
myQosLevel=2
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData, myQosLevel)
```
## Handling commands
{: #handling_commands}

When the device client connects, it automatically subscribes to any command that is specified for this device. To process specific commands, you need to register a command callback method. The messages are returned as an instance of the Command class, which contains the following properties:

|Property|Data type|Description|
|:---|:---|
|`command`|String|Identifies the command.|
|`format`|String|The format can be any string, for example JSON.|
|`data`|Dictionary|The data for the payload. Maximum length is 131072 bytes.|
|`timestamp`|Date and time|The date and time of the event.|


```python

def myCommandCallback(cmd):
  print("Command received: %s" % cmd.data)
  if cmd.command == "setInterval":
    if 'interval' not in cmd.data:
      print("Error - command is missing required information: 'interval'")
    else:
      interval = cmd.data['interval']
  elif cmd.command == "print":
    if 'message' not in cmd.data:
      print("Error - command is missing required information: 'message'")
    else:
      print(cmd.data['message'])

...
client.connect()
client.commandCallback = myCommandCallback
```

## Custom message format support
{: #custom_message_format}

By default, the message format is set to ``json``, which means that the library supports the encoding and decoding of Python dictionary objects in JSON format. When the message format is set to ``json-iotf``, the message is encoded in accordance with the {{site.data.keyword.iot_short_notm}} JSON Payload specification. To add support for your own custom message formats, see the [Custom Message Format sample ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-python/tree/master/samples/customMessageFormat){: new_window} in GitHub.

When you create a custom encoder module, you must register it in the device client as outlined in the following example:

```python

import myCustomCodec

client.setMessageEncoderModule("custom", myCustomCodec)
client.publishEvent("status", "custom", myData)
```
If an event is sent in an unknown format or if a device does not recognize the format, the device library returns a ``MissingMessageDecoderException`` condition.
