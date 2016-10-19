---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 適用於裝置開發人員的 Java
{: #java}

前次更新：2016 年 8 月 2 日
{: .last-updated}


您可以在 {{site.data.keyword.iot_full}} 上使用 Java 來建置及自訂與組織互動的裝置。使用提供的資訊及範例，利用 Java 開始開發您的裝置。
{:shortdesc}

## 下載 Java 用戶端及資源
{: #java_client_download}

若要存取適用於 {{site.data.keyword.iot_short_notm}} 的 Java 用戶端程式庫及範例，請移至 GitHub 中的 [iot-java](https://github.com/ibm-watson-iot/iot-java) 儲存庫，並完成安裝指示。


## 建構子
{: #constructor}

建構子會建置用戶端實例，並接受包含下列定義的 Properties 物件：

|定義 |說明 |
|:---|:---|
|`org` |您的組織 ID。這是必要欄位。如果您使用的是「快速入門」流程，請指定 `quickstart`。|
|`type`  |您的裝置類型。這是必要欄位。|
|`id`  |您的裝置 ID。這是必要欄位。|
|`auth-method`   |要使用的鑑別方法。目前唯一支援的值是 `token`。|
|`auth-token`   |將裝置安全地連接至 Watson IoT Platform 的鑑別記號。|
|`clean-session`|true 或 false 值，只有在要於可延續訂閱模式中連接應用程式時才是必要項目。`clean-session` 預設為 `true`。|

**附註：**若要在可延續訂閱模式中連接裝置，請將 `clean-session` 設為 `false`。如需全新階段作業的相關資訊，請參閱 [MQTT 文件](../../reference/mqtt/index.html#subscription-buffers-and-clean-session)的「訂閱緩衝區及全新階段作業」一節。

Properties 物件會建立用來與 {{site.data.keyword.iot_short_notm}} 模組互動的定義。

下列程式碼顯示處於「快速入門」模式的裝置發佈事件。

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

您可以使用包含 properties 物件的名稱/值配對的配置檔，而非直接使用 Properties 物件。如果您使用的是包含 Properties 物件的配置檔，請使用下列程式碼格式：

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

呼叫 connect 函數來連接至 {{site.data.keyword.iot_short_notm}}。connect 函數會採用選用的布林參數 `autoRetry`，其預設為 `true`。`autoRetry` 參數容許在發生 MqttException 錯誤時重新連接程式庫。請注意，當發生 MqttSecurityException 錯誤時，程式庫不會嘗試重新連接，因為使用了不正確的裝置登錄詳細資料，即使 `autoRetry` 參數設為 `true` 也一樣。

```
DeviceClient myClient = new DeviceClient(options);

myClient.connect(true);
```

在順利連線至 {{site.data.keyword.iot_short_notm}} 服務之後，裝置用戶端可以執行下列作業：發佈事件，以及從應用程式訂閱裝置指令。


## 發佈事件
{: #publishing_events}

事件是裝置用來將資料發佈至 {{site.data.keyword.iot_short_notm}} 的機制。裝置會控制事件的內容，並指派所傳送之每一個事件的名稱。

{{site.data.keyword.iot_short_notm}} 實例接收到事件時，所收到事件的認證可識別傳送端裝置，這表示，裝置無法假冒另一個裝置。

可在三個[服務品質 (QoS) 水準](../../reference/mqtt/index.html#qos-levels)的任一個上發佈事件，這些水準由 MQTT 通訊協定予以定義。依預設，事件是在 QoS=0 時發佈。

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

您可以為發佈的事件提高 [QoS 水準](../../reference/mqtt/index.html#qos-levels)。QoS 水準大於零的事件可能需要較長的發佈時間，因為包括額外的確認接收資訊。

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

//Registered flow allows 0, 1 and 2 QoS
myClient.publishEvent("status", event, 2);
```

### 使用 HTTP 發佈事件

除了 MQTT 之外，透過下列步驟，裝置還可以使用 HTTP 將事件發佈至 {{site.data.keyword.iot_short_notm}}：

* 使用內容檔建構 DeviceClient 實例。
* 建構需要發佈的事件。
* 指定事件名稱，並使用 `publishEventOverHTTP()` 方法來發佈事件，如下列程式碼所示：

``` sourceCode
DeviceClient myClient = new DeviceClient(deviceProps);

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

int httpCode = myClient.publishEventOverHTTP("blink", event);
```

您可以在 [HttpDeviceEventPublish] 裝置範例中找到整個程式碼。

根據內容檔中的設定，`publishEventOverHTTP()` 方法會在「快速入門」模式或已登錄流程模式中發佈事件。當內容檔的「組織 ID」是 `quickstart` 時，`publishEventOverHTTP()` 方法會將事件發佈至裝置範例快速入門服務，並以一般 HTTP 格式發佈事件。在內容檔中使用有效的已登錄組織時，此方法一律以 HTTPS（即 HTTP over SSL）發佈事件，所以全部通訊都是安全的。

HTTP 通訊協定提供「最多一次」遞送，這與 MQTT 通訊協定的「最多一次」(QoS 0) 服務品質水準類似。當您使用「最多一次」遞送來發佈事件時，應用程式必須在發生錯誤時實作重試邏輯。

[HttpDeviceEventPublish]: https://github.com/ibm-messaging/iot-device-samples/blob/master/java/device-samples/src/main/java/com/ibm/iotf/sample/client/device/HttpDeviceEventPublish.java

## 處理指令
{: #handling_commands}

當裝置用戶端連接時，它會自動訂閱此裝置的任何指令。若要處理特定指令，您必須登錄指令回呼方法。
會以 Command 類別的實例傳回訊息，而這個實例具有下列內容：

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

如需使用「{{site.data.keyword.iot_short_notm}} Java 用戶端」程式庫開發之裝置及裝置管理範例的清單，請參閱 [GitHub 儲存庫](https://github.com/ibm-messaging/iot-device-samples/tree/master/java)。
