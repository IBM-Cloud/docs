---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# MQTT connectivity for devices
{: #mqtt}

## Client connections
{: #client_connections}

Every registered organization has a unique endpoint, which must be used when you connect MQTT clients for devices in that organization.



```
org_id.messaging.internetofthings.ibmcloud.com
```

### Unencrypted client connections

For unencrypted client connections, connect on port **1883**.

**Important:** Devices submit information to the {{site.data.keyword.iot_full}} as plain text, including the authentication credentials for the device. To secure the transmission, always use an encrypted connection.


### Encrypted client connections

For encrypted client connections, connect on port **8883**, or for WebSockets, connect on port **443**.

Many client libraries require that you provide the server's public certificate in PEM format. To view the entire certificate chain for \*.messaging.internetofthings.ibmcloud.com, go to [messaging.pem](https://github.com/ibm-messaging/iot-python/blob/master/src/ibmiotf/messaging.pem).

**Tip:** Some SSL client libraries do not support domains that include a wildcard. If you cannot successfully change libraries, disable certificate checking.

**Prerequisites:** {{site.data.keyword.iot_short_notm}} requires Transport Layer Security (TLS) V1.2 and the following cipher suites:

- ECDHE-RSA-AES256-GCM-SHA384
- AES256-GCM-SHA384
- ECDHE-RSA-AES128-GCM-SHA256
- AES128-GCM-SHA256 *(as of 1 June 2015)*



**Note:** **Device support in Quickstart**

When you connect to the Quickstart service, authentication (or registration) is not required and the ``orgId`` must be set to ``quickstart``.

The Quickstart service does not currently support MQTT quality of service (QoS) levels greater than zero. This is the fastest level and offers no confirmation of receipt.

If you are writing device code for use with Quickstart, be aware that some of the  {{site.data.keyword.iot_short_notm}} service features are not supported. The following features are not supported in Quickstart mode:

-  Subscribing to commands
-  Device Management Protocol
-  Clean or durable sessions

Also, messages sent from devices at a rate greater than 1 per second might be discarded.

## MQTT client identifier
{: #mqtt_client_id}

For a device to successfully authenticate, define each MQTT client ID in the following format:

```
    d:org_id:device_type:device_id
```

Where:
-  The lowercase **d** character identifies the client as a device
-  org_id is the unique six character organization ID that was generated when you registered the service alphanumeric string that was assigned when you first registered the service.
-  **type\_id** is intended to be used as an identifier for the type
   of device that is connecting. It might be useful to think of this as analogous
   to a model number.
-  **device\_id** must uniquely identify a device across all devices of
   a specific device\_type, it might be useful to think of this as
   analogous to a serial number.

**Note:** When you assign values for ``type_id`` and ``device_id``, you can use any scheme of your choice, however the following restrictions apply to both parameters:

- The maximum length is 36 characters, which can consist of any of the following:
    - Alpha-numeric characters (``a-z``, ``A-Z``, ``0-9``)
    - Dashes (-)
    - Underscores (_)
    - Dots(.)


## MQTT authentication
{: #mqtt_authentication}

### Username

The {{site.data.keyword.iot_short_notm}} service currently supports token-based authentication only for devices, as such there is only one valid user name for devices today.

A value of ``use-token-auth`` indicates to the service that the authentication token for the device will be passed as the password for the MQTT connection.


### Password

If you are using token based authentication, submit the device authentication token as the password when making your MQTT connection.


## Publishing events
{: #publishing_events}

Devices can only publish to the event topics in the following format:

```
iot-2/evt/event_id/fmt/format_string
```

-  **event\_id** is the ID of the event, for example "status".  The event ID can be any string permitted by MQTT.  Subscriber applications must use this string in their subscription topic to receive the events published on this topic if wildcards are not used.
-  **format\_string** is the format of the event payload, for example "json".  The format can be any string permitted by MQTT.  Subscriber applications must use this string in their subscription topic to receive events published on this topic if wildcards are not used.  If the format is not "json", then messages will not be stored in the Historian.

**Important:** The message payload is limited to a maximum of 131072 bytes.  Messages larger than this will be rejected.


## Subscribing to commands
{: #subscribing_to_commands}

Devices can only subscribe to command topics in the following format:

```
iot-2/cmd/command_id/fmt/format_string
```
Where:

-  **command\_id** is the ID of the command, for example, "update".  The command ID can be any string that is permitted by the MQTT protocol.  A device must use this string in its subscription topic to receive commands published on this topic if wildcards are not used.
-  **format\_string** is the format of the command payload, for example "json".  The format can be any string that is permitted by the MQTT protocol.  A device must use this string in its subscription topic in order to receive commands published on this topic if wildcards are not used.

Devices cannot subscribe to events from other devices. A device receives commands that are published specifically to only its own device.

## Managed devices
{: #managed-devices}

Support for device lifecycle management is optional. The Device Management Protocol uses the same MQTT connection that your device already uses for events and command control.

### Quality of service levels and clean session

Managed devices can publish messages with a quality of service (QoS) level of zero or one. If a QoS value of one is set, messages from the device are queued, if necessary. Messages from
the device must not be retained messages.

{{site.data.keyword.iot_short_notm}} publishes requests with a QoS level of one to a support queue of messages. To queue messages that are sent when a managed device is offline, configure the device to use ``cleansession=false``.

**Warning:**
  If your managed device uses a durable subscription of ``cleansession=false``, any device management commands that are sent to your device while it is offline will be
  reported as failed operations if the device does not reconnect to the service before the
  request times out. However, when the device reconnects, those requests will
  be actioned by the device.


When handling request failures, it is important to take this into account if you are using durable subscriptions for your managed devices.

### Topics

A managed device is required to subscribe to the following topic to handle requests and responses from the {{site.data.keyword.iot_short_notm}} service:

```
iotdm-1/#
```


A managed device publishes to topics specific to the type of management request that is being performed, as follows:

- The managed device will publish device management responses on ``iotdevice-1/response``
- For other topics that a managed device might publish to, see [Device Management Protocol](device_mgmt/index.html) and [Device management requests](device_mgmt/requests.html)



### Message format

All messages are sent in JSON format. There are two types of messages.


1. Requests  
Requests are formatted as outlined in the following code sample:
```

        {  "d": {...}, "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056" }
```
Where:

 - ``d`` carries any data relevant to the request.
 - ``reqId`` is an identifier of the request, and must be copied into a response. If a response is not required, omit this field.

2. Responses  
Responses are formatted as outlined in the following code sample:
```
        {
            "rc": 0,
            "message": "success",
            "d": {...},
            "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056"
        }
```
Where:  
 - "rc" is a result code of the original request.
 - ``message`` is an optional element with a text description of the response code.
 - ``d`` is an optional data element accompanying the response.
 - ``reqId`` is the request ID of the original request, which is used to correlate responses with requests. The device must ensure that all request IDs are unique.  When responding to {{site.data.keyword.iot_short_notm}} requests, the correct ``reqId`` value must be sent in the response.

For more information about specific request and response messages, see [Device Management Protocol](device_mgmt/index.html) and [Device Management Requests](device_mgmt/requests.html).
