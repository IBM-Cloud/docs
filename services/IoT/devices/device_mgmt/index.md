---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Device Management Protocol
{: #index}

## Introduction
{: #introduction}

The {{site.data.keyword.iot_full}} recognizes two classes of device: **managed devices** and **unmanaged devices**.

**Managed devices** are defined as devices that contain a device management agent. A device management agent is a set of logic that allows the device to interact with the {{site.data.keyword.iot_short_notm}} Device Management service by using the Device Management Protocol. Managed devices can perform device management operations including location updates, firmware downloads and updates, reboots, and factory resets.

The Device Management Protocol defines a set of supported operations. A device management agent can support a subset of the operations, but the **manage** and **unmanage** operations must be supported. A device that supports firmware action operations must also support observation.

The Device Management Protocol is built on top of the MQTT messaging protocol. For more information about how the Device Management Protocol interacts with MQTT, see [MQTT connectivity for devices](../mqtt.html).


### The device management lifecycle

1. A device and its associated device type are created in the {{site.data.keyword.iot_short_notm}} by using either the dashboard or the REST API.
2. A device connects to the {{site.data.keyword.iot_short_notm}} and uses the **managed devices** operation to become a managed device.
3. You can view and manipulate the metadata for a device by using the device operations. These operations - for example firmware update and device restart operations - are outlined in the 'Device model' documentation. For more information about the device model, see [Device model](https://console.ng.bluemix.net/docs/services/IoT/reference/device_model.html).
4. A device can communicate updates about its location, diagnostic information, and error codes by using the Device Management Protocol.
5. To handle defunct devices in large device populations, the **managed devices** operation request includes an optional lifetime parameter. The lifetime parameter is the number of seconds in which the device must make another **managed devices** request to avoid being classified as dormant and becoming an unmanaged device.
6. When a device is decommissioned, you can remove it from the {{site.data.keyword.iot_short_notm}} by using the dashboard or the REST API.

Refer to recipe [Connect Raspberry Pi as Managed Device to IBM Watson IoT Platform](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-managed-device-to-ibm-iot-foundation/).

### Return code summary


The following table shows the return codes that are generated at various stages during the device management lifecycle.

|Return code |Message |
|:---|:---|
|200   |Operation succeeded|
|202   |Accepted (for initiating commands)|
|204   |Changed (for attribute updates)|
|400   |Bad request (for example, if a device is not in the appropriate state for this command)|
|404   |Attribute was not found (also used if the operation was published to an invalid topic)|
|409   |Resource could not be updated due to a conflict (for example, the resource is being updated by two simultaneous requests, so the update can be retried later)|
|500   |Unexpected device error|
|501   |Operation not implemented|


## Manage Device requests
{: #manage_device_request}

A device uses the Manage Device request to become a managed device. The Manage Device request must be the first device management request that is sent by the device after connecting to the {{site.data.keyword.iot_short_notm}}. A device management agent typically sends this type of request whenever it starts or restarts.

**Important:** Support for this operation is mandatory for any managed devices.


### Topic for a Manage Device request

A device publishes a Manage Device request to the following topic:

```
iotdevice-1/mgmt/manage
```

The server responds to a Manage Device request on the following topic:

```
iotdm-1/response
```




### Message format for a Manage Device request


In a Manage Device request, the ``d`` field and all of its subfields are optional. The ``metadata`` and ``deviceInfo`` field values replace the corresponding attributes for the sending device if they are sent.

The optional ``lifetime`` field specifies the length of time in seconds in which the device must send another Manage Device request to avoid being classified as dormant and becoming an unmanaged device. If the ``lifetime`` field is omitted or set to ``0``, the managed device does not become dormant. The minimum supported setting for the ``lifetime`` field is ``3600`` seconds, which is 1 hour.

The optional fields ``supports.deviceActions`` and ``supports.firmwareActions`` indicate the capabilities of the device management agent. If ``supports.deviceActions`` is set, then the agent supports both restart and factory reset actions. For a device that does not distinguish between a restart and a factory reset, it is acceptable to use the same behavior for both actions. If ``supports.firmwareActions`` is set, the agent supports both firmware download and firmware update actions.

The following sample shows the request format:

```
Outgoing message from the device:

Topic: iotdevice-1/mgmt/manage
{
    "d": {
        "metadata":{},
        "lifetime": number,
        "supports": {
            "deviceActions": boolean,
            "firmwareActions": boolean
        },
        "deviceInfo": {
            "serialNumber": "string",
            "manufacturer": "string",
            "model": "string",
            "deviceClass": "string",
            "description" :"string",
            "fwVersion": "string",
            "hwVersion": "string",
            "descriptiveLocation": "string"
        }
    },
    "reqId": "string"
}
```

The following sample shows the response format:

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```


### Response codes for a Manage Device request

|Response code |Message |
|:---|:---|
|200   |The operation was successful.|
|400   |The input message does not match the expected format, or one of the values is out of the valid range.|
|404   |The topic name is incorrect, or the device is not in the database.|
|409   |A conflict occurred during the device database update. To resolve this conflict, simplify the operation if necessary.|


## Unmanage Device requests
{: #manage-unmanage}


A device uses an Unmanage Device request when it no longer needs to be managed. When a device becomes unmanaged, {{site.data.keyword.iot_short_notm}} no longer sends new device management requests to the device. Unmanaged devices continue to publish error codes, log messages, and location messages.
**Important:** Support for this operation is mandatory for any managed devices.

### Topic for an Unmanage Device request


A device publishes an Unmanage Device request to the following topic:

```
iotdevice-1/mgmt/unmanage
```

The server responds to an Unmanage Device request on the following topic:

```
iotdm-1/response
```

### Message format for an Unmanage Device request

Request format:

```
Outgoing message from the device:

Topic: iotdevice-1/mgmt/unmanage
{
    "reqId": "string"
}
```

Response format:

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### Response codes for an Unmanage Device request

|Response code |Message |
|:---|:---|
|200   |The operation was successful.|
|400   |The input message does not match the expected format, or one of the values is out of the valid range.|
|404   |The topic name is incorrect, or the device is not in the database.|
|409   |A conflict occurred during the device database update. To resolve this conflict, simplify the operation if necessary.|


## Update Location requests
{: #update-location}

A device uses an Update Location request to manage the location data for a device. The location metadata for a device can be updated in {{site.data.keyword.iot_short_notm}} in the following ways:

#### Automatic device location updates
- The device notifies {{site.data.keyword.iot_short_notm}} about the location update. The device retrieves its location from a GPS receiver and sends a device management message to the {{site.data.keyword.iot_short_notm}} instance to update its location. The time stamp captures the time at which the location was retrieved from the GPS receiver. The time stamp is valid even if there is a delay in sending the location update message. If time stamp is omitted from the device management message, the date and time of the message receipt is used to update the location metadata.

#### Manual device location updates by using the REST API
- You can manually set the location metadata for a static device by using the {{site.data.keyword.iot_short_notm}} REST API when the device is registered. You can also modify the location later. The time stamp setting is optional, but when omitted, the current date and time is set in the location metadata for the device.

### Location updates that are triggered by devices

Devices that can determine their location can choose to notify the {{site.data.keyword.iot_short_notm}} device management server about location changes.

### Topic for an Update Location request that is triggered by a device:


A device publishes an Update Location request to the following topic:

```
iotdevice-1/device/update/location
```

The server responds to an Update Location request on the following topic:

```
iotdm-1/response
```

### Location update that is triggered by users or apps


When a user or application updates the location of an active managed device, the device retrieves an update message.




### Topic for an Update Location request that is triggered by users or apps


The server publishes an Update Location request to the following topic:

```
iotdm-1/device/update
```

### Message format for an Update location request


The ``measuredDateTime`` field is the date of location measurement. The ``updatedDateTime`` field is the date of the update to the device information. For efficiency reasons, the {{site.data.keyword.iot_short_notm}} sometimes batches updates to location information so that the updates are slightly delayed. The latitude and longitude must be specified in decimal degrees by using World Geodetic System 1984 (WGS84).

Whenever location is updated, the values that are provided for latitude, longitude, elevation, and uncertainty are considered a single multi-value update. The latitude and longitude are mandatory and must both be provided with each update.  Elevation and uncertainty are optional and can be omitted.

If an optional value is provided on an update and then omitted on a later update, the earlier value is deleted by the later update. Each update is considered a complete multi-value set.

### Location updates that are triggered by device


Request format:

```
Outgoing message from the device:

Topic: iotdevice-1/device/update/location
{
    "d": {
        "longitude": number,
        "latitude": number,

        "elevation": number,
        "measuredDateTime": "string in ISO8601 format",
        "updatedDateTime": "string in ISO8601 format",
        "accuracy": number
    },
    "reqId": "string"
}
```

Response format:

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### Response codes for an Update Location request

|Response code |Message |
|:---|:---|
|200   |The operation was successful.|
|400   |The input message does not match the expected format, or one of the values is out of the valid range.|
|404   |The topic name is incorrect, or the device is not in the database.|
|409   |A conflict occurred during the device database update. To resolve this conflict, simplify the operation if necessary.|


### Location updates that are triggered by users or apps


The following sample outlines the payload format:

```
Incoming message from the server:

Topic: iotdm-1/device/update
{
    "d": {
        "fields": [
            {
                "field": "location",
                "value": {
                    "latitude": number,
                    "longitude": number,
                    "elevation": number,
                    "accuracy": number,
                    "measuredDateTime": "string in ISO8601 format"
                }
            }
        ]
    }
}
```

**Note:** The ``reqID`` parameter is not used, because the device is not required to respond.

## Update Device Attribute requests
{: #update-attributes}

By using the REST API, {{site.data.keyword.iot_short_notm}} can send a request to a device to update the value of one or more of the following device attributes:


|Attribute | More information|
|:---|:---|
|location  | See [Update location](index.html#update-location)|
|metadata  | Optional|
|deviceInfo | Optional|
|mgmt.firmware | See [Firmware update process](requests.html#firmware-actions-update)|

### Topic for an Update Device Attributes request


The server publishes the device update request to the following topic:

```
iotdm-1/device/update
```


### Message format for an Update Device Attributes request


The following sample outlines the payload format for the request:

```
Incoming message from the server:

Topic: iotdm-1/device/update
{
    "d": {
        "fields": [
            {
                "field": "location",
                "value": ""
            }
        ]
    }
}
```


## Add Error Codes requests
{: #diag-add-error-code}

Devices can choose to notify the {{site.data.keyword.iot_short_notm}} device management server about changes to their error status by using the Add Error Codes request type.

### Topic for an Add Error Codes request


A device publishes an Add Error Codes request to the following topic:

```
iotdevice-1/add/diag/errorCodes
```

### Message format for an Add Error Codes request


The value that is associated with `errorCode` is the current device error code and must be added to the {{site.data.keyword.iot_short_notm}}.

Request format:

```
Outgoing message from the device:

Topic: iotdevice-1/add/diag/errorCodes
{
    "d": {
        "errorCode": number
    },
    "reqId": "string"
}
```

Response format:

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### Response codes for an Add Error Codes request

|Response code |Message |
|:---|:---|
|200   |The operation was successful.|
|400   |The input message does not match the expected format, or one of the values is out of the valid range.|
|404   |The topic name is incorrect, or the device is not in the database.|
|409   |A conflict occurred during the device database update. To resolve this conflict, simplify the operation if necessary.|


## Clear Error Codes requests
{: #diag-clear-error-codes}

Devices can request that {{site.data.keyword.iot_short_notm}} clears all error codes for the device by using the Clear Error Codes request type.

### Topic for a Clear Error Codes request


A device publishes this request to the following topic:

```
iotdevice-1/clear/diag/errorCodes
```

### Message format for a Clear Error Codes request


Request format:

```
Outgoing message from the device:

Topic: iotdevice-1/clear/diag/errorCodes
{
    "reqId": "string"
}
```

Response format:

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### Response codes for a Clear Error Codes request

|Response code |Message |
|:---|:---|
|200   |The operation was successful.|
|400   |The input message does not match the expected format, or one of the values is out of the valid range.|
|404   |The topic name is incorrect, or the device is not in the database.|
|409   |A conflict occurred during the device database update. To resolve this conflict, simplify the operation if necessary.|


## Add Log requests
{: #diag-add-log}

Devices can choose whether to notify {{site.data.keyword.iot_short_notm}} device management support about changes by adding a new log entry. Log entries include a log message, time stamp, severity, and optional base64-encoded binary diagnostic data.

### Topic for an Add Log request
A device publishes this request to the following topic:

```
iotdevice-1/add/diag/log
```


### Message format for an Add Log request

The following table describes the format of the outgoing message attributes:

|Attribute |Description |
|:---|:---|
|`message`|Specifies a diagnostic message that needs to be added to {{site.data.keyword.iot_short_notm}}|
|`timestamp`|Specifies the date and time of the log entry in ISO8601 format |
|`data`|Specifies optional base64-encoded diagnostic data|
|`severity`|Specifies the severity of the message (0: informational, 1: warning, 2: error)|


Request format:

```
Outgoing message from the device:

Topic: iotdevice-1/add/diag/log
{
    "d": {
        "message": string,
        "timestamp": string,
        "data": string,
        "severity": number
    },
    "reqId": "string"
}
```

Response format:

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```


### Response codes for an Add Log request

|Response code |Message |
|:---|:---|
|200   |The operation was successful.|
|400   |The input message does not match the expected format, or one of the values is out of the valid range.|
|404   |The topic name is incorrect, or the device is not in the database.|
|409   |A conflict occurred during the device database update. To resolve this conflict, simplify the operation if necessary.|

## Clear Logs requests
{: #diag-clear-logs}

Devices can request that {{site.data.keyword.iot_short_notm}} clear all of the log entries for the device by using the Clear Logs request type.

### Topic for a Clear Logs request


A device publishes a Clear Logs request to the following topic:

```
iotdevice-1/clear/diag/log
```

### Message format for a Clear Logs request


Request format:

```
Outgoing message from the device:

Topic: iotdevice-1/clear/diag/log
{
    "reqId": "string"
}
```

Response format:

```
Incoming message from the device:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### Response codes for a Clear Logs request

|Response code |Message |
|:---|:---|
|200   |The operation was successful.|
|400   |The input message does not match the expected format, or one of the values is out of the valid range.|
|404   |The topic name is incorrect, or the device is not in the database.|
|409   |A conflict occurred during the device database update. To resolve this conflict, simplify the operation if necessary.|

## Observe Attribute Changes requests
{: #observations-observe}

{{site.data.keyword.iot_short_notm}} can send an Observe Attribute Change request to a device to observe changes of one or more device attributes by using the Observe Attribute Changes request type. When the device receives the request, it must send a notification request to {{site.data.keyword.iot_short_notm}} whenever the values of the observed attributes change.

**Important:** Devices must implement, observe, notify, and cancel operations in order to support [Firmware Actions- Update](requests.html#firmware-actions-update)  request types.

### Topic for an Observe Attribute Changes request


The server publishes an Observe Attribute Changes request to the following topic:

```
iotdm-1/observe
```

### Message format for an Observe Attribute Changes request


The `fields` array is an array of the device attribute from the device model. If a complex field, such as `mgmt.firmware` is specified, it is expected that its underlying fields are updated at the same time so that only a single notification message is generated.

The `message` parameter that is used in the response can be specified if the value of the `rc` parameter is not `200`. If any specified parameter value cannot be retrieved, the value of the `rc` parameter must be set to either `404` if the device is not found, or to `500` for any other reason. When values for parameters cannot be found, the `fields` array should contain elements which have `field` set to the name of each parameter that could not be read. The `value` parameter should be omitted. For the response code parameter to be set to `200`, both `field` and `value` must be specified, where `value` is the current value of an attribute that is identified by the value of the `field` parameter.

Request format:

```
Incoming message from the server:

Topic: iotdm-1/observe
{
    "d": {
        "fields": [
            "string"
        ]
    },
    "reqId": "string"
}
```

Response format:

```
Outgoing message from the device:

Topic: iotdevice-1/response
{
    "rc": number,
    "message": "string",
    "d": {
        "fields": [
            {
                "field": "field_name",
                "value": "field_value"
            }
        ]
    },
    "reqId": "string"
}
```


## Cancel Attribute Observation requests
{: #observations-cancel}

{{site.data.keyword.iot_short_notm}} can send a request to a device to cancel the current observation of one or more device attributes by using the Cancel Attribute Observation request type. The `fields` part of the request is an array of the device attribute names from the device model, for example, `location`, `mgmt.firmware`, or `mgmt.firmware.state` parameters.

The `message` parameter must be specified if the value of the `rc` parameter is not `200`.

**Important:** Devices must implement, observe, notify, and cancel operations in order to support [Firmware Actions- Update](requests.html#firmware-actions-update) request types.

### Topic for a Cancel Attribute Observation request


The server publishes a Cancel Attribute Observation request to the following topic:

```
iotdm-1/cancel
```


### Message format for a Cancel Attribute Observation request


Request format:

```
Incoming message from the server:

Topic: iotdm-1/cancel
{
    "d": {
        "fields": [
            "string"
        ]
    },
    "reqId": "string"
}
```

Response format:

```
Outgoing message from the device:

Topic: iotdevice-1/response
{
    "rc": number,
    "message": "string",
    "reqId": "string"
}
```



## Notify Attribute Changes requests
{: #observations-notify}

{{site.data.keyword.iot_short_notm}} can make an observation request for a specific attribute or a set of values by using the Notify Attribute Changes request type. When the value of the attribute or attributes changes, the device must send a notification that contains the latest value.

The value of the `field_name` parameter is the name of the attribute that changed, and the `field_value` is the current value of the attribute. The attribute can be a complex field. If multiple values in a complex field are updated as a result of a single operation, only a single notification message is sent.

When the notify request is processed successfully, the value of the `rc` parameter is set to `200`. If the request is not correct, the value of the `rc` parameter is set to `400`. If the parameter that is specified in the notify request is not observed, the value of the `rc` parameter is set to `404`.

**Important:** Devices must implement observe, notify, and cancel operations in order to support [Firmware Actions- Update](requests.html#firmware-actions-update) request types.


### Topic for a Notify Attribute Change request


A device publishes a Notify Attribute Change request to the following topic:

```
iotdevice-1/notify
```


### Message format for a Notify Attribute Change request


Request format:

```
Outgoing message from the device:

Topic: iotdevice-1/notify
{
    "d": {
        "field": "field_name",
        "value": "field_value"
    }
    "reqId": "string"
}
```

Response format:

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": number,
    "reqId": "string"
}
```

### Response codes for a Notify Attribute Change request

|Response code |Message |
|:---|:---|
|200   |The operation was successful.|
|400   |The input message does not match the expected format, or one of the values is out of the valid range.|
|404   |The topic name is incorrect, or the device is not in the database, or there is no observation for the field that was reported.|
|409   |A conflict occurred during the device database update. To resolve this conflict, simplify the operation if necessary.|
|500   |An internal error occurred.|
