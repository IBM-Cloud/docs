---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Python for application developers
{: #python}


For more information, see:

-  The [iot-python](https://github.com/ibm-messaging/iot-python) repository in GitHub.
-  The [ibmiotf](https://pypi.python.org/pypi/ibmiotf) repository on PyPi.


## Constructor
{: #constructor}


The constructor builds the client instance, and accepts an options dict containing the following definitions:

| Definition     |Description     |
|----------------|----------------|
|``orgId``   |Your organization ID
|``appId``   |The unique ID of an application within your organization|
|``auth-method``   |Method of authentication whereby the only value that is currently supported is ``apikey``)|
|``auth-key``   |An optional API key, which is required when auth-method is set to ``apikey``|
|``auth-token``   |An API key token, which is required when auth-method is set to ``apikey``|

If no options dict is provided, the client connects to the{{site.data.keyword.iot_full}}  Quickstart service, and defaults to an unregistered device. The options dict creates definitions that are used to interact with the {{site.data.keyword.iot_full}} module.

```

    import ibmiotf.application
    try:
      options = {
        "org": organization,
        "id": appId,
        "auth-method": authMethod,
        "auth-key": authKey,
        "auth-token": authToken
      }
      client = ibmiotf.application.Client(options)
    except ibmiotf.ConnectionException  as e:
      ...
```

### Using a configuration file


If you are not using an options dict as shown above, you must include a configuration file that contains an options dict with the following code format:

```

    import ibmiotf.application
    try:
      options = ibmiotf.application.ParseConfigFile(configFilePath)
      client = ibmiotf.application.Client(options)
    except ibmiotf.ConnectionException  as e:
      ...
```
The application configuration file must also be in the following format:

```

    [application]
    org=$orgId
    id=$myApplication
    auth-method=apikey
    auth-key=$key
    auth-token=$token

```



## API calls
{: #api_calls}


Each method in the API client responds with either a valid JSON or boolean response in the case of success or IoTFCReSTException in the case of failure. The IoTFCReSTException contains the following properties, which an application can parse to get more information about the failure.

* httpcode - HTTP Status Code
* message - Exception message containing the reason for the failure
* response - JsonElement containing the partial response if any otherwise null

In the event of failure, the application needs to parse the response to see whether the action is partially successful or not.



## Subscribing to device events
{: #subscribe_device_events}

Events are the mechanism by which devices publish data to the {{site.data.keyword.iot_short_notm}} instance. The device controls the content of the event and assigns a name for each event that it sends.

When an event is received by the {{site.data.keyword.iot_short_notm}} instance, the credentials of the received event identify the sending device, making it impossible for a device to impersonate another device.





By default, applications subscribe to all events from all connected devices. Use the type, ID, event, and msgFormat parameters to control the scope of the subscription. A single client can support multiple subscriptions. The following code samples provide examples of how to subscribe to devices that are dependent on device type, ID, event, and msgFormat parameters.


### Subscribing to subscribe to all events from all devices


```

    import ibmiotf.application

    options = ibmiotf.application.ParseConfigFile(configFilePath)
    client = ibmiotf.application.Client(options)

    client.connect()
    client.subscribeToDeviceEvents()
```

### Subscribing to all events from all devices of a specific type


```

    import ibmiotf.application

    options = ibmiotf.application.ParseConfigFile(configFilePath)
    client = ibmiotf.application.Client(options)

    client.connect()
    client.subscribeToDeviceEvents(deviceType=myDeviceType)
```

### Subscribing to a specific event from all devices


```

    import ibmiotf.application

    options = ibmiotf.application.ParseConfigFile(configFilePath)
    client = ibmiotf.application.Client(options)

    client.connect()
    client.subscribeToDeviceEvents(event=myEvent)
```

### Subscribing to a specific event from two or more different devices


```

    import ibmiotf.application

    options = ibmiotf.application.ParseConfigFile(configFilePath)
    client = ibmiotf.application.Client(options)

    client.connect()
    client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, event=myEvent)
    client.subscribeToDeviceEvents(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId, event=myEvent)
```
### Subscribing to all events published by a device in JSON format


```

    import ibmiotf.application

    options = ibmiotf.application.ParseConfigFile(configFilePath)
    client = ibmiotf.application.Client(options)

    client.connect()
    client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, msgFormat="json")
```


## Handling events from devices
{: #handling_events_devices}

To process the events received by your subscriptions you need to register an event callback method. The messages are returned as an instance of the Event class:

* event.device - string (uniquely identifies the device across all types of devices in the organization)
* event.deviceType - string
* event.deviceId - string
* event.event - string
* event.format - string
* event.data - dict
* event.timestamp - datetime

```

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


```

    import ibmiotf.application

    options = ibmiotf.application.ParseConfigFile(configFilePath)
    client = ibmiotf.application.Client(options)

    client.connect()
    client.subscribeToDeviceStatus()
```

### Subscribing to status updates for all devices of a specific type


```

    import ibmiotf.application

    options = ibmiotf.application.ParseConfigFile(configFilePath)
    client = ibmiotf.application.Client(options)

    client.connect()
    client.subscribeToDeviceStatus(deviceType=myDeviceType)
```

### Subscribing to status updates for two different devices


```

    import ibmiotf.application

    options = ibmiotf.application.ParseConfigFile(configFilePath)
    client = ibmiotf.application.Client(options)

    client.connect()
    client.subscribeToDeviceStatus(deviceType=myDeviceType, deviceId=myDeviceId)
    client.subscribeToDeviceStatus(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId)
```


## Handling status updates from devices
{: #handling_device_updates}

To process the status updates received by your subscriptions you need to register an event callback method. The messages are returned as an instance of the Status class.

The following properties are set for both "Connect" and "Disconnect" status events:

* status.clientAddr - string
* status.protocol - string
* status.clientId - string
* status.user - string
* status.time - datetime
* status.action - string
* status.connectTime - datetime
* status.port - integer

The following properties are only set when the action is "Disconnect":

* status.writeMsg - integer
* status.readMsg - integer
* status.reason - string
* status.readBytes - integer
* status.writeBytes - integer

```

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

```

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

```

    import ibmiotf.application

    options = ibmiotf.application.ParseConfigFile(configFilePath)
    client = ibmiotf.application.Client(options)

    client.connect()
    commandData={'rebootDelay' : 50}
    client.publishCommand(myDeviceType, myDeviceId, "reboot", "json", myData)
```


## Organization details
{: #org_details}

Applications can use the ``getOrganizationDetails()`` method to retrieve the details about the configuration of the organization.

```

    import ibmiotf.application

    options = ibmiotf.application.ParseConfigFile(configFilePath)
    client = ibmiotf.application.Client(options)

    try:
        orgDetail = client.api.getOrganizationDetails()
    except IoTFCReSTException as e:
        print("ERROR [" + e.httpcode + "] " + e.message)
```

For information about the request & response model and the HTTP status code, refer to the Organization Configuration section of the [{{site.data.keyword.iot_short_notm}} API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html).


## Bulk device operations
{: #bulk_device_ops}

Applications can use bulk operations to get, add, or remove multiple devices simultaneously.

For information about the list of query parameters, the request & response model and http status code, see the Bulk Operations section of the [{{site.data.keyword.iot_short_notm}} API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Bulk_Operations/).


### Retrieving device information

Bulk device information can be retrieved using the ``getAllDevices()`` method. This method retrieves information on all registered devices in the organization. Each request can contain a maximum of 512KB.

The response contains parameters required by the application to retrieve the dictionary *results* from the response to get the array of devices returned. Other parameters in the response are required to make further calls, for example, the ``_bookmark`` element can be used to page through results. Issue the first request without specifying a bookmark, then take the bookmark returned in the response and provide it on the request for the next page. Repeat until the end of the result set indicated by the absence of a bookmark. Each request must use exactly the same values for the other parameters, otherwise the results are undefined.



```

    import ibmiotf.application

    options = ibmiotf.application.ParseConfigFile(configFilePath)
    client = ibmiotf.application.Client(options)

    try:
        deviceList = client.api.getAllDevices()
    except IoTFCReSTException as e:
        print("ERROR [" + e.httpcode + "] " + e.message)

```
### Adding multiple devices


The ``addMultipleDevices()`` method can be used to add one or more devices to your {{site.data.keyword.iot_short_notm}} organization. A request must be no larger than 512KB. The response contains the authentication tokens that were generated for each device. Ensure that you make a copy of the authentication tokens, as if you lose the authentication tokens, they cannot be retrieved.


```

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


The ``deleteMultipleDevices()`` method can be used to delete multiple devices from an {{site.data.keyword.iot_short_notm}}
organization. A request must be no larger than 512KB.

```

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

The device types that you create in your organization can be used to create templates for adding devices. Through the {{site.data.keyword.iot_short_notm}} API features, your applications can list, create, delete, view, or update device types in your organization.

For information about query parameters, the request & response model, and HTTP status codes, see the 'Device types' section of the [IBM {{site.data.keyword.iot_short_notm}} API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html) documentation.


### Retrieving all device types

You can use the ``getAllDeviceTypes()`` method to retrieve all of the device types that are in your {{site.data.keyword.iot_short_notm}} organization.
The response contains parameters required by the application to retrieve the dictionary *results* from the response to get the array of devices returned. Other parameters in the response are required to make further calls, for example, the ``_bookmark`` element can be used to page through results. Issue the first request without specifying a bookmark, then take the bookmark returned in the response and provide it on the request for the next page. Repeat this process until the end of the result set indicated by the absence of a bookmark. Each request must use exactly the same values for the other parameters, or the results will be undefined.



```

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


The ``addDeviceType()`` method can be used to register a device type to your {{site.data.keyword.iot_short_notm}} instance. In each request, you must first define the device information and the device metadata elements that you want to be applied to all devices of this type. The device information element is comprised of several variables, which include serial number, manufacturer, model, class, description, firmware, hardware versions, and descriptive location. The metadata element is comprised of custom variables and values, which can be defined by the user.


```

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


The ``deleteDeviceType()`` method can be used to delete a device type from your  {{site.data.keyword.iot_short_notm}} organization.

```

    import ibmiotf.application

    options = ibmiotf.application.ParseConfigFile(configFilePath)
    client = ibmiotf.application.Client(options)

    try:
        success = client.api.deleteDeviceType("myDeviceType")
    except IoTFCReSTException as e:
        print("ERROR [" + e.httpcode + "] " + e.message)
```

### Retrieving information for specific device types


Use the ``getDeviceType()`` method to retrieve information for a specific device type. The ``typeId`` of the device type that you want to retrieve must be specified.
as a parameter.

```

    import ibmiotf.application

    options = ibmiotf.application.ParseConfigFile(configFilePath)
    client = ibmiotf.application.Client(options)

    try:
        deviceTypeInfo = client.api.getDeviceType("myDeviceType")
    except IoTFCReSTException as e:
        print("ERROR [" + e.httpcode + "] " + e.message)
```

### Updating a device type


Use the ``updateDeviceType()`` method to modify the properties of a device type. When you use this method, you must first specify the ``typeId`` of the device type to be updated, and then specify the ``description``, ``deviceInfo``, and ``metadata`` elements.

```

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

Device operations made available through the API include listing, adding, removing, viewing, updating, viewing location, and viewing device management information of devices in a
 {{site.data.keyword.iot_short_notm}} organization.

For information about the query parameters, the request & response model, and the HTTP status code, see the 'Device section' of the [{{site.data.keyword.iot_short_notm}} API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html).


### Retrieving devices of a particular device type

The *retrieveDevices()* method can be used to retrieve all the devices of a particular device type in an organization in a {{site.data.keyword.iot_short_notm}} instance, as outlined in the following example:


```

     print("\nRetrieving All existing devices")
     print("Retrieved Devices = ", apiCli.retrieveDevices(deviceTypeId))
```

The response contains the parameters and application that needed to retrieve the dictionary *results* from the response to get the array of devices returned. Other parameters in the response are required to make further calls. For example, the *_bookmark* element can be used to page through results. Issue the first request without specifying a bookmark, then take the bookmark returned in the response and provide it on the request for the next page. Repeat until the end of the result set indicated by the absence of a bookmark. Each request must use exactly the same values for the other parameters, or the results are undefined.



In order to pass the *_bookmark* or any other condition, the overloaded method must be used. The overloaded method takes the parameters in the form of dictionary as shown in the following example:

```
    response = apiClient.retrieveDevices("iotsample-ardunio", parameters);
```

The previous code sample sorts the response based on device ID, and then uses the bookmark to page through the results.

### Adding a device


The *registerDevice()* method is used to add a device to a {{site.data.keyword.iot_short_notm}} organization. The *registerDevice()* method adds a single device to your {{site.data.keyword.iot_short_notm}} organization. The parameters that you can specify when you add a device are:

- deviceTypeId: *Optional*. Assigns a device type to the device. If there is a conflict between variables defined by the device type and variables defined by deviceInfo, the device specific variables will take precedence.
- deviceId: *Mandatory*.
- authToken: *Optional*. If no authentication token is supplied, one will be generated and included in the response.
- deviceInfo: *Optional*. This parameter is optional, and can contain a number of variables, including: serialNumber, manufacturer, model, deviceClass, description, firmware and hardware versions, and descriptiveLocation.
- metadata: *Optional*. Metadata can optionally be added in the form of custom field:value string pairs. An example is given in the next code sample on this page.
- location: *Optional*. This parameter contains the longitude, latitude, elevation, accuracy, and mesauredDateTime variables.

For more information on these parameters, and the response format and codes, see the [API documentation](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Devices/post_device_types_typeId_devices).

When using the *registerDevice()* method, you must define the mandatory deviceID parameter and any of the optional parameters that you require for your device, then call the method using the parameters you selected.

### Sample code for adding a device type


Insert the following code after the constructor code in a .py file. The sample demonstrates a method for adding a device type by defining the deviceId, authToken, metadata, deviceInfo, and location parameters.

```

    deviceId = "200020002000"
    authToken = "password"
    metadata = {"customField1": "customValue1", "customField2": "customValue2"}
    deviceInfo = {"serialNumber": "001", "manufacturer": "Blueberry", "model": "abc1", "deviceClass": "A", "descriptiveLocation" : "Bangalore", "fwVersion" : "1.0.1", "hwVersion" : "12.01"}
    location = {"longitude" : "12.78", "latitude" : "45.90", "elevation" : "2000", "accuracy" : "0", "measuredDateTime" : "2015-10-28T08:45:11.662Z"}

    apiCli.registerDevice(deviceTypeId, deviceId, metadata, deviceInfo, location)
```
### Deleting a device

Use the *deleteDevice()* method to remove a device from an organization on the {{site.data.keyword.iot_short_notm}} organization. When you delete a device using the *deleteDevice()* method, you must specify the deviceTypeId and deviceId parameters.

The following code sample outlines the format that is required for this method:

```
    apiCli.deleteDevice(deviceTypeId, deviceId)
```

### Getting a device

Use the *getDevice()* method to remove a device from an organization on the {{site.data.keyword.iot_short_notm}}. When you retrieve device details using the *getDevice()* method, you must specify the deviceTypeId and deviceId parameters

The following code sample provides an outline of the format required for this method.





```
	  apiCli.getDevice(deviceTypeId, deviceId)
```


### Retrieving all devices

Use the *getAllDevices()* method to retrieve all devices within an organization on the {{site.data.keyword.iot_short_notm}}.

```
	  apiCli.getAllDevices({'typeId' : deviceTypeId})
```

### Updating a service


Use the *updateDevice()* method to modify one or more properties of a device. Any property in the deviceInfo or metadata parameters can be updated. In order to update a device property, it must be defined above the method. The status parameter should contain "alert": True. The ``alert``property controls whether a device displays error codes in the {{site.data.keyword.iot_short_notm}} user interface. By default, the ``enabled`` property is set to true.

```
    status = { "alert": { "enabled": True }  }
    apiCli.updateDevice(deviceTypeId, deviceId, metadata2, deviceInfo, status)
```

### Sample code for updating ``deviceInfo`` properties


The following code sample identifies a specific device and then updates several properties under the deviceInfo parameter.

```

	  status = { "alert": { "enabled": True } }
	  deviceInfo = {descriptiveLocation: "London", hwVersion: "2.0.1", fwVersion: "2.5.1"}
    apiCli.updateDevice("MyDeviceType", "200020002000", deviceInfo, status)
```

### Retrieving location information


The *getDeviceLocation()* method can be used to retrieve the location information of a device. The parameters required for retrieving the location data are deviceTypeId and deviceId.

```

	  apiClient.getDeviceLocation("iotsample-ardunio", "ardunio01")
```  

The response to this method contains the longitude, latitude, elevation, accuracy, measuredTimeStamp, and updatedTimeStamp properties.

### Updating location information


Use the *updateDeviceLocation()* method to modify the location information for a device. Similarly to updating device properties, the deviceLocation parameter must be defined with the changes you wish to apply. The code sample below demonstrates changing the location data for a given device.

```

    deviceLocation = { "longitude": 0, "latitude": 0, "elevation": 0, "accuracy": 0, "measuredDateTime": "2015-10-28T08:45:11.673Z"}
    apiCli.updateDeviceLocation(deviceTypeId, deviceId, deviceLocation)
```

If a date is not supplied, the current date and time is used.


### Get management information


Use the *getDeviceManagementInformation()* method to get the device management information for a device. The response contains the last activity date-time, the device's dormant status (true/false), support for device and firmware actions, and firmware data. For a comprehensive list of response content, see the relevant API documentation.

The following code sample will return the device management information for a device with the deviceId "00aabbccde03", with deviceTypeId "iotsample-arduino".


```
    apiCli.getDeviceManagementInformation("iotsample-arduino", "00aabbccde03")
```

## Device diagnostic operations
{: #device_diag_ops}

Applications can use device diagnostic operations to clear logs, retrieve all or specific logs for a device, add log information, delete logs, clear error codes, get device error codes, and add an error codes.

For more detailed information on query and response models, response codes, and query parameters, see the {{site.data.keyword.iot_short_notm}} API documentation.

### Get diagnostic logs


Use the *getAllDiagnosticLogs()* method to retrieve all diagnostic logs for a specific device. The *getAllDiagnosticLogs()* method requires the deviceTypeId and deviceId parameters.

```

    apiCli.getAllDiagnosticLogs(deviceTypeId, deviceId)
```

The response model for this method contains the logId, message, severity, data, and timestamp.

### Clearing diagnostic logs for a device


Use the *clearAllDiagnosticLogs()* method to delete all diagnostic logs for a specific device. The required parameters are deviceTypeId and deviceId. Be careful when deleting log files, as they cannot be recovered after they are deleted.

```

    apiCli.clearAllDiagnosticLogs(deviceTypeId, deviceId)
```

### Adding a diagnostic log


Use the *addDiagnosticLog()* method to add an entry in the diagnostic log of the device. The log can be pruned as the new entry is added. If no date is supplied, the current date and time are added to the entry. To use this method, you need to define a 'logs' parameter with the following variables:

- message: This variable is mandatory, and contains the new diagnostic message.
- severity: This variable is optional. If used, the value corresponds to the severity of the diagnostic log, and should be 0, 1, or 2, corresponding to the informational, warning, and error categories.
- data: This variable is optional, and contains diagnostic data.
- timestamp: This variable is optional, and contains the date and time of the log entry in ISO8601 format. If this variable is not included, the current date and time are used.

The other parameters that are required in the method are the deviceTypeId and deviceId values for the device.

The following code sample contains an example of the *addDiagnosticLog()* method.

```
    logs = { "message": "MessageContent", "severity": 0, "data": "LogData"}
    apiCli.addDiagnosticLog(deviceTypeId, deviceId, logs)
```

### Retrieving a specific diagnostic log


Use the  *getDiagnosticLog()* method to retrieve a specific diagnostic log for a specified device based on the log ID. The required parameters for this method are deviceTypeId, deviceId, and logId.

```
    apiCli.getDiagnosticLog(deviceTypeId, deviceId, logId)
```

### Deleting a diagnostic log


Use the *deleteDiagnosticLog()* method to delete a specific diagnostic log. In order to specify a diagnostic log, the deviceTypeId, deviceId, and logID parameters must be supplied.

```

	  apiCli.deleteDiagnosticLog(deviceTypeId, deviceId, logId)
```

### Retrieving device error codes


Use the *getAllDiagnosticErrorCodes()* method to retrieve all diagnostic error codes that are associated with a specific device.

```

	  apiCli.getAllDiagnosticErrorCodes(deviceTypeId, deviceId)
```

### Clear diagnostic error codes


Use the *clearAllErrorCodes()* method to clear the list of error codes that are associated with the device. The list is replaced with a single error code of zero.

```

    apiCli.clearAllErrorCodes(deviceTypeId, deviceId)
```

### Adding a single diagnostic error code


The *addErrorCode()* method is used to add an error code to the list of error codes associated with the device. The list can be pruned as the new entry is added. The parameters required in the method are deviceTypeId, deviceId, and errorCode. The errorCode parameter contains the following variables:

- errorCode: This variable is mandatory and should be set as an integer. This sets the number of the error code to be created.
- timestamp: This variable is optional, and contains the date and time of the log entry in ISO8601 format. If this variable is not included, it is automatically added with the current date and time.

```

    errorCode = { "errorCode": 1234, "timestamp": "2015-10-29T05:43:57.112Z" }
    apiCli.addErrorCode(deviceTypeId, deviceId, errorCode)
```

## Connection problem determination
{: #connection_problem_determination}

Use the *getDeviceConnectionLogs()* method to list connection log events for a device. Connection log events can be used to help diagnose connectivity problems between the device and the {{site.data.keyword.iot_short_notm}} service. The entries record successful connection, unsuccessful connection attempts, intentional disconnection and server-initiated disconnection events.

```

	  apiCli.getDeviceConnectionLogs(deviceTypeId, deviceId)
```

The response includes a list of log entries, which contain log messages and time stamps.



## Historical event retrieval
{: #historical_event_retrieval}

The historical event retrieval operations that are described in this section can be used to view events from all devices, view events from a device type, or to view events for a specific device.

For information about the query parameters, the request & response model and HTTP status code, see the Historical event retrieval section of the [{{site.data.keyword.iot_short_notm}} API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html).


### Viewing events from all devices

Use the *getHistoricalEvents()* method to view events across all devices registered to the organization.

```

    print("Historical Events = ", apiCli.getHistoricalEvents())
```

The response of the *getHistoricalEvents()* method contains some parameters and the application needs to retrieve the JSON element *events* from the response to get the array of events returned. Other parameters in the response are required to make further call, for example, the *_bookmark* element can be used to page through results. Issue the first request without specifying a bookmark, then take the bookmark returned in the response and provide it on the request for the next page. Repeat until the end of the result set indicated by the absence of a bookmark. Each request must use exactly the same values for the other parameters, otherwise the results are undefined.

In order to pass the *_bookmark* or any other condition, the overloaded method must be used. The overloaded method takes the parameters in the form of dictionary as outlined in the following code sample:

```

    startTime = math.floor(time.mktime((2013, 10, 10, 17, 3, 38, 0, 0, 0)) * 1000)
    endTime =  math.floor(time.mktime((2015, 10, 29, 17, 3, 38, 0, 0, 0)) * 1000)
    duration = {'start' : startTime, 'end' : endTime }
    apiCli.getHistoricalEvents(options = duration))
```
The previous code sample returns the events between the start and end time.

### Viewing events from a device type


Use the *getHistoricalEvents()* method to view events from all the devices of a particular device type.

```

	  apiCli.getHistoricalEvents(deviceType = 'iotsample-arduino', options = duration)
```

The response will contain some parameters and the application needs to retrieve the JSON element *events* from the response to get the array of events returned. As mentioned in the *view events from all devices* section, the overloaded method can be used to control the output.


### Viewing events from a device


Use the *getHistoricalEvents()* method to view events from a specific device. DeviceTypeId and deviceId parameters are required in order to use this method.

```

    apiCli.getHistoricalEvents(deviceType, deviceId, options = duration)
```

The response of the the *getHistoricalEvents()* method contains more parameters, and the application needs to retrieve the JSON element *events* from the response to get the array of events returned.
