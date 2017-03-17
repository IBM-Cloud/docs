---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Device model
{: #device_model}

The device model describes the metadata and management characteristics of a device. The device database in the {{site.data.keyword.iot_full}} is the master
source of device information. Applications and managed devices can send updates, including location changes or the progress of a firmware update to the device database. As soon as these updates are received by the {{site.data.keyword.iot_short_notm}}, the database is updated and the information is made available to applications.

**Note:** With the exception of the [device management extension](#devicemanagementextension), the entire device model is available for both managed and unmanaged devices. However, an unmanaged device cannot directly update its device model in the database.

## Device identification
{: #device_id}

Every device has a `typeId` and a `deviceId` attribute. Typically, the `typeId` represents the model of your device, whereas the `deviceId` can represent its serial number. In
your {{site.data.keyword.iot_short_notm}} organization, the combination of `typeId` and `deviceId` must be unique for each device.

In addition to these attributes, the {{site.data.keyword.iot_short_notm}} constructs another identifier for each device. This identifier is called the `clientId`. The `clientId` is based on your `organizationId` and on the  `typeId` and `deviceId` values of the device. The `clientId` provides a way to uniquely identify an individual device. The characters that can be used in these identifiers are restricted so that they are compatible with communication protocols and REST APIs.

The following optional device identifiers can also be used:

- deviceInfo.manufacturer
- deviceInfo.serialNumber
- deviceInfo.model
- deviceInfo.deviceClass
- deviceInfo.description

For more information on the identifiers and descriptions of their comparative identifiers in other device management standards, see [Attributes](#attributes).


## Identifiers and device types
{: #id_and_device_types}

Every device that is connected to the {{site.data.keyword.iot_short_notm}} is associated with a device type. Device types are groups of devices that share characteristics or behaviors.

A device type has a set of attributes. When a device is added to the {{site.data.keyword.iot_short_notm}}, the attributes in its device type are used as a template. If the device has a value, that value is used. If the device does not have a value, the device type value is used. For example, the device type could have a value for the ``deviceInfo.fwVersion`` attribute, which reflects the firmware version at the time of manufacture. This value is copied from the device type into the devices when they are added. When a device is added, if the ``deviceInfo.fwVersion`` value already exists it is not overwritten.

When an attribute of a device type is updated, only new devices that are registered inherit the modifications made to the device type template.

## Attributes
{: #attributes}

The following table shows the list of attributes that can apply to devices in the {{site.data.keyword.iot_short_notm}}. Italicized attributes can also apply to device types.

Key:
  - API : Can be updated by using APIs
  - DMA : Can be updated by using Device Management Agent
  - R: Read-only
  - W: Write and read
  - A: Append

Attribute                        | Type       | Description                                       | API | DMA   
------------- | ------------- | ------------- | ------------- | -------------  |
 clientId                         | string     | The client ID that is used with MQTT connections          |  R  |   -  
 *typeId*                         | string     | Device type                                       |  R  |   -  
 deviceId                         | string     | Device ID                                         |  R  |    -
 classId                          | string     | Class of device ("Device" or "Gateway")           |  R  |   -  
 gatewayTypeId                    | string     | Type ID of the gateway that this device is using       |  R  |    -
 gatewayId                        | string     | Device ID of the gateway that this device is using     |  R  |   -  
 status.alert                     | boolean    | Indicates whether the device has an alert                   |  W  |  -   
 *deviceInfo.serialNumber*        | string     | The serial number of the device                   |  W  |  W    
 *deviceInfo.manufacturer*        | string     | The manufacturer of the device                    |  W  |  W   
 *deviceInfo.model*               | string     | The model of the device                           |  W  |  W  
 *deviceInfo.deviceClass*         | string     | The class of the device                           |  W  |  W  
 *deviceInfo.description*         | string     | The descriptive name of the device                |  W  |  W  
 *deviceInfo.fwVersion*           | string     | The firmware version that is currently known to be on the device    |  W  |  W  
 *deviceInfo.hwVersion*           | string     | The hardware version of the device                |  W  |  W  
 *deviceInfo.descriptiveLocation* | string     | The descriptive location, such as a room, building number, or a geographical region      |  W  |  W  
 *metadata*                       | complex    | Free-form metadata                                |  W  |  W  
 added.auth.id                    | string     | The ID that added the device                          |  R  |   -  
 added.dateTime                   | string     | ISO8601 date-time: Date and time the device was added |  R  |    -
 refs.diag.errorCodes             | string     | URI of diagnostics extension for error codes, if present |  R  |   -  
 refs.diag.logs                   | string     | URI of diagnostics extension for logs, if present        |  R  |   -  
 refs.location                    | string     | URI of location extension, if present             |  R  |   -  
 refs.mgmt                        | string     | URI of device management extension, is present                 |  R  |    -



## Extended attributes
{: #extended_attributes}

In addition to core attributes listed above in the Attributes section, there are additional attributes that are treated as extensions to the core device model. Simple queries about the device return information from the core device model, but not the extensions. Information from the extensions must be specifically requested.


Extension Name    | Prefix of attributes | Purpose      
------------- | ------------- | -------------                                         
 Diagnostics       | diag                 | Error logs and diagnostic information                 
 Location          | location             | Location of the device, potentially updated regularly
 Device management | mgmt                 | Device management actions, such as firmware update       


### Diagnostics extension


The diagnostics attributes are optional and are only present for devices that have error log information. These attributes are intended for diagnosing device problems, not for troubleshooting connectivity to the {{site.data.keyword.iot_short_notm}}. The amount of information that is stored in diagnostic attributes can be very large and must therefore be specifically queried.

Diagnostic log information is stored as an array of entries. Each entry consists of a message, an indication of severity, a timestamp and an optional byte-array of data. You can append entries by using an API. However, appending entries can cause earlier entries to be lost in order to keep the size of the diagnostic logs manageable.


Attribute            | Type       | Description                                                 | API | DMA
------------- | ------------- | ------------- | ------------- | -------------
 diag.errorCodes[]    | array of </br> integer(s)  | Array of error codes                                        |  A  |  A  
 diag.log[]           | array      | Array of diagnostic data                                    |  A  |  A  
 diag.log[].message   | string     | Diagnostic message                                          |  -   |    -
 diag.log[].timestamp | string     | ISO8601 date-time: Date and time of log entry               |  -   |    -
 diag.log[].logData   | string     | byte: Diagnostic data, base-64 encoded                      |  -   |    -
 diag.log[].severity  | number     | Severity of message, 0: informational, 1: warning, 2: error |  -   |    -


### Location extension

The location attributes are optional and are only present for devices that have location information. The location information is stored separately to allow the use of storage mechanisms that are better suited to dynamic information. This can be important when information is updated frequently, for example in the case of a mobile device.

For solutions that place significant importance on frequent location updates, it is expected that the location will be treated as part of the device's event payload, which enables higher update rates, simpler historical storage, and easier data analysis.


Attribute                 | Type   | Description                                             | API | DMA
------------- | ------------- | ------------- | ------------- | -------------
 location.longitude        | number | Longitude in decimal degrees using WGS84                |  W  |  W  
 location.latitude         | number | Latitude in decimal degrees using WGS84                 |  W  |  W  
 location.elevation        | number | Elevation in meters using WGS84                         |  W  |  W  
 location.measuredDateTime | string |ISO8601 date-time: Date and time of location measurement |  W  |  W  
 location.updatedDateTime  | string | ISO8601 date-time: Date and time                        |  R  |   
 location.accuracy         | number | Accuracy of the position in meters                      |  W  |  W  


### Device management extension
{: #devicemanagementextension}

The management attributes are only present for managed devices. When a managed device becomes dormant it becomes unmanaged, and the ``mgmt.`` attributes are deleted. The ``mgmt.`` attributes are set by the {{site.data.keyword.iot_short_notm}} as a result of processing device management requests. These attributes cannot be directly written by using the API.

Devices have a management lifecycle, which is defined by their status as managed devices. The device management agent on the device is responsible for sending a Manage Device request by using the device management protocol. To deal with defunct devices in large device populations, a managed device can be set to send a Manage Device request regularly. A managed device becomes dormant if this request is not sent to {{site.data.keyword.iot_short_notm}} for a specified period of time. To facilitate this functionality, the Manage Device request has an optional lifetime parameter. When the {{site.data.keyword.iot_short_notm}} receives a Manage Device request that has the lifetime parameter set, it calculates the time before another Manage Device request is required and stores it in the  ``mgmt.dormantDateTime`` attribute.


Attribute                     | Type    | Description                             | API | DMA
------------- | ------------- | ------------- | ------------- | -------------
 mgmt.dormant                   | boolean | Indicates whether the device has become dormant                  |  R  |  -
 mgmt.dormantDateTime           | string  | ISO8601 date-time: Date and time at which the managed device will become dormant   |  R  |  -   
 mgmt.lastActivityDateTime      | string  | ISO8601 date-time: Date and time of last activity, updated periodically    |  R  |    -
 mgmt.supports.deviceActions    | boolean | Indicates whether the device supports Reboot and Factory Reset actions  |  R  |   -  
 mgmt.supports.firmwareActions  | boolean | Indicates whether the device supports Firmware Download and Firmware Update actions    |  R  |     -
 mgmt.firmware.version          | string  | The version of the firmware that is on the device              |  R  |  W  
 mgmt.firmware.name             | string  | The name of the firmware that is used on the device      |  R  |  W  
 mgmt.firmware.uri              | string  | The URI from which the firmware image can be downloaded |  R  |  W  
 mgmt.firmware.verifier         | string  | The verifier, such as a checksum for the firmware image that is used to validate its integrity |  R  |  W  
 mgmt.firmware.state            | number  | Indicates the state of firmware download               |  R  |  W  
 mgmt.firmware.updateStatus     | number  | Indicates the status of the update                     |  R  |  W  
 mgmt.firmware.updatedDateTime  | string  | ISO8601 date-time: Date of last update                 |  R  |    -
