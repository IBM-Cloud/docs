---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# MQTT connectivity for gateways
{: #mqtt}

MQTT is the primary protocol that devices and applications use to communicate with the {{site.data.keyword.iot_full}}. Client libraries, information, and samples are provided to help you to use MQTT clients as gateways to connect your devices to {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Client connections
{: #client_connections}

For information about client security and how to connect MQTT clients as gateways, see [Connecting applications, devices, and gateways to {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).

## MQTT authentication
{: #authentication}
For gateways and devices, {{site.data.keyword.iot_short_notm}} uses MQTT token-based authentication.

To enable MQTT authentication, submit a user name and password when you make an MQTT connection.

### User name
{: #username}

The user name is the same value for all gateways: ``use-token-auth``. This value causes {{site.data.keyword.iot_short_notm}} to use the gateway's authentication token, which is specified as the password.

### Password
{: #password}

The password for each gateway is the unique authentication token that was generated when the gateway was registered with {{site.data.keyword.iot_short_notm}}.

## Publishing events
{: #pub_events}

A gateway can publish events from itself and on behalf of any device that is connected through the gateway. To publish events, use the following topic and substitute the appropriate `typeId` and `deviceId` based on the intended origin of the event:

<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/evt/<var class="keyword varname">eventId</var>/fmt/<var class="keyword varname">formatString</var></pre>
{: codeblock}


**Example**


|    |'typeID'|'deviceID'|
|:---|:---|:---|
|Gateway 1 |mygateway |gateway1 |
|Device 1 |mydevice |device1 |

-   Gateway 1 can publish its own status events:  
    ``iot-2/type/mygateway/id/gateway1/evt/status/fmt/json``
-   Gateway 1 can publish status events on behalf of Device 1:  
    ``iot-2/type/mydevice/id/device1/evt/status/fmt/json``

**Important:** The message payload is limited to a maximum of 131072 bytes. Messages larger than this limit are rejected.

### Retained messages
{{site.data.keyword.iot_short_notm}} organizations are not authorized to publish retained MQTT messages. If a gateway sends a retained message, the {{site.data.keyword.iot_short_notm}} service overrides the retained message flag when it is set to true and processes the message as if the retained message flag is set to false.

## Subscribing to commands
{: #subscribing_cmds}

A gateway can subscribe to commands that are directed at the gateway itself and to any device in the organization, including other gateways. To subscribe to commands, use the following topic and substitute the appropriate `typeId` and `deviceId`:

<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/cmd/<var class="keyword varname">commandId</var>/fmt/<var class="keyword varname">formatString</var></pre>
{: codeblock}

The MQTT `+` wildcard can be used for `typeId`, `deviceId`, `commandId`, and `formatString` to subscribe to multiple command sources.

**Example:**

|Device |`typeId`|`deviceId`|
|:---|:---|
|Gateway 1| mygateway   | gateway1   |
|Device 1 | mydevice    | device1    |


-   Gateway 1 can subscribe to commands directed at the gateway:  
    `iot-2/type/mygateway/id/gateway1/cmd/+/fmt/+`
-   Gateway 1 can subscribe to commands sent to Device 1:  
    `iot-2/type/mydevice/id/device1/cmd/+/fmt/+`
-   Gateway 1 can subscribe to any command that is sent to devices of type `mydevice`:  
     `iot-2/type/mydevice/id/+/cmd/+/fmt/+`

**Important:** MQTT persistent sessions that are specified as `cleansession=false`, do not search for devices that connect to gateways. If a device connects to gateway A, and then later connects to gateway B, it does not receive any messages that were published to gateway A for that device while it was disconnected. A gateway owns the MQTT client and subscription, but not the devices that are connected to the gateway.

## Gateway auto-registration
{: #auto-reg}

Gateway devices can automatically register devices that are connected to them. When a gateway publishes a message or subscribes to a topic on behalf of an unregistered device, that device is automatically registered.

Registration requests from gateway devices are throttled to 128 pending requests at a time. Attempting to connect many new devices might cause a delay in the registration of the devices through the gateway.

**Warning**

If the gateway fails to register a device automatically, it does not attempt to register that device again for a short time. Any messages or subscriptions from the failed device are dropped during that time.

## Gateway notifications
{: #notification}

When errors occur during the validation of the publish or subscribe topic or during automatic registration, a notification is sent to the gateway device. A gateway can receive these notifications by subscribing to the following topic, substituting the `typeId` and `deviceId` values:

```
iot-2/type/**typeId**/id/**deviceId**/notify
```
<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/notify</pre>
{: codeblock}

Messages that are received on the notify topic use the following format:

```   
{
   "Request": "<Request_Type>",
   "Time": "<Timestamp>",
   "Topic": "<Topic>",
   "Type": "<Device_Type>",
   "Id": "<Device_Id>",
   "Client": "<Client_ID>",
   "RC": "<Return_Code>",
   "Message": "<Message>"
}
```
Where
-   `Request_Type` values are either `publish` or `subscribe`
-   `Timestamp` is the time in the ISO 8601 format
-   `Topic` is the request topic from the gateway
-   `Device_Type` is the device type from the topic
-   `Device_Id` is the device ID from the topic
-   `Client_ID` is the client ID of the request
-   `Return_Code` is the return code
-   `Message` is the error message

A gateway can receive the following notifications:

-   Topic does not match any allowed topic rules.
-   Device type is not valid.
-   Device ID is not valid.
-   Maximum number of devices per gateway is reached.
-   Maximum number of devices per organization is reached.
-   Failed to create device because of internal errors.

## Managed gateways
{: #managed_gateways}

Support for device lifecycle management is optional. The device management protocol that is used by {{site.data.keyword.iot_short_notm}} uses the same MQTT connection that the gateway uses for events and command control.

### Quality of service levels and clean session
{: #quality_service}

Managed gateways can publish messages that have a quality of service (QoS) level of 0 or 1.

Messages with QoS=0 can be discarded and do not persist after the messaging server is restarted. Messages with QoS=1 can be queued and do persist after the messaging server is restarted. The durability of the subscription determines whether a request is queued. The ``cleansession`` parameter of the connection that made the subscription determines the durability of the subscription.  

{{site.data.keyword.iot_short_notm}} publishes requests that have a QoS level of 1 to support queuing of messages. To queue messages that are sent while a managed gateway is not connected, configure the device not to use clean sessions by setting the ``cleansession`` parameter to false.

**Warning**

When a managed gateway uses a durable subscription, device management commands that are sent to the gateway while it is offline are reported as failed operations if the gateway does not reconnect to the service before the request times out. When the gateway reconnects, those requests are processed by the gateway. Durable subscriptions are specified by the ``cleansession=false`` parameter.

The gateway owns the MQTT session, regardless of the devices that are behind it. When a device submits a subscription request through a gateway, the request does not roam to other gateways, regardless of whether the ``cleansession=false`` options is set.

### Topics
{: #topics}

A managed gateway must subscribe to the following topics to handle requests and responses from {{site.data.keyword.iot_short_notm}}:

-   The managed gateway subscribes to device management responses on:  
<pre class="pre">iotdm-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/response/+</pre>
{: codeblock}
-   The managed gateway subscribes to device management requests on:  
<pre class="pre">iotdm-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/+</pre>
{: codeblock}

A managed gateway publishes the following responses and requests:

- Device management responses are published on:  
<pre class="pre">iotdevice-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/response/</pre>
{: codeblock}
- Device management requests are published on:  
<pre class="pre">iotdevice-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/</pre>
{: codeblock}

The gateway can process Device Management Protocol messages for both itself and on behalf other connected devices by using the relevant **typeId** and **deviceId**.

### Message format
{: #msg_format}

All messages are sent in JSON format.

**Requests**

Requests are formatted as shown in the following code sample:

```   
    {  "d": {...}, "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056" }
```

-   `d` carries any data that is relevant to the request
-   `reqId` is an identifier of the request and must be copied into a response. If a response is not required, the field is not used.

**Responses**

Responses are formatted as shown in the following code sample:

```
    {
        "rc": 0,
        "message": "success",
        "d": {...},
        "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056"
    }
```
Where:
-   `rc` is a result code of the original request.
-   `message` is an optional element with a text description of the response code.
-   `d` is an optional data element that accompanies the response.
-   `reqId` is the request ID of the original request. The request ID is used to correlate responses with requests, and the device needs to ensure that all request IDs are unique. Responses to {{site.data.keyword.iot_short_notm}} requests must contain the correct `reqId` value.
