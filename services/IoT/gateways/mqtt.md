---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# MQTT connectivity for gateways

Use MQTT clients as gateways to connect your devices to your {{site.data.keyword.iot_full}} instance.

{:shortdesc}

## MQTT client connection
{: #MQTT_client_connection}

Every registered organization has a unique endpoint, which must be used when connecting MQTT clients for gateways in that organization.

```
org_id.messaging.internetofthings.ibmcloud.com
```

**Note:** In the {{site.data.keyword.iot_short_notm}} dashboard, devices and gateways that are connected directly to the {{site.data.keyword.iot_short_notm}} display a status icon to indicate that they are  connected. The dashboard displays devices that are connected indirectly through a gateway as disconnected as it does not have any knowledge of a devices connectivity to the gateway.


### Unencrypted client connection
{: #unencrypted_connection}

For unencrypted client connections, connect on port **1883**.

**Important:** Applications in the {{site.data.keyword.iot_short_notm}} submit information as plain text, including the API key and authentication token. To secure the transmission, always use an encrypted connection.


### Encrypted client connection
{: #encrypted_connection}

For encrypted client connections, connect on port **8883**, or for WebSockets, connect on port **443**.

Many client libraries require that you provide the server's public certificate in PEM format. To view the entire certificate chain for
\*.messaging.internetofthings.ibmcloud.com, go to [messaging.pem](https://github.com/ibm-messaging/iot-python/blob/master/src/ibmiotf/messaging.pem).

**Tip:** Some SSL client libraries do not support domains that include a wildcard. If you cannot successfully change libraries, disable certificate checking.

**Prerequisites:** {{site.data.keyword.iot_short_notm}} requires Transport Layer Security (TLS) V1.2 and the following cipher suites:
- ECDHE-RSA-AES256-GCM-SHA384
- AES256-GCM-SHA384
- ECDHE-RSA-AES128-GCM-SHA256
- AES128-GCM-SHA256 *(as of 1 June 2015)*




## MQTT client identifier
{: #client_identifier}

For a gateway to successfully authenticate, you must define each MQTT client ID by using the following format:

```
   g:*orgId*:*typeId*:*deviceId*
```
Where:
-   Lowercase **g** identifies that the client is a gateway
-   org_id is the unique six character organization ID that was generated when you registered the service alphanumeric string that was assigned when you first registered the service.
-   **typeId** is intended to be used as an identifier of the type of gateway connecting, it may be useful to think of this as analogous
    to a model number.
-   **deviceId** must uniquely identify a gateway device across all gateways of a specific type, it may be useful to think of this as analogous to a serial number.

**Note:** You can use any scheme of your choice when assigning values for `typeId` and `deviceId`, however the following restrictions apply to both values:
-   Maximum length of 36 characters
-   Must comprise only alpha-numeric characters (`a-z`, `A-Z`, `0-9`) and the following special characters:
 -   dash (`-`)
 -   underscore (`_`)
 -   dot (`.`)


## MQTT authentication
{: #authentication}

### Username
{: #username}

The service currently only supports token-based authentication for devices, as such there is only one valid user name for gateways today.

A value of `use-token-auth` indicates to the service that the authentication token for the gateway will be passed as the password for the MQTT connection.

### Password
{: #password}

When using token based authentication submit the device authentication token as the password when making your MQTT connection.

## Publishing events
{: #pub_events}

A gateway can publish events from itself and on behalf of any device connected via the gateway by using the following topic and substituting in the appropriate `typeId` and `deviceId` based on the intended origin of the event:

```
iot-2/type/**typeId**/id/**deviceId**/evt/**eventId**/fmt/**formatString**
```

**Example**


|               | 'typeID'    | 'deviceID' |
| ------------- |-------------| ---------- |
| Gateway 1     | mygateway   | gateway1   |
| Device 1      | mydevice    | device1    |



-   Gateway 1 can publish its own status events:  
    `iot-2/type/mygateway/id/gateway1/evt/status/fmt/json`
-   Gateway 1 can publish status events on behalf of Device 1:  
    `iot-2/type/mydevice/id/device1/evt/status/fmt/json`

**Important:** The message payload is limited to a maximum of 131072 bytes. Messages larger than this will be rejected.

## Subscribing to commands
{: #subscribing_cmds}

A gateway can subscribe to commands directed at the gateway itself and
to any device connected via the gateway by using the following topic and
substituting in the appropriate `typeId` and `deviceId`:

```
iot-2/type/**typeId**/id/**deviceId**/cmd/**commandId**/fmt/**formatString**
```

The MQTT `+` wildcard can be used for `typeId`, `deviceId`, `commandId` and `formatString` to subscribe to multiple command sources.

**Example**

|               | 'typeID'    | 'deviceID' |
| ------------- |-------------| ---------- |
| Gateway 1     | mygateway   | gateway1   |
| Device 1      | mydevice    | device1    |

-   Gateway 1 can subscribe to commands directed at the gateway:  
    `iot-2/type/mygateway/id/gateway1/cmd/+/fmt/+`
-   Gateway 1 can subscribe to commands sent to Device 1:  
    `iot-2/type/mydevice/id/device1/cmd/+/fmt/+`
-   Gateway 1 can subscribe any command sent to devices of type
    "mydevice":  
     `iot-2/type/mydevice/id/+/cmd/+/fmt/+`

**Warning**

MQTT persistent sessions (cleansession=false) do not roam for devices that connect to gateways. What this means is that if a device connects to gateway A, then later connects to gateway B, it does not receive any messages that had been published to gateway A for that device while it was disconnected. A gateway owns the MQTT client and subscription, not the devices which are connected to the gateway.

## Gateway auto-registration
{: #auto-reg}

Gateway devices have the ability to automatically register devices which are connected to them. When a gateway publishes a message or subscribes to a topic on behalf of another device, that device will automatically be registered if it does not already exist.

Registration requests from gateway devices are throttled to 10 pending requests at a time. If trying to connect many new devices to a gateway which have not previously been registered, then there may be some delay in the registration of the devices through the gateway.

Gateway devices are limited to 500 active devices at a time. If exceeded, publish and subscribe requests for new devices will be dropped. The count is reset on gateway disconnect.

**Warning**

If the gateway fails to automatically register a device, then it will not attempt to register that device again for a short period of time. Any messages or subscriptions from the failed device will be dropped during that time.

## Gateway notifications
{: #notification}

When errors occur during the validation of the publish or subscribe topic, or during automatic registration, a notification will be sent to the gateway device. A gateway can receive these notifications by subscribing to the following topic, substituting the `typeId` and `deviceId` values:

```
 ot-2/type/**typeId**/id/**deviceId**/notify
```
Messages received on the notify topic will have the following format:

```   
{
   "Request": "<Request_Type>",
   "Time": "<Timestamp>",
   "Topic": "<Topic>",
   "Type": "<Device_Type>",
   "Id": "<Device_Id>",
   "Client": "<Client_ID",
   "RC": <Return_Code>,
   "Message": "<Message>"
}
```

-   Request\_Type: Either publish or subscribe
-   Timestamp: Time in ISO 8601 Format
-   Topic: The request topic from the gateway
-   Device\_Type: The device type from the topic
-   Device\_Id: The device id from the topic
-   ClientID: The client id of the request
-   RC: The return code
-   Message: The error message

Notifications a gateway can receive:

-   Topic does not match with any allowed topic rules.
-   Device type is not valid.
-   Device id is not valid.
-   Maximum number of devices per gateway has been reached.
-   Maximum number of devices per organization has been reached.
-   Failed to create device due to internal errors.

## Managed gateways
{: #managed_gateways}

Support for device lifecycle management is optional, the device management protocol used by {{site.data.keyword.iot_short_notm}} utilises the same MQTT connection that your gateway already uses for events and command control.

### Quality of service levels and clean session
{: #quality_service}

Managed gateways can publish messages with Quality of Service (QoS) level of 0 or 1. If QoS 1 is used, messages from the gateway will be queued if necessary. Messages from the gateway must not be retained messages.

The {{site.data.keyword.iot_short_notm}} publishes requests with a QoS level of 1 to support queuing of messages. In order to queue messages sent while a managed gateway is not connected, the device should use `cleansession=false`.

**Warning**

If your managed gateway uses a durable subscription (cleansession=false) you need to be aware that device management commands sent to your gateway while it is offline will be reported as failed operations, however, when the gateway later connects those requests will be actioned by the gateway.

When handling failures it is important to take this into account if you are using durable subscriptions for your managed gateways.

### Topics
{: #topics}

A managed gateway is required to subscribe to two topics to handle requests and responses from {{site.data.keyword.iot_short_notm}}:

-   The managed gateway will subscribe to device management responses on:  
    `iotdm-1/type/<typeId>/id/<deviceId>/response/+`
-   The managed gateway will subscribe to device management requests on:  
    `iotdm-1/type/<typeId>/id/<deviceId>/+`

A managed gateway will publish to two topics:

-   The managed gateway will publish device management responses on:  
    `iotdevice-1/type/<typeId>/id/<deviceId>/response/`
-   The managed gateway will publish device management requests on:  
    `iotdevice-1/type/<typeId>/id/<deviceId>/`

The gateway is able to process Device Management Protocol messages for both itself and on behalf other connected devices by using the relevant
&lt;typeId&gt; and &lt;deviceId&gt;.

### Message format
{: #msg_format}

All messages are sent in JSON format. There are two types of message.

1.  Requests

    Requests are formatted as follows:

    ```   
    {  "d": {...}, "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056" }
    ```

    -   `d` carries any data relevant to the request
    -   `reqId` is an identifier of the request, and must be copied into a response. If a response is not required, the field should be omitted.

2.  Responses

    Responses are formatted as follows:

    ```   
    {
        "rc": 0,
        "message": "success",
        "d": {...},
        "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056"
    }
    ```
    -   "rc" is a result code of the original request.
    -   `message` is an optional element with a text description of the response code.
    -   `d` is an optional data element accompanying the response.
    -   `reqId` is the request ID of the original request. This is used to correlate responses with requests, and the device needs to ensure that all request IDs are unique. When responding to {{site.data.keyword.iot_short_notm}} requests, the correct `reqId` value must be sent in the response.
