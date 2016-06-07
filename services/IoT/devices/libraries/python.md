---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Python for device developers
{: #python}

For more information, see the following resources:

-  The [iot-python](https://github.com/ibm-messaging/iot-python) repository in GitHub.
-  The [ibmiotf](https://pypi.python.org/pypi/ibmiotf) repository in PyPi.




## Constructor
{: #constructor}

The constructor builds the client instance, and accepts an options dict that contains the following definitions:

| Definition    |Description     |
|----------------|----------------|
|``org`` |Your organization ID|
|``type``   |The type of your device|
|``id``   |The  ID of your device|
|``auth-method``   |Method of authentication, whereby the only value that is currently supported is “token”)|
|``auth-token``   |API key token, which is required only if ``auth-method`` is set to 'token'|

If options dict is not provided, the client connects to the {{site.data.keyword.iot_full}} Quickstart, and defaults to an unregistered device. The options dict creates definitions that are used to interact with the {{site.data.keyword.iot_short_notm}} module.

```
import ibmiotf.device
try:
  options = {
    "org": organization,
    "type": deviceType,
    "id": deviceId,
    "auth-method": authMethod,
    "auth-token": authToken
  }
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
  ...
```

### Using a configuration file


Instead of including an options dict directly, you can use a configuration file containing an options dict. If you are using a configuration file that contains an options dict, use the following code format.

``` sourceCode
import ibmiotf.device
try:
  options = ibmiotf.device.ParseConfigFile(configFilePath)
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
  ...
```

The content of the configuration file must be in the following format:
```
    [device]
    org=$orgId
    type=$myDeviceType
    id=$myDeviceId
    auth-method=token
    auth-token=$token
```
**Note:** The dollar ($) character is not required.

## Publishing events
{: #publishing_events}

Events are the mechanism by which devices publish data to the {{site.data.keyword.iot_short_notm}}. The device controls the content of the event and assigns a name for each event it sends.

When an event is received by the {{site.data.keyword.iot_short_notm}} instance, the credentials of the received event identify the sending device, making it impossible for a device to impersonate another device.

Events can be published with any of the three quality of service (QoS) levels that are defined by the MQTT protocol.  By default, events are published with a QoS level of zero.

### Publish event using default quality of service
```
client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData)
```

### Increasing the QoS level for an event

You can increase the [quality of service(QoS) level](../../reference/mqtt/mqtt.html#qos-levels) for events that are published. Events with a higher QoS level than zero might take longer to publish, due to the extra confirmation receipt information that is included.

**Note:** The Quickstart flow mode only supports a QoS level of zero.

```
client.connect()
myQosLevel=2
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData, myQosLevel)
```


## Handling commands
{: #handling_commands}

When the device client connects, it automatically subscribes to any command that is specified for this device.  To process specific commands, you need to register a command
callback method. The messages are returned as an instance of the Command class, which contains the following properties:

* command - string
* format - string
* data - dict
* timestamp - date and time

```
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

By default, `msgFormat` is set to `json`, which means that the library supports the encoding and decoding of Python dictionary objects in JSON format. When `msgFormat` is set to `json-iotf`, the message is encoded in accordance with the {{site.data.keyword.iot_short_notm}} JSON Payload specification. To add support for your own custom message formats, see the [Custom Message Format sample in GitHub](https://github.com/ibm-messaging/iot-python/tree/master/samples/customMessageFormat).

When you create a custom encoder module, you must register it in the device client. If you try to use an unknown message format when you send an event, or if the device receives a command in a format that it does not know how to decode, the library will return a `MissingMessageDecoderException` condition.

```
sourceCode
import myCustomCodec

client.setMessageEncoderModule("custom", myCustomCodec)
client.publishEvent("status", "custom", myData)
```
