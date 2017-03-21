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


# Python for application developers
{: #python}


You can use Python to build and develop applications that interact with your organization on {{site.data.keyword.iot_full}}. The Python client for {{site.data.keyword.iot_short_notm}} provides an API to facilitate simple interaction with {{site.data.keyword.iot_short_notm}} features by abstracting away the underlying protocols such as MQTT and HTTP.

{:shortdesc}

Use the information and examples that are provided to start developing your applications by using Python.

## Downloading the Python client and resources
{: #python_client_download}

To access the Python client for {{site.data.keyword.iot_short_notm}} and other available resources, go to the [iot-python ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/iot-python){: new_window} repository in GitHub and complete the installation instructions.

## Constructor
{: #constructor}

The options dictionary creates definitions that are used to interact with the  {{site.data.keyword.iot_short_notm}} module. The constructor builds the client instance and accepts an options dictionary that contains the following definitions:

|Definition|Description |
|:-----|:-----|
|`orgId`|Your organization ID.|
|`appId`|The unique ID of an application in your organization.|
|`auth-method`|The method of authentication. The only method that is supported is `apikey`.|
|`auth-key`|An optional API key, which you must specify when you set the value of auth-method to `apikey`.|
|`auth-token`|An API key token, which is also required when you set the value of auth-method to `apikey`.|
|`clean-session`|A true or false value that is required only if you want to connect the application in durable subscription mode. By default, `clean-session` is set to true.|


If no options dictionary is provided, the client connects to the {{site.data.keyword.iot_short_notm}} Quickstart service as an unregistered device.

```python

import ibmiotf.application
try:
  options = {
    "org": organization,
    "id": appId,
    "auth-method": authMethod,
    "auth-key": authKey,
    "auth-token": authToken,
    "clean-session": true
  }
  client = ibmiotf.application.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

### Using a configuration file


If you are not using an options dictionary, you must include a configuration file that contains an options dictionary in the following code format:

```python

import ibmiotf.application
try:
  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)
except ibmiotf.ConnectionException as e:
...
```
The application configuration file must be in the following format:

```python

[application]
org=orgId
id=myApplication
auth-method=apikey
auth-key=key
auth-token=token
clean-session=true/false

```

## API calls
{: #api_calls}

Each method in the API client responds with either:

- A valid JSON or Boolean response if successful
- An IoTFCReSTException exception if unsuccessful

To get more information about why an API call failed, or to see whether the action is partially successful, an application can parse the properties of an exception response. The IoTFCReSTException exception response contains the following properties:

|Property|Description|
|:---|:---|
|``httpcode``|The HTTP status code.|
|``message``|An exception message that contains the reason for the failure.|
|``response``|The JSON element that contains the partial response. If none exists, this value is set to null.|

## Subscribing to device events
{: #subscribe_device_events}

Events are the mechanism by which devices publish data to the {{site.data.keyword.iot_short_notm}} instance. The device controls the content of the event and assigns a name for each event that it sends.

When an event is received by the {{site.data.keyword.iot_short_notm}} instance, the credentials of the received event identify the sending device, which makes it impossible for a device to impersonate another device.

By default, applications subscribe to all events from all connected devices. Use the deviceType, deviceId, event, and msgFormat parameters to control the scope of the subscription. A single client can support multiple subscriptions. The following code samples show how you can use deviceType, deviceId, event, and msgFormat parameters to define the scope of a subscription:


### Subscribing to all events from all devices


```python

import ibmiotf.application
  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents()
```

### Subscribing to all events from all devices of a specific type


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType)
```

### Subscribing to a specific event from all devices


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(event=myEvent)
```

### Subscribing to a specific event from two or more different devices

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, event=myEvent)
client.subscribeToDeviceEvents(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId, event=myEvent)
```

### Subscribing to all events that are published in JSON format

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, msgFormat="json")
```

## Handling events from devices
{: #handling_events_devices}

To process the events that are received by your subscriptions, you need to register an event callback method. The messages are returned as an instance of the Event class:

|Property|Data type|Description|
|:---|:---|
|``event.device``|String|Uniquely identifies the device across all types of devices in the organization|
|``event.deviceType``|String|Identifies the device type. Typically, the deviceType is a grouping for devices that perform a specific task, for example "weatherballoon".|
|``event.deviceId``|String|Represents the ID of the device. Typically, for a given device type, the deviceId is a unique identifier of that device, for example a serial number or MAC address.|
|``event.event``|String|Typically used to group specific events, for example "status", "warning" and "data".
|``event.format``|String|The format can be any string, for example JSON.
|``event.data``|Dictionary|The data for the message payload. Maximum length is 131072 bytes.
|``event.timestamp``|Date and time|The date and time of the event|

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  def myEventCallback(event):
      str = "%s event '%s' received from device [%s]: %s"
      print(str % (event.format, event.event, event.device, json.dumps(event.data)))

...
client.connect()
client.deviceEventCallback = myEventCallback
client.subscribeToDeviceEvents()
```


## Subscribing to device status
{: #subscribe_device_status}


By default, when you subscribe to device status, status updates are received for all connected devices. Use the type and ID parameters to control the scope of the subscription. A single client can support multiple subscriptions.

### Subscribing to status updates for all devices


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus()
```

### Subscribing to status updates for all devices of a specific type


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus(deviceType=myDeviceType)
```

### Subscribing to status updates for two different devices


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus(deviceType=myDeviceType, deviceId=myDeviceId)
client.subscribeToDeviceStatus(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId)
```

## Handling status updates from devices
{: #handling_device_updates}

Status Events

To process the status updates that are received by your subscriptions, you need to register an event callback method. The messages are returned as an instance of the Status class.

There are two types of status events, ``Connect`` events and ``Disconnect`` events. All status events include the following properties:

|Property|Data type|
|:---|:---|
|``status.clientAddr``|String|
|``status.protocol``|String|
|``status.clientId``|String|
|``status.user``|String|
|``status.time``|Date and time|
|``status.action``|String|
|``status.connectTime``|Date and time|
|``status.port``|Integer|


The ``status.action`` property determines whether a status event is of type ``Connect`` or ``Disconnect``.

``Disconnect`` status events include the following extra properties:

|Property|Data type|
|:---|:---|
|``status.writeMsg``|Integer|
|``status.readMsg``|Integer|
|``status.reason``|String|
|``status.readBytes``|Integer|
|``status.writeBytes``|Integer|

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

def myStatusCallback(status):

  if status.action == "Disconnect":
    str = "%s - device %s - %s (%s)"
    print(str % (status.time.isoformat(), status.device, status.action, status.reason))
    else:
      print("%s - %s - %s" % (status.time.isoformat(), status.device, status.action))
  ...
client.connect()
client.deviceStatusCallback = myStatusCallback
client.subscribeToDeviceStstus()
```


## Publishing events from devices
{: #publishing_device_events}

Applications can publish events as if they originated from a device.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent(myDeviceType, myDeviceId, "status", "json", myData)
```


## Publishing commands to devices
{: #publishing_commands_devices}


Applications can publish commands to connected devices.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
commandData={'rebootDelay' : 50}
client.publishCommand(myDeviceType, myDeviceId, "reboot", "json", commandData)
```


## Organization details
{: #org_details}

Applications can use the ``getOrganizationDetails()`` method to retrieve the details about the configuration of the organization.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    orgDetail = client.api.getOrganizationDetails()
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```

For information about the request and response model and HTTP status codes, refer to the Organization Configuration section of the [{{site.data.keyword.iot_short_notm}} API ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.


## Bulk device operations
{: #bulk_device_ops}

Your applications can use bulk operations to get, add, or remove multiple devices simultaneously.

For information about the list of query parameters, the request and response model, and HTTP status codes, see the 'Bulk Operations' section of the [{{site.data.keyword.iot_short_notm}} API ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Bulk_Operations/){: new_window}.


### Retrieving device information

Bulk device information can be retrieved by using the ``getAllDevices()`` method. This method retrieves information on all registered devices in the organization. Each request can contain a maximum of 512 KB.

The response contains parameters that are required by the application. Use the dictionary results from the response to get the array of devices that is returned. Other parameters in the response are required to make more calls, for example, the ``_bookmark`` element can be used to page through results. Submit the first request without specifying a bookmark, then take the bookmark that is returned in the response and provide it on the request for the next page. Repeat until the end of the result set, which is indicated by the absence of a bookmark. Each request must use the same values for the other parameters, otherwise the results will be undefined.


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    deviceList = client.api.getAllDevices()
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```
### Adding multiple devices


Use the ``addMultipleDevices()`` method to add one or more devices to your {{site.data.keyword.iot_short_notm}} organization. A request can be no larger than 512 KB. The response contains the authentication tokens that were generated for each device. Ensure that you make a copy of the authentication tokens because if you lose the authentication tokens, they cannot be retrieved.


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  listOfDevicesToAdd = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
  deviceList = client.api.addMultipleDevices(listOfDevicesToAdd)
except IoTFCReSTException as e:
  print("ERROR [" + e.httpcode + "] " + e.message)
```

### Deleting multiple devices


Use the ``deleteMultipleDevices()`` method to delete multiple devices from an {{site.data.keyword.iot_short_notm}}
organization. A request can be no larger than 512 KB.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  listOfDevicesToDelete = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
      deviceList = client.api.deleteMultipleDevices(listOfDevicesToDelete)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```


## Device type operations
{: #device_type_ops}

The device types that you create in your organization can be used to create templates for adding devices. By using the {{site.data.keyword.iot_short_notm}} API features, your applications can list, create, delete, view, or update device types in your organization.

For information about query parameters, the request and response model, and HTTP status codes, see the 'Device types' section of the [{{site.data.keyword.iot_short_notm}} API ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window} documentation.


### Retrieving all device types

Use the ``getAllDeviceTypes()`` method to retrieve all of the device types that are in your {{site.data.keyword.iot_short_notm}} organization.
Use the dictionary results from the response to get the array of devices that is returned. Other parameters in the response are required to make more calls, for example, the ``_bookmark`` element can be used to page through results. Submit the first request without specifying a bookmark, then take the bookmark that is returned in the response and provide it on the request for the next page. Repeat this process until the end of the result set, which is indicated by the absence of a bookmark. Each request must use the same values for the other parameters, otherwise the results will be undefined.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

 listOfDevicesToAdd = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
   options = {'_limit' : 2}
   deviceTypeList = client.api.getAllDeviceTypes(options)
except IoTFCReSTException as e:
   print("ERROR [" + e.httpcode + "] " + e.message)

```

### Adding a device type

Use the ``addDeviceType()`` method to register a device type to your {{site.data.keyword.iot_short_notm}} instance. In each request, you must first define the device information and the device metadata elements that you want to be applied to all devices of this type. The device information element consists of several variables, which include serial number, manufacturer, model, class, description, firmware, hardware versions, and descriptive location. The metadata element consists of custom variables and values, which can be defined by the user.


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  info = {
      "serialNumber": "100087",
      "manufacturer": "ACME Co.",
      "model": "7865",
      "deviceClass": "A",
      "description": "My shiny device",
      "fwVersion": "1.0.0",
      "hwVersion": "1.0",
      "descriptiveLocation": "Office 5, D Block"
  }
  meta = {
      "customField1": "customValue1",
      "customField2": "customValue2"
  }

try:
      deviceType = client.api.addDeviceType(deviceType = "myDeviceType", description = "My first device type", deviceInfo = info, metadata = meta)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```

### Deleting a device type


Use the ``deleteDeviceType()`` method to delete a device type from your  {{site.data.keyword.iot_short_notm}} organization.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
      success = client.api.deleteDeviceType("myDeviceType")
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```

### Retrieving information for specific device types


Use the ``getDeviceType()`` method to retrieve information for a specific device type. The ``typeId`` of the device type that you want to retrieve must be specified as a parameter.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    deviceTypeInfo = client.api.getDeviceType("myDeviceType")
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```

### Updating a device type


Use the ``updateDeviceType()`` method to modify the properties of a device type. When you use the ``updateDeviceType()`` method, first specify the ``typeId`` of the device type to be updated and then specify the following elements:

- ``description``
- ``deviceInfo``
- ``metadata``

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  info = {
      "serialNumber": "100087",
      "manufacturer": "ACME Co.",
      "model": "7865",
      "deviceClass": "A",
      "description": "My shiny device",
      "fwVersion": "1.0.0",
      "hwVersion": "1.0",
      "descriptiveLocation": "Office 5, D Block"
  }
  meta = {
      "customField1": "customValue1",
      "customField2": "customValue2",
      "customField3": "customValue3"
  }

try:
      updatedDeviceTypeInfo = client.api.updateDeviceType("myDeviceType", "New description", deviceInfo, metadata)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```


## Device operations
{: #device_ops}

Device operations that are made available in the API include listing, adding, removing, viewing, updating, viewing location, and viewing device management information of devices in a
 {{site.data.keyword.iot_short_notm}} organization.

For information about the query parameters, the request and response model, and HTTP status codes, see the 'Device section' of the [{{site.data.keyword.iot_short_notm}} API ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.


### Retrieving devices of a particular device type

Use the ``retrieveDevices()`` method to retrieve all the devices of a particular device type in an organization in a {{site.data.keyword.iot_short_notm}} instance, which is shown in the following example:


```python

   print("\nRetrieving All existing devices")
   print("Retrieved Devices = ", apiCli.retrieveDevices(deviceTypeId))
```

Use the dictionary results from the response to get the array of devices that is returned. Other parameters in the response are required to make more calls, for example, the *_bookmark* element can be used to page through the results. Submit the first request without specifying a bookmark, then take the bookmark that is returned in the response and provide it on the request for the next page. Repeat until the end of the result set, which is indicated by the absence of a bookmark. Each request must use the same values for the other parameters, otherwise the results will be undefined.

To pass the *_bookmark* or any other condition, the overloaded method must be used. The overloaded method takes the parameters in the form of dictionary as shown in the following example:

```python
response = apiClient.retrieveDevices("iotsample-arduino", parameters);
```

The previous code sample sorts the response based on device ID and then uses the bookmark to page through the results.

### Adding a device


To add a device to a {{site.data.keyword.iot_short_notm}} organization, use the ``registerDevice()`` method. The ``registerDevice()`` method adds a single device to your {{site.data.keyword.iot_short_notm}} organization. When you add a device, you can specify the following parameters:

|Parameter|Requirement|Description
|:---|:---|
|``deviceTypeId``|Optional|Assigns a device type to the device. If a conflict exists between the variables that are defined by the device type and the variables that are defined by the ``deviceInfo`` variable, the device-specific variables take precedence.|
|``deviceId``|Mandatory||
|``authToken``|Optional|If not provided, an authentication token is generated and included in the response.|
|``deviceInfo``|Optional|Contains several variables that include serialNumber, manufacturer, model, deviceClass, description, descriptiveLocation, firmware, and hardware versions.|
|``metadata``|Optional|Custom field value string pairs, as outlined in [Sample code for adding a device type](#sample_device_type).|
|``location``|Optional|Contains the longitude, latitude, elevation, accuracy, and measuredDateTime variables.|

For more information about these parameters and the response format and codes, see the [API documentation ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Devices/post_device_types_typeId_devices){: new_window}.

When you use the ``registerDevice()`` method, define the mandatory deviceID parameter and the optional parameters that you require for your device and then call the method by using the parameters that you selected.

### Sample code for adding a device type
{: #sample_device_type}

Insert the following code after the constructor code in a Python(.py) script file. The sample demonstrates a method for adding a device type by defining the deviceId, authToken, metadata, deviceInfo, and location parameters.

```python

deviceId = "200020002000"
authToken = "password"
metadata = {"customField1": "customValue1", "customField2": "customValue2"}
deviceInfo = {"serialNumber": "001", "manufacturer": "Blueberry", "model": "abc1", "deviceClass": "A", "descriptiveLocation" : "Bangalore", "fwVersion" : "1.0.1", "hwVersion" : "12.01"}
location = {"longitude" : "12.78", "latitude" : "45.90", "elevation" : "2000", "accuracy" : "0", "measuredDateTime" : "2015-10-28T08:45:11.662Z"}

apiCli.registerDevice(deviceTypeId, deviceId, metadata, deviceInfo, location)
```
### Deleting a device

Use the ``deleteDevice()`` method to remove a device from an organization on the {{site.data.keyword.iot_short_notm}} organization. When you delete a device by using the ``deleteDevice()`` method, you must specify the deviceTypeId and deviceId parameters.

The following code sample outlines the format that is required for this method:

```python
apiCli.deleteDevice(deviceTypeId, deviceId)
```

### Getting a device

Use the ``getDevice()`` method to retrieve a device from an organization on the {{site.data.keyword.iot_short_notm}}. When you retrieve device details by using the ``getDevice()`` method, you must specify the deviceTypeId and deviceId parameters

The following code sample provides an outline of the format that is required for this method.

```python
apiCli.getDevice(deviceTypeId, deviceId)
```

### Retrieving all devices

Use the ``getAllDevices()`` method to retrieve all devices in an organization on the {{site.data.keyword.iot_short_notm}}.

```python
apiCli.getAllDevices({'typeId' : deviceTypeId})
```

### Updating a device

To modify one or more properties of a device, use the ``updateDevice()`` method.

You can update any property in the deviceInfo or metadata parameters. To update a device property, define  the deviceInfo parameter before you call the ``updateDevice()`` method. The status parameter must contain ``alert``: True. The alert property controls whether a device displays error codes in the {{site.data.keyword.iot_short_notm}} user interface and must be set by default to ``enabled``: True, as outlined in the following code example:

```python
status = { "alert": { "enabled": True }  }
apiCli.updateDevice(deviceTypeId, deviceId, metadata2, deviceInfo, status)
```

### Sample code for updating deviceInfo properties

The following code sample identifies a specific device and then updates several properties of the deviceInfo parameter.

```python
status = { "alert": { "enabled": True } }
deviceInfo = {descriptiveLocation: "London", hwVersion: "2.0.1", fwVersion: "2.5.1"}
apiCli.updateDevice("MyDeviceType", "200020002000", deviceInfo, status)
```

### Retrieving location information


Use the ``getDeviceLocation()`` method to retrieve the location information of a device. The parameters that are required for retrieving the location data are deviceTypeId and deviceId.

```python
apiClient.getDeviceLocation("iotsample-arduino", "arduino01")
```  

The response to this method contains the longitude, latitude, elevation, accuracy, measuredTimeStamp, and updatedTimeStamp properties.

### Updating location information


Use the ``updateDeviceLocation()`` method to modify the location information for a device. As with updating the device properties, the deviceLocation parameter must be defined with the changes that you would like to apply. The following code sample demonstrates changing the location data for a specific device:

```python
deviceLocation = { "longitude": 0, "latitude": 0, "elevation": 0, "accuracy": 0, "measuredDateTime": "2015-10-28T08:45:11.673Z"}
apiCli.updateDeviceLocation(deviceTypeId, deviceId, deviceLocation)
```

If a date is not supplied, the current date and time is used.


### Get management information


Use the ``getDeviceManagementInformation()`` method to get the device management information for a device. The response contains the last activity date-time, the device's dormant status (True/False), support for device and firmware actions, and firmware data. For a comprehensive list of response content, see the relevant API documentation.

The following code sample returns the device management information for a device with a deviceId that is set to "00aabbccde03" and a deviceTypeId that is set to "iotsample-arduino":

```
apiCli.getDeviceManagementInformation("iotsample-arduino", "00aabbccde03")
```

## Device diagnostic operations
{: #device_diag_ops}

Use the device diagnostic operations for implementing the following troubleshooting and log management tasks:
- Clearing logs
- Retrieving all or specific logs for a device
- Adding log information
- Deleting logs
- Clearing error codes
- Retrieving device error codes
- Adding error codes

For more information about query and response models, response codes, and query parameters, see the [API documentation ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window} {{site.data.keyword.iot_short_notm}} API documentation.

### Get diagnostic logs


Use the ``getAllDiagnosticLogs()`` method to retrieve all diagnostic logs for a specific device. The ``getAllDiagnosticLogs()`` method requires the deviceTypeId and deviceId parameters.

```python
apiCli.getAllDiagnosticLogs(deviceTypeId, deviceId)
```

The response model for this method contains the log ID, message, severity, data, and time stamp properties.

### Clearing diagnostic logs for a device


Use the ``clearAllDiagnosticLogs()`` method to delete all diagnostic logs for a specific device. The required parameters are deviceTypeId and deviceId. Be careful when you delete log files, because they cannot be recovered after they are deleted.

```python
apiCli.clearAllDiagnosticLogs(deviceTypeId, deviceId)
```

### Adding a diagnostic log


Use the ``addDiagnosticLog()`` method to add an entry in the diagnostic log of the device. The log can be pruned when the new entry is added. If no date is supplied, the current date and time are added to the entry. To use this method, you need to define a 'logs' parameter with the following variables:


|Variable|Requirement|Description|
|:---|:---|:---|
|``message``|Mandatory|Contains the diagnostic message that you would like to add|
|``severity``|Optional|Corresponds to the severity of the diagnostic log and can be set to either 0, 1, or 2, which corresponds to the informational, warning, and error categories|
|``data``|Optional|Contains diagnostic data|
|``timestamp``|Optional|Contains the date and time of the log entry in ISO8601 format but if not specified, the current date and time are used|


The other parameters that are required in the method are the deviceTypeId and deviceId values for the device.

The following code sample contains an example of the ``addDiagnosticLog()`` method:

```python
logs = { "message": "MessageContent", "severity": 0, "data": "LogData"}
apiCli.addDiagnosticLog(deviceTypeId, deviceId, logs)
```

### Retrieving a specific diagnostic log


Use the  ``getDiagnosticLog()`` method to retrieve a specific diagnostic log for a specified device based on the log ID. The required parameters for this method are deviceTypeId, deviceId, and logId.

```python
apiCli.getDiagnosticLog(deviceTypeId, deviceId, logId)
```

### Deleting a diagnostic log


Use the ``deleteDiagnosticLog()`` method to delete a specific diagnostic log. To specify a diagnostic log, the deviceTypeId, deviceId, and logID parameters must be supplied.

```python
apiCli.deleteDiagnosticLog(deviceTypeId, deviceId, logId)
```

### Retrieving device error codes


Use the ``getAllDiagnosticErrorCodes()`` method to retrieve all diagnostic error codes that are associated with a specific device.

```python
apiCli.getAllDiagnosticErrorCodes(deviceTypeId, deviceId)
```

### Clear diagnostic error codes


Use the ``clearAllErrorCodes()`` method to clear the list of error codes that are associated with the device. The list is replaced with a single error code of zero.

```python
apiCli.clearAllErrorCodes(deviceTypeId, deviceId)
```

### Adding a single diagnostic error code


Use the ``addErrorCode()`` method to add an error code to the list of error codes that are associated with the device. The list can be pruned when the new entry is added. The parameters that are required in the method are deviceTypeId, deviceId, and errorCode. The errorCode parameter contains the following variables:

- errorCode: This variable is mandatory and should be set as an integer. This variable sets the number of the error code that is created.
- timestamp: This variable is optional and contains the date and time of the log entry in ISO8601 format. If this variable is not included, it is automatically added with the current date and time.

```python
errorCode = { "errorCode": 1234, "timestamp": "2015-10-29T05:43:57.112Z" }
apiCli.addErrorCode(deviceTypeId, deviceId, errorCode)
```

## Connection problem determination
{: #connection_problem_determination}

Use the ``getDeviceConnectionLogs()`` method to list connection log events for a device. Connection log events can be used to help diagnose connectivity problems between the device and the {{site.data.keyword.iot_short_notm}} service. The entries record successful connection, unsuccessful connection attempts, intentional disconnection, and server-initiated disconnection events.

```
apiCli.getDeviceConnectionLogs(deviceTypeId, deviceId)
```

The response includes a list of log entries, which contain log messages and time stamps.
