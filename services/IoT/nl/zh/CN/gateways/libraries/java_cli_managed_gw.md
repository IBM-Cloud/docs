---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-20"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 使用 Java 开发受管网关
{: #java_cli_managed_gw}

网关在管理连接到自己的设备方面起着十分重要的作用。许多设备都是非常基本的设备，没有任何设备管理功能，所以这些基本设备需要通过网关进行管理。在 {{site.data.keyword.iot_full}} 中，受管网关是指可以管理连接到自己的设备并提供设备管理功能（例如，固件、位置和诊断更新）的网关。
{:shortdesc}

通过使用 {{site.data.keyword.iot_short}} Java™ 客户机库和提供的信息，可以开发 Java 代码，以将网关转换为受管网关。此外，还提供了样本来帮助您开发 Java 代码，以将网关连接到“设备管理”服务以及运行设备管理操作。

## 设备管理服务
{: #dm_service}

{{site.data.keyword.iot_short}}“设备管理”(DM) 服务提供了多种设备管理功能，可供网关用于管理连接到自己的设备。

受管网关会运行设备管理代理程序，后者作为通过网关连接到 {{site.data.keyword.iot_short}} 的所有设备的代理运行。

### 设备管理代理程序

通过网关间接连接到 {{site.data.keyword.iot_short}} 的设备可以使用网关设备支持的各种连接协议。

`ManagedGateway` 实例是一种设备管理代理程序，提供了用于执行一个或多个设备管理操作（例如，参与设备管理活动，更新错误代码、日志、位置和固件或设备操作）的方法的列表。

网关上的设备管理代理程序会转换并处理连接设备的连接协议，这将确保设备可以由 {{site.data.keyword.iot_short}} 进行管理。通过设备管理代理程序，网关不仅仅是已连接设备与 {{site.data.keyword.iot_short}} 之间的透明隧道。例如，如果连接到网关的设备无法下载固件，那么网关上的设备管理代理程序可以执行以下操作：
- 拦截要求设备下载固件的请求
- 为设备下载固件
- 在网关上存储设备固件

在将来某个时间点，当系统指示设备执行升级时，网关上的设备管理代理程序可以将固件推送到该设备并进行更新。

## 创建设备模型
{: #create_device_model}

在 {{site.data.keyword.iot_short}} 中，设备模型描述了设备和网关的元数据和管理特征。设备数据库是设备或网关信息的主来源。应用程序和受管设备可以发送位置更新、固件升级进度更新和其他类型的更新。{{site.data.keyword.iot_short}} 接收到更新后，就会更新设备数据库，使这些信息可供连接应用程序使用。

在 {{site.data.keyword.iot_short}} Java 客户机库中，设备模型由 `DeviceData` Java 类表示。

要创建 `DeviceData` 类，请创建以下对象：

- `DeviceInfo`（可选）
- `DeviceLocation`（可选，仅当要向设备通知有关位置的信息时才是必需的，此通知由应用程序通过 {{site.data.keyword.iot_short}} API 设置）
- `DeviceFirmware`（可选）
- `DeviceMetadata`（可选）

有关更多信息，请参阅[设备模型](../../reference/device_model.html)。

### DeviceInfo

以下代码片段包含样本数据，显示了如何创建 `DeviceInfo` 和 `DeviceMetadata` 对象：

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

以下代码片段概述了如何使用先前样本中创建的 `DeviceInfo` 和 `DeviceMetadata` 对象来创建 `DeviceData` 类：

```java
DeviceData deviceData = new DeviceData.Builder().
                         deviceInfo(deviceInfo).
            metadata(metadata).
             build();
```

每个网关和每个连接的设备都必须具有自己的 `DeviceData` 类定义，才能在 {{site.data.keyword.iot_short}} 中表示自身。对于网关，`DeviceData` 类会在构造 `ManagedGateway` 实例的过程中传递到库。对于连接的设备，`DeviceData` 类会作为 `sendDeviceManageRequest()` 对象的一部分传递到库。

## ManagedGateway 构造函数
{: #construct_managed_gateway}

`ManagedGateway` 是一个 Java 类，用于将网关作为受管网关连接到 {{site.data.keyword.iot_short}}，使其可以对自身或对连接的设备至少执行一个设备管理操作。`ManagedGateway` 实例还可用于执行常规网关操作，例如发布网关事件、连接设备事件和侦听来自应用程序的命令。`ManagedGateway` 实例是设备管理代理程序。

在 `ManagedGateway` 类中，两种不同的构造方法（构造方法一和构造方法二）支持不同的用户模式。

### 构造方法一

构造方法一用于通过接受包含以下所有属性的 `DeviceData` 类来构造 `ManagedGateway` 实例：

| 属性     |描述     |
|----------------|----------------|
|`Organization-ID` |组织标识。|
|`Gateway-Type` |网关设备的类型。|
|`Gateway-ID` |网关设备的标识。|
|`Authentication-Method`|认证方法。支持的唯一方法是“token”。|
|`Authentication-Token`|API 密钥令牌。|
|`auth-key`   |可选的 API 密钥，将 auth-method 的值设置为 `apikey` 时必须指定。|
|`auth-token`   |API 密钥令牌，将 auth-method 的值设置为 `apikey` 时，此参数也是必需的。 |
|`clean-session`|true 或 false 值，仅当要以持久预订方式连接网关时是必需的。缺省情况下，`clean-session` 设置为 `true`。|
|`Port`|要连接到的端口号。指定 8883 或 443。如果未指定端口号，缺省情况下客户机将通过端口号 8883 连接到 {{site.data.keyword.iot_short_notm}}。|
|`WebSocket`|true 或 false 值，仅当要使用 WebSocket 连接网关时是必需的。|
|`MaxInflightMessages`  |设置连接的最大未完成消息数。缺省值为 100。|
|`Automatic-Reconnect`  |true 或 false 值，要自动将处于断开连接状态的设备重新连接到 {{site.data.keyword.iot_short_notm}} 时是必需的。缺省值为 false。|
|`Disconnected-Buffer-Size`|客户机处于断开连接状态时可以存储在内存中的最大消息数。缺省值为 5000。|

**注：**要以持久预订方式连接网关，请将 `clean-session` 设置为 `false`。有关 `clean-session` 属性的更多信息，请参阅 [MQTT 文档](../../reference/mqtt/index.html#subscription-buffers-and-clean-session)的“预订缓冲区和干净会话”部分。

以下代码概述了如何创建 `ManagedGateway` 实例：

```java
Properties options = new Properties();
options.setProperty("Organization-ID", "uguhsp");
options.setProperty("Gateway-Type", "iotsample-arduino");
options.setProperty("Gateway-ID", "00aabbccde03");
options.setProperty("Authentication-Method", "token");
options.setProperty("Authentication-Token", "AUTH TOKEN FOR DEVICE");

ManagedGateway ManagedGateway = new ManagedGateway(options, deviceData);
```

### 构造方法二

构造方法二用于通过接受 `DeviceData` 对象和 MQTT 客户机实例来构造 `ManagedGateway` 实例。构造方法二还要求实例中的 `DeviceData` 对象包含设备类型和设备标识，如以下代码样本中所概述：

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

**注：**如果要针对定制设备进行开发，请使用“构造方法二”，因为此构造方法会使用现有连接的 MQTT 客户机实例来创建受管网关实例，这样您可以利用设备管理操作。将 Java 客户机库用于所有设备功能。

## 来自网关的设备管理请求
{: #dm_requests}

### 从网关发送管理请求

要指示网关参与设备管理活动，请调用 `sendGatewayManageRequest()` 方法，如以下代码样本中所概述：

```java
managedGateway.sendGatewayManageRequest(0, true, true);
```
如果设备尚未连接到 {{site.data.keyword.iot_short}}，那么管理请求会在内部发起连接请求。

`sendGatewayManageRequest()` 方法接受以下参数：

| 参数     |描述     |
|----------------|----------------|
|`lifetime`|时间长度（以秒为单位），设备必须在此期间发送另一个管理设备类型请求，才能避免被分类为休眠而变成非受管设备。如果省略 `lifetime` 字段或将其设置为 0，那么受管设备不会变为休眠。`lifetime` 字段支持的最小值设置为 3600 秒（1 小时）。|
|`supportFirmwareActions`|true 或 false 值，用于确定网关是否支持固件操作。网关还必须添加固件处理程序才可处理固件请求。|
|`supportDeviceActions`|true 或 false 值，用于确定网关是否支持设备操作。网关还必须添加设备操作处理程序才可处理重新引导和恢复出厂设置请求。|


`ManagedGateway` 实例是一种设备管理代理程序，提供了用于执行一个或多个设备管理操作（例如，参与设备管理活动，更新错误代码、日志、位置和固件或设备操作）的方法的列表。

### 从连接的设备发送管理请求

要允许在网关后面连接的设备参与网关上的设备管理活动，请调用 `sendDeviceManageRequest()` 方法。

`sendDeviceManageRequest()` 方法接受所连接设备的详细信息以及 `lifetime`、`supportFirmwareActions` 和 `supportDeviceActions` 参数。网关还可以使用重载的 `sendDeviceManageRequest()` 方法来为连接的设备定义 `DeviceData` 对象。

#### 从连接的设备发送管理请求的示例

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, lifetime, true, true);
```

### 从网关发送取消管理请求

不再需要对网关进行管理时，要停止该网关上的设备管理活动，请调用 `sendGatewayUnmanageRequet()` 方法。调用 `sendGatewayUnmanageRequet()` 后，{{site.data.keyword.iot_short}} 不会再发送针对网关的任何新的设备管理请求，并且会拒绝所有来自网关的设备管理请求，但 **Manage** 请求除外。不会拒绝来自网关后面的设备的请求。

#### 从网关发送取消管理请求的示例

```java
managedGateway.sendGatewayUnmanageRequet();
```

### 从连接的设备发送取消管理请求

不再需要对位于网关后面的设备进行管理时，要将已连接设备从受管状态移至非受管状态，该网关可以调用 `sendDeviceUnmanageRequet()` 方法。调用 `sendDeviceUnmanageRequet()` 后，{{site.data.keyword.iot_short}} 不会再发送针对该设备的任何新的设备管理请求，并且会拒绝所有来自该网关的针对该已连接设备的设备管理请求，但 **Manage** 请求除外。

#### 从连接的设备发送取消管理请求的示例

```java
managedGateway.sendDeviceUnmanageRequet();
```

## 位置更新
{: #location_updates}

### 发送网关位置更新

可以确定其位置的网关可以选择向 {{site.data.keyword.iot_short}} 通知有关位置更改的信息。网关可以调用某个重载的 `updateLocation()` 方法来更新设备的位置。

```java
    // update the location with latitude, longitude, and elevation.
int rc = managedGateway.updateGatewayLocation(30.28565, -97.73921, 10);
if(rc == 200) {
    System.out.println("Location updated successfully!");
} else {
System.err.println("Failed to update the location!");
    }
```

### 发送已连接设备的位置更新

网关可以调用相应的 `updateDeviceLocation()` 设备方法来更新已连接设备的位置。重载方法可用于指定 `measuredDateTime` 方法。

```java
// update the location of the attached device with latitude, longitude, and elevation
int rc = managedGateway.updateDeviceLocation(typeId, deviceId, 30.28565, -97.73921, 10);
```
有关位置更新的更多信息，请参阅[设备管理请求](../../devices/device_mgmt/index.html#/update-location#update-location)。

## 错误代码处理
{: #errors}

### 创建和删除网关错误代码

网关可以选择向 {{site.data.keyword.iot_short}} 通知有关其错误状态更改的信息。网关可以调用 `addErrorCode()` 方法向 {{site.data.keyword.iot_short}} 添加最新错误代码。

```java
int rc = managedGateway.addGatewayErrorCode(300);
```

可以通过调用 `clearErrorCodes()` 方法从 {{site.data.keyword.iot_short}} 中清除网关的错误代码，如下所示：

```java
int rc = managedGateway.clearGatewayErrorCodes();
```

### 创建和删除已连接设备的错误代码

网关还可调用相应的设备方法来添加或清除已连接设备的错误代码：

```java
int rc = managedGateway.addDeviceErrorCode(typeId, deviceId, 300);
rc = managedGateway.clearDeviceErrorCodes(typeId, deviceId);
```

### 创建和删除网关日志消息

网关可以选择通过添加新日志条目向 {{site.data.keyword.iot_short}} 通知有关更改的信息。日志条目包含以下各项：

- 消息字符串
- 时间戳记
- 严重性
- （可选）基本 64 位编码的二进制诊断数据

网关可以调用 `addGatewayLog()` 方法来发送日志消息，如以下样本中所概述：

```java
// An example Log event
String message = "Firmware Download Progress (%): " + 50;
Date timestamp = new Date();
LogSeverity severity = LogSeverity.informational;
int rc = managedGateway.addGatewayLog(message, timestamp, severity);
```

可以通过调用 `clearLogs()` 方法从 {{site.data.keyword.iot_short}} 中清除日志消息：

```java
rc = managedGateway.clearGatewayLogs();
```

### 创建和删除已连接设备的日志

与此类似，网关可以调用相应的设备方法来创建或清除已连接设备的日志，如以下代码样本中所概述：

```java

// An example log event:
String message = "Firmware Download Progress (%): " + 50;
Date timestamp = new Date();
LogSeverity severity = LogSeverity.informational;
int rc = managedGateway.addDeviceLog(typeId, deviceId, message, timestamp, severity);
```

要清除已连接设备的日志，请通过指定已连接设备的详细信息来调用 `clearDeviceLogs()` 方法，如以下代码样本中所概述：

```java
int rc = managedGateway.clearDeviceLogs(typeId, deviceId);
```

设备诊断操作旨在提供有关网关或设备错误的信息。不会提供与 {{site.data.keyword.iot_short}} 的设备连接相关的诊断信息。

有关诊断操作的更多信息，请参阅[设备管理请求](../../devices/device_mgmt/index.html#/update-location#update-location)。

## 固件更新和操作
{: #firmware}

固件更新过程分为两个不同的操作：

- 下载固件
- 更新固件

网关必须执行以下活动来支持对其自身和对其所连接设备的固件操作：

1. 可选：构造 `DeviceFirmware` 对象。
2. 向服务器通知有关固件操作支持的信息。
3. 创建固件操作处理程序。
4. 向 `ManagedGateway` 添加处理程序。

### 步骤 1：构造 `DeviceFirmware` 对象

为了执行固件操作，网关可以选择为自身以及为其连接的设备构造 `DeviceFirmware` 对象，然后将其添加到 `DeviceData` 对象，如以下样本中所概述：

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

对于连接的设备，构造的 `DeviceData` 对象可以在发送管理请求时传递到库，如以下代码样本中所概述：

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, deviceData, lifetime, supportFirmwareActions, supportDeviceActions);
```

`DeviceFirmware` 对象表示网关或已连接设备的当前固件，并用于向 {{site.data.keyword.iot_short}} 报告固件下载和固件更新操作的状态。如果 `DeviceFirmware` 对象不是由网关构造的，那么库会创建一个空对象，并向 {{site.data.keyword.iot_short}} 报告状态。

### 步骤 2：向服务器通知有关固件操作支持的信息

网关或其连接的设备需要将固件操作标志设置为 true，以便服务器能够发起固件请求。此更改可以通过在管理请求中传递 `supportFirmwareActions` 参数值 true 来实现。

网关可以调用以下方法向服务器通知有关其固件支持的信息：
```java
managedGateway.sendGatewayManageRequest(3600, true, false);
```

与此类似，网关可以调用相应的设备方法来通知有关已连接设备的固件支持的信息：

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, deviceData, 3600, true, false);
```

向设备管理服务器通知该支持后，服务器随后会将固件操作转发到网关以用于网关自身或位于网关后面的设备。

### 步骤 3：创建固件操作处理程序

为了支持固件操作，网关需要创建一个处理程序并将其添加到 `managedGateway`。该处理程序必须扩展 `DeviceFirmwareHandler` 类并实现以下方法：

```java
public abstract void downloadFirmware(DeviceFirmware deviceFirmware);
public abstract void updateFirmware(DeviceFirmware deviceFirmware);
```

**注**：只能有一个处理程序添加到库以同时用于将固件下载或更新请求重定向到的网关和已连接设备。该实现必须创建一个线程或线程池，以同时处理多个固件请求。

您可以在[网关样本 GitHub 存储库 ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java){: new_window} 中找到线程池处理程序的样本实现。

### `downloadFirmware` 的样本实现

该实现必须添加逻辑，以使用 `DeviceFirmware` 对象来下载固件并报告下载状态。如果固件下载操作成功，那么固件的状态必须设置为“DOWNLOADED”，并且 `UpdateStatus` 属性必须设置为“SUCCESS”。

如果固件下载期间发生错误，那么状态必须设置为“IDLE”，并且 `updateStatus` 属性必须设置为以下某个错误状态值：

- OUT_OF_MEMORY
- CONNECTION_LOST
- INVALID_URI

样本固件下载实现如以下代码样本中所示：

**重要信息：**提供的代码样本不包括线程池部分。有关固件处理程序的完整实现，[IBM Java 网关样本 GitHub 存储库 ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java){: new_window} 中提供了相应样本。

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

受管网关可以使用验证器来检查下载的固件映像的完整性，并向 {{site.data.keyword.iot_short}} 报告状态。验证器可以由网关在以下阶段中进行设置：

- 在启动期间创建“DeviceFirmware”对象时
- 应用程序提交“downloadFirmware”请求时

#### 示例

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

完整的代码位于 [GatewayFirmwareHandlerSample](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java) 网关管理样本中。

### `updateFirmware` 的样本实现

该实现必须创建单独的线程并添加逻辑，以使用 `DeviceFirmware` 对象来安装下载的固件并报告更新状态。如果固件更新操作成功，那么固件的状态必须设置为“IDLE”，并且 `updateStatus` 值必须设置为“SUCCESS”。

如果固件更新期间发生错误，那么 `updateStatus` 值必须设置为以下某个错误状态值：

* OUT_OF_MEMORY
* UNSUPPORTED_IMAGE

以下代码样本概述了可以如何对 Raspberry Pi 设备实现固件更新：

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

完整的代码位于[网关样本 GitHub 存储库 ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java){: new_window} 中的 `GatewayFirmwareHandlerSample` 样本中。

### 步骤 4：向 `ManagedGateway` 添加处理程序

创建处理程序后，必须将其添加到 `ManagedGateway` 实例，以便有来自 {{site.data.keyword.iot_short}} 的固件操作请求时，Java 客户机库能调用相应的方法。

```java
GatewayFirmwareHandlerSample fwHandler = new GatewayFirmwareHandlerSample();
mgdGateway.addFirmwareHandler(fwHandler);
```

有关固件操作的更多信息，请参阅[设备管理请求 ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://docs.internetofthings.ibmcloud.com/devices/device_mgmt/requests.html#/firmware-actions#firmware-actions){: new_window}。

## 设备操作
{: #dev_actions}

{{site.data.keyword.iot_short}} 支持以下设备操作：

- 重新引导
- 恢复出厂设置

网关必须执行以下活动来支持对其自身以及对位于其后面的设备的设备操作。

1. 向服务器通知有关设备操作支持的信息。
2. 创建设备操作处理程序。
3. 向 `ManagedGateway` 添加处理程序。

### 步骤 1：向服务器通知有关设备操作支持的信息

要对网关及其连接的设备执行重新引导或恢复出厂设置操作，网关必须首先向 {{site.data.keyword.iot_short}} 通知有关该支持的信息。此操作可以通过在发送 **Manage** 请求时传递 `supportDeviceActions` 参数值 true 来执行。

网关可以调用以下方法向服务器通知有关其设备操作支持的信息：

```java
// Last parameter represents the device action support
managedGateway.sendGatewayManageRequest(3600, true, true);
```

网关可以调用相应的设备方法来通知有关已连接设备的设备操作支持的信息：

```java
// Last parameter represents the device action support
managedGateway.sendDeviceManageRequest(typeId, deviceId, 0, true, true);
```

向设备管理服务器通知该支持后，服务器随后会将设备操作请求转发到设备。

### 步骤 2：创建设备操作处理程序

为了支持设备操作，网关需要创建一个处理程序并将其添加到 `managedGateway` 实例。该处理程序必须扩展 `DeviceActionHandler` 类并实现以下方法：

```java
public abstract void handleReboot(DeviceAction action);
public abstract void handleFactoryReset(DeviceAction action);
```

**注**：只能有一个处理程序添加到库以同时用于将设备操作请求重定向到的网关和已连接设备。该实现必须创建一个线程或线程池，以同时处理多个设备操作请求。使用线程池的样本处理程序实现在 [iot-gateway-samplesGitHub 存储库 ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayActionHandlerSample.java){: new_window} 中进行演示。

### `handleReboot` 的样本实现

该实现必须创建单独的线程并添加逻辑，以使用 `DeviceAction` 对象来重新引导网关并报告重新引导的状态。接收到请求后，网关必须先向服务器通知有关该支持或不支持的信息，然后再继续执行实际重新引导。如果样本无法重新引导设备或者在重新引导期间发生其他任何错误，那么网关可以在可选消息中更新状态。以下代码样本中提供了 Raspberry Pi 设备的样本重新引导实现：

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

使用线程池的完整样本处理程序实现在 [iot-gateway-samples GitHub 存储库 ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayActionHandlerSample.java){: new_window} 中进行演示。


### `handleFactoryReset` 的样本实现

该实现必须创建单独的线程并添加逻辑，以使用 DeviceAction 对象将网关和已连接设备恢复到出厂设置并报告恢复状态。接收到请求后，网关需要先向服务器通知有关该支持或不支持的信息，然后再继续执行实际恢复。恢复出厂设置实现的基本概述如以下代码样本中所示：

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

### 步骤 3：向 `ManagedGateway` 添加处理程序

创建处理程序后，必须将其添加到 `ManagedGateway` 实例，以便有来自 {{site.data.keyword.iot_short}} 的针对网关或已连接设备的设备操作请求时，Java 客户机库能调用相应的方法。

```java
GatewayActionHandlerSample actionHandler = new GatewayActionHandlerSample();
mgdGateway.addDeviceActionHandler(actionHandler);
```

有关设备操作的更多信息，请参阅[设备管理请求 ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](../../devices/device_mgmt/requests.html#/device-actions-reboot#device-actions-reboot){: new_window}。

## 设备管理扩展包
{: #dme}

设备管理扩展 (DME) 软件包是一种 JSON 文档，用于定义一组定制设备管理操作。可以在支持这些操作的一个或多个设备上启动这些操作。启动操作的方法是使用 {{site.data.keyword.iot_short}} 仪表板或者设备管理 REST API。

有关 DME 软件包格式的更多信息，请参阅[扩展设备管理](../../devices/device_mgmt/custom_actions.html)。

### 支持定制设备管理操作

扩展包中定义的设备管理操作可以在支持这些操作的网关或者已连接设备上启动。

设备在向 {{site.data.keyword.iot_short}} 发布管理请求时指定自己支持的操作类型。为了让设备能够接收在特定扩展包中定义的定制操作，设备必须在发布管理请求时在支持对象中指定该扩展的捆绑软件标识。

网关可以使用捆绑软件标识的列表来调用 `manage()` API，以通知 {{site.data.keyword.iot_short}} 对于在管理请求中提供的捆绑软件标识列表，网关或已连接设备支持 DME 操作。

以下代码片段用于发布管理请求以通知 {{site.data.keyword.iot_short}} 此网关支持 DME 操作：

```java
List<String> bundleIds = new ArrayList<String>();
bundleIds.add("example-dme-actions-v1");

mgdGateway.sendGatewayManageRequest(0, false, false, bundleIds);
```

最后一个参数指定设备支持的定制操作。

与此类似，网关可以调用相应的设备方法来告知已连接设备所支持的 DME 操作：

```java
List<String> bundleIds = new ArrayList<String>();
bundleIds.add("example-dme-actions-v1");

mgdGateway.sendDeviceManageRequest(typeId, deviceId, 0, false, false, bundleIds);
```

### 处理定制设备管理操作

在网关或已连接到 {{site.data.keyword.iot_short}} 的设备上启动定制操作时，将向该网关发布一条 MQTT 消息。该消息中包含被指定为请求一部分的参数。网关必须添加 CustomActionHandler 才能接收和处理该消息。该消息将作为 `CustomAction` 类的实例返回，并包含下列属性：

| 属性     | 数据类型     | 描述 |
|----------------|----------------|----------------|
|`bundleId` |字符串 | DME 的唯一标识。|
|`actionId` |字符串|被启动的定制操作。|
|`typeId` |字符串|在其上启动定制操作的设备类型。|
|`deviceId` |字符串|在其上启动定制操作的设备。|
|`payload` |字符串|包含 JSON 格式参数列表的实际消息。|
|`reqId` |字符串|用于响应定制操作请求的请求标识。|

以下代码是实施 `CustomActionHandler` 的样本：

```java
import java.util.HashMap;
import java.util.Map;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.LinkedBlockingQueue;

import com.google.gson.JsonArray;
import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.ibm.iotf.client.CustomAction;
import com.ibm.iotf.client.CustomAction.Status;
import com.ibm.iotf.devicemgmt.CustomActionHandler;

public class MyCustomActionHandler extends CustomActionHandler implements Runnable {

	// 用于容纳并处理命令以便顺利处理 MQTT 消息的队列
	private BlockingQueue<CustomAction> queue = new LinkedBlockingQueue<CustomAction>();
	// 用于容纳每个设备的发布时间间隔的映射
	private Map<String, Long> intervalMap = new HashMap<String, Long>();

	@Override
	public void run() {
		while(true) {
			CustomAction action = null;
			try {
				action = queue.take();
				System.out.println(" "+action.getActionId()+ " "+action.getPayload());
				JsonArray fields = action.getPayload().get("d").getAsJsonObject().get("fields").getAsJsonArray();
				for(JsonElement field : fields) {
					JsonObject fieldObj = field.getAsJsonObject();
					if("PublishInterval".equals(fieldObj.get("field").getAsString())) {
						long val = fieldObj.get("value").getAsLong();
						String key = action.getTypeId() + ":" + action.getDeviceId();
						long publishInterval = val * 1000;
						intervalMap.put(key, publishInterval);
						System.out.println("Updated the publish interval to "+val);
					}
				}
				action.setStatus(Status.OK);

			} catch (InterruptedException e) {}
		}
	}

	public long getPublishInterval(String deviceType, String deviceId) {
		String key = deviceType + ":" + deviceId;
		Long val = intervalMap.get(key);
		if(val == null) {
			return 1000; // default is 1 second
		} else {
			return val.longValue();
		}
	}

	@Override
	public void handleCustomAction(CustomAction action) {
		try {
			queue.put(action);
			} catch (InterruptedException e) {
		}

	}
}
```

将 `CustomActionHandler` 添加到 `ManagedGateway` 实例之后，只要应用程序启动了任何操作，就会调用 `handleCustomAction()` 方法。

以下代码样本概述了如何将 `CustomActionHandler` 添加到 `ManagedGateway` 实例。

```java
MyCustomActionHandler handler = new MyCustomActionHandler();
mgdGateway.addCustomActionHandler(handler);
```

网关在接收定制操作消息后，会完成该操作，或者以表明无法完成该操作的错误代码做出响应。网关必须使用 *setStatus()* 方法来设置操作状态：

```java
action.setStatus(Status.OK);
```

有关 DME 的更多信息，请参阅[扩展设备管理请求 ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](../../devices/device_mgmt/custom_actions.html){: new_window}。

## 侦听设备属性更改
{: #listen_device_attributes}

每当有来自 {{site.data.keyword.iot_short}} 的更新请求时，Java 客户机库都会更新相应的对象。这些更新请求由应用程序直接发起或使用 {{site.data.keyword.iot_short}} REST API 通过固件更新间接发起。除了更新这些属性外，该库还提供一种机制，使得每当更新设备属性时，都能通知网关。

可以由此类型操作更新的属性是网关或已连接设备的位置、元数据、设备信息和固件。

要收到有关属性更改的通知，网关必须向其关注的对象添加属性更改侦听器，如以下代码样本中所概述：

```java
deviceLocation.addPropertyChangeListener(listener);
firmware.addPropertyChangeListener(listener);
deviceInfo.addPropertyChangeListener(listener);
metadata.addPropertyChangeListener(listener);
```

此外，网关还必须实现用于接收通知的 `propertyChange()` 方法，如以下样本实现中所概述：

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

有关更新设备属性的更多信息，请参阅[设备管理请求 ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://docs.internetofthings.ibmcloud.com/devices/device_mgmt/index.html#/update-device-attributes#update-device-attributes){: new_window}。

## 样本
{: #samples}

有多个样本可帮助您将网关和位于网关后面的设备连接到您的 {{site.data.keyword.iot_short_notm}} 实例。这些样本使用 {{site.data.keyword.iot_short_notm}} Java 客户机库，并位于[网关样本 GitHub 存储库 ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples){: new_window} 中。

## 诀窍
{: #recipes}

有关显示如何将 Rasberry Pi 设备作为受管网关连接到 {{site.data.keyword.iot_short_notm}} 并管理已连接设备的诀窍，请参阅 [Raspberry Pi as a managed gateway in {{site.data.keyword.iot_short_notm}} ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/){: new_window}。

此诀窍说明了可以如何使用 {{site.data.keyword.iot_short_notm}} 的设备管理协议从充当网关的 Raspberry Pi 设备来管理 Arduino Uno 设备以及执行设备管理操作，例如重新引导设备或添加最简单的程序。
