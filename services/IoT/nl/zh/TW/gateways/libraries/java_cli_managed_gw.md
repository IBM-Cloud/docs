---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 使用 Java 開發受管理閘道
{: #java_cli_managed_gw}

閘道扮演管理與其連接的裝置的重要角色。許多裝置都十分基本而且沒有裝置管理功能，因此需要從閘道管理這些基本裝置。在 {{site.data.keyword.iot_full}} 中，受管理閘道是可管理與其連接的裝置的閘道，並提供裝置管理功能（例如韌體、位置及診斷更新）。
{:shortdesc}

使用 {{site.data.keyword.iot_short}} Java™ 用戶端程式庫以及所提供的資訊，您可以開發將閘道轉換成受管理閘道的 Java 程式碼。我們也會提供範例，以協助您開發將閘道連接至「裝置管理」服務以及執行裝置管理作業的 Java 程式碼。

## 裝置管理服務
{: #dm_service}

「{{site.data.keyword.iot_short}} 裝置管理 (DM)」服務提供裝置管理功能，以讓閘道管理與其連接的裝置。

受管理閘道會執行裝置管理代理程式，而裝置管理代理程式是當作透過閘道連接至 {{site.data.keyword.iot_short}} 的所有裝置的 Proxy 來執行。

### 裝置管理代理程式

如果閘道裝置支援各種連線通訊協定，則透過閘道間接連接至 {{site.data.keyword.iot_short}} 的裝置就可以使用這些連線通訊協定。

`ManagedGateway` 實例是裝置管理代理程式，提供一份執行一個以上裝置管理動作的方法清單（例如，參與裝置管理活動，更新錯誤碼、日誌、位置及韌體或裝置的動作）。

閘道上的裝置管理代理程式會轉換及處理連接裝置的連線通訊協定，以確保 {{site.data.keyword.iot_short}} 可以管理裝置。透過裝置管理代理程式，閘道就不只是所連接裝置與 {{site.data.keyword.iot_short}} 之間的透通通道。例如，如果連接至閘道的裝置無法下載韌體，則閘道上的裝置管理代理程式可以執行下列動作：
- 截取裝置下載韌體的要求
- 下載裝置的韌體
- 將裝置韌體儲存在閘道上

在稍後的復原點，指示裝置執行升級時，閘道上的裝置管理代理程式可以將韌體推送至裝置，並進行更新。

## 建立裝置模型
{: #create_device_model}

在 {{site.data.keyword.iot_short}} 中，裝置機型說明裝置及閘道的 meta 資料及管理性質。裝置資料庫是裝置或閘道資訊的主要來源。應用程式及受管理裝置可以傳送位置更新、韌體升級進度更新，以及其他類型的更新。{{site.data.keyword.iot_short}} 收到更新之後，就會更新裝置資料庫，讓連接應用程式可以使用該資訊。

在 {{site.data.keyword.iot_short}} Java 用戶端程式庫中，以 `DeviceData` Java 類別代表裝置機型。

若要建立 `DeviceData` 類別，請建立下列物件：

- `DeviceInfo`（選用）
- `DeviceLocation`（選用，只有在想要通知裝置有關應用程式透過 {{site.data.keyword.iot_short}} API 所設定的位置時才是必要項目）
- `DeviceFirmware`（選用）
- `DeviceMetadata`（選用）

如需相關資訊，請參閱[裝置機型](../../reference/device_model.html)。

### DeviceInfo

下列包含取樣資料的程式碼 Snippet 顯示如何建立 `DeviceInfo` 及 `DeviceMetadata` 物件：

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

下列程式碼 Snippet 概述如何使用前一個範例中所建立的 `DeviceInfo` 及 `DeviceMetadata` 物件來建立 `DeviceData` 類別：

```java
DeviceData deviceData = new DeviceData.Builder().
                         deviceInfo(deviceInfo).
            metadata(metadata).
            build();
```

每個閘道及每個連接的裝置都必須有自己的 `DeviceData` 類別定義，以在 {{site.data.keyword.iot_short}} 中代表它自己。對於閘道，`DeviceData` 類別是在建構 `ManagedGateway` 實例時傳遞至程式庫。對於連接的裝置，`DeviceData` 類別會傳遞至程式庫，以作為 `sendDeviceManageRequest()` 物件的一部分。

## ManagedGateway 建構子
{: #construct_managed_gateway}

`ManagedGateway` 是一種 Java 類別，可將閘道連接至 {{site.data.keyword.iot_short}}，以作為可針對本身或連接的裝置執行至少一個裝置管理作業的受管理閘道。`ManagedGateway` 實例也可以用來執行一般閘道作業，例如，發佈閘道事件、連接裝置事件，以及接聽來自應用程式的指令。`ManagedGateway` 實例是一個裝置管理代理程式。

在 `ManagedGateway` 類別中，兩個不同的建構子（「建構子一」及「建構子二」）支援不同的使用者型樣。

### 建構子一

「建構子一」藉由接受包含所有下列內容的 `DeviceData` 類別來建構 `ManagedGateway` 實例：

| 內容     |說明     |
|----------------|----------------|
|`Organization-ID` |您的組織 ID。|
|`Gateway-Type` |閘道裝置的類型。|
|`Gateway-ID` |閘道裝置的 ID。|
|`Authentication-Method`|鑑別方法。唯一支援的方法是 "token"。|
|`Authentication-Token`|API 金鑰記號。|
|`auth-key`   |選用性的 API 金鑰，當 auth-method 的值設為 `apikey` 時必須指定的項目。|
|`auth-token`   |API 金鑰記號，當 auth-method 的值設為 `apikey` 時也為必要項目。 |
|`clean-session`|true 或 false 值，只有在要以可延續訂閱模式連接閘道時才是必要項目。`clean-session` 預設為 `true`。|
|`Port`|要連接至的埠號。指定 8883 或 443。如果您未指定埠號，則用戶端預設會透過埠號 8883 連接至 {{site.data.keyword.iot_short_notm}}。|
|`WebSocket`|true 或 false 值，只有在要使用 Websocket 連接閘道時才是必要項目。|
|`MaxInflightMessages`  |設定連線的進行中訊息數目上限。預設值為 100。|
|`Automatic-Reconnect`  |true 或 false 值，要將處於斷線狀態的裝置自動重新連接至 {{site.data.keyword.iot_short_notm}} 時為必要項目。預設值為 false。|
|`Disconnected-Buffer-Size`|用戶端斷線時，可以儲存在記憶體中的訊息數目上限。預設值為 5000。|

**附註：**若要以可延續訂閱模式連接閘道，請將 `clean-session` 設為 `false`。如需 `clean-session` 內容的相關資訊，請參閱 [MQTT 文件](../../reference/mqtt/index.html#subscription-buffers-and-clean-session)的「訂閱緩衝區及全新階段作業」一節。

下列程式碼概述如何建立 `ManagedGateway` 實例：

```java
Properties options = new Properties();
options.setProperty("Organization-ID", "uguhsp");
options.setProperty("Gateway-Type", "iotsample-arduino");
options.setProperty("Gateway-ID", "00aabbccde03");
options.setProperty("Authentication-Method", "token");
options.setProperty("Authentication-Token", "AUTH TOKEN FOR DEVICE");

ManagedGateway ManagedGateway = new ManagedGateway(options, deviceData);
```

### 建構子二

「建構子二」藉由接受 `DeviceData` 物件及 MQTT 用戶端實例來建構 `ManagedGateway` 實例。「建構子二」也需要實例中的 `DeviceData` 物件包括裝置類型及裝置 ID，如下列程式碼範例所概述：

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

**附註：**如果您針對自訂裝置進行開發，請使用「建構子二」，因為此建構子會使用現有已連接的 MQTT 用戶端實例來建立受管理閘道實例，讓您可以利用裝置管理作業。請使用 Java 用戶端程式庫進行所有裝置功能。

## 閘道的裝置管理要求
{: #dm_requests}

### 從閘道傳送管理要求

若要指示閘道參與裝置管理活動，請呼叫 `sendGatewayManageRequest()` 方法，如下列程式碼範例所概述：

```java
managedGateway.sendGatewayManageRequest(0, true, true);
```
如果裝置尚未連接至 {{site.data.keyword.iot_short}}，則管理要求會在內部起始連接要求。

`sendGatewayManageRequest()` 方法接受下列參數：

| 參數     |說明     |
|----------------|----------------|
|`lifetime`|時間長度（以秒為單位），閘道必須在這段時間內傳送另一個管理裝置類型要求，才能避免被分類為休眠以及變成未受管理裝置。如果省略 `lifetime` 欄位，或設為 0，則受管理閘道不會變成休眠。`lifetime` 欄位的最低支援設定是 3600 秒（1 小時）。|
|`supportFirmwareActions`|true 或 false 值，決定閘道是否支援韌體動作。閘道也必須新增韌體處理程式來處理韌體要求。|
|`supportDeviceActions`|true 或 false 值，決定閘道是否支援裝置動作。閘道也必須新增裝置動作處理程式來處理重新開機及重設為原廠設定要求。|


`ManagedGateway` 實例是裝置管理代理程式，提供一份執行一個以上裝置管理動作的方法清單（例如，參與裝置管理活動，更新錯誤碼、日誌、位置及韌體或裝置的動作）。

### 從連接的裝置傳送管理要求

若要容許透過閘道連接的裝置參與閘道上的裝置管理活動，請呼叫 `sendDeviceManageRequest()` 方法。

`sendDeviceManageRequest()` 方法會接受連接的裝置以及 `lifetime`、`supportFirmwareActions` 及 `supportDeviceActions` 參數的詳細資料。閘道也可以使用超載的 `sendDeviceManageRequest()` 方法來定義連接的裝置的 `DeviceData` 物件。

#### 從連接的裝置傳送管理要求的範例

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, lifetime, true, true);
```

### 從閘道傳送取消管理要求

不再需要管理閘道時，若要停止閘道上的裝置管理活動，請呼叫 `sendGatewayUnmanageRequet()` 方法。呼叫 `sendGatewayUnmanageRequet()` 時，{{site.data.keyword.iot_short}} 不會再傳送閘道的任何新裝置管理要求，並拒絕所有來自閘道的裝置管理要求，但**管理**要求除外。不會拒絕來自閘道後方的裝置的要求。

#### 從閘道傳送取消管理要求的範例

```java
managedGateway.sendGatewayUnmanageRequet();
```

### 從連接的裝置傳送取消管理要求

不再需要管理閘道後方的裝置時，若要將連接的裝置從受管理狀態移至未受管理狀態，則閘道可以呼叫 `sendDeviceUnmanageRequet()` 方法。呼叫 `sendDeviceUnmanageRequet()` 時，{{site.data.keyword.iot_short}} 不會再傳送裝置的新裝置管理要求，並拒絕所有來自閘道且適用於連接的裝置的裝置管理要求，但**管理**要求除外。

#### 從連接的裝置傳送取消管理要求的範例

```java
managedGateway.sendDeviceUnmanageRequet();
```

## 位置更新項目
{: #location_updates}

### 傳送閘道位置更新

可判定其位置的閘道可以選擇將位置變更通知 {{site.data.keyword.iot_short}}。閘道可以呼叫其中一個超載的 `updateLocation()` 方法來更新裝置的位置。

```java
    // update the location with latitude, longitude, and elevation.
int rc = managedGateway.updateGatewayLocation(30.28565, -97.73921, 10);
if(rc == 200) {
    System.out.println("Location updated successfully!");
} else {
System.err.println("Failed to update the location!");
    }
```

### 傳送連接的裝置位置更新

閘道可以呼叫對應的 `updateDeviceLocation()` 裝置方法來更新連接的裝置的位置。超載方法可以用來指定 `measuredDateTime` 方法。  

```java
// update the location of the attached device with latitude, longitude, and elevation
int rc = managedGateway.updateDeviceLocation(typeId, deviceId, 30.28565, -97.73921, 10);
```
如需位置更新的相關資訊，請參閱[裝置管理要求](../../devices/device_mgmt/index.html#/update-location#update-location)。

## 錯誤碼處理
{: #errors}

### 建立及刪除閘道錯誤碼

閘道可以選擇將其錯誤狀態變更通知 {{site.data.keyword.iot_short}}。閘道可以呼叫 `addErrorCode()` 方法，以將現行錯誤碼新增至 {{site.data.keyword.iot_short}}。

```java
int rc = managedGateway.addGatewayErrorCode(300);
```

呼叫 `clearErrorCodes()` 方法，即可從 {{site.data.keyword.iot_short}} 中清除閘道的錯誤碼，如下所示：

```java
int rc = managedGateway.clearGatewayErrorCodes();
```

### 建立及刪除連接的裝置的錯誤碼

閘道也可以呼叫對應的裝置方法，以新增或清除連接的裝置的錯誤碼：

```java
int rc = managedGateway.addDeviceErrorCode(typeId, deviceId, 300);
rc = managedGateway.clearDeviceErrorCodes(typeId, deviceId);
```

### 建立及刪除閘道日誌訊息

閘道可以選擇將新增日誌項目的變更通知 {{site.data.keyword.iot_short}}。日誌項目包括下列項目：

- 訊息字串
- 時間戳記
- 嚴重性
- 選用性 base64 編碼的二進位診斷資料

閘道可以呼叫 `addGatewayLog()` 方法來傳送日誌訊息，如下列範例所概述：

```java
// An example Log event
String message = "Firmware Download Progress (%): " + 50;
Date timestamp = new Date();
LogSeverity severity = LogSeverity.informational;
int rc = managedGateway.addGatewayLog(message, timestamp, severity);
```

呼叫 `clearLogs()` 方法，即可從 {{site.data.keyword.iot_short}} 中清除日誌訊息：

```java
rc = managedGateway.clearGatewayLogs();
```

### 建立及刪除連接的裝置的日誌

同樣地，閘道可以呼叫對應的裝置方法來建立或清除連接的裝置的日誌，如下列程式碼範例所概述：

```java

// An example log event:
String message = "Firmware Download Progress (%): " + 50;
Date timestamp = new Date();
LogSeverity severity = LogSeverity.informational;
int rc = managedGateway.addDeviceLog(typeId, deviceId, message, timestamp, severity);
```

若要清除連接的裝置的日誌，請指定連接的裝置的詳細資料來呼叫 `clearDeviceLogs()` 方法，如下列程式碼範例所概述：

```java
int rc = managedGateway.clearDeviceLogs(typeId, deviceId);
```

裝置診斷作業旨在提供閘道或裝置錯誤的相關資訊。它們不會提供有關 {{site.data.keyword.iot_short}} 之裝置連線的診斷資訊。

如需診斷作業的相關資訊，請參閱[裝置管理要求](../../devices/device_mgmt/index.html#/update-location#update-location)。

## 韌體更新項目和動作
{: #firmware}

韌體更新程序分成兩個不同的動作：

- 下載韌體
- 更新韌體

閘道必須執行下列活動，才能支援本身及其連接的裝置的韌體動作：

1. 選用項目：建構 `DeviceFirmware` 物件。
2. 將韌體動作支援通知伺服器。
3. 建立韌體動作處理程式。
4. 將處理程式新增至 `ManagedGateway`。

### 步驟 1：建構 `DeviceFirmware` 物件

若要執行韌體動作，閘道可以選擇性地建構本身及其連接的裝置的 `DeviceFirmware` 物件，然後將它新增至 `DeviceData` 物件，如下列範例所概述：

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

對於連接的裝置，傳送管理要求時，可以將建構的 `DeviceData` 物件傳遞至程式庫，如下列程式碼範例所概述：

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, deviceData, lifetime, supportFirmwareActions, supportDeviceActions);
```

`DeviceFirmware` 物件代表閘道或連接的裝置的現行韌體，而且用來向 {{site.data.keyword.iot_short}} 報告韌體下載及韌體更新動作的狀態。如果閘道未建構 `DeviceFirmware` 物件，則程式庫會建立空的物件，並向 {{site.data.keyword.iot_short}} 報告狀態。

### 步驟 2：將關韌體動作支援通知伺服器

閘道或其連接的裝置需要將韌體動作旗標設為 true，伺服器才能起始韌體要求。在管理要求中傳遞 `supportFirmwareActions` 參數的 true 值，即可達成這項變更。

閘道可以呼叫下列方法，將其韌體支援通知伺服器：
```java
managedGateway.sendGatewayManageRequest(3600, true, false);
```

同樣地，閘道可以呼叫對應的裝置方法來通知連接的裝置的韌體支援：

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, deviceData, 3600, true, false);
```

向裝置管理伺服器通知這項支援時，伺服器接著會將韌體動作轉遞至閘道本身或其後方的裝置的閘道。

### 步驟 3：建立韌體動作處理程式

若要支援韌體動作，閘道需要建立一個處理程式，並將其新增至 `managedGateway`。處理程式必須擴充 `DeviceFirmwareHandler` 類別，並實作下列方法：

```java
public abstract void downloadFirmware(DeviceFirmware deviceFirmware);
public abstract void updateFirmware(DeviceFirmware deviceFirmware);
```

**附註**：只能將一個處理程式新增至閘道及連接的裝置的程式庫，而在閘道及連接的裝置中，會重新導向韌體下載或更新要求。實作必須建立一個執行緒或一個執行緒儲存區來同時處理多個韌體要求。

您可以在[閘道範例 GutHub 儲存庫 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java){: new_window} 中找到 threadpool 處理程式的範例實作。

### `downloadFirmware` 的範例實作

實作必須新增邏輯，以使用 `DeviceFirmware` 物件來下載韌體並報告下載的狀態。如果韌體下載作業成功，則韌體的狀態必須設為 'DOWNLOADED'，而且 `UpdateStatus` 內容必須設為 'SUCCESS'。

如果韌體下載期間發生錯誤，則狀態必須設為 'IDLE'，而且 `updateStatus` 內容必須設為下列其中一個錯誤狀態值：

- OUT_OF_MEMORY
- CONNECTION_LOST
- INVALID_URI

下列程式碼範例顯示範例韌體下載實作：

**重要事項：**提供的程式碼範例不包括執行緒儲存區區段。如需韌體處理程式的完整實作，您可以在 [IBM Java 閘道範例 GitHub 儲存庫 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java){: new_window} 中找到範例。

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

受管理閘道可以使用驗證器來檢查已下載韌體映像檔的完整性，然後將狀態回報給 {{site.data.keyword.iot_short}}。在下列階段期間，閘道可以設定驗證器：

- 建立 'DeviceFirmware' 物件時的啟動期間
- 應用程式提交 'downloadFirmware' 要求時

#### 範例

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

您可以在閘道管理範例 [GatewayFirmwareHandlerSample](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java) 中找到完整程式碼。

### `updateFirmware` 的範例實作

實作必須建立個別執行緒，並新增邏輯，以使用 `DeviceFirmware` 物件來安裝已下載的韌體，並報告更新的狀態。如果韌體更新作業成功，則韌體的狀態必須設為 'IDLE'，而且 `updateStatus` 值必須設為 'SUCCESS'。

如果韌體更新期間發生錯誤，則 `updateStatus` 值必須設為下列其中一個錯誤狀態值：

* OUT_OF_MEMORY
* UNSUPPORTED_IMAGE

下列程式碼範例概述如何實作 Raspberry Pi 裝置的韌體更新：

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

您可以在[閘道範例 GitHub 儲存庫 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java){: new_window} 的 `GatewayFirmwareHandlerSample` 範例中找到完整程式碼。

### 步驟 4：將處理程式新增至 `ManagedGateway`

建立處理程式時，必須將它新增至 `ManagedGateway` 實例，以在有來自 {{site.data.keyword.iot_short}} 的韌體動作要求時，Java 用戶端程式庫會呼叫對應的方法。

```java
GatewayFirmwareHandlerSample fwHandler = new GatewayFirmwareHandlerSample();
mgdGateway.addFirmwareHandler(fwHandler);
```

如需韌體動作的相關資訊，請參閱[裝置管理要求 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.internetofthings.ibmcloud.com/devices/device_mgmt/requests.html#/firmware-actions#firmware-actions){: new_window}。

## 裝置動作
{: #dev_actions}

{{site.data.keyword.iot_short}} 支援下列裝置動作：

- 重新開機
- 重設為原廠設定

閘道必須執行下列活動，才能支援本身及其後方的裝置的裝置動作。

1. 將裝置動作支援通知伺服器。
2. 建立裝置動作處理程式。
3. 將處理程式新增至 `ManagedGateway`。

### 步驟 1：將裝置動作支援通知伺服器

若要執行閘道及其連接的裝置的重新開機或重設為原廠設定的動作，閘道必須先將支援通知 {{site.data.keyword.iot_short}}。傳送 **Manage** 要求時，傳遞 `supportDeviceActions` 參數的 true 值，即可執行此動作。

閘道可以呼叫下列方法，將其裝置動作支援通知伺服器：

```java
// Last parameter represents the device action support
managedGateway.sendGatewayManageRequest(3600, true, true);
```

閘道可以呼叫對應的裝置方法來通知連接的裝置的裝置動作支援：

```java
// Last parameter represents the device action support
managedGateway.sendDeviceManageRequest(typeId, deviceId, 0, true, true);
```

向裝置管理伺服器通知這項支援時，伺服器接著會將裝置動作要求轉遞至裝置。

### 步驟 2：建立裝置動作處理程式

若要支援裝置動作，閘道需要建立一個處理程式，並將其新增至 `managedGateway` 實例。處理程式必須擴充 `DeviceActionHandler` 類別，並提供下列方法的實作：

```java
public abstract void handleReboot(DeviceAction action);
public abstract void handleFactoryReset(DeviceAction action);
```

**附註：**只能將一個處理程式新增至閘道及連接的裝置的程式庫，而在閘道及連接的裝置中，會重新導向裝置動作要求。實作必須建立一個執行緒或一個執行緒儲存區來同時處理多個裝置動作要求。[iot-gateway-samples GitHub 儲存庫 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayActionHandlerSample.java){: new_window} 中示範使用 threadpool 的處理程式實作範例。

### `handleReboot` 的範例實作

實作必須建立個別執行緒，並新增邏輯，以使用 `DeviceAction` 物件將閘道及連接的裝置重新開機，並報告重新開機的狀態。接收要求之後，閘道必須先將支援或失敗通知伺服器，再繼續進行實際重新開機。如果範例無法將裝置重新開機，或在重新開機期間發生任何其他錯誤，則閘道可以更新選用訊息中的狀態。下列程式碼範例提供 Raspberry Pi 裝置的重新開機實作範例：

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

[iot-gateway-samples GitHub 儲存庫 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayActionHandlerSample.java){: new_window} 中示範使用 threadpool 的處理程式實作完整範例。


### `handleFactoryReset` 的範例實作

實作必須建立個別執行緒，並新增邏輯，以使用 DeviceAction 物件將閘道及連接的裝置重設為原廠設定，並報告重設的狀態。接收要求之後，閘道需要先將支援或失敗通知伺服器，再繼續進行實際重設。下列程式碼範例顯示重設為原廠設定實作的基本大綱：

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

### 步驟 3：將處理程式新增至 `ManagedGateway`

建立處理程式時，必須將它新增至 `ManagedGateway` 實例，以在有來自 {{site.data.keyword.iot_short}} 的閘道或連接的裝置的裝置動作要求時，「Java 用戶端」程式庫會呼叫對應的方法。

```java
GatewayActionHandlerSample actionHandler = new GatewayActionHandlerSample();
mgdGateway.addDeviceActionHandler(actionHandler);
```

如需裝置動作的相關資訊，請參閱[裝置管理要求 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](../../devices/device_mgmt/requests.html#/device-actions-reboot#device-actions-reboot){: new_window}。

## 接聽裝置屬性變更
{: #listen_device_attributes}

只要有來自 {{site.data.keyword.iot_short}} 的更新要求，Java 用戶端程式庫即會更新對應的物件。這些更新要求是由應用程式使用 {{site.data.keyword.iot_short}} REST API 透過韌體更新直接或間接起始。除了更新這些屬性之外，程式庫所提供的機制還包含在更新裝置屬性時通知閘道。

這類型作業可更新的屬性是閘道或連接的裝置的位置、meta 資料、裝置資訊及韌體。

若要在屬性變更時接獲通知，閘道必須將內容變更接聽器新增至感興趣的物件，如下列程式碼範例所概述：

```java
deviceLocation.addPropertyChangeListener(listener);
firmware.addPropertyChangeListener(listener);
deviceInfo.addPropertyChangeListener(listener);
metadata.addPropertyChangeListener(listener);
```

閘道也必須在其接收通知的位置實作 `propertyChange()` 方法，如下列範例實作所概述：

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

如需更新裝置屬性的相關資訊，請參閱[裝置管理要求 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.internetofthings.ibmcloud.com/devices/device_mgmt/index.html#/update-device-attributes#update-device-attributes){: new_window}。

## 範例
{: #samples}

我們提供了數個範例，以協助您將閘道及閘道後方的裝置連接至 {{site.data.keyword.iot_short_notm}} 實例。這些範例使用 {{site.data.keyword.iot_short_notm}} Java 用戶端程式庫，並位於[閘道範例 GitHub 儲存庫 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples){: new_window} 中。

## 秘訣
{: #recipes}

如需顯示如何將 Raspberry Pi 裝置當作受管理閘道連接至 {{site.data.keyword.iot_short_notm}} 以及管理連接的裝置的秘訣，請參閱 [Raspberry Pi 在 {{site.data.keyword.iot_short_notm}} 中作為受管理閘道 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/){: new_window}。

此秘訣說明如何使用 {{site.data.keyword.iot_short_notm}} 的「裝置管理」通訊協定，以從作為閘道的 Raspberry Pi 裝置管理 Arduino Uno 裝置，以及執行裝置管理作業（例如，將裝置重新開機，或新增概略圖程式）。
