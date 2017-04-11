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

# 使用 Java 開發受管理裝置
{: #java_deviceManagement}

##簡介
{: #introduction}

在 {{site.data.keyword.iot_full}} 中，受管理裝置是可執行裝置管理作業（例如韌體、位置及診斷更新）的裝置。
使用 {{site.data.keyword.iot_short}} Java™ 用戶端程式庫以及所提供的資訊，您可以開發將連接的裝置轉換成受管理裝置的 Java 程式碼。我們也會提供範例，以協助您開發將裝置連接至「裝置管理」服務以及執行裝置管理作業的 Java 程式碼。

如需應用程式如何使用 Java 用戶端程式庫以與裝置互動的相關資訊，請參閱[適用於應用程式開發人員的 Java](../../applications/libraries/java.html)。

## 裝置管理
{: #device_management}

[裝置管理](../reference/device_mgmt.html)功能透過管理裝置的其他功能來加強 {{site.data.keyword.iot_short_notm}} 服務。裝置管理會區別受管理與未受管理的裝置：

-   **受管理裝置**定義為已安裝管理代理程式的裝置。管理代理程式會傳送及接收裝置 meta 資料，並回應來自 {{site.data.keyword.iot_short_notm}} 的裝置管理指令。
-   **未受管理裝置**是任何沒有裝置管理代理程式的裝置。所有裝置在生命週期開始時都是未受管理裝置，並且可以透過將裝置管理代理程式中的訊息傳送至 {{site.data.keyword.iot_short_notm}}，來轉移為受管理裝置。

## 連接至 {{site.data.keyword.iot_short_notm}} Device Management 服務
{: #connecting_dm_service}

## 建立裝置資料
{: #creating_device_data}

[裝置機型](../reference/device_model.html)說明裝置的 meta 資料及管理性質。{{site.data.keyword.iot_short_notm}} 中的裝置資料庫是裝置資訊的主要來源。應用程式和受管理裝置能夠將更新傳送至資料庫，例如位置或「韌體更新」的進度。{{site.data.keyword.iot_short_notm}} 收到這些更新之後，就會更新裝置資料庫，而應用程式就能使用該資訊。

`DeviceData` 是 ibmiotf 用戶端程式庫中的裝置機型，包括下列物件：

-   DeviceInfo（必要）
-   DeviceLocation（如果裝置支援位置更新，則為必要）
-   DiagnosticErrorCode（如果裝置要更新 ErrorCode，則為必要）
-   DiagnosticLog（如果裝置要更新「日誌」資訊，則為必要）
-   DeviceFirmware（如果裝置支援「韌體動作」，則為必要）
-   DeviceMetadata（選用）

下列程式碼範例顯示如何利用範例資料，建立必要的 `DeviceInfo` 物件及選用性的 `DeviceMetadata` 物件：

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

使用下列程式碼範例來建立 `DeviceData` 物件，其中包含您在前一個範例中建立的 `DeviceInfo` 及 `DeviceMetadata` 物件。

  ```
  DeviceData deviceData = new DeviceData.Builder().
               deviceInfo(deviceInfo).
               metadata(metadata).
               build();
  ```

## 建構 ManagedDevice
{: #construct_managed_device}

`ManagedDevice` 是一種裝置類別，可將裝置當作受管理裝置連接至 {{site.data.keyword.iot_short_notm}}，並讓裝置可以執行一個以上的裝置管理作業。您也可以使用 `ManagedDevice` 實例來執行一般裝置作業，例如發佈裝置事件及接聽來自應用程式的指令。

`ManagedDevice` 會顯示下列建構子，支援不同的使用者型樣：

**建構子一**

「建構子一」會在 {{site.data.keyword.iot_short_notm}} 中建構 `ManagedDevice` 實例，方法為接受 `DeviceData` 及所有下列必要內容：

|內容 |說明 |
|:---|:---|
|`Organization-ID` |您的組織 ID|
|`Device-Type` |您的裝置類型。一般而言，deviceType 是執行特定作業的裝置分組，例如，"weatherballoon"。|
|`Device-ID` |您的裝置 ID。一般而言，針對給定的裝置類型，deviceId 是該裝置的唯一 ID（例如，序號或 MAC 位址）。|
|`Authentication-Method` |要使用的鑑別方法。目前唯一支援的值是 `token`。|
|`Authentication-Token` |將裝置安全地連接至 Watson IoT Platform 的鑑別記號。|


下列程式碼概述如何建立 `ManagedDevice` 實例。

```
Properties options = new Properties();
options.setProperty("Organization-ID", "uguhsp");
options.setProperty("Device-Type", "iotsample-arduino");
options.setProperty("Device-ID", "00aabbccde03");
options.setProperty("Authentication-Method", "token");
options.setProperty("Authentication-Token", "AUTH TOKEN FOR DEVICE");

ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
```

如果已使用 `DeviceClient` 實例，您將注意到內容的名稱略有不同，而且會鏡映 {{site.data.keyword.iot_short_notm}} 儀表板中的名稱。若要從 `DeviceClient` 移轉至 `ManagedDevice`，您可以建構 `ManagedDevice` 實例來繼續使用早期格式，如下列範例所概述：

```
Properties options = new Properties();
options.setProperty("org", "uguhsp");
options.setProperty("type", "iotsample-arduino");
options.setProperty("id", "00aabbccde03");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");
ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
```

**建構子二**

同時接受 `DeviceData` 及 `MqttClient` 實例，來建構 `ManagedDevice` 實例。此建構子需要您使用其他裝置屬性（如「裝置類型」及「裝置 ID」）來建立 `DeviceData`，如下列範例所概述：

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

**附註：**此建構子可協助自訂裝置使用者，使用已建立及已連接的 `MqttClient` 實例來建立 `ManagedDevice` 實例，以充分運用裝置管理作業。但是，對於所有裝置功能，我們建議使用者使用程式庫。

## 管理

`Manage` 裝置可以呼叫 manage() 方法來參與裝置管理活動。如果裝置尚未連接至 {{site.data.keyword.iot_short_notm}}，則管理要求會在內部起始連接要求。

```
managedDevice.manage();
```

裝置可以使用超載管理 (lifetime) 方法，為給定的時間範圍登錄裝置。時間範圍指定時間長度，裝置必須在這段時間內傳送另一個**管理裝置**要求，來避免被回復為未受管理裝置並標示為休眠。

```
managedDevice.manage(3600);
```

如需 `Manage` 作業的相關資訊，請參閱 [文件]。

  [documentation]:../device_mgmt/operations/manage.html

## 取消管理

當裝置不再需要管理時，可呼叫 unmanage() 方法。{{site.data.keyword.iot_short_notm}} 將不再傳送新的裝置管理要求至此裝置，而且來自此裝置的所有裝置管理要求都將遭到拒絕，但**管理裝置**要求除外。

```
managedDevice.unmanage();
```

如需 `Unmanage` 作業的相關資訊，請參閱 [文件]。

  [documentation]:../device_mgmt/operations/manage.html

## 位置更新
{: #construct_location_update}
可以判定其位置的裝置可以選擇將位置變更通知 {{site.data.keyword.iot_short_notm}}。為了更新位置，裝置需要先使用 `DeviceLocation` 物件來建立 `DeviceData` 實例。

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

當裝置連接至 {{site.data.keyword.iot_short_notm}} 時，您可以使用下列方法來更新位置：

```
int rc = deviceLocation.sendLocation();
if(rc == 200) {
        System.out.println("Current location (" + deviceLocation.toString() + ")");
} else {
            System.err.println("Failed to update the location");
}
```

對於裝置位置的後續更新，可以藉由修改 `DeviceLocation` 物件的內容來進行，如下列範例所概述：

```
int rc = deviceLocation.update(40.28, -98.33, 11);
if(rc == 200) {
    System.out.println("Current location (" + deviceLocation.toString() + ")");
} else {
    System.err.println("Failed to update the location");
}
```

update() 方法會將新位置通知 {{site.data.keyword.iot_short_notm}}。

如需更新位置的相關資訊，請參閱鏈結的[文件](../device_mgmt/operations/update.html)。



## 附加及清除錯誤碼
{: #appending_error_codes}

裝置可以選擇將其錯誤狀態中的變更通知 {{site.data.keyword.iot_short_notm}}。為了傳送錯誤碼，裝置需要建構 `DiagnosticErrorCode` 物件，如下列範例所概述：

```
DiagnosticErrorCode errorCode = new DiagnosticErrorCode(0);

DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceErrorCode(errorCode).
             metadata(metadata).
             build();
```

裝置一連接至 {{site.data.keyword.iot_short_notm}} 後，就可以呼叫 send() 方法來傳送 `ErrorCode`，如下所示：

```
errorCode.send();
```

稍後，可以呼叫 append 方法，將任何新的 `ErrorCode` 輕鬆地新增至 {{site.data.keyword.iot_short_notm}}，如下所示：

```
int rc = errorCode.append(500);
if(rc == 200) {
    System.out.println("Current Errorcode (" + errorCode + ")");
} else {
    System.out.println("Errorcode addition failed!");
}
```

同時，也可以呼叫 clear() 方法，從 {{site.data.keyword.iot_short_notm}} 中清除 `ErrorCodes`，如下所示：

```
int rc = errorCode.clear();
if(rc == 200) {
    System.out.println("ErrorCodes are cleared successfully!");
} else {
    System.out.println("Failed to clear the ErrorCodes!");
}
```

## 附加及清除日誌訊息

裝置可以選擇新增日誌項目，以將變更通知 {{site.data.keyword.iot_short_notm}}。日誌項目包含下列資訊：
- 日誌訊息
- 時間戳記
- 嚴重性
- base64 編碼的二進位診斷資料（選用）

為了傳送日誌訊息，裝置需要建構 `DiagnosticLog` 物件，如下列範例所概述：

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

裝置一連接至 {{site.data.keyword.iot_short_notm}} 後，就可以呼叫 send() 方法來傳送日誌訊息，如下列範例所概述：

```
log.send();
```

或者，可以呼叫 append 方法，將任何新的日誌訊息輕鬆地新增至 {{site.data.keyword.iot_short_notm}}，如下列範例所概述：

```
int rc = log.append("sample log", new Date(), DiagnosticLog.LogSeverity.informational);

if(rc == 200) {
    System.out.println("Current Log (" + log + ")");
} else {
    System.out.println("Log Addition failed");
}
```

同時，也可以呼叫 clear 方法，清除 {{site.data.keyword.iot_short_notm}} 中的日誌訊息，如下列範例所概述：

```
rc = log.clear();
if(rc == 200) {
    System.out.println("Logs are cleared successfully");
} else {
    System.out.println("Failed to clear the Logs")
}
```

裝置診斷作業旨在提供裝置錯誤的相關資訊，因此不會提供與 {{site.data.keyword.iot_short_notm}} 之裝置連線相關的診斷資訊。

如需「診斷」作業的相關資訊，請參閱[文件](../device_mgmt/operations/diagnostics.html)。

## 韌體動作
{: #firmware_actions}

「韌體更新」程序分成兩個不同的動作：

* 下載韌體
* 更新韌體

裝置需要執行下列活動，才能支援韌體動作：

**1. 建構 DeviceFirmware 物件**

為了執行韌體動作，裝置需要建構 `DeviceFirmware` 物件，並將它新增至 `DeviceData`，如下所示：

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

`DeviceFirmware` 物件代表裝置的現行韌體，而且將用來向 {{site.data.keyword.iot_short_notm}} 報告韌體下載及「韌體更新」動作的狀態。

**2. 將「韌體」動作支援通知伺服器**

裝置需要將韌體動作旗標設為 true，伺服器才能起始韌體要求。以布林值呼叫下列方法，即可達成此作業：

```
managedDevice.supportsFirmwareActions(true);
managedDevice.manage();
```

當管理要求通知 {{site.data.keyword.iot_short_notm}} 韌體動作支援相關事宜時，在設定韌體動作支援之後，需要立即呼叫 manage() 方法。

**3. 建立韌體動作處理程式**

為了支援「韌體」動作，裝置需要建立一個處理程式，並將其新增至 `ManagedDevice`。處理程式必須擴充 `DeviceFirmwareHandler` 類別，並實作下列方法：

```
public abstract void downloadFirmware(DeviceFirmware deviceFirmware);
public abstract void updateFirmware(DeviceFirmware deviceFirmware);
```

**3.1 downloadFirmware 的範例實作**

實作必須新增邏輯，以使用 `DeviceFirmware` 物件，下載韌體並報告下載的狀態。如果韌體下載作業成功，則狀態會設為 `DOWNLOADED`，然後 `UpdateStatus` 會設為 `SUCCESS`。

如果韌體下載期間發生錯誤，則狀態會設為 `IDLE`，然後 `updateStatus` 會設為下列其中一個錯誤狀態值：

* `OUT_OF_MEMORY
* CONNECTION_LOST
* INVALID_URI`

下列範例概述 Raspberry Pi 裝置的韌體下載實作：

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

裝置可以使用驗證器，檢查已下載韌體映像檔的完整性，並將狀態回報給 {{site.data.keyword.iot_short_notm}}。驗證器可由裝置在啟動期間（建立「DeviceFirmware 物件」時）進行設定，或者由應用程式當作「下載韌體」要求的一部分進行設定。驗證相同的範例程式碼如下：

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

如需整個程式碼，請參閱 [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java) 裝置管理範例。



**3.2 updateFirmware 的範例實作**

實作必須新增邏輯，透過 `DeviceFirmware` 物件安裝已下載的韌體，並報告更新的狀態。如果「韌體更新」作業成功，則韌體的狀態應該設為 IDLE，而且 `updateStatus` 應該設為 `SUCCESS`。

如果「韌體更新」期間發生錯誤，則 `updateStatus` 應設為其中一個錯誤狀態值：

`* OUT_OF_MEMORY
* UNSUPPORTED_IMAGE`

下面顯示 Raspberry Pi 裝置的「韌體更新」實作範例：

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

您可在裝置管理範例 [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java) 中找到完整程式碼。


**4. 將處理程式新增至 ManagedDevice**

已建立的處理程式需要新增至 ManagedDevice 實例，以便在有一個來自 {{site.data.keyword.iot_short_notm}} 的「韌體」動作要求時，ibmiotf 用戶端程式庫會呼叫對應方法。

```
DeviceFirmwareHandlerSample fwHandler = new DeviceFirmwareHandlerSample();
deviceData.addFirmwareHandler(fwHandler);
```

如需「韌體」動作的相關資訊，請參閱[此頁面](../device_mgmt/operations/firmware_actions.html)。

## 裝置動作

{{site.data.keyword.iot_short_notm}} 支援下列裝置動作：

* 重新開機
* 重設為原廠設定

裝置需要執行下列活動，才能支援「裝置動作」：

**1. 將「裝置動作」支援通知伺服器**

為了執行「重新開機」及「重設為原廠設定」，裝置首先需要將其支援通知 {{site.data.keyword.iot_short_notm}}。以布林值呼叫下列方法，即可達成此作業：

```
managedDevice.supportsDeviceActions(true);
    managedDevice.manage();
```

當管理要求通知 {{site.data.keyword.iot_short_notm}} 裝置動作支援相關事宜時，在設定裝置動作支援之後，需要立即呼叫 manage() 方法。

**2. 建立裝置動作處理程式**

為了支援裝置動作，裝置需要建立一個處理程式，並將其新增至 ManagedDevice。處理程式必須擴充 DeviceActionHandler 類別，並提供下列方法的實作：

```
public abstract void handleReboot(DeviceAction action);
public abstract void handleFactoryReset(DeviceAction action);
```

**2.1 handleReboot 的範例實作**

實作必須新增邏輯，透過 DeviceAction 物件重新開啟裝置，並報告重新開機的狀態。只有在發生失敗時，裝置才需要更新狀態以及選用性訊息（因為成功作業會將裝置重新開機，而且裝置程式碼將沒有控制權可更新 {{site.data.keyword.iot_short_notm}}）。下面顯示 Raspberry Pi 裝置的重新開機實作範例：

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

您可在裝置管理範例 [DeviceActionHandlerSample] 中找到完整程式碼。

  [DeviceActionHandlerSample]: https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceActionHandlerSample.java

**2.2 handleFactoryReset 的範例實作**

實作必須新增邏輯，透過 DeviceAction 物件將裝置重設為原廠設定，並報告狀態。只有在發生失敗時，裝置才需要更新狀態以及選用性訊息（因為在此過程中，裝置會重新開機，而且裝置程式碼將沒有控制權可更新 {{site.data.keyword.iot_short_notm}} 的狀態）。「重設為原廠設定」實作的架構如下所示：

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

**3. 將處理程式新增至 ManagedDevice**

已建立的處理程式需要新增至 ManagedDevice 實例，以便在有一個來自 {{site.data.keyword.iot_short_notm}} 的裝置動作要求時，ibmiotf 用戶端程式庫會呼叫對應方法。

```
DeviceActionHandlerSample actionHandler = new DeviceActionHandlerSample();
deviceData.addDeviceActionHandler(actionHandler);
```

如需「裝置動作」的相關資訊，請參閱[此頁面](../device_mgmt/operations/device_actions.html)。



## 接聽裝置屬性變更
{: #listen_device_attribute}

每當有一個來自 {{site.data.keyword.iot_short_notm}} 的更新要求，此 ibmiotf 用戶端程式庫即會更新對應物件。這些更新要求是由應用程式透過 {{site.data.keyword.iot_short_notm}} REST API 直接或間接（韌體更新）起始。除了更新這些屬性之外，程式庫所提供的機制還包含在更新裝置屬性時通知裝置。

此作業可以更新的屬性為 `location`、`metadata`、`device information` 及 `firmware`。

若要接獲通知，裝置必須在感興趣的物件上新增內容變更接聽器。

```
deviceLocation.addPropertyChangeListener(listener);
firmware.addPropertyChangeListener(listener);
deviceInfo.addPropertyChangeListener(listener);
metadata.addPropertyChangeListener(listener);
```

此外，裝置也需要在其接收通知的位置實作 `propertyChange()` 方法。下列範例概述如何實作此作業：

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

如需更新裝置屬性的相關資訊，請參閱[此頁面](../device_mgmt/operations/update.html)。

## 範例
{: #examples}

-   [SampleRasPiDMAgent](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgent.java) - 顯示如何在 Raspberry Pi 上執行各種裝置管理作業的範例代理程式碼。
-   [SampleRasPiManagedDevice](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiManagedDevice.java) - 顯示如何同時執行裝置作業及管理作業的範例程式碼。
-   [SampleRasPiDMAgentWithCustomMqttAsyncClient](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgentWithCustomMqttAsyncClient.java) - 搭配自訂 MqttAsyncClient 的範例代理程式碼。
-   [SampleRasPiDMAgentWithCustomMqttClient](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgentWithCustomMqttClient.java) - 搭配自訂 MqttClient 的範例代理程式碼。
-   [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java) - Raspberry Pi 之 FirmwareHandler 的範例實作。
-   [DeviceActionHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceActionHandlerSample.java) - DeviceActionHandler 的範例實作。
-   [ManagedDeviceWithLifetimeSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/ManagedDeviceWithLifetimeSample.java) - 此範例顯示如何在指定生命期限的情況下傳送一般管理要求。
-   [DeviceAttributesUpdateListenerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceAttributesUpdateListenerSample.java) - 顯示如何接聽各種裝置屬性變更的範例接聽器程式碼。
-   [NonBlockingDiagnosticsErrorCodeUpdateSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/NonBlockingDiagnosticsErrorCodeUpdateSample.java) - 此範例顯示如何新增 ErrorCode，而無需等待來自伺服器的回應。

##秘訣
{: #Recipes}

請參閱顯示如何將 Raspberry Pi 裝置當作受管理裝置連接至 {{site.data.keyword.iot_short_notm}} 的[秘訣](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-managed-device-to-ibm-iot-foundation/)，以使用此用戶端程式庫逐步執行各種裝置管理作業。
