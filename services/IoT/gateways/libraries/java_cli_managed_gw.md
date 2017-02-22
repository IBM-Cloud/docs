---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-12-06"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Developing managed gateways by using Java
{: #java_cli_managed_gw}

Gateways play an important role in the management of the devices that are connected to them. Many devices are very basic and have no device management capabilities, so these basic devices need to be managed from a gateway. In {{site.data.keyword.iot_full}}, a managed gateway is a gateway that can manage the devices that are connected to it and provide device management capabilities, such as firmware, location, and diagnostic updates.
{:shortdesc}

By using the {{site.data.keyword.iot_short}} Java™ client library and the information that is provided, you can develop Java code to turn your gateway into a managed gateway. Samples are also provided to help you develop Java code to connect a gateway to the Device Management service and run device management operations.

## Device Management service
{: #dm_service}

The {{site.data.keyword.iot_short}} Device Management (DM) service provides device management capabilities for gateways to manage the devices that are connected to them.

A managed gateway runs a device management agent, which runs as a proxy for all devices that connect to {{site.data.keyword.iot_short}} through the gateway.

### Device management agent

Devices that connect to {{site.data.keyword.iot_short}} indirectly through a gateway can use various connection protocols, if they are supported by the gateway device.

The `ManagedGateway` instance is a device management agent that provides a list of methods to perform one or more device management actions, for example, participating in device management activity, updating error codes, logs, location and firmware or device actions.

The device management agent on the gateway converts and processes the connection protocol of the connecting devices, which ensure that the device can be managed by {{site.data.keyword.iot_short}}. Through the device management agent, the gateway becomes more than a transparent tunnel between the attached device and {{site.data.keyword.iot_short}}. For example, if a device that is connected to a gateway is unable to download firmware, the device management agent on the gateway can do the following actions:
- Intercept a request for a device to download firmware
- Download the firmware for the device
- Store the device firmware on the gateway

At a later point in time, when the device is instructed to do the upgrade, the device management agent on the gateway can push the firmware to the device and update it.

## Creating the device model
{: #create_device_model}

In {{site.data.keyword.iot_short}}, the device model describes the metadata and management characteristics of devices and gateways. The device database is the master source of device or gateway information. Applications and managed devices can send location updates, firmware upgrade progess updates, and other types of updates. When updates are received by {{site.data.keyword.iot_short}}, the device database is updated so that the information is available to connecting applications.

In the {{site.data.keyword.iot_short}} Java client library, the device model is represented by the `DeviceData` Java class.

To create the `DeviceData` class, create the following objects:

- `DeviceInfo` (Optional)
- `DeviceLocation` (Optional, required only if the device wants to be notified about the location that is set by the application through the {{site.data.keyword.iot_short}} API)
- `DeviceFirmware` (Optional)
- `DeviceMetadata` (optional)

For more information, see [device model](../../reference/device_model.html).

### DeviceInfo

The following code snippet that contains sample data shows how to create the `DeviceInfo` and `DeviceMetadata` objects:

```java
DeviceInfo deviceInfo = new DeviceInfo.Builder().
                           serialNumber("10087").
                           manufacturer("IBM").
                           model("7865").
                           deviceClass("A").
                           description("My RasPi Device").
                           fwVersion("1.0.0").
                           hwVersion("1.0").
                           descriptiveLocation("EGL C").
                           build();

/**
  * Create a DeviceMetadata object
 **/
JsonObject data = new JsonObject();
data.addProperty("customField", "customValue");
DeviceMetadata metadata = new DeviceMetadata(data);

```

The following code snippet outlines how to create the `DeviceData` class by using the `DeviceInfo` and `DeviceMetadata` objects that were created in the previous sample:

```java
DeviceData deviceData = new DeviceData.Builder().
                         deviceInfo(deviceInfo).
                         metadata(metadata).
                         build();
```

Every gateway and every attached device must have its own `DeviceData` class definition to represent itself in {{site.data.keyword.iot_short}}. For gateways, the `DeviceData` class is passed to the library as part of constructing the `ManagedGateway` instance. For attached devices, the `DeviceData` class is passed to the library as part of the `sendDeviceManageRequest()` object.

## ManagedGateway constructors
{: #construct_managed_gateway}

`ManagedGateway` is a Java class that connects a gateway to {{site.data.keyword.iot_short}} as a managed gateway that can do at least one device management operation either for itself or for the attached devices. A `ManagedGateway` instance can also be used to do normal gateway operations, such as publishing gateway events, attaching device events, and listening for commands from applications. The `ManagedGateway` instance is a device management agent.

In the `ManagedGateway` class, two different constructors, Constructor One and Constructor Two, support different user patterns.

### Constructor One

Constructor One constructs a `ManagedGateway` instance by accepting a `DeviceData` class that contains all of the following properties:

| Property     |Description     |
|----------------|----------------|
|`Organization-ID` |Your organization ID.|
|`Gateway-Type` |The type of your gateway device.|
|`Gateway-ID` |The ID of the gateway device.|
|`Authentication-Method`|The method of authentication. The only method that is supported is "token".|
|`Authentication-Token`|The API key token.|
|`auth-key`   |An optional API key, which you must specify when you set the value of auth-method to `apikey`.|
|`auth-token`   |An API key token, which is also required when you set the value of auth-method to `apikey`. |
|`clean-session`|A true or false value that is required only if you want to connect the gateway in durable subscription mode. By default, `clean-session` is set to `true`.|
|`Port`|The port number to connect to. Specify either 8883 or 443. If you do not specify a port number, the client connects to {{site.data.keyword.iot_short_notm}} on port number 8883 by default.|
|`WebSocket`|A true or false value that is required only if you want to connect the gateway by using websockets.|
|`MaxInflightMessages`  |Sets the maximum number of in-flight messages for the connection. The default value is 100.|
|`Automatic-Reconnect`  |A true or false value that is required when you want to automatically reconnect the device to {{site.data.keyword.iot_short_notm}} while it is in a disconnected state. The default value is false.|
|`Disconnected-Buffer-Size`|The maximum number of messages that can be stored in memory while the client is disconnected. The default value is 5000.|

**Note:** To connect the gateway in durable subscription mode, set `clean-session` to `false`. For more information about the `clean-session` property, see the 'Subscription Buffers and Clean Session' section of the [MQTT documentation](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

The following code outlines how to create a `ManagedGateway` instance:

```java
Properties options = new Properties();
options.setProperty("Organization-ID", "uguhsp");
options.setProperty("Gateway-Type", "iotsample-arduino");
options.setProperty("Gateway-ID", "00aabbccde03");
options.setProperty("Authentication-Method", "token");
options.setProperty("Authentication-Token", "AUTH TOKEN FOR DEVICE");

ManagedGateway ManagedGateway = new ManagedGateway(options, deviceData);
```

### Constructor Two

Constructor Two constructs a `ManagedGateway` instance by accepting a `DeviceData` object and the MQTT client instance. Constructor Two also requires that the `DeviceData` object in the instance includes the device type and the device ID, as outlined in the following code sample:

```java
// Code that constructs either a synchronous or asynchronous MQTT client instance of mqttClient.
.....

// Code that constructs the DeviceData object
DeviceData deviceData = new DeviceData.Builder().
                         typeId("Gateway-Type").
                         deviceId("Gateway-ID").
                         deviceInfo(deviceInfo).
                         metadata(metadata).
                         build();

....
ManagedGateway ManagedGateway = new ManagedGateway(mqttClient, deviceData);

```

**Note:**  If you are developing for custom devices, use Constructor Two, because this constructor creates a managed gateway instance by using the existing connected MQTT client instance so that you can leverage device management operations. Use the Java client library for all of the device functions.

## Device management requests from a gateway
{: #dm_requests}

### Sending a manage request from a gateway

To instruct a gateway to participate in device management activities, invoke the `sendGatewayManageRequest()` method, which is outlined in the following code sample:

```java
managedGateway.sendGatewayManageRequest(0, true, true);
```
The manage request initiates a connect request internally if the device is not connected to {{site.data.keyword.iot_short}} already.

The `sendGatewayManageRequest()` method accepts following parameters:

| Parameter     |Description     |
|----------------|----------------|
|`lifetime`|The length of time in seconds within which the gateway must send another manage device type request to avoid being classified as dormant and becoming an unmanaged device. If the `lifetime` field is omitted or set to 0, the managed gateway does not become dormant. The minimum supported setting for the `lifetime` field is 3600 seconds (1 hour).|
|`supportFirmwareActions`|A true or false value that determines whether the gateway supports firmware actions. The gateway must also add a firmware handler to handle the firmware requests.|
|`supportDeviceActions`|A true or false value that determines whether the gateway supports device actions. The gateway must also add a device action handler to handle the reboot and factory reset requests.|


The `ManagedGateway` instance is a device management agent that provides a list of methods to perform one or more device management actions, for example, participating in device management activity, updating error codes, logs, location and firmware or device actions.

### Sending a manage request from attached devices

To allow devices that are connected behind a gateway to participate in device management activities on the gateway, invoke the `sendDeviceManageRequest()` method.

The `sendDeviceManageRequest()` method accepts the details of the attached devices and the `lifetime`, `supportFirmwareActions`, and `supportDeviceActions` parameters. A gateway can also use the overloaded `sendDeviceManageRequest()` method to define the `DeviceData` object for the attached device.

#### Example of sending a manage request from attached devices

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, lifetime, true, true);
```

### Sending an unmanage request from a gateway

When a gateway no longer needs to be managed, to stop device management activities on the gateway, invoke the `sendGatewayUnmanageRequet()` method.  When `sendGatewayUnmanageRequet()` is invoked, {{site.data.keyword.iot_short}} no longer sends any new device management requests for the gateway, and all of the device management requests from the gateway are rejected, except for **Manage** requests. Requests from devices that are behind the gateway are not rejected.

#### Example of sending an unmanage request from a gateway

```java
managedGateway.sendGatewayUnmanageRequet();
```

### Sending an unmanage request from attached devices

When a device that is behind a gateway no longer needs to be managed, to move an attached device from a managed state to an unmanaged state, the gateway can invoke the `sendDeviceUnmanageRequet()` method. When `sendDeviceUnmanageRequet()` is invoked, {{site.data.keyword.iot_short}} no longer sends new device management requests for the device, and all of device management requests from the gateway that are for the attached device are rejected, except for **Manage** requests.

#### Example of sending an unmanage request from attached devices

```java
managedGateway.sendDeviceUnmanageRequet();
```

## Location updates
{: #location_updates}

### Sending gateway location updates

Gateways that can determine their location can choose to notify {{site.data.keyword.iot_short}} about location changes. The gateway can invoke one of the overloaded `updateLocation()` methods to update the location of the device.

```java
    // update the location with latitude, longitude, and elevation.
int rc = managedGateway.updateGatewayLocation(30.28565, -97.73921, 10);
if(rc == 200) {
    System.out.println("Location updated successfully!");
} else {
System.err.println("Failed to update the location!");
    }
```

### Sending attached device location updates

The gateway can invoke the corresponding `updateDeviceLocation()` device method to update the location of the attached devices. The overloaded method can be used to specify the `measuredDateTime` method.  

```java
// update the location of the attached device with latitude, longitude, and elevation
int rc = managedGateway.updateDeviceLocation(typeId, deviceId, 30.28565, -97.73921, 10);
```
For more information about location updates, see [Device management requests](../../devices/device_mgmt/index.html#/update-location#update-location).

## Error code handling
{: #errors}

### Creating and deleting gateway error codes

A gateway can choose to notify {{site.data.keyword.iot_short}} about changes to its error status. The gateway can invoke the `addErrorCode()` method to add the current error code to {{site.data.keyword.iot_short}}.

```java
int rc = managedGateway.addGatewayErrorCode(300);
```

Error codes for a gateway can be cleared from {{site.data.keyword.iot_short}} by calling the `clearErrorCodes()` method, as shown:

```java
int rc = managedGateway.clearGatewayErrorCodes();
```

### Creating and deleting error codes for attached devices

A gateway can also invoke the corresponding device method to add or clear error codes for the attached devices:

```java
int rc = managedGateway.addDeviceErrorCode(typeId, deviceId, 300);
rc = managedGateway.clearDeviceErrorCodes(typeId, deviceId);
```

### Creating and deleting gateway log messages

A gateway can choose to notify {{site.data.keyword.iot_short}} about changes by adding a new log entry. A log entry includes the following items:

- Message string
- Time stamp
- Severity
- Optionally, base64-encoded binary diagnostic data

Gateways can invoke the `addGatewayLog()` method to send log messages, which is outlined in the following sample:

```java
// An example Log event
String message = "Firmware Download Progress (%): " + 50;
Date timestamp = new Date();
LogSeverity severity = LogSeverity.informational;
int rc = managedGateway.addGatewayLog(message, timestamp, severity);
```

Log messages can be cleared from {{site.data.keyword.iot_short}} by calling the `clearLogs()` method:

```java
rc = managedGateway.clearGatewayLogs();
```

### Creating and deleting logs for attached devices

Similarly, the gateway can invoke the corresponding device method to create or clear the logs for the attached devices, which is outlined in the following code sample:

```java

// An example log event:
String message = "Firmware Download Progress (%): " + 50;
Date timestamp = new Date();
LogSeverity severity = LogSeverity.informational;
int rc = managedGateway.addDeviceLog(typeId, deviceId, message, timestamp, severity);
```

To clear the logs of attached devices, invoke the `clearDeviceLogs()` method by specifying the details of the attached device, which is outlined in the following code sample:

```java
int rc = managedGateway.clearDeviceLogs(typeId, deviceId);
```

The device diagnostics operations are intended to provide information about gateway or device errors. They do not provide diagnostic information about a devices connection to {{site.data.keyword.iot_short}}.

For more information about the diagnostics operation, see [Device management requests](../../devices/device_mgmt/index.html#/update-location#update-location).

## Firmware updates and actions
{: #firmware}

The firmware update process is separated into two distinct actions:

- Downloading firmware
- Updating firmware

The gateway must do the following activities to support firmware actions for both itself and for its attached devices:

1. Optional: Construct a `DeviceFirmware` object.
2. Inform the server about the firmware action support.
3. Create the firmware action handler.
4. Add the handler to `ManagedGateway`.

### Step 1: Constructing a `DeviceFirmware` Object

To do firmware actions, a gateway can optionally construct a `DeviceFirmware` object for itself and for its attached devices and then add it to the `DeviceData` object, which is outlined in the following sample:

```java
DeviceFirmware firmware = new DeviceFirmware.Builder().
			version("Firmware.version").
			name("Firmware.name").
			url("Firmware.url").
			verifier("Firmware.verifier").
			state(FirmwareState.IDLE).				
			build();

DeviceData deviceData = new DeviceData.Builder().
			deviceInfo(deviceInfo).
			deviceFirmware(firmware).
			metadata(metadata).
			build();

ManagedGateway ManagedGateway = new ManagedGateway(options, deviceData);
managedGateway.connect();
```

For attached devices, the constructed `DeviceData` object can be passed to the library while sending the manage request, as outlined in the following code sample:

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, deviceData, lifetime, supportFirmwareActions, supportDeviceActions);
```

The `DeviceFirmware` object represents the current firmware of the gateway or attached device and is used to report the status of the firmware download and firmware update actions to {{site.data.keyword.iot_short}}. If the `DeviceFirmware` object is not constructed by the gateway, the library creates an empty object and reports the status to {{site.data.keyword.iot_short}}.

### Step 2: Informing the server about the firmware action support

The gateway or its attached devices need to set the firmware action flag to true in order for the server to initiate the firmware request. This change can be achieved by passing a true value for the `supportFirmwareActions` parameter in the manage request.

The gateway can invoke the following method to inform the server about its firmware support:
```java
managedGateway.sendGatewayManageRequest(3600, true, false);
```

Similarly, the gateway can invoke the corresponding device method to inform the firmware support of attached devices:

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, deviceData, 3600, true, false);
```

When the support is informed to the device management server, the server then forwards the firmware actions to the gateway for either the gateway itself or the devices that are behind it.

### Step 3: Creating the firmware action handler

To support the firmware action, the gateway needs to create a handler and add it to `managedGateway`. The handler must extend a `DeviceFirmwareHandler` class and implement the following methods:

```java
public abstract void downloadFirmware(DeviceFirmware deviceFirmware);
public abstract void updateFirmware(DeviceFirmware deviceFirmware);
```

**Note**: There must be only one handler added to the library for both the gateway and attached devices where the firmware download or update requests are redirected. The implementation must create a thread or a pool of threads to handle multiple firmware requests at the same time.

You can find a sample implementation of a threadpool handler in the [Gateway samples GutHub repository](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java).

### A sample implementation of `downloadFirmware`

The implementation must add logic to download the firmware and report the status of the download by using the `DeviceFirmware` object. If the firmware download operation is successful, then the state of the firmware must be set to 'DOWNLOADED' and the `UpdateStatus` property must be set to 'SUCCESS'.

If an error occurs during a firmware download, the state must be set to 'IDLE', and the `updateStatus` property must be set to one of the following error status values:

- OUT_OF_MEMORY
- CONNECTION_LOST
- INVALID_URI

A sample firmware download implementation is shown in the following code sample:

**Important:** The code sample that is provided does not include the thread pool section. For the complete implementation of the firmware handler, a sample is available in the [IBM Java gateway samples GitHub repository ](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java).

```java
public void downloadFirmware(DeviceFirmware deviceFirmware) {
	boolean success = false;
	URL firmwareURL = null;
	URLConnection urlConnection = null;

	try {
		firmwareURL = new URL(deviceFirmware.getUrl());
		urlConnection = firmwareURL.openConnection();
		if(deviceFirmware.getName() != null) {
			downloadedFirmwareName = deviceFirmware.getName();
		} else {
			// use the time stamp as the name
			downloadedFirmwareName = "firmware_" +new Date().getTime()+".deb";
		}

		File file = new File(downloadedFirmwareName);
		BufferedInputStream bis = new BufferedInputStream(urlConnection.getInputStream());
		BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(file.getName()));

		int data = bis.read();
		if(data != -1) {
			bos.write(data);
			byte[] block = new byte[1024];
			while (true) {
				int len = bis.read(block, 0, block.length);
				if(len != -1) {
					bos.write(block, 0, len);
				} else {
					break;
				}
			}
			bos.close();
			bis.close();
			success = true;
		} else {
			//There is no data to read, so set an error
			deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.INVALID_URI);
		}
	} catch(MalformedURLException me) {
		// Invalid URL, so set the status to reflect the same,
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.INVALID_URI);
	} catch (IOException e) {
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.CONNECTION_LOST);
	} catch (OutOfMemoryError oom) {
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.OUT_OF_MEMORY);
	}

		if(success == true) {
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.SUCCESS);
		deviceFirmware.setState(FirmwareState.DOWNLOADED);
	} else {
		deviceFirmware.setState(FirmwareState.IDLE);
	}
}
```

A managed gateway can check the integrity of the downloaded firmware image by using the verifier and then report the status back to {{site.data.keyword.iot_short}}. The verifier can be set by the gateway during the following stages:

- During startup when the 'DeviceFirmware' object is created
- When an application submits a 'downloadFirmware' request

#### Example

```java
private boolean verifyFirmware(File file, String verifier) throws IOException {
	FileInputStream fis = null;
	String md5 = null;
	try {
		fis = new FileInputStream(file);
		md5 = org.apache.commons.codec.digest.DigestUtils.md5Hex(fis);
		System.out.println("Downloaded Firmware MD5 sum:: "+ md5);
	} catch (FileNotFoundException e) {
		e.printStackTrace();
	} catch (IOException e) {
		e.printStackTrace();
	} finally {
		fis.close();
	}
	if(verifier.equals(md5)) {
		System.out.println("Firmware verification successful");
		return true;
	}
	System.out.println("Download firmware checksum verification failed."
			+ "Expected "+verifier + " found "+md5);
	return false;
}
```

The complete code can be found in the gateway management sample [GatewayFirmwareHandlerSample](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java).

### A sample implementation of `updateFirmware`

The implementation must create a separate thread and add logic to install the downloaded firmware and report the status of the update by using the `DeviceFirmware` object. If the firmware update operation is successful, then the state of the firmware must be set to 'IDLE', and the `updateStatus` value must be set to 'SUCCESS'.

If an error occurs during a firmware update, the `updateStatus` value must be set to one of the following error status values:

* OUT_OF_MEMORY
* UNSUPPORTED_IMAGE

The following code sample outlines how you can implement a firmware update for a Raspberry Pi device:

```java
public void updateFirmware(DeviceFirmware deviceFirmware) {
	try {
		ProcessBuilder pkgInstaller = null;
		Process p = null;
		pkgInstaller = new ProcessBuilder("sudo", "dpkg", "-i", downloadedFirmwareName);
		boolean success = false;
		try {
			p = pkgInstaller.start();
			boolean status = waitForCompletion(p, 5);
			if(status == false) {
				p.destroy();
				deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
				return;
			}
			System.out.println("Firmware Update command "+status);
			deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.SUCCESS);
			deviceFirmware.setState(FirmwareState.IDLE);
		} catch (IOException e) {
			e.printStackTrace();
			deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
		} catch (InterruptedException e) {
			e.printStackTrace();
			deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
		}
	} catch (OutOfMemoryError oom) {
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.OUT_OF_MEMORY);
	}
}
```

The complete code can be found in the `GatewayFirmwareHandlerSample` sample that is in the [Gateway samples GitHub repository](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java).

### Step 4: Adding the handler to `ManagedGateway`

When a handler is created, it must be added to the `ManagedGateway` instance so that the Java client library invokes the corresponding method when there is a firmware action request from {{site.data.keyword.iot_short}}.

```java
GatewayFirmwareHandlerSample fwHandler = new GatewayFirmwareHandlerSample();
mgdGateway.addFirmwareHandler(fwHandler);
```

For more information about firmware actions, see [Device management requests](https://docs.internetofthings.ibmcloud.com/devices/device_mgmt/requests.html#/firmware-actions#firmware-actions).

## Device Actions
{: #dev_actions}

{{site.data.keyword.iot_short}} supports the following device actions:

- Reboot
- Factory reset

The gateway must do the following activities to support device actions for itself and also for the devices that are behind it.

1. Inform the server about the device actions support.
2. Create the device action handler.
3. Add the handler to `ManagedGateway`.

### Step 1: Informing the server about the device actions support

To do a reboot or a factory reset action for a gateway and its attached devices, the gateway must first inform {{site.data.keyword.iot_short}} about the support. This action can be done by passing a true value for the `supportDeviceActions` parameter when sending the **Manage** request.

A gateway can invoke the following method to inform the server about its device action support:

```java
// Last parameter represents the device action support
managedGateway.sendGatewayManageRequest(3600, true, true);
```

A gateway can invoke the corresponding device method to inform the device action support of attached devices:

```java
// Last parameter represents the device action support
managedGateway.sendDeviceManageRequest(typeId, deviceId, 0, true, true);
```

When the support is informed to the device management server, the server then forwards the device action requests to the device.

### Step 2: Creating the device action handler

To support the device action, the gateway needs to create a handler and add it to `managedGateway` instance. The handler must extend a `DeviceActionHandler` class and provide implementation for the following methods:

```java
public abstract void handleReboot(DeviceAction action);
public abstract void handleFactoryReset(DeviceAction action);
```

**Note:** There must be only one handler added to the library for both the gateway and attached devices where the device action requests are redirected. The implementation must create a thread or a pool of threads to handle multiple device action requests at the same time. A sample handler implementation that uses a threadpool is demonstrated in the [iot-gateway-samples GitHub repository](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayActionHandlerSample.java).

### A sample implementation of `handleReboot`

The implementation must create a separate thread and add logic to reboot the gateway and attached device and report the status of the reboot by using a `DeviceAction` object. After receiving the request, the gateway must first inform the server about the support or failure before proceeding with the actual reboot. If the sample can't reboot the device or any other error occurs during the reboot, the gateway can update the status in an optional message. A sample reboot implementation for a Raspberry Pi device is provided in the following code sample:

```java
public void handleReboot(DeviceAction action) {
	ProcessBuilder processBuilder = null;
	Process p = null;
	processBuilder = new ProcessBuilder("sudo", "shutdown", "-r", "now");
	boolean status = false;
	try {
		p = processBuilder.start();
		// wait for say 2 minutes before giving it up
		status = waitForCompletion(p, 2);
	} catch (IOException e) {
		action.setMessage(e.getMessage());
	} catch (InterruptedException e) {
		action.setMessage(e.getMessage());
	}
	if(status == false) {
		action.setStatus(DeviceAction.Status.FAILED);
	}
}
```

The complete sampler handler implementation that uses a threadpool is demonstrated in the [iot-gateway-samples GitHub repository](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayActionHandlerSample.java).


### A sample implementation of `handleFactoryReset`

The implementation must create a separate thread and add logic to reset the gateway and attached device to factory settings and report the status of the reset by using the DeviceAction object. When the request is receieved, the gateway first needs to inform the server about the support or failure before proceeding with the actual reset. The basic outline of the factory reset implementation is shown in the following code sample:

```java
public void handleFactoryReset(DeviceAction action) {
	try {
		// code to perform Factory reset
	} catch (IOException e) {
		action.setMessage(e.getMessage());
	}
	if(status == false) {
		action.setStatus(DeviceAction.Status.FAILED);
	}
}
```

### Step 3: Adding the handler to `ManagedGateway`

When a handler is created, it must be added to the `ManagedGateway` instance so that the Java Client library invokes the corresponding method when there is a device action request from {{site.data.keyword.iot_short}} for the gateway or attached devices.

```java
GatewayActionHandlerSample actionHandler = new GatewayActionHandlerSample();
mgdGateway.addDeviceActionHandler(actionHandler);
```

For more information about device actions, see [Device management requests](../../devices/device_mgmt/requests.html#/device-actions-reboot#device-actions-reboot).

## Listening for device attribute changes
{: #listen_device_attributes}

The Java client library updates the corresponding objects whenever there is an update request from {{site.data.keyword.iot_short}}. These update requests are initiated by the application either directly or indirectly through a firmware update by using the {{site.data.keyword.iot_short}} REST API. Apart from updating these attributes, the library provides a mechanism whereby the gateway can be notified whenever a device attribute is updated.

Attributes that can be updated by this type of operation are location, metadata, device information, and firmware of the gateway or attached devices.

To be notified about attribute changes, the gateway must add a property change listener to the objects that it is interested in, which is outlined in the following code sample:

```java
deviceLocation.addPropertyChangeListener(listener);
firmware.addPropertyChangeListener(listener);
deviceInfo.addPropertyChangeListener(listener);
metadata.addPropertyChangeListener(listener);
```

The gateway must also implement the `propertyChange()` method where it receives the notification, which is outlined in the following sample implementation:

```java
public void propertyChange(PropertyChangeEvent evt) {
	if(evt.getNewValue() == null) {
		return;
	}
	Object value = (Object) evt.getNewValue();
		switch(evt.getPropertyName()) {
		case "metadata":
			DeviceMetadata metadata = (DeviceMetadata) value;
			System.out.println("Received an updated metadata -- "+ metadata);
			break;

			case "location":
			DeviceLocation location = (DeviceLocation) value;
			System.out.println("Received an updated location -- "+ location);
			break;

			case "deviceInfo":
			DeviceInfo info = (DeviceInfo) value;
			System.out.println("Received an updated device info -- "+ info);
			break;

			case "mgmt.firmware":
			DeviceFirmware firmware = (DeviceFirmware) value;
			System.out.println("Received an updated device firmware -- "+ firmware);
			break;		
	}
}
```

For more information about updating the device attributes, see [Device management requests](https://docs.internetofthings.ibmcloud.com/devices/device_mgmt/index.html#/update-device-attributes#update-device-attributes).

## Samples
{: #samples}

Several samples are available to help you connect gateways and devices that are behind gateways to your {{site.data.keyword.iot_short_notm}} instance. The samples use the {{site.data.keyword.iot_short_notm}} Java client library and are located in the [Gateway Samples GitHub repository](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples).

## Recipes
{: #recipes}

For a recipe that shows you how to connect a Rasberry Pi device as a managed gateway to {{site.data.keyword.iot_short_notm}} and manage the attached devices, see [Raspberry Pi as a managed gateway in {{site.data.keyword.iot_short_notm}} ](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/).

The recipe explains how you can use the Device Management protocol of {{site.data.keyword.iot_short_notm}} to manage an Arduino Uno device from a Raspberry Pi device that acts as a gateway and do device management operations, such as rebooting the device or adding a sketch program.
