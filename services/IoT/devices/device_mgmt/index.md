---

copyright:
  years: 2015, 2016

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

The {{site.data.keyword.iot_full}} recognizes two classes of device; **managed devices** and **unmanaged devices**.

**Managed devices** are defined as devices that contain a device management agent. A device management agent is a set of logic that allows the device to interact with the {{site.data.keyword.iot_short_notm}} Device Management service by using the Device Management Protocol. Managed devices can perform device management operations, including location updates, firmware downloads and updates, reboots, and factory resets.

The Device Management Protocol defines a set of supported operations. A device management agent can support a subset of the operations, but the **managed devices** and **unmanaged devices** operations must be supported. A device supporting firmware action operations must also support observation.



The Device Management Protocol is built on top of the MQTT messaging protocol. For more information about how the Device Management Protocol interacts with MQTT, see [MQTT connectivity for devices](../mqtt.html).


### The device management lifecycle


1. A device and its associated device type are created in the {{site.data.keyword.iot_short_notm}} by using either the dashboard or the REST API.
2. A device connects to the {{site.data.keyword.iot_short_notm}}, and uses the **managed devices** operation to become a managed device.
3. You can view and manipulate the metadata for a device through device operations, as outlined in 'Device model', for example, firmware update and device restart operations.
4. A device can communicate updates about its location, diagnostic information, and error codes, through the Device Management Protocol.
5. To handle defunct devices in large device populations, the **managed devices** operation request includes an optional lifetime' parameter. The 'lifetime' parameter is the number of seconds within which the device must make another **managed devices** request to avoid being classified as dormant and becoming an unmanaged device.
6. When a device is decommissioned, you can remove it from the {{site.data.keyword.iot_short_notm}} by using the dashboard or the REST API.

### Return code summary


The following list outlines the return codes that are generated at various stages during the device management lifecycle.

- 200: Operation succeeded
- 202: Accepted (for initiating commands)
- 204: Changed (for attribute updates)
- 400: Bad request, for example, if a device is not in the appropriate state for this command
- 404: Attribute was not found, this code is also used if the operation was published to an invalid topic
- 409: Resource could not be updated due to a conflict, for example, the resource is being updated by two simultaneous requests, so update could be retried later
- 500: Unexpected device error
- 501: Operation not implemented


