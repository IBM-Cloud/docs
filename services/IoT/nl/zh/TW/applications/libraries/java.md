---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 適用於應用程式開發人員的 Java
{: #java}


您可以使用 Java™ 來建置及自訂應用程式，在 {{site.data.keyword.iot_full}} 上與組織互動。我們提供了 {{site.data.keyword.iot_short_notm}} 的 Java 用戶端程式庫、文件及範例，以協助您開始進行應用程式開發。

{:shortdesc}

## 下載 Java 用戶端及資源
{: #java_client_download}

前次更新：2016 年 10 月 25 日
{: .last-updated}

若要存取適用於 {{site.data.keyword.iot_short_notm}} 的 Java 用戶端程式庫及範例，請移至 GitHub 中的 [iot-java](https://github.com/ibm-watson-iot/iot-java) 儲存庫，並完成安裝指示。


## 建構子
{: #constructor}

建構子會建置用戶端實例，並接受包含下列定義的 `Properties` 物件：

| 定義     |說明     |
|----------------|----------------|
|`org` |必須設為組織 ID 的必要值。如果您使用的是 Quickstart 流程，請指定 `quickstart`。|
|`id` |組織中應用程式的唯一 ID。|
|`auth-method`  |鑑別方法。唯一支援的方法是 `apikey`。|
|`auth-key`   |選用性的 API 金鑰，當 auth-method 的值設為 `apikey` 時必須指定的項目。|
|`auth-token`   |API 金鑰記號，當 auth-method 的值設為 `apikey` 時也為必要項目。 |
|`clean-session`|true 或 false 值，只有在要於可延續訂閱模式中連接應用程式時才是必要項目。`clean-session` 預設為 `true`。|
|`Port`|要連接至的埠號。指定 8883 或 443。如果您未指定埠號，則用戶端預設會透過埠號 8883 連接至 {{site.data.keyword.iot_short_notm}}。|
|`MaxInflightMessages`  |設定連線的進行中訊息數目上限。預設值為 100。|
|`Automatic-Reconnect`  |true 或 false 值，要將處於斷線狀態的裝置自動重新連接至 {{site.data.keyword.iot_short_notm}} 時為必要項目。預設值為 false。|
|`Disconnected-Buffer-Size`|用戶端斷線時，可以儲存在記憶體中的訊息數目上限。預設值為 5000。|
|`shared-subscription`|必須在要建置可擴充應用程式來平衡多個應用程式實例的訊息負載時設為 true 的布林值。如需相關資訊，請參閱[可擴充應用程式](../mqtt.html#scalable_apps)。

`Properties` 物件會建立用來與 {{site.data.keyword.iot_short_notm}} 模組互動的定義。如果您未指定此物件的內容，或指定 `quickstart`，則用戶端會連接至 {{site.data.keyword.iot_short_notm}} 的 Quickstart 服務，作為已取消登錄的裝置。

下列程式碼範例顯示如何在 `quickstart` 模式中建構應用程式用戶端 (`ApplicationClient`) 實例：

```
    import com.ibm.iotf.client.app.ApplicationClient;
    import java.util.Properties;

    Properties options = new Properties();
    options.put("org", "quickstart");

    ApplicationClient myClient = new ApplicationClient(options);
```

下列程式碼範例顯示如何在已登錄流程模式中建構應用程式用戶端 (`ApplicationClient`) 實例：

```
    Properties options = new Properties();
    options.put("org", "uguhsp");
    options.put("id", "app" + (Math.random() * 10000));
    options.put("Authentication-Method","apikey");
    options.put("API-Key", "<API-Key>");
    options.put("Authentication-Token", "<Authentication-Token>");

    ApplicationClient myClient = new ApplicationClient(options);
```

### 使用配置檔

您可以使用包含 `Properties` 物件的名稱/值配對的配置檔，而非直接包含 `Properties` 物件，如下列程式碼範例所概述：

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    ...
```
指定的應用程式配置檔必須為下列格式：

```
    [application]
    org=$orgId
    id=$myApplication
    auth-method=apikey
    auth-key=$key
    auth-token=$token
    enable-shared-subscription=true|false
```

## 連接至 {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

若要連接至 {{site.data.keyword.iot_short_notm}}，請使用 `connect()` 函數。`connect()` 函數包含稱為 `autoRetry` 的選用性布林參數，它會決定程式庫是否在有 MqttException 連線失敗時嘗試重新連接。`autoRetry` 預設為 true。如果 MqttSecurityException 連線因為傳遞的裝置登錄詳細資料不正確而失敗，則程式庫不會嘗試重新連接，即使 `autoRetry` 設為 true 也一樣。

若要設定 MQTT 的「保留作用中」間隔，您可以選擇性地使用 `setKeepAliveInterval(int)` 方法，然後再呼叫 `connect()` 函數。`setKeepAliveInterval(int)` 值的測量單位為秒，它定義傳送訊息或接收訊息之間的時間間隔上限。使用時，用戶端可以偵測伺服器何時無法再使用，而不用等待 TCP/IP 逾時期間結束。用戶端確保在每一個「保留作用中」間隔期間至少有一個訊息在網路之間流動。如果在逾時期間沒有收到任何資料相關訊息，則用戶端會傳送伺服器所確認的小型 `ping` 訊息。`setKeepAliveInterval(int)` 預設為 60 秒。若要停用用戶端上的「保留作用中」處理特性，請將 `setKeepAliveInterval(int)` 值設為 0。

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    myClient.setKeepAliveInterval(120);
    myClient.connect();
```

若要控制連線失敗時發生的重試次數，請在 myClient.connect() 函數中指定整數，如下列程式碼 Snippet 所概述：

```
    DeviceClient myClient = new DeviceClient(options);
    myClient.setKeepAliveInterval(120);
    myClient.connect(10);
```

應用程式用戶端在順利連接至 {{site.data.keyword.iot_short_notm}} 服務之後，即可訂閱裝置事件及狀態，也可以發佈裝置事件及指令。

## 訂閱裝置事件
{: #subscribing_device_events}

事件是裝置用來將資料發佈至 {{site.data.keyword.iot_short_notm}} 的機制。裝置會控制事件的內容，並指派名稱給它傳送的每個事件。

{{site.data.keyword.iot_short_notm}} 實例收到事件時，所收到事件的認證可識別傳送端裝置，這表示，裝置無法假冒另一個裝置。


應用程式預設會訂閱所有已連接裝置的所有事件。請使用裝置類型、裝置 ID、事件及訊息格式參數，以控制訂閱的範圍。下列程式碼範例顯示如何使用這些參數來定義訂閱的範圍：

### 訂閱所有裝置的所有事件


```
    myClient.connect();
    myClient.subscribeToDeviceEvents();
```
### 訂閱特定類型之所有裝置的所有事件


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino");
```

### 訂閱特定裝置的所有事件


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee");
```
### 訂閱兩個以上不同裝置的特定事件

```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee", "myEvent");
    myClient.subscribeToDeviceEvents("iotsample-arduino", "10aabbccddee", "myEvent");
```
### 訂閱以 JSON 格式發佈的事件


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee", "myEvent", "json", 0);
```

**附註**：單一用戶端可以支援多個訂閱。

## 處理裝置的事件
{: #handling_device_events}

若要處理訂閱所收到的事件，請登錄事件回呼方法。會以 Event 類別的實例傳回訊息，而這個實例具有下列參數：

|參數|資料類型|說明|
|:---|:---|
|`event.device`|字串|在組織所有類型裝置中唯一地識別出該裝置。|
|`event.deviceType`|字串|識別裝置類型。一般而言，deviceType 是執行特定作業的裝置分組，例如，"weatherballoon" 可以是裝置類型。|
|`event.deviceId`|字串|代表裝置的 ID。一般而言，對於特定裝置類型，deviceId 是該裝置的唯一 ID（例如，序號或 MAC 位址）。|
|`event.event`|字串|一般用來將特定事件分組（例如，"status"、"warning" 及 "data"）。|
|`event.format`|字串|格式可以是任何字串（例如，JSON）。  |
|`event.data`|字典|訊息有效負載的資料。長度上限是 131072 個位元組。|
|`event.timestamp`|日期和時間|事件的日期和時間|


下列程式碼提供事件回呼的範例實作：

```
  import com.ibm.iotf.client.app.Event;
  import com.ibm.iotf.client.app.EventCallback;
  import com.ibm.iotf.client.app.Command;

  import java.util.concurrent.BlockingQueue;
  import java.util.concurrent.LinkedBlockingQueue;

  /**
    * A sample Event callback class that processes the device events in a separate thread.
    *
    */
   class MyEventCallback implements EventCallback, Runnable {

	// A queue to hold and process the Events for smooth handling of MQTT messages
	private BlockingQueue<Event> evtQueue = new LinkedBlockingQueue<Event>();

	public void processEvent(Event e) {
		try {
			evtQueue.put(e);
		} catch (InterruptedException e1) {
			e1.printStackTrace();
		}
	}

	@Override
	public void processCommand(Command cmd) {
		System.out.println("Command received:: " + cmd);
	}

	@Override
	public void run() {
		while(true) {
			Event e = null;
			try {
				e = evtQueue.take();
				// In this example, the only output is the event
				System.out.println("Event:: " + e.getDeviceId() + ":" + e.getEvent() + ":" + e.getPayload());
			} catch (InterruptedException e1) {
				// Ignore the Interuppted exception, retry
				continue;
			}
		}
	}
    }
```

將事件回呼新增至 ApplicationClient 時，只要發佈符合訂閱的事件，就會呼叫 `processEvent()` 方法。下列 Snippet 顯示如何將事件回呼新增至 ApplicationClient 實例：



```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToDeviceEvents();
```

如同訂閱裝置事件，應用程式也可以訂閱傳送至裝置的指令。下列程式碼範例顯示如何訂閱組織中所有裝置的所有指令：

```

    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToDeviceCommands();
```

超載方法可用來控制指令訂閱。將指令傳送至符合指令訂閱的裝置時，會呼叫 `processCommand()` 方法。


## 訂閱裝置狀態
{: #subscribing_device_status}

如同訂閱裝置事件，應用程式可以訂閱裝置狀態，例如裝置連接至 {{site.data.keyword.iot_short_notm}}，及與其中斷連接。此訂閱預設會訂閱所有已連接裝置的狀態更新。請使用裝置類型及裝置 ID 參數，以控制訂閱的範圍。下列程式碼範例顯示如何使用這些參數來定義訂閱的範圍：

### 訂閱所有裝置的狀態更新

```
    myClient.connect();
    myClient.subscribeToDeviceStatus();
```

### 訂閱特定類型之所有裝置的狀態更新


```

    myClient.connect();
    myClient.subscribeToDeviceStatus("iotsample-arduino");
```

### 訂閱兩個不同裝置的狀態更新


```

    myClient.connect();
    myClient.subscribeToDeviceStatus("iotsample-arduino", "00aabbccddee");
    myClient.subscribeToDeviceStatus("iotsample-arduino", "10aabbccddee");
```

**附註**：單一用戶端可以支援多個訂閱。

## 處理裝置的狀態更新
{: #handling_device_status_updates}

若要處理訂閱所收到的狀態更新，您需要登錄狀態事件回呼方法。針對 `Connect` 及 `Disconnect` 狀態事件，會以 Status 類別的實例傳回訊息，而這個實例包含下列參數：


| 參數     |資料類型     |
|----------------|----------------|
|`status.clientAddr` |字串|
|`status.protocol`  |字串|
|`status.clientId`   |字串|
|`status.user`   |字串|
|`status.time`   |java.util.Date|
|`status.action` |字串|
|`status.connectTime`   |java.util.Date|
|`status.port`|整數|

只有在狀態事件是 `Disconnect` 時，才會設定下列內容：

| 內容     |資料類型     |
|----------------|----------------|
|`status.writeMsg` |整數|
|`status.readMsg`  |整數|
|`status.reason`   |字串|
|`status.readBytes`   |整數|
|`status.writeBytes`   |整數|


下列程式碼範例提供「狀態」回呼的範例實作：

```

  private static class MyStatusCallback implements StatusCallback {

      public void processApplicationStatus(ApplicationStatus status) {
          System.out.println("Application Status = " + status.getPayload());
      }

      public void processDeviceStatus(DeviceStatus status) {
          if(status.getAction() == "Disconnect") {
              System.out.println("device: "+status.getDeviceId()
                                  + "  time: "+ status.getTime()
                                  + "  action: " + status.getAction()
                                  + "  reason: " + status.getReason());
          } else {
              System.out.println("device: "+status.getDeviceId()
                                  + "  time: "+ status.getTime()
                                  + "  action: " + status.getAction());
          }
      }
  }
```

將狀態回呼新增至應用程式用戶端時，只要符合準則的裝置連接至 {{site.data.keyword.iot_short_notm}} 或與它中斷連線，就會呼叫 `processDeviceStatus()` 方法。下列程式碼範例顯示如何將狀態回呼實例新增至應用程式用戶端：

```

    myClient.connect()
    myClient.setStatusCallback(new MyStatusCallback());
    myClient.subscribeToDeviceStatus();
```
應用程式可以訂閱任何其他應用程式狀態（例如應用程式連接至 {{site.data.keyword.iot_short_notm}}，及與其中斷連接）。下列程式碼 Snippet 顯示如何訂閱 {{site.data.keyword.iot_short_notm}} 組織的應用程式狀態：

```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToApplicationStatus();
```
超載方法可用來控制特定應用程式的狀態訂閱。只要符合準則的應用程式連接至 {{site.data.keyword.iot_short_notm}} 或與它中斷連線，就會呼叫 `processApplicationStatus()` 方法。


## 發佈裝置的事件
{: #publishing_events_devices}

下列程式碼範例顯示應用程式可以如何發佈事件，就彷彿事件是源自裝置一樣。

```

    myClient.connect()

    //Generate the event to be published
    JsonObject event = new JsonObject();
    event.addProperty("name", "foo");
    event.addProperty("cpu",  60);
    event.addProperty("mem",  40);

    // publish the event on behalf of device
    myClient.publishEvent(deviceType, deviceId, "blink", event);
```


事件可以透過不同的格式（例如，JSON、字串、二進位等）進行發佈。程式庫預設會以 JSON 格式發佈事件，但如果您想要，可以指定不同格式的資料。例如，若要以字串格式發佈資料，請使用下列程式碼 Snippet。

```
    myClient.connect();
    String data = "cpu:"+60;
    status = myClient.publishEvent("load", data, "text", 2);
```
**附註：**在前一個程式碼範例中，事件的有效負載必須為字串格式。

任何 XML 資料都可以轉換為字串並進行發佈，如下所示：

```
    status = myClient.publishEvent("load", xmlConvertedString, "xml", 2);
```

同樣地，若要以二進位格式發佈事件，請使用位元組陣列，如下列範例所概述：

```
    myClient.connect();
    byte[] cpuLoad = new byte[] {60, 35, 30, 25};
    status = myClient.publishEvent("blink", cpuLoad , "binary", 1);
```

### 使用 HTTP 發佈事件
{: #publishing_events_http}

除了使用 MQTT 之外，您還可以配置應用程式透過 HTTP 將裝置事件發佈至 {{site.data.keyword.iot_short_notm}}。下列步驟概述透過 HTTP 發佈裝置事件的順序：

1. 使用內容檔建構 ApplicationClient 實例。
2. 建構需要發佈的事件。
3. 指定事件名稱、裝置類型及裝置 ID。
4. 使用 `publishEventOverHTTP`() 方法發佈事件，如下列程式碼範例所示：

```
    	ApplicationClient myClient = new ApplicationClient(props);

    	JsonObject event = new JsonObject();
    	event.addProperty("name", "foo");
    	event.addProperty("cpu",  90);
    	event.addProperty("mem",  70);

    	boolean status = myClient.publishApplicationEventforDeviceOverHTTP(deviceId, deviceType, "blink", event, ContentType.json);
```

如需完整程式碼範例，請參閱 [HttpApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpApplicationDeviceEventPublish.java) 應用程式範例。

根據內容檔中的設定，`publishEventOverHTTP()` 方法會在 Quickstart 流程或已登錄流程中發佈事件。在內容檔中將 `quickstart` 指定為組織 ID 時，`publishEventOverHTTP()` 方法會以一般 HTTP 格式將事件發佈至 {{site.data.keyword.iot_short_notm}} 的 Quickstart 服務。在內容檔中指定有效的已登錄組織時，一律會使用 HTTPS 來發佈事件，因此，所有通訊都是安全的。

HTTP 通訊協定提供「最多一次」遞送，這與 MQTT 通訊協定的「最多一次」(QoS 0) 服務品質水準類似。當您使用「最多一次」遞送來發佈事件時，應用程式必須在發生錯誤時實作重試邏輯。


## 將指令發佈至裝置
{: #publishing_commands_devices}

應用程式可以將指令發佈至已連接的裝置，如下列範例所示：

```

    myClient.connect()

    //Generate the event to be published
    JsonObject data = new JsonObject();
    data.addProperty("name", "stop-rotation");
    data.addProperty("delay",  0);

    //Registered flow allows 0, 1 and 2 QoS
    myAppClient.publishCommand(deviceType, deviceId, "stop", data);
```

### 使用 HTTP 發佈指令
{: #publishing_commands_http}

除了使用 MQTT 之外，您還可以配置應用程式透過 HTTP 將指令發佈至已連接的裝置。下列步驟概述使用 HTTP 發佈裝置事件的順序：

1. 使用內容檔建構 ApplicationClient 實例
2. 建構需要發佈的指令
3. 指定指令名稱、裝置類型及裝置 ID
4. 使用 `publishCommandOverHTTP`() 方法發佈指令，如下列程式碼所示：

```

    	ApplicationClient myClient = new ApplicationClient(props);

    	// Generate a JSON object of the event to be published
	JsonObject event = new JsonObject();
	event.addProperty("reboot", 5);

	boolean response = myClient.publishCommandOverHTTP("execute", event);
```

若要檢視完整程式碼範例，請參閱 [HttpCommandPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpCommandPublish.java) 應用程式範例。

HTTP 通訊協定提供「最多一次」遞送，這與 MQTT 通訊協定的「最多一次」(QoS 0) 服務品質水準類似。當您使用「最多一次」遞送來發佈指令時，應用程式必須在發生錯誤時實作重試邏輯。如需相關資訊，請參閱[應用程式的 HTTP REST API](../api.html)。


## 範例
{: #samples}

-  [MQTTApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/MQTTApplicationDeviceEventPublish.java) - 顯示如何發佈裝置事件的範例應用程式。
-   [RegisteredApplicationCommandPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationCommandPublish.java) - 顯示如何將指令發佈至裝置的範例應用程式。
-  [RegisteredApplicationSubscribeSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationSubscribeSample.java) - 顯示如何訂閱不同事件（例如裝置事件、裝置指令、裝置狀態及應用程式狀態）的範例應用程式。
-   [SharedSubscriptionSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/SharedSubscriptionSample.java) - 顯示如何建置可擴充應用程式來平衡多個應用程式實例之間訊息負載的範例應用程式。
-  [Backup-restore-sample](https://github.com/ibm-messaging/iot-backup-restore-sample) - 顯示如何在 {{site.data.keyword.cloudant}} 中備份及還原裝置配置的範例。
