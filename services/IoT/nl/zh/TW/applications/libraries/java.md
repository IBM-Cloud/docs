---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 適用於應用程式開發人員的 Java
{: #java}

前次更新：2016 年 9 月 7 日
{: .last-updated}

您可以在 {{site.data.keyword.iot_full}} 上使用 Java 來建置及自訂與組織互動的應用程式。使用提供的資訊及範例，利用 Java 開始開發您的應用程式。
{:shortdesc}

## 下載 Java 用戶端及資源
{: #java_client_download}

若要存取適用於 {{site.data.keyword.iot_short_notm}} 的 Java 用戶端程式庫及範例，請移至 GitHub 中的 [iot-java](https://github.com/ibm-watson-iot/iot-java) 儲存庫，並完成安裝指示。


## 建構子
{: #constructor}

建構子會建置用戶端實例，並接受包含下列定義的 `Properties` 物件：

| 定義     |說明     |
|----------------|----------------|
|`org` |您的組織 ID。這是必要值。如果您使用的是「快速入門」流程，請指定 `quickstart`。|
|`id` |組織中應用程式的唯一 ID。|
|`auth-method`  |鑑別方法，目前唯一支援的值是 `apikey`。|
|`auth-key`   |選用的 API 金鑰，當 auth-method 設為 `apikey` 時為必要項目。  |
|`auth-token`   |API 金鑰記號，當 auth-method 設為 `apikey` 時為必要項目。 |
|`clean-session`|true 或 false 值，只有在要於可延續訂閱模式中連接應用程式時才是必要項目。`clean-session` 預設為 `true`。|
|`shared-subscription`|布林值。如果您想要建置可擴充應用程式來平衡多個應用程式實例的訊息負載，請設為 `true`。如需相關資訊，請參閱[可擴充應用程式](mqtt.html#/scalable-applications#scalable-applications)。

`Properties` 物件會建立用來與 {{site.data.keyword.iot_short_notm}} 模組互動的定義。如果您未指定此物件的內容，或指定 `quickstart`，則用戶端會連接至 {{site.data.keyword.iot_short_notm}} 的「快速入門」服務，作為已取消登錄的裝置。

下列程式碼範例顯示如何在 `quickstart` 模式中建構 ApplicationClient 實例：

```
    import com.ibm.iotf.client.app.ApplicationClient;
    import java.util.Properties;

    Properties options = new Properties();
    options.put("org", "quickstart");

    ApplicationClient myClient = new ApplicationClient(options);
```

下列程式碼範例顯示如何在已登錄流程模式中建構 ApplicationClient 實例：

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

您可以使用包含 `Properties` 物件的名稱/值配對（格式如下）的配置檔，而非直接包括 `Properties` 物件：

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    ...
```
應用程式配置檔必須為下列格式：

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

若要連接至 {{site.data.keyword.iot_short_notm}}，請使用 `connect()` 函數。`connect()` 函數包括稱為 `autoRetry` 的選用布林參數，以決定程式庫是否在 MqttException 連線失敗時嘗試重新連接。`autoRetry` 預設為 true。如果 MqttSecurityException 連線因為傳遞的裝置登錄詳細資料不正確而失敗，則程式庫不會嘗試重新連接，即使 `autoRetry` 設為 `true`。

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);

    myClient.connect();
```

順利連接至 {{site.data.keyword.iot_short_notm}} 服務之後，您的應用程式用戶端可以訂閱裝置事件、訂閱裝置狀態，以及發佈裝置事件和指令。

## 訂閱裝置事件
{: #subscribing_device_events}

事件是裝置用來將資料發佈至 {{site.data.keyword.iot_short_notm}} 的機制。裝置會控制事件的內容，並指派所傳送之每一個事件的名稱。

{{site.data.keyword.iot_short_notm}} 實例接收到事件時，所收到事件的認證可識別傳送端裝置，這表示，裝置無法假冒另一個裝置。


應用程式預設會訂閱所有已連接裝置的所有事件。使用裝置類型、裝置 ID、事件及訊息格式參數，以控制訂閱的範圍。下列程式碼範例顯示如何使用這些參數來定義訂閱的範圍：

### 訂閱所有裝置的所有事件


```
    myClient.connect();
    myClient.subscribeToDeviceEvents();
```
### 訂閱特定類型的所有裝置的所有事件


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
|`event.device`|字串|唯一識別組織中所有類型裝置的裝置。|
|`event.deviceType`|字串|識別裝置類型。一般而言，deviceType 是執行特定作業（例如，"weatherballoon"）的裝置分組。|
|`event.deviceId`|字串|代表裝置的 ID。一般而言，針對給定的裝置類型，deviceId 是該裝置的唯一 ID（例如，序號或 MAC 位址）。|
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

如同訂閱裝置事件，應用程式可以訂閱裝置狀態（例如 {{site.data.keyword.iot_short_notm}} 的裝置連接及中斷連接）。此訂閱預設會訂閱所有已連接裝置的狀態更新。使用裝置類型及裝置 ID 參數，以控制訂閱的範圍。下列程式碼範例顯示如何使用這些參數來定義訂閱的範圍：

### 訂閱所有裝置的狀態更新項目

```
    myClient.connect();
    myClient.subscribeToDeviceStatus();
```

### 訂閱特定類型的所有裝置的狀態更新項目


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
|`status.clientAddr` |string|
|`status.protocol`  |string|
|`status.clientId`   |string|
|`status.user`   |string|
|`status.time`   |java.util.Date|
|`status.action` |string|
|`status.connectTime`   |java.util.Date|
|`status.port`|integer|

只有在狀態事件是 `Disconnect` 時，才會設定下列內容：

| 內容     |資料類型     |
|----------------|----------------|
|`status.writeMsg` |integer|
|`status.readMsg`  |integer|
|`status.reason`   |string|
|`status.readBytes`   |integer|
|`status.writeBytes`   |integer|


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

將狀態回呼新增至 ApplicationClient 時，只要符合準則的裝置連接或與 {{site.data.keyword.iot_short_notm}} 中斷連接，就會呼叫 `processDeviceStatus()` 方法。下列程式碼範例顯示如何將狀態回呼實例新增至 ApplicationClient：

```

    myClient.connect()
    myClient.setStatusCallback(new MyStatusCallback());
    myClient.subscribeToDeviceStatus();
```
應用程式可以訂閱任何其他應用程式狀態（例如 Watson IoT Platform 的應用程式連接及中斷連接）。下列程式碼 Snippet 顯示如何訂閱組織中的應用程式狀態：

```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToApplicationStatus();
```
超載方法可用來控制特定應用程式的狀態訂閱。只要符合準則的應用程式連接或與 {{site.data.keyword.iot_short_notm}} 中斷連接，就會呼叫 processApplicationStatus() 方法。


## 發佈來自裝置的事件
{: #publishing_events_devices}

下列程式碼範例顯示應用程式可以如何發佈事件，讓事件彷彿是源自裝置。

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

### 使用 HTTP 發佈事件
{: #publishing_events_http}

除了 MQTT 之外，透過完成下列步驟，您還可以配置應用程式使用 HTTP 將裝置事件發佈至 {{site.data.keyword.iot_short_notm}}：

* 使用內容檔建構 ApplicationClient 實例
* 建構需要發佈的事件
* 指定事件名稱、裝置類型及裝置 ID
* 使用 `publishEventOverHTTP`() 方法發佈事件，如下列程式碼所示：

```

    	ApplicationClient myClient = new ApplicationClient(props);

    	JsonObject event = new JsonObject();
    	event.addProperty("name", "foo");
    	event.addProperty("cpu",  90);
    	event.addProperty("mem",  70);

    	code = myClient.publishEventOverHTTP(deviceType, deviceId, "blink", event);
```

如需完整程式碼範例，請參閱下列應用程式範例：

[HttpApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpApplicationDeviceEventPublish.java)

根據內容檔中的設定，`publishEventOverHTTP()` 方法會在「快速入門流程」或「已登錄流程」中發佈事件。`quickstart` 是內容檔中所指定的「組織 ID」時，`publishEventOverHTTP()` 方法會以一般 HTTP 格式將事件發佈至 {{site.data.keyword.iot_short_notm}} 的「快速入門」服務。在內容檔中指定有效的已登錄組織時，一律會使用 HTTPS 來發佈事件，因此，所有通訊都是安全的。

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


## 範例
{: #examples}


-  [MQTTApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/MQTTApplicationDeviceEventPublish.java) - 顯示如何發佈裝置事件的範例應用程式。
-   [RegisteredApplicationCommandPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationCommandPublish.java) - 顯示如何將指令發佈至裝置的範例應用程式。
-  [RegisteredApplicationSubscribeSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationSubscribeSample.java) - 顯示如何訂閱不同事件（例如裝置事件、裝置指令、裝置狀態及應用程式狀態）的範例應用程式。
-   [SharedSubscriptionSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/SharedSubscriptionSample.java) - 顯示如何建置可擴充應用程式來平衡多個應用程式實例的訊息負載的範例應用程式。
-  [備份及還原範例](https://github.com/ibm-messaging/iot-backup-restore-sample) - 顯示如何在 Cloudant NoSQL 資料庫中備份及還原裝置配置的範例。
