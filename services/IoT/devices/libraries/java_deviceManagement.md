---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Java client library - managed devices
{: #java_deviceManagement}

##Introduction
{: #introduction}

This client library describes how to use devices with the Java 'ibmiotf' client library. For help with getting started with this module, see [Java Client Library - Introduction](../java/javaintro.html).

This section contains information on how devices can to the {{site.data.keyword.iot_full}} Device Management service using Java and perform device management operations like Firmware Update, location update, and diagnostics update.

The Device section contains information on how devices can publish events and handle commands using the Java ibmiotf Client Library.

The Applications section contains information on how applications can use the Java ibmiotf Client Library to interact with devices.

## Device Management
{: #device_management}

The [device management](../reference/device_mgmt.html) feature enhances the {{site.data.keyword.iot_short_notm}} service with more capabilities for managing devices. Device management makes a distinction between managed and unmanaged devices:

-   **Managed devices** are defined as devices which have a management agent installed. The management agent sends and receives device metadata and responds to device management commands from the {{site.data.keyword.iot_short_notm}}.
-   **Unmanaged devices** are any devices which do not have a device management agent. All devices begin their lifecycle as unmanaged devices, and can transition to managed devices by sending a message from a device management agent to the {{site.data.keyword.iot_short_notm}}.

## Connecting to the {{site.data.keyword.iot_short_notm}} Device Management service
{: #connecting_dm_service}

## Creating device data
{: #creating_device_data}

The [device model](../reference/device_model.html) describes the metadata and management characteristics of a device. The device database in the {{site.data.keyword.iot_short_notm}} is the master source of device information. Applications and managed devices are able to send updates to the database such as a location or the progress of a Firmware Update. Once these updates are received by the {{site.data.keyword.iot_short_notm}}, the device database is updated, making the information available to applications.

`DeviceData` is the device model in the ibmiotf client library and includes the following objects:

-   DeviceInfo (required)
-   DeviceLocation (required if the device supports location update)
-   DiagnosticErrorCode (required if the device wants to update the ErrorCode)
-   DiagnosticLog (required if the device wants to update Log information)
-   DeviceFirmware (required if the device supports Firmware Actions)
-   DeviceMetadata (optional)

The following code sample shows how to create the mandatory object `DeviceInfo` object along with an optional `DeviceMetadata` object with sample data:

```
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

Use the following code sample to create a `DeviceData` object that includes the `DeviceInfo` and `DeviceMetadata` objects that you created in the previous sample.

  ```
  DeviceData deviceData = new DeviceData.Builder().
               deviceInfo(deviceInfo).
               metadata(metadata).
               build();
  ```

## Construct ManagedDevice
{: #construct_managed_device}

`ManagedDevice` is a device class that connects the device as a managed device to {{site.data.keyword.iot_short_notm}} and enables the device to perform one or more device management operations. You can also use a `ManagedDevice` instance to do normal device operations like publishing device events and listening for commands from an application.

`ManagedDevice` exposes the following constructors, which support the different user patterns:

**Constructor One**

Constructs a `ManagedDevice` instance by accepting the `DeviceData` and the following properties,

* Organization-ID - Your organization ID
* Device-Type - The type of your device
* Device-ID - The ID of your device
* Authentication-Method - Method of authentication (The only value currently supported is "token")
* Authentication-Token - API key token

All of the listed properties are required to interact with the {{site.data.keyword.iot_short_notm}}.

The following code outlines how you can create a `ManagedDevice` instance:

```
Properties options = new Properties();
options.setProperty("Organization-ID", "uguhsp");
options.setProperty("Device-Type", "iotsample-arduino");
options.setProperty("Device-ID", "00aabbccde03");
options.setProperty("Authentication-Method", "token");
options.setProperty("Authentication-Token", "AUTH TOKEN FOR DEVICE");

ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
```

If you are already using `DeviceClient`, you will notice that the names of the properties are slightly different, and mirror the names in the {{site.data.keyword.iot_short_notm}} dashboard. To migrate from `DeviceClient` to `ManagedDevice` can continue to use the earlier format by constructing the `ManagedDevice` instance as outlined in the folliwing sample:

```
Properties options = new Properties();
options.setProperty("org", "uguhsp");
options.setProperty("type", "iotsample-arduino");
options.setProperty("id", "00aabbccde03");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");
ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
```

**Constructor Two**

Construct a `ManagedDevice` instance by accepting both the `DeviceData` and `MqttClient` instances. This constructor requires that `DeviceData` is created with additional device attributes like Device Type and Device ID, as outlined in the following sample:

```
// Code that constructs the MqttClient (either Synchronous or Asynchronous MqttClient)
.....

// Code that constructs the DeviceData
DeviceData deviceData = new DeviceData.Builder().
             typeId("Device-Type").
             deviceId("Device-ID").
             deviceInfo(deviceInfo).
             metadata(metadata).
             build();

....
ManagedDevice managedDevice = new ManagedDevice(mqttClient, deviceData);
```

**Note:** This constructor helps custom device users to create a `ManagedDevice` instance with the already created and connected `MqttClient` instance to take advantage of device management operations. But we recommend the users to use the library for all the device functionalities.

## Manage

The `Manage` device can invoke manage() method to participate in device management activities. The manage request initiates a connect request internally if the device is not already connected to the {{site.data.keyword.iot_short_notm}}.

```
managedDevice.manage();
```

The device can use overloaded manage (lifetime) method to register the device for a given time frame. The time frame specifies the length of time within which the device must send another **Manage device** request in order to avoid being reverted to an unmanaged device and marked as dormant.

```
managedDevice.manage(3600);
```

For more information about the `Manage` operation, see the [documentation].

  [documentation]:../device_mgmt/operations/manage.html

## Unmanage

A device can invoke unmanage() method when it no longer needs to be managed. The {{site.data.keyword.iot_short_notm}} will no longer send new device management requests to this device and all device management requests from this device will be rejected other than a **Manage device** request.

```
managedDevice.unmanage();
```

For more information about the `Unmanage` operation, see the [documentation].

  [documentation]:../device_mgmt/operations/manage.html

## Location update
{: #construct_location_update}
Devices that can determine their location can choose to notify the {{site.data.keyword.iot_short_notm}} about location changes. In order to update the location, the device needs to create a `DeviceData` instance with the `DeviceLocation` object first.

```
// Construct the location object with latitude, longitude and elevation
DeviceLocation deviceLocation = new DeviceLocation.Builder(30.28565, -97.73921).
                            elevation(10).
                            build();
DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceLocation(deviceLocation).
             metadata(metadata).
             build();
```

When the device is connected to {{site.data.keyword.iot_short_notm}}, you can update the location by using the following method:

```
int rc = deviceLocation.sendLocation();
if(rc == 200) {
        System.out.println("Current location (" + deviceLocation.toString() + ")");
} else {
            System.err.println("Failed to update the location");
}
```

Subsequent updates to device location can be updated by modifying the properties of the `DeviceLocation` object, as outlined in the following sample:

```
int rc = deviceLocation.update(40.28, -98.33, 11);
if(rc == 200) {
    System.out.println("Current location (" + deviceLocation.toString() + ")");
} else {
    System.err.println("Failed to update the location");
}
```

The update() method informs the {{site.data.keyword.iot_short_notm}} about the new location.

For more information about the updating locations, see the linked [documentation](../device_mgmt/operations/update.html).



## Appending and clearing error codes
{: #appending_error_codes}

Devices can choose to notify the {{site.data.keyword.iot_short_notm}} about changes in their error status. In order to send error codes, the device needs to construct a `DiagnosticErrorCode` object as outlined in the following sample:

```
DiagnosticErrorCode errorCode = new DiagnosticErrorCode(0);

DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceErrorCode(errorCode).
             metadata(metadata).
             build();
```

As soon as the device is connected to {{site.data.keyword.iot_short_notm}}, the `ErrorCode` can be sent by calling the send() method as follows:

```
errorCode.send();
```

Later, any new `ErrorCodes` can be easily added to the {{site.data.keyword.iot_short_notm}} by calling the append method as follows:

```
int rc = errorCode.append(500);
if(rc == 200) {
    System.out.println("Current Errorcode (" + errorCode + ")");
} else {
    System.out.println("Errorcode addition failed!");
}
```

Also, the `ErrorCodes` can be cleared from {{site.data.keyword.iot_short_notm}} by calling the clear() method as follows:

```
int rc = errorCode.clear();
if(rc == 200) {
    System.out.println("ErrorCodes are cleared successfully!");
} else {
    System.out.println("Failed to clear the ErrorCodes!");
}
```

## Appending and clearing log messages

Devices can choose to notify the {{site.data.keyword.iot_short_notm}} about changes by adding a new log entry. A log entry includes the following information:
- Log message
- Time stamp
- Severity
- Base64-encoded binary diagnostic data (optional)

In order to send log messages, the device needs to construct a `DiagnosticLog` object as outlined in the following sample:

```
DiagnosticLog log = new DiagnosticLog(
            "Simple Log Message",
            new Date(),
            DiagnosticLog.LogSeverity.informational);

DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceLog(log).
             metadata(metadata).
             build();
```

As soon as the device is connected to {{site.data.keyword.iot_short_notm}}, the log message can be sent by calling the send() method as outlined in the following sample:

```
log.send();
```

Afterwards, any new log messages can be easily added to the {{site.data.keyword.iot_short_notm}} by calling the append method as outlined in the following sample:

```
int rc = log.append("sample log", new Date(), DiagnosticLog.LogSeverity.informational);

if(rc == 200) {
    System.out.println("Current Log (" + log + ")");
} else {
    System.out.println("Log Addition failed");
}
```

Also, the log messages can be cleared from {{site.data.keyword.iot_short_notm}} by calling the clear method as outlined in the following sample:

```
rc = log.clear();
if(rc == 200) {
    System.out.println("Logs are cleared successfully");
} else {
    System.out.println("Failed to clear the Logs")
}
```

The device diagnostics operations are intended to provide information on device errors, and do not provide diagnostic information relating to the devices connection to the {{site.data.keyword.iot_short_notm}}.

For more information about the Diagnostics operation, refer to the [documentation](../device_mgmt/operations/diagnostics.html).

## Firmware actions
{: #firmware_actions}

The Firmware Update process is separated into two distinct actions:

* Downloading firmware
* Updating firmware

The device needs to do the following activities to support firmware actions:

**1. Construct DeviceFirmware Object**

In order to perform firmware actions the device needs to construct the `DeviceFirmware` object and add it to `DeviceData` as follows:

```
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

ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
managedDevice.connect();
```

The `DeviceFirmware` object represents the current firmware of the device and will be used to report the status of the firmware download and Firmware Update actions to {{site.data.keyword.iot_short_notm}}.

**2. Inform the server about the Firmware action support**

The device needs to set the firmware action flag to true in order for the server to initiate the firmware request. This can be achieved by invoking a following method with a boolean value:

```
managedDevice.supportsFirmwareActions(true);
managedDevice.manage();
```

As the manage request informs the {{site.data.keyword.iot_short_notm}} about the firmware action support, manage() method needs to be called right after setting the firmware action support.

**3. Create the Firmware Action Handler**

In order to support the Firmware action, the device needs to create a handler and add it to `ManagedDevice`. The handler must extend a `DeviceFirmwareHandler` class and implement the following methods:

```
public abstract void downloadFirmware(DeviceFirmware deviceFirmware);
public abstract void updateFirmware(DeviceFirmware deviceFirmware);
```

**3.1 Sample implementation of downloadFirmware**

The implementation must add logic to download the firmware and report the status of the download by using a `DeviceFirmware` object. If the the firmware download operation is successful, then the status is set to `DOWNLOADED` and then `UpdateStatus` is set to `SUCCESS`.

If an error occurs during the firmware download, the state is set to `IDLE` and then the `updateStatus` is be set to one of the following error status values:

* `OUT_OF_MEMORY
* CONNECTION_LOST
* INVALID_URI`

The following sample outlines a firmware download implementation for a Raspberry Pi device :

```
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
            // use the timestamp as the name
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

A device can check the integrity of the downloaded firmware image using the verifier and report the status back to {{site.data.keyword.iot_short_notm}}. The verifier can be set by the device during the startup (while creating the DeviceFirmware Object) or as part of the Download Firmware request by the application. A sample code to verify the same is below:

```
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
    System.out.println("Download firmware checksum verification failed.. "
            + "Expected "+verifier + " found "+md5);
    return false;
}
```

For the entire code, see the [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java) device management sample.



**3.2 Sample implementation of updateFirmware**

The implementation must add logic to install the downloaded firmware and report the status of the update through the `DeviceFirmware` object. If the Firmware Update operation is successful, then the state of the firmware should to be set to IDLE and `updateStatus` should be set to `SUCCESS`.

If an error occurs during Firmware Update, `updateStatus` should be set to one of the error status values:

`* OUT_OF_MEMORY
* UNSUPPORTED_IMAGE`

A sample Firmware Update implementation for a Raspberry Pi device is shown below:

```
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

The complete code can be found in the device management sample [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java).


**4. Add the handler to ManagedDevice**

The created handler needs to be added to the ManagedDevice instance so that the ibmiotf client library invokes the corresponding method when there is a Firmware action request from {{site.data.keyword.iot_short_notm}}.

```
DeviceFirmwareHandlerSample fwHandler = new DeviceFirmwareHandlerSample();
deviceData.addFirmwareHandler(fwHandler);
```

Refer to [this page](../device_mgmt/operations/firmware_actions.html) for more information about the Firmware action.

## Device Actions

The {{site.data.keyword.iot_short_notm}} supports the following device actions:

* Reboot
* Factory Reset

The device needs to do the following activities to support Device Actions:

**1. Inform server about the Device Actions support**

In order to perform Reboot and Factory Reset, the device needs to inform the {{site.data.keyword.iot_short_notm}} about its support first. This can achieved by invoking a following method with a boolean value:

```
managedDevice.supportsDeviceActions(true);
    managedDevice.manage();
```

As the manage request informs the {{site.data.keyword.iot_short_notm}} about the device action support, manage() method needs to be called right after setting the device action support.

**2. Create the Device Action Handler**

In order to support the device action, the device needs to create a handler and add it to ManagedDevice. The handler must extend a DeviceActionHandler class and provide implementation for the following methods:

```
public abstract void handleReboot(DeviceAction action);
public abstract void handleFactoryReset(DeviceAction action);
```

**2.1 Sample implementation of handleReboot**

The implementation must add a logic to reboot the device and report the status of the reboot via DeviceAction object. The device needs to update the status along with a optional message only when there is a failure (because the successful operation reboots the device and the device code will not have a control to update the {{site.data.keyword.iot_short_notm}}). A sample reboot implementation for a Raspberry Pi device is shown below:

```
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

The complete code can be found in the device management sample [DeviceActionHandlerSample].

  [DeviceActionHandlerSample]: https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceActionHandlerSample.java

**2.2 Sample implementation of handleFactoryReset**

The implementation must add a logic to reset the device to factory settings and report the status via DeviceAction object. The device needs to update the status along with a optional message only when there is a failure (because as part of this process, the device reboots and the device will not have a control to update status to {{site.data.keyword.iot_short_notm}}). The skeleton of the Factory Reset implementation is shown below:

```
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

**3. Add the handler to ManagedDevice**

The created handler needs to be added to the ManagedDevice instance so that the ibmiotf client library invokes the corresponding method when there is a device action request from {{site.data.keyword.iot_short_notm}}.

```
DeviceActionHandlerSample actionHandler = new DeviceActionHandlerSample();
deviceData.addDeviceActionHandler(actionHandler);
```

Refer to [this page](../device_mgmt/operations/device_actions.html) for more information about the Device Action.



## Listen for device attribute changes
{: #listen_device_attribute}

This ibmiotf client library updates the corresponding objects whenever there is an update request from the {{site.data.keyword.iot_short_notm}}, these update requests are initiated by the application either directly or indirectly (Firmware Update) via the {{site.data.keyword.iot_short_notm}} REST API. Apart from updating these attributes, the library provides a mechanism where the device can be notified whenever a device attribute is updated.

Attributes that can be updated by this operation are `location`, `metadata`, `device information`, and `firmware`.

To be notified, the device must add a property change listener on the objects of interest.

```
deviceLocation.addPropertyChangeListener(listener);
firmware.addPropertyChangeListener(listener);
deviceInfo.addPropertyChangeListener(listener);
metadata.addPropertyChangeListener(listener);
```

Also, the device needs to implement the `propertyChange()` method where it receives the notification. The following sample outlines how this can be implemented:

```
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

For more information about updating the device attributes, see [this page](../device_mgmt/operations/update.html).

## Examples
{: #examples}

-   [SampleRasPiDMAgent](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgent.java) - A sample agent code that shows how to perform various device management operations on Raspberry Pi.
-   [SampleRasPiManagedDevice](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiManagedDevice.java) - A sample code that shows how one can perform both device operations and management operations.
-   [SampleRasPiDMAgentWithCustomMqttAsyncClient](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgentWithCustomMqttAsyncClient.java) - A sample agent code with custom MqttAsyncClient.
-   [SampleRasPiDMAgentWithCustomMqttClient](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgentWithCustomMqttClient.java) - A sample agent code with custom MqttClient.
-   [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java) - A sample implementation of FirmwareHandler for Raspberry Pi.
-   [DeviceActionHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceActionHandlerSample.java) - A sample implementation of DeviceActionHandler
-   [ManagedDeviceWithLifetimeSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/ManagedDeviceWithLifetimeSample.java) - A sample that shows how to send regular manage request with lifetime specified.
-   [DeviceAttributesUpdateListenerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceAttributesUpdateListenerSample.java) - A sample listener code that shows how to listen for a various device attribute changes .
-   [NonBlockingDiagnosticsErrorCodeUpdateSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/NonBlockingDiagnosticsErrorCodeUpdateSample.java) - A sample that shows how to add ErrorCode without waiting for response from the server.

##s Recipes
{: #Recipes}

Refer to [the recipe](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-managed-device-to-ibm-iot-foundation/) that shows how to connect the Raspberry Pi device as managed device to {{site.data.keyword.iot_short_notm}} to perform various device management operations in step by step using this client library.