## Manage device
{: #manage_device_request}

A device uses the 'Manage Device' request to become a managed device. The 'Manage Device' request must be the first device management request sent by the device after connecting to the {{site.data.keyword.iot_short_notm}}. A device management agent typically sends this type of request whenever it starts or restarts.

**Important:** Support for this operation is mandatory for any managed devices.



### Topic

A device publishes this request to the following topic:

```
iotdevice-1/mgmt/manage
```

The server responds to this request on the following topic:

```
iotdm-1/response
```




### Message format


For the request, the ``d`` field and all of its subfields are optional. The ``metadata`` and ``deviceInfo`` field values replace the corresponding attributes for the sending device if they are sent.

The optional ``lifetime`` field specifies the length of time in seconds within which the device must send another 'Manage eDvice' request to avoid reverting back to an unmanaged device state that is classified as dormant. If omitted or if set to ``0``, the managed device does not become dormant. The minimum supported setting for the ``lifetime`` field is ``3600`` seconds(one hour).

The optional fields, ``supports.deviceActions`` and ``supports.firmwareActions``, indicate the capabilities of the device management agent. If ``supports.deviceActions`` is set, then the agent supports both restart and factory reset actions. For a device that does not distinguish between a restart and a factory reset, it is acceptable to use the same behavior for both actions. If ``supports.firmwareActions`` is set, the agent supports both firmware download and firmware update actions.

The following sample outlines the request format:

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

The following sample outlines the response format:

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```


### Response codes


- 200: The operation was successful.
- 400: The input message does not match the expected format, or one of the values is out of the valid range.
- 404: The topic name is incorrect, or the device is not in the database.
- 409: A conflict occurred during the device database update. To resolve this, simplify the operation if necessary.


## Unmanage device
{: #manage-unmanage}


A device uses an 'Unmanage Device' request when it no longer needs to be managed. The {{site.data.keyword.iot_short_notm}} no longer sends new device management requests to this device and all device management requests from the device are rejected, except for 'Manage Device' requests.

**Important:** Support for this operation is mandatory for any managed devices.

### Topic


A device publishes this request to the following topic:

```
iotdevice-1/mgmt/unmanage
```

The server responds to this request on the following topic:

```
iotdm-1/response
```

### Message format

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

### Response codes


- 200: The operation was successful.
- 400: The input message does not match the expected format, or one of the values is out of the valid range.
- 404: The topic name is incorrect, or the device is not in the database.
- 409: A conflict occurred during the device database update. To resolve this, simplify the operation if necessary.

## Update location
{: #update-location}

The location metadata for a device can be updated in {{site.data.keyword.iot_short_notm}} in two ways:

#### Automatic device location updates
- The device notifies {{site.data.keyword.iot_short_notm}} about the location update: The device retrieves its location from a GPS receiver and sends a device management message to the {{site.data.keyword.iot_short_notm}} instance to update its location. The time stamp captures the time at which the location was retrieved from the GPS receiver. This means that the time stamp is valid, even when there is a delay in sending the location update message. If time stamp is omitted from the device management message, the date and time of the message receipt is used to update the  location metadata.

#### Manual device location updates through the REST API
- You can manually set the location metadata for a static device through the {{site.data.keyword.iot_short_notm}} REST API when the device is registered. You can also modify the location later. The time stamp setting is optional, but when omitted, the current date and time is set in the location metadata for the device.

### Location update triggered by device

Devices that can determine their location can choose to notify the {{site.data.keyword.iot_short_notm}} device management server about location changes.

### Topic


A device publishes this request to the following topic:

```
iotdevice-1/device/update/location
```

The server responds to this request on the following topic:

```
iotdm-1/response
```

### Location update triggered by user or app


When a user or application updates the location of an active managed device the device retrieves an update message.




### Topic


The server publishes this request to the following topic:

```
iotdm-1/device/update
```

### Message format


The "measuredDateTime" is the date of location measurement. The "updatedDateTime" is the date of the update to the device information. For efficiency reasons, the {{site.data.keyword.iot_short_notm}} sometimes batches updates to location information so that the updates are slightly delayed. The "latitude" and "longitude" must be specified in decimal degrees using WGS84.

Whenever location is updated, the values provided for latitude, longitude, elevation and uncertainty are considered as a single multi-value update. The latitude and longitude are mandatory and must both be provided with each update.  Elevation and uncertainty are optional and can be omitted.

If an optional value is provided on an update and then omitted on a later update, the earlier value is deleted by the later update. Each update is considered as a complete multi-value set.

### Location update triggered by device


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

### Response codes


- 200: The operation was successful.
- 400: The input message does not match the expected format, or one of the values is out of the valid range.
- 404: The topic name is incorrect, or the device is not in the database.
- 409: A conflict occurred during the device database update. To resolve this, simplify the operation if necessary.

### Location update triggered by users or apps


Payload format:

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

**Note:** There is no reqId as a response by device is not required.

## Update device attributes
{: #update-attributes}

Through the REST API, {{site.data.keyword.iot_short_notm}} can send a request to a device to update one or more of the following device attribute values:


Attribute        | Value       | More information
----- | ----- | -----
Location  | location | See'Update location'
Metadata | metadata | Optional
Device information | deviceInfo | Optional
Firmware | mgmt.firmware |See 'Firmware update process'

The "value" is the new value of the device attribute. It is a complex field matching the device model.




### Topic


The server publishes the device update request to the following topic:

```
iotdm-1/device/update
```


### Message format


Payload format:

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


## Add error code
{: #diag-add-error-code}

Devices can choose to notify the {{site.data.keyword.iot_short_notm}} device management server about changes to their error status.

### Topic


A device publishes this request to the following topic:

```
iotdevice-1/add/diag/errorCodes
```

### Message format


The “errorCode” is a current device error code that needs to be added to the {{site.data.keyword.iot_short_notm}}.

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

### Response codes


- 200: The operation was successful.
- 400: The input message does not match the expected format, or one of the values is out of the valid range.
- 404: The topic name is incorrect, or the device is not in the database.
- 409: A conflict occurred during the device database update. To resolve this, simplify the operation if necessary.



## Clear error codes
{: #diag-clear-error-codes}

Devices can request that {{site.data.keyword.iot_short_notm}} clears all error codes for the device.

### Topic


A device publishes this request to the following topic:

```
iotdevice-1/clear/diag/errorCodes
```

### Message format


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

### Response codes


- 200: The operation was successful.
- 400: The input message does not match the expected format, or one of the values is out of the valid range.
- 404: The topic name is incorrect, or the device is not in the database.
- 409: A conflict occurred during the device database update. To resolve this, simplify the operation if necessary.





## Add log
{: #diag-add-log}

Devices can choose whether to notify {{site.data.keyword.iot_short_notm}} device management support about changes by adding a new log entry. Log entries include a log message, time stamp, severity, and optionally base64-encoded binary diagnostic data.

### Topic
A device publishes this request to the following topic:

```
iotdevice-1/add/diag/log
```


### Message format

Where:

- "message" is a diagnostic message that needs to be added to {{site.data.keyword.iot_short_notm}}
- "timestamp" is the date and time of the log entry in ISO8601 format
- "data" is optional base64-encoded diagnostic data
- "severity" is the severity of the message (0: informational, 1: warning, 2: error)

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


### Response codes


- 200: The operation was successful.
- 400: The input message does not match the expected format, or one of the values is out of the valid range.
- 404: The topic name is incorrect, or the device is not in the database.
- 409: A conflict occurred during the device database update. To resolve this, simplify the operation if necessary.


## Clear logs
{: #diag-clear-logs}

Devices can request {{site.data.keyword.iot_short_notm}} to clear all of the log entries for the device.

### Topic


A device publishes this request to the following topic:

```
iotdevice-1/clear/diag/log
```

### Message format


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

### Response codes


- 200: The operation was successful.
- 400: The input message does not match the expected format, or one of the values is out of the valid range.
- 404: The topic name is incorrect, or the device is not in the database.
- 409: A conflict occurred during the device database update. To resolve this, simplify the operation if necessary.



## Observe attribute changes
{: #observations-observe}

{{site.data.keyword.iot_short_notm}} can send this request to a device to observe changes of one or more device attributes. When the device receives this request, it must send a notification request ("notify" message) to {{site.data.keyword.iot_short_notm}} whenever the observed attributes value changes.

**Important:** Devices must implement, observe, notify, and cancel operations in order to support [Firmware Actions- Update](requests.html#firmware-actions-update).

### Topic


The server publishes this request to the following topic:

```
iotdm-1/observe
```

### Message format


The "fields" field is an array of the device attribute names from the device model. For example, values could be "location", "mgmt.firmware" or "mgmt.firmware.state". If a complex field, such as "mgmt.firmware" is specified, it is expected that its underlying fields are updated at the same time, such that only a single notify message is generated.

The "message" field used in the response can be specified if the value of "rc" is not 200. If any specified field value cannot be retrieved, the value of
"rc" must be set to either 404 (if not found) or 500 (any other reason). When values for fields to be observed cannot be found, "fields" should contain an array of elements with "field" set to the name of each field that could not be read, "value" fields should be omitted. For the response code to be set to 200, both "field" and "value" must be specified, where "value" is the current value of an attribute that is identified by "field" content.

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


## Cancel attribute observation
{: #observations-cancel}

{{site.data.keyword.iot_short_notm}} can send this request to a device to cancel the current observation of one or more device attributes. The "fields" is an array of the device attribute names from the device model, for example, values could be "location", "mgmt.firmware" or "mgmt.firmware.state".

The "message" field must be specified if "rc" is not 200.

**Important:** Devices must implement, observe, notify, and cancel operations in order to support [Firmware Actions- Update](requests.html#firmware-actions-update).

### Topic


The server publishes this request to the following topic:

```
iotdm-1/cancel
```


### Message format


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



## Notify attribute changes
{: #observations-notify}

{{site.data.keyword.iot_short_notm}} can make an observation request referring to a specific attribute or a set of values. When the value of the attribute or attributes changes, the device must send a notification that contains the latest value.

The "field_name" value is the name of the attribute that changed, and the "field_value" is the current value of the attribute. The attribute can be a complex field, if multiple values in a complex field are updated as a result of a single operation, only a single notification message is sent.

When the notify request is processed successfully, the value of "rc" is set to 200. If the request is not correct, the value of "rc" is set to 400. If the field specified in the notify request is not observed, the value of "rc" is set to 404.

**Important:** Devices must implement observe, notify, and cancel operations in order to support [Firmware Actions- Update](requests.html#firmware-actions-update).


### Topic


A device publishes this request to the following topic:

```
iotdevice-1/notify
```


### Message format


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

### Response codes


- 200: The operation was successful.
- 400: The input message does not match the expected format, or one of the values is out of the valid range.
- 404: The topic name is incorrect, the device is not in the database, or there is no observation for the field reported.
- 409: A conflict occurred during the device database update. To resolve this, simplify the operation if necessary.
- 500: An internal error occurred, contact IBM Support.
