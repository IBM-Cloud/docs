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


# MQTT connectivity for devices
{: #mqtt}

MQTT is the primary protocol that devices and applications use to communicate with the {{site.data.keyword.iot_full}}. Client libraries, information, and samples are provided to help you to connect and integrate your devices with {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Client connections
{: #client_connections}

For information about client security and how to connect MQTT clients to devices in {{site.data.keyword.iot_short_notm}}, see [Connecting applications, devices, and gateways to {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).


## Connecting devices to the Quickstart service
{: #connecting_devices}

The Quickstart service is the fastest level of service. It offers no confirmation of receipt and does not support MQTT quality of service (QoS) levels greater than zero. When you connect to the Quickstart service, authentication or registration is not required, and the ``orgId`` must be set to ``quickstart``.

If you are writing device code for use with Quickstart, be aware that the following {{site.data.keyword.iot_short_notm}} service features are not supported in Quickstart mode:

-  Subscribing to commands
-  Device Management Protocol
-  Clean or durable sessions

**Important:** Messages that are sent from devices at a rate greater than one per second might be discarded.


## MQTT authentication
{: #mqtt_authentication}

For gateways and devices, {{site.data.keyword.iot_short_notm}} uses MQTT token-based authentication.

To enable MQTT authentication, submit a user name and password when you make an MQTT connection.

### User name

The user name is the same value for all devices: ``use-token-auth``. This value causes {{site.data.keyword.iot_short_notm}} to use the device's authentication token, which is specified as the password.

### Password

The password for each device is the unique authentication token that was generated when the device was registered with {{site.data.keyword.iot_short_notm}}.

## Publishing events
{: #publishing_events}

Devices publish to the event topics in the following format:

<pre class="pre">iot-2/evt/<var class="keyword varname">event_id</var>/fmt/<var class="keyword varname">format_string</var></pre>
{: codeblock}

Where

-  **event_id** is the ID of the event, for example ``status``.  The event ID can be any string that is valid in MQTT. If wildcards are not used, subscriber applications must use this string in their subscription topic to receive the events that are published on their topic.
-  **format_string** is a string that defines the content type of the message payload so that the receiver of the message can determine how to parse the content. Common content type values include but are not limited to "json", "xml", "txt", and "csv". The value can be any string that is valid in MQTT.

**Important:** The message payload is limited to a maximum of 131072 bytes. Messages larger than this limit are rejected.

### Retained messages
{{site.data.keyword.iot_short_notm}} organizations are not authorized to publish retained MQTT messages. If a device sends a retained message, the {{site.data.keyword.iot_short_notm}} service overrides the retained message flag when it is set to true and processes the message as if the retained message flag is set to false.


## Subscribing to commands
{: #subscribing_to_commands}

Devices can subscribe to command topics in the following format:

<pre class="pre">iot-2/cmd/<var class="keyword varname">command_id</var>/fmt/<var class="keyword varname">format_string</var></pre>
{: codeblock}

Where
 - **command_id** is the ID of the command, for example, ``update``. The command ID can be any string that is valid in the MQTT protocol.  If wildcards are not used, a device must use this string in its subscription topic to receive commands that are published on their topic.
 - **format_string** is a string that defines the content type of the command payload so that the receiver of the command can determine how to parse the content. Common content type values include but are not limited to "json", "xml", "txt", and "csv". The value can be any string that is valid in MQTT.

Devices cannot subscribe to events from other devices. A device receives commands that are published only to its own device.

## Managed devices
{: #managed-devices}

Support for device lifecycle management is optional. The Device Management Protocol uses the same MQTT connection that your device already uses for events and command control.

### Quality of service levels and clean session

Managed devices can publish messages that have a quality of service (QoS) level of 0 or 1.

Messages with QoS=0 can be discarded and do not persist after the messaging server is restarted. Messages with QoS=1 can be queued and do persist after the messaging server is restarted. The durability of the subscription determines whether a request is queued. The ``cleansession`` parameter of the connection that made the subscription determines the durability of the subscription.  

{{site.data.keyword.iot_short_notm}} publishes requests that have a QoS level of 1 to support queuing of messages. To queue messages that are sent while a managed device is not connected, configure the device not to use clean sessions by setting the ``cleansession`` parameter to false.

**Warning:**
  If your managed device uses a durable subscription, any commands that are sent to your device while it is offline are reported as failed operations if the device does not reconnect to the service before the request times out. However, when the device reconnects, those requests are processed by the device. A durable subscription is specified by the ``cleansession=false`` parameter.

### Topics

A managed device is required to subscribe to the following topic to handle requests and responses from the {{site.data.keyword.iot_short_notm}} service:

```
iotdm-1/#
```


A managed device publishes to topics that are specific to the type of management request that is being performed:

- The managed device publishes device management responses on ``iotdevice-1/response``.
- For other topics that a managed device can publish to, see [Device Management Protocol](device_mgmt/index.html) and [Device management requests](device_mgmt/requests.html).



### Message format

All messages are sent in JSON format.

**Requests**  
Requests are formatted as shown in the following code sample:

<pre class="pre">{  "d": {...}, "<var class="keyword varname">reqId</var>": "b53eb43e-401c-453c-b8f5-94b73290c056" }</pre>
{: codeblock}

Where:

 - **d** carries any data that is relevant to the request.
 - **reqId** is an identifier of the request and must be copied into a response. If a response is not required, you can omit the *reqId* field.

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
 - **rc** is a result code of the original request.
 - **message** is an optional element with a text description of the response code.
 - **d** is an optional data element that accompanies the response.
 - **reqId** is the request ID of the original request, which is used to correlate responses with requests. The device must ensure that all request IDs are unique. Responses to {{site.data.keyword.iot_short_notm}} requests must include the correct **reqId** value.

For more information about specific request and response messages, see [Device Management Protocol](device_mgmt/index.html) and [Device Management Requests](device_mgmt/requests.html).
