---

copyright:
  years: 2015, 2017
lastupdated: "2016-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 使用 Java 开发受管设备
{: #java_deviceManagement}

##简介
{: #introduction}

在 {{site.data.keyword.iot_full}} 中，受管设备是指可以执行设备管理操作（例如，固件、位置和诊断更新）的设备。使用提供的 {{site.data.keyword.iot_short}} Java™ 客户机库和信息可以开发 Java 代码，以用于将连接的设备转换为受管设备。此外，还提供了样本来帮助您开发 Java 代码，以用于将设备连接到“设备管理”服务以及运行设备管理操作。

有关应用程序可以如何使用 Java 客户机库与设备进行交互的更多信息，请参阅[针对应用程序开发者的 Java](../../applications/libraries/java.html)。

## 设备管理
{: #device_management}

[设备管理](../reference/device_mgmt.html)功能通过更多设备管理功能使 {{site.data.keyword.iot_short_notm}} 服务得到增强。设备管理可区分受管设备和非受管设备：

-   **受管设备**定义为安装了管理代理程序的设备。管理代理程序发送和接收设备元数据，并对来自 {{site.data.keyword.iot_short_notm}} 的设备管理命令进行响应。
-   **非受管设备**是指没有设备管理代理程序的任何设备。所有设备在其生命周期一开始都是非受管设备，随后可以通过将消息从设备管理代理程序发送到 {{site.data.keyword.iot_short_notm}} 来转换为受管设备。

## 连接到 {{site.data.keyword.iot_short_notm}} Device Management 服务
{: #connecting_dm_service}

## 创建设备数据
{: #creating_device_data}

[设备模型](../reference/device_model.html)描述设备的元数据和管理特征。{{site.data.keyword.iot_short_notm}} 中的设备数据库是设备信息的主来源。应用程序和受管设备都能够向数据库发送更新，例如“固件更新”的位置或进度。一旦 {{site.data.keyword.iot_short_notm}} 接收到这些更新，就会更新设备数据库，使这些信息可供应用程序使用。

`DeviceData` 是 ibmiotf 客户机库中的设备模型，包含以下对象：

-   DeviceInfo（必需）
-   DeviceLocation（如果设备支持位置更新，那么是必需的）
-   DiagnosticErrorCode（如果希望设备更新 ErrorCode，那么是必需的）
-   DiagnosticLog（如果希望设备更新日志信息，那么是必需的）
-   DeviceFirmware（如果设备支持“固件操作”，那么是必需的）
-   DeviceMetadata（可选）

以下代码样本显示了如何使用样本数据创建必需的 `DeviceInfo` 对象以及可选的 `DeviceMetadata` 对象：

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

使用以下代码样本可创建包含在上一个样本中所创建 `DeviceInfo` 和 `DeviceMetadata` 对象的 `DeviceData` 对象。

  ```
  DeviceData deviceData = new DeviceData.Builder().
               deviceInfo(deviceInfo).
               metadata(metadata).
               build();
  ```

## 构造 ManagedDevice
{: #construct_managed_device}

`ManagedDevice` 是设备类，用于将设备作为受管设备连接到 {{site.data.keyword.iot_short_notm}}，并使设备能够执行一个或多个设备管理操作。还可以使用 `ManagedDevice` 实例来执行常规设备操作，如发布设备事件和侦听来自应用程序的命令。

`ManagedDevice` 公开以下构造方法，这些构造方法支持不同的用户模式：

**构造方法一**

构造方法一用于通过接受 `DeviceData` 和以下所有必需属性，在 {{site.data.keyword.iot_short_notm}} 中构造 `ManagedDevice` 实例：

|属性 |描述 |
|:---|:---|
|`Organization-ID` |组织的标识|
|`Device-Type` |设备类型。通常，deviceType 是对执行特定任务的设备的一种分组，例如“weatherballoon”。|
|`Device-ID` |设备的标识。通常，对于给定设备类型，deviceId 是该设备的唯一标识，例如序列号或 MAC 地址。|
|`Authentication-Method` |要使用的认证方法。当前支持的唯一值是 `token`。|
|`Authentication-Token` |用于将设备安全连接到 Watson IoT Platform 的认证令牌。|


以下代码概述了可如何创建 `ManagedDevice` 实例：

```
Properties options = new Properties();
options.setProperty("Organization-ID", "uguhsp");
options.setProperty("Device-Type", "iotsample-arduino");
options.setProperty("Device-ID", "00aabbccde03");
options.setProperty("Authentication-Method", "token");
options.setProperty("Authentication-Token", "AUTH TOKEN FOR DEVICE");

ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
```

如果已经在使用 `DeviceClient` 实例，那么您将注意到属性的名称略有不同，并且会在 {{site.data.keyword.iot_short_notm}} 仪表板中制作名称的镜像。要从 `DeviceClient` 迁移到 `ManagedDevice`，可以通过构造 `ManagedDevice` 实例来继续使用较早的格式，如以下示例中所示：

```
Properties options = new Properties();
options.setProperty("org", "uguhsp");
options.setProperty("type", "iotsample-arduino");
options.setProperty("id", "00aabbccde03");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");
ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
```

**构造方法二**

通过同时接受 `DeviceData` 和 `MqttClient` 实例来构造 `ManagedDevice` 实例。此构造方法需要使用额外的设备属性（例如，设备类型和设备标识）来创建 `DeviceData`，如以下样本中所示：

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

**注：**此构造方法可帮助定制设备用户通过已创建且已连接的 `MqttClient` 实例来创建 `ManagedDevice` 实例，以充分利用设备管理操作。但我们建议用户对所有设备功能均使用该库。

## 管理

`Manage` 设备可以调用 manage() 方法来参与设备管理活动。如果设备尚未连接到 {{site.data.keyword.iot_short_notm}}，那么管理请求会在内部发出连接请求。

```
managedDevice.manage();
```

设备可以使用重载的 manage(lifetime) 方法针对给定的时间范围注册该设备。该时间范围指定的时间长度表示，设备必须在此期间发送另一个**管理设备**请求，才能避免还原为非受管设备并被标记为休眠。

```
managedDevice.manage(3600);
```

有关 `Manage` 操作的更多信息，请参阅 [文档]。

  [documentation]:../device_mgmt/operations/manage.html

## 取消管理

当设备不再需要接受管理时，它可以调用 unmanage() 方法。{{site.data.keyword.iot_short_notm}} 不会再向此设备发送新的设备管理请求，并且来自此设备的所有设备管理请求中，除了**管理设备**请求外，其他请求都会被拒绝。

```
managedDevice.unmanage();
```

有关 `Unmanage` 操作的更多信息，请参阅 [文档]。

  [documentation]:../device_mgmt/operations/manage.html

## 位置更新
{: #construct_location_update}
可以确定其位置的设备可以选择向 {{site.data.keyword.iot_short_notm}} 通知有关位置更改的信息。为了更新位置，设备首先需要使用 `DeviceLocation` 对象创建 `DeviceData` 实例。

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

设备连接到 {{site.data.keyword.iot_short_notm}} 后，可以使用以下方法来更新位置：

```
int rc = deviceLocation.sendLocation();
if(rc == 200) {
        System.out.println("Current location (" + deviceLocation.toString() + ")");
} else {
            System.err.println("Failed to update the location");
}
```

对设备位置的后续更新可以通过修改 `DeviceLocation` 对象来进行更新，如以下示例中所示：

```
int rc = deviceLocation.update(40.28, -98.33, 11);
if(rc == 200) {
    System.out.println("Current location (" + deviceLocation.toString() + ")");
} else {
    System.err.println("Failed to update the location");
}
```

update() 方法会向 {{site.data.keyword.iot_short_notm}} 通知有关新位置的信息。

有关更新位置的更多信息，请参阅链接的[文档](../device_mgmt/operations/update.html)。



## 附加和清除错误代码
{: #appending_error_codes}

设备可以选择向 {{site.data.keyword.iot_short_notm}} 通知有关其错误状态更改的信息。为了发送错误代码，设备需要构造 `DiagnosticErrorCode` 对象，如以下样本中所示：

```
DiagnosticErrorCode errorCode = new DiagnosticErrorCode(0);

DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceErrorCode(errorCode).
             metadata(metadata).
             build();
```

只要设备连接到 {{site.data.keyword.iot_short_notm}}，就能通过调用 send() 方法来发送 `ErrorCode`，如下所示：

```
errorCode.send();
```

稍后，可以通过调用 append 方法将任何新的 `ErrorCodes` 轻松添加到 {{site.data.keyword.iot_short_notm}}，如下所示：

```
int rc = errorCode.append(500);
if(rc == 200) {
    System.out.println("Current Errorcode (" + errorCode + ")");
} else {
    System.out.println("Errorcode addition failed!");
}
```

此外，还可以通过调用 clear() 方法从 {{site.data.keyword.iot_short_notm}} 中清除 `ErrorCodes`，如下所示：

```
int rc = errorCode.clear();
if(rc == 200) {
    System.out.println("ErrorCodes are cleared successfully!");
} else {
    System.out.println("Failed to clear the ErrorCodes!");
}
```

## 附加和清除日志消息

设备可以选择通过添加新日志条目向 {{site.data.keyword.iot_short_notm}} 通知有关更改的信息。日志条目包含以下信息：
- 日志消息
- 时间戳记
- 严重性
- 基本 64 位编码的二进制诊断数据（可选）

为了发送日志消息，设备需要构造 `DiagnosticLog` 对象，如以下样本中所示：

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

只要设备连接到 {{site.data.keyword.iot_short_notm}}，就能通过调用 send() 方法来发送日志消息，如以下样本中所示：

```
log.send();
```

此后，可以通过调用 append 方法，将任何新的日志消息轻松添加到 {{site.data.keyword.iot_short_notm}}，如以下样本中所示：

```
int rc = log.append("sample log", new Date(), DiagnosticLog.LogSeverity.informational);

if(rc == 200) {
    System.out.println("Current Log (" + log + ")");
} else {
    System.out.println("Log Addition failed");
}
```

此外，还可以通过调用 clear 方法从 {{site.data.keyword.iot_short_notm}} 中清除日志消息，如以下样本中所示：

```
rc = log.clear();
if(rc == 200) {
    System.out.println("Logs are cleared successfully");
} else {
    System.out.println("Failed to clear the Logs")
}
```

设备诊断操作旨在提供有关设备错误的信息，而不会提供与 {{site.data.keyword.iot_short_notm}} 的设备连接相关的诊断信息。

有关 Diagnostics 操作的更多信息，请参阅[文档](../device_mgmt/operations/diagnostics.html)。

## 固件操作
{: #firmware_actions}

“固件更新”过程分为两个不同的操作：

* 下载固件
* 更新固件

设备需要执行以下活动来支持固件操作：

**1. 构造 DeviceFirmware 对象**

为了执行固件操作，设备需要构造 `DeviceFirmware` 对象，并将其添加到 `DeviceData`，如下所示：

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

`DeviceFirmware` 对象表示设备的当前固件，并将用于向 {{site.data.keyword.iot_short_notm}} 报告固件下载和“固件更新”操作的状态。

**2. 向服务器通知有关固件操作支持的信息**

设备需要将固件操作标记设置为 true，以便服务器能够发出固件请求。这可通过使用布尔值调用以下方法来实现：

```
managedDevice.supportsFirmwareActions(true);
managedDevice.manage();
```

由于管理请求会向 {{site.data.keyword.iot_short_notm}} 通知有关固件操作支持的信息，因此需要在设置固件操作支持后立即调用 manage() 方法。

**3. 创建固件操作处理程序**

为了支持固件操作，设备需要创建一个处理程序并将其添加到 `ManagedDevice`。该处理程序必须扩展 `DeviceFirmwareHandler` 类并实现以下方法：

```
public abstract void downloadFirmware(DeviceFirmware deviceFirmware);
public abstract void updateFirmware(DeviceFirmware deviceFirmware);
```

**3.1 downloadFirmware 的样本实现**

该实现必须添加逻辑，以使用 `DeviceFirmware` 对象来下载固件和报告下载状态。如果固件下载操作成功，那么状态会设置为 `DOWNLOADED`，随后 `UpdateStatus` 会设置为 `SUCCESS`。

如果固件下载期间发生错误，那么状态会设置为 `IDLE`，随后 `updateStatus` 会设置为以下某个错误状态值：

* `OUT_OF_MEMORY
* CONNECTION_LOST
* INVALID_URI`

以下样本概述了 Raspberry Pi 设备的固件下载实现：

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

设备可以使用验证器来检查下载的固件映像的完整性，并向 {{site.data.keyword.iot_short_notm}} 报告状态。验证器可由设备在启动期间（创建 DeviceFirmware 对象时）设置，也可以作为“下载固件”请求的组成部分由应用程序设置。用于验证是否一致的样本代码如下：

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

有关完整代码，请参阅 [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java) 设备管理样本。



**3.2 updateFirmware 的样本实现**

该实现必须添加逻辑，以通过 `DeviceFirmware` 对象来安装下载的固件和报告更新状态。如果“固件更新”操作成功，那么固件的状态应该设置为 IDLE，并且 `updateStatus` 应该设置为 `SUCCESS`。

如果“固件更新”期间发生错误，那么 `updateStatus` 应该设置为以下某个错误状态值：

`* OUT_OF_MEMORY
* UNSUPPORTED_IMAGE`

Raspberry Pi 设备的样本“固件更新”实现如下所示：

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

完整的代码位于 [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java) 设备管理样本中。


**4. 向 ManagedDevice 添加处理程序**

创建的处理程序需要添加到 ManagedDevice 实例，以便有来自 {{site.data.keyword.iot_short_notm}} 的固件操作请求时，ibmiotf 客户机库能调用相应的方法。

```
DeviceFirmwareHandlerSample fwHandler = new DeviceFirmwareHandlerSample();
deviceData.addFirmwareHandler(fwHandler);
```

请参阅[本页](../device_mgmt/operations/firmware_actions.html)，以获取有关固件操作的更多信息。

## 设备操作

{{site.data.keyword.iot_short_notm}} 支持以下设备操作：

* 重新引导
* 恢复出厂设置

设备需要完成以下活动来支持设备操作：

**1. 向服务器通知有关设备操作支持的信息**

为了执行“重新引导”和“恢复出厂设置”，设备首先需要向 {{site.data.keyword.iot_short_notm}} 通知有关其支持的信息。这可通过使用布尔值调用以下方法来实现：

```
managedDevice.supportsDeviceActions(true);
    managedDevice.manage();
```

由于管理请求会向 {{site.data.keyword.iot_short_notm}} 通知有关设备操作支持的信息，因此需要在设置设备操作支持后立即调用 manage() 方法。

**2. 创建设备操作处理程序**

为了支持设备操作，设备需要创建一个处理程序并将其添加到 ManagedDevice。该处理程序必须扩展 DeviceActionHandler 类并实现以下方法：

```
public abstract void handleReboot(DeviceAction action);
public abstract void handleFactoryReset(DeviceAction action);
```

**2.1 handleReboot 的样本实现**

该实现必须添加用于重新引导设备的逻辑，并且通过 DeviceAction 对象报告重新引导的状态。仅当存在故障时，设备才需要更新状态以及可选的消息（因为成功的操作会重新引导设备，并且设备代码将没有控件来更新 {{site.data.keyword.iot_short_notm}}）。下面显示了 Raspberry Pi 设备的样本重新引导实现：

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

完整的代码位于 [DeviceActionHandlerSample] 设备管理样本中。

  [DeviceActionHandlerSample]: https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceActionHandlerSample.java

**2.2 handleFactoryReset 的样本实现**

该实现必须添加用于将设备恢复为出厂设置的逻辑，并且通过 DeviceAction 对象报告状态。仅当存在故障时，设备才需要更新状态以及可选的消息（因为作为此过程的一部分，设备会重新引导，并且设备将没有控件来向 {{site.data.keyword.iot_short_notm}} 更新状态）。下面显示了“恢复出厂设置”实现的框架：

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

**3. 向 ManagedDevice 添加处理程序**

创建的处理程序需要添加到 ManagedDevice 实例，以便有来自 {{site.data.keyword.iot_short_notm}} 的设备操作请求时，ibmiotf 客户机库能调用相应的方法。

```
DeviceActionHandlerSample actionHandler = new DeviceActionHandlerSample();
deviceData.addDeviceActionHandler(actionHandler);
```

请参阅[本页](../device_mgmt/operations/device_actions.html)，以获取有关设备操作的更多信息。



## 侦听设备属性更改
{: #listen_device_attribute}

每当有来自 {{site.data.keyword.iot_short_notm}} 的更新请求时，此 ibmiotf 客户机库都会更新相应的对象，这些更新请求由应用程序通过 {{site.data.keyword.iot_short_notm}} REST API 直接或间接（固件更新）发出。除更新这些属性外，该库还提供一种机制，使设备能够在其属性已更新时得到通知。

可以由此操作更新的属性为 `location`、`metadata`、`device information` 和 `firmware`。

要获取通知，设备必须在相关对象上添加属性更改侦听器。

```
deviceLocation.addPropertyChangeListener(listener);
firmware.addPropertyChangeListener(listener);
deviceInfo.addPropertyChangeListener(listener);
metadata.addPropertyChangeListener(listener);
```

此外，设备还需要在接收通知的地方实现 `propertyChange()` 方法。以下样本概述了可以如何实现此操作：

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

有关更新设备属性的更多信息，请参阅[本页](../device_mgmt/operations/update.html)。

## 示例
{: #examples}

-   [SampleRasPiDMAgent](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgent.java) - 显示如何在 Raspberry Pi 上执行各种设备管理操作的样本代理程序代码。
-   [SampleRasPiManagedDevice](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiManagedDevice.java) - 显示如何执行设备操作和管理操作的样本代码。
-   [SampleRasPiDMAgentWithCustomMqttAsyncClient](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgentWithCustomMqttAsyncClient.java) - 具有定制 MqttAsyncClient 的样本代理程序代码。
-   [SampleRasPiDMAgentWithCustomMqttClient](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgentWithCustomMqttClient.java) - 具有定制 MqttClient 的样本代理程序代码。
-   [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java) - 针对 Raspberry Pi 的 FirmwareHandler 的样本实现。
-   [DeviceActionHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceActionHandlerSample.java) - DeviceActionHandler 的样本实现
-   [ManagedDeviceWithLifetimeSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/ManagedDeviceWithLifetimeSample.java) - 显示如何发送具有指定生命周期的定期管理请求的样本。
-   [DeviceAttributesUpdateListenerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceAttributesUpdateListenerSample.java) - 显示如何侦听各种设备属性更改的样本侦听器代码。
-   [NonBlockingDiagnosticsErrorCodeUpdateSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/NonBlockingDiagnosticsErrorCodeUpdateSample.java) - 显示如何添加 ErrorCode 而不等待来自服务器的响应的样本。

##诀窍
{: #Recipes}

请参阅[诀窍](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-managed-device-to-ibm-iot-foundation/)，其中显示了如何将 Raspberry Pi 设备作为受管设备连接到 {{site.data.keyword.iot_short_notm}}，以通过此客户机库逐步执行各种设备管理操作。
