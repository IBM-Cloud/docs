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

# 適用於裝置開發人員的 Java
{: #java}

您可以使用 Java™ 來建置及自訂裝置，在 {{site.data.keyword.iot_full}} 上與組織互動。我們提供了 {{site.data.keyword.iot_short_notm}} 的 Java 用戶端程式庫、文件及範例，以協助您開始進行裝置開發。
{:shortdesc}

## 下載 Java 用戶端及資源
{: #java_client_download}

若要存取適用於 {{site.data.keyword.iot_short_notm}} 的 Java 用戶端程式庫及範例，請移至 GitHub 中的 [iot-java ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-watson-iot/iot-java){: new_window} 儲存庫，並完成安裝指示。

## 建構子
{: #constructor}

建構子會建置用戶端實例，並接受包含下列定義的 `Properties` 物件：

|定義 |說明 |
|:----|:----|
|`org` |必須設為組織 ID 的必要值。如果您使用的是 Quickstart 流程，請指定 `quickstart`。|
|`type`  |指定裝置類型的必要值。|
|`id`  |指定裝置唯一 ID 的必要值。|
|`auth-method`  |要使用的鑑別方法。唯一支援的方法是 `token`。|
|`auth-token`   |將裝置安全地連接至 {{site.data.keyword.iot_short_notm}} 的鑑別記號。|
|`clean-session`|true 或 false 值，只有在要於可延續訂閱模式中連接應用程式時才是必要項目。`clean-session` 預設為 true。|
|`Port`|要連接至的埠號。指定 8883 或 443。如果您未指定埠號，則用戶端預設會透過埠號 8883 連接至 {{site.data.keyword.iot_short_notm}}。|
|`MaxInflightMessages`  |設定連線的進行中訊息數目上限。預設值為 100。|
|`Automatic-Reconnect`  |true 或 false 值，要將處於斷線狀態的裝置自動重新連接至 {{site.data.keyword.iot_short_notm}} 時為必要項目。預設值為 false。|
|`Disconnected-Buffer-Size`|用戶端斷線時，可以儲存在記憶體中的訊息數目上限。預設值為 5000。|
|`WebSocket`|true 或 false 值，要使用與 {{site.data.keyword.iot_short_notm}} 的 Websocket 連線時為必要項目。預設值為 false。|

**附註：**若要在可延續訂閱模式中連接裝置，請將 `clean-session` 設為 `false`。如需全新階段作業的相關資訊，請參閱 [MQTT 文件](../../reference/mqtt/index.html#subscription-buffers-and-clean-session)的「訂閱緩衝區及全新階段作業」一節。

`Properties` 物件會建立用來與 {{site.data.keyword.iot_short_notm}} 模組互動的定義。

下列程式碼範例顯示裝置如何以 Quickstart 模式發佈事件。

```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class QuickstartDeviceEventPublish {

    public static void main(String[] args) {

        //Provide the device specific data using Properties class
        Properties options = new Properties();
        options.setProperty("org", "quickstart");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generate a JSON object of the event to be published
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Quickstart flow allows only QoS = 0
        myClient.publishEvent("status", event, 0);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

下列程式碼範例顯示裝置如何在已登錄流程中發佈事件。


```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class RegisteredDeviceEventPublish {

    public static void main(String[] args) {

        //Provide the device specific data, as well as Auth-key and token using Properties class
        Properties options = new Properties();

        options.setProperty("org", "uguhsp");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");
        options.setProperty("auth-method", "token");
        options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generate a JSON object of the event to be published
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Registered flow allows 0, 1 and 2 QoS
        myClient.publishEvent("status", event);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

### 使用配置檔

您可以使用包含 Properties 物件的名稱/值配對的配置檔，而非直接使用 `Properties` 物件。如果您要使用包含 `Properties` 物件的配置檔，請使用下列程式碼格式：

```
package com.ibm.iotf.sample.client.device;

import java.io.File;
import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class RegisteredDeviceEventPublishPropertiesFile {

    public static void main(String[] args) {
        //Provide the device specific data, as well as Auth-key and token using Properties class
        Properties options = DeviceClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generate a JSON object of the event to be published
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Registered flow allows 0, 1 and 2 QoS
        myClient.publishEvent("status", event, 1);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

配置檔的內容必須為下列格式：

```
    [device]
    org=$orgId
    typ=$myDeviceType
    id=$myDeviceId
    auth-method=token
    auth-token=$token
```

## 連接至 {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}


若要連接至 {{site.data.keyword.iot_short_notm}}，請使用 `connect()` 函數。`connect()` 函數包含稱為 `autoRetry` 的選用性布林參數，它會決定程式庫是否在有 MqttException 連線失敗時嘗試重新連接。`autoRetry` 預設為 true。如果 MqttSecurityException 連線因為傳遞的裝置登錄詳細資料不正確而失敗，則程式庫不會嘗試重新連接，即使 `autoRetry` 設為 true 也一樣。

若要設定 MQTT 的「保留作用中」間隔，您可以選擇性地使用 `setKeepAliveInterval(int)` 方法，然後再呼叫 `connect()` 函數。`setKeepAliveInterval(int)` 值的測量單位為秒，它定義傳送訊息或接收訊息之間的時間間隔上限。使用時，用戶端可以偵測伺服器何時無法再使用，而不用等待 TCP/IP 逾時期間結束。用戶端確保在每一個「保留作用中」間隔期間至少有一個訊息在網路之間流動。如果在逾時期間沒有收到任何資料相關訊息，則用戶端會傳送伺服器所確認的小型 `ping` 訊息。`setKeepAliveInterval(int)` 預設為 60 秒。若要停用用戶端上的「保留作用中」處理特性，請將 `setKeepAliveInterval(int)` 值設為 0。


```
DeviceClient myClient = new DeviceClient(options);
myClient.setKeepAliveInterval(120);
myClient.connect(true);
```

若要控制連線失敗時發生的重試次數，請使用超載的 connect(int numberOfTimesToRetry) 函數。


```
DeviceClient myClient = new DeviceClient(options);
myClient.setKeepAliveInterval(120);
myClient.connect(10);
```

裝置在順利連接至 {{site.data.keyword.iot_short_notm}} 之後，即可從應用程式中發佈事件及訂閱裝置指令。


## 發佈事件
{: #publishing_events}

事件是裝置用來將資料發佈至 {{site.data.keyword.iot_short_notm}} 的機制。裝置會控制事件的內容，並指派名稱給它傳送的每個事件。

{{site.data.keyword.iot_short_notm}} 實例收到事件時，所收到事件的認證可識別傳送端裝置，這表示，裝置無法假冒另一個裝置。

可使用三種[服務品質 (QoS) 水準](../../reference/mqtt/index.html#qos-levels)的任一種發佈事件，這些水準由 MQTT 通訊協定定義。依預設，事件是以 QoS=0 來發佈。

### 在預設 QoS 水準發佈事件

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

myClient.publishEvent("status", event);
```


### 提高事件的 QoS 水準

您可以為發佈的事件提高 [QoS 水準](../../reference/mqtt/index.html#qos-levels)。QoS 水準大於零的事件可能需要較長的發佈時間，因為包含額外的確認接收資訊。

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

//Registered flow allows 0, 1 and 2 QoS
myClient.publishEvent("status", event, 2);
```

### 以自訂格式發佈事件

事件可以透過不同的格式（例如，JSON、字串、二進位等）進行發佈。程式庫預設會以 JSON 格式發佈事件，但如果您想要，可以指定不同格式的資料。例如，若要以字串格式發佈資料，請使用下列程式碼 Snippet。

```
myClient.connect();

String data = "cpu:"+getProcessCpuLoad();
status = myClient.publishEvent("load", data, "text", 2);
```

**附註：**在前一個程式碼範例中，事件的有效負載必須為字串格式。


任何 XML 資料都可以轉換為字串格式並進行發佈，如下所示：

```
status = myClient.publishEvent("load", xmlConvertedString, "xml", 2);
```

同樣地，若要以二進位格式發佈事件，請使用位元組陣列，如下列範例所概述：

```
myClient.connect();

byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = myClient.publishEvent("blink", cpuLoad , "binary", 1);
```

### 使用 HTTP 發佈事件
{: #publishing_events_http}


除了使用 MQTT 之外，您還可以配置裝置透過 HTTP 將事件發佈至 {{site.data.keyword.iot_short_notm}}。下列步驟概述透過 HTTP 發佈事件的順序：

1. 使用內容檔建構 `DeviceClient` 實例。
2. 建構需要發佈的事件。
3. 指定事件名稱，然後使用 `publishEventOverHTTP()` 方法來發佈事件，如下列程式碼範例所示：

``` sourceCode
DeviceClient myClient = new DeviceClient(deviceProps);

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

boolean response  = myClient.api().publishDeviceEventOverHTTP("blink", event, ContentType.json);
```

若要檢視整個程式碼，請參閱 [HttpDeviceEventPublish] 裝置範例。

根據內容檔中的設定，`publishEventOverHTTP()` 方法會以 Quickstart 模式或已登錄流程模式發佈事件。內容檔的組織 ID 設為 `quickstart` 時，`publishEventOverHTTP()` 方法會將事件發佈至裝置範例 Quickstart 服務，並以一般 HTTP 格式發佈事件。在內容檔中指定有效的已登錄組織時，會透過 HTTPS 安全地發佈事件。

HTTP 通訊協定提供「最多一次」遞送，這與 MQTT 通訊協定的「最多一次」(QoS 0) 服務品質水準類似。當您使用「最多一次」遞送來發佈事件時，應用程式只要發生錯誤就必須實作重試邏輯。

[HttpDeviceEventPublish]: https://github.com/ibm-messaging/iot-device-samples/blob/master/java/device-samples/src/main/java/com/ibm/iotf/sample/client/device/HttpDeviceEventPublish.java

## 處理指令
{: #handling_commands}

當裝置用戶端連接時，它會自動訂閱此裝置的任何指令。若要處理特定指令，您必須登錄指令回呼方法。
會以 `Command` 類別的實例傳回訊息，而這個實例包含下列內容：

| 內容     |資料類型     | 說明|
|----------------|----------------|
|`payload` |java.lang.String| 訊息有效負載的資料。|
|`format`  |java.lang.String| 格式可以是任何字串（例如，JSON）。|
|`command`   |java.lang.String|識別指令。|
|`timestamp`   |org.joda.time.DateTime|事件的日期和時間。|


``` sourceCode
package com.ibm.iotf.sample.client.device;

import java.util.Properties;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.LinkedBlockingQueue;


import com.ibm.iotf.client.device.Command;
import com.ibm.iotf.client.device.CommandCallback;
import com.ibm.iotf.client.device.DeviceClient;


//Implement the CommandCallback class to provide the way in which you want the command to be handled
class MyNewCommandCallback implements CommandCallback, Runnable {

    // A queue to hold & process the commands for smooth handling of MQTT messages
    private BlockingQueue<Command> queue = new LinkedBlockingQueue<Command>();

    /**
    * This method is invoked by the library whenever there is command matching the subscription criteria
    */
    @Override
    public void processCommand(Command cmd) {
        try {
            queue.put(cmd);
            } catch (InterruptedException e) {
        }
    }

    @Override
    public void run() {
        while(true) {
            Command cmd = null;
            try {
                //In this sample, we just display the command
                cmd = queue.take();
                System.out.println("COMMAND RECEIVED = '" + cmd.getCommand() + "'\twith Payload = '" + cmd.getPayload() + "'");
            } catch (InterruptedException e) {}
        }
    }
}

public class RegisteredDeviceCommandSubscribe {


    public static void main(String[] args) {

        //Provide the device specific data, as well as Auth-key and token using Properties class
        Properties options = new Properties();

        options.setProperty("org", "uguhsp");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");
        options.setProperty("auth-method", "token");
        options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Pass the above implemented CommandCallback as an argument to this device client
        myClient.setCommandCallback(new MyNewCommandCallback());

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();
    }
}
```

## 範例
{: #samples}

如需使用 {{site.data.keyword.iot_short_notm}} Java 用戶端程式庫開發之裝置及裝置管理範例的清單，請參閱 [iot-device-samples GitHub 儲存庫 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-messaging/iot-device-samples/tree/master/java){: new_window}。
