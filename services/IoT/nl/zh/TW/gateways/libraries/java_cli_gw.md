---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-30"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

#使用 Java 在 {{site.data.keyword.iot_short_notm}} 上開發閘道
{: #java_cli_gw}

如果您的裝置無法直接連接至 {{site.data.keyword.iot_full}} 上的組織，您可以使用 Java™ 來建置及自訂閘道。我們提供了 {{site.data.keyword.iot_short_notm}} 的 Java 用戶端程式庫、文件及範例，以協助您開始進行閘道開發。
{:shortdesc}

## 下載 Java 用戶端及資源
{: #java_client_download}

若要存取適用於 {{site.data.keyword.iot_short_notm}} 的 Java 用戶端程式庫及範例，請移至 GitHub 中的 [iot-java](https://github.com/ibm-watson-iot/iot-java) 儲存庫，並完成安裝指示。

## 建構子
{: #constructor}

建構子會建置閘道用戶端實例，並接受包含下列定義的 `Properties` 物件：

|定義 |說明 |
|:----|:----|
|`org`|必須設為組織 ID 的必要值。如果您使用的是 Quickstart 流程，請指定 `quickstart`。|
|`domain`|傳訊端點 URL（選用）。如果您未指定網域的值，則 URL 會預設為 `internetofthings.ibmcloud.com`（即 {{site.data.keyword.iot_short_notm}} 正式作業伺服器）。|
|`type`|指定閘道類型的必要值。|
|`id` |指定閘道唯一 ID 的必要值。|
|`auth-method`|要使用的鑑別方法。唯一支援的方法是 `token`。|
|`auth-token`|將閘道安全地連接至 {{site.data.keyword.iot_short_notm}} 的 API 金鑰鑑別記號。|
|`clean-session`|true 或 false 值，只有在要以可延續訂閱模式連接閘道時才是必要項目。`clean-session` 預設為 true。|
|`WebSocket`|true 或 false 值，只有在要使用 Websocket 連接閘道時才是必要項目。|
|`Port`|要連接至的埠號。指定 8883 或 443。如果您未指定埠號，則用戶端預設會透過埠號 8883 連接至 {{site.data.keyword.iot_short_notm}}。|
|`MaxInflightMessages`|設定連線的進行中訊息數目上限。預設值為 100。|
|`Automatic-Reconnect`|true 或 false 值，要將處於斷線狀態的閘道自動重新連接至 {{site.data.keyword.iot_short_notm}} 時為必要項目。預設值為 false。|
|`Disconnected-Buffer-Size`|用戶端斷線時，可以儲存在記憶體中的訊息數目上限。預設值為 5000。|

**附註：**若要以可延續訂閱模式連接閘道，請將 `clean-session` 設為 `false`。如需全新階段作業的相關資訊，請參閱 [MQTT 文件](../../reference/mqtt/index.html#subscription-buffers-and-clean-session)的「訂閱緩衝區及全新階段作業」一節。

`Properties` 物件會建立用來與 {{site.data.keyword.iot_short_notm}} 模組互動的定義。

下列程式碼範例顯示如何建構閘道用戶端實例：

```java
Properties options = new Properties();
options.setProperty("org", "<Your organization ID>");
options.setProperty("type", "<The gateway device type>");
options.setProperty("id", "The gateway device ID");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "API token");
GatewayClient gwClient = new GatewayClient(options);

```


### 使用配置檔

您可以使用包含閘道 Properties 物件的名稱/值配對的配置檔，而非直接使用 `Properties` 物件來建立閘道實例。若要使用配置檔來建置閘道的 `Properties` 物件，請使用下列程式碼格式：

```Java
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
...
```

配置檔的內容必須為下列格式：

```java
[Gateway]
org=$orgId
domain=$domain
typ=$myGatewayDeviceType
id=$myGatewayDeviceId
auth-method=token
auth-token=$token

```

## 連接至 {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

若要連接至 {{site.data.keyword.iot_short_notm}}，請使用 `connect()` 函數。`connect()` 函數包括稱為 `autoRetry` 的選用布林參數，可決定程式庫是否在 MQTT 異常狀況 (MqttException) 連線失敗時嘗試重新連接。`autoRetry` 預設為 true。如果 MqttSecurityException 連線因為傳遞的裝置登錄詳細資料不正確而失敗，則程式庫不會嘗試重新連接，即使 `autoRetry` 設為 true 也一樣。

若要設定 MQTT 的保留作用中間隔，您可以選擇性地先使用 `setKeepAliveInterval(int)` 方法，然後再呼叫 `connect()` 函數。`setKeepAliveInterval(int)` 值的測量單位為秒，它定義傳送訊息或接收訊息之間的時間間隔上限。指定 `setKeepAliveInterval(int)` 值時，用戶端可偵測到伺服器無法再使用，而不需要等待 TCP/IP 逾時期間結束。用戶端確保在每一個保留作用中間隔期間至少有一則訊息在網路之間流動。如果在逾時期間沒有收到任何資料相關訊息，則用戶端會傳送伺服器所確認的小型 `ping` 訊息。`setKeepAliveInterval(int)` 預設為 60 秒。若要停用用戶端上的保留作用中處理特性，請將 `setKeepAliveInterval(int)` 值設為 0。

```java
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
gwClient.setKeepAliveInterval(80);
gwClient.connect();
```

若要控制連線失敗時發生的重試次數，請使用超載的 connect(int numberOfTimesToRetry) 函數。

```java
GatewayClient gwClient = new GatewayClient(props);
gwClient.setKeepAliveInterval(80);
gwClient .connect(10);
```

閘道用戶端順利連接至 {{site.data.keyword.iot_short_notm}} 之後，閘道可以針對本身同時代表連接至閘道的裝置發佈事件以及訂閱指令。

## 登錄閘道後方的裝置
{: #register_device_gateway}

您可以自動或使用 API 開發程式碼，來登錄在連接至 {{site.data.keyword.iot_short_notm}} 實例的閘道後方的裝置。

### 自動裝置登錄
只要閘道針對與其連接的裝置發佈任何事件或訂閱任何指令，您就可以在 {{site.data.keyword.iot_short_notm}} 上自動登錄裝置。

### API 裝置登錄
您也可以使用 {{site.data.keyword.iot_short_notm}} API，向 {{site.data.keyword.iot_short_notm}} 實例登錄在閘道後方的裝置。

若要簡化使用 {{site.data.keyword.iot_short_notm}} API 進行開發，請呼叫 api() 方法來起始 API 用戶端實例，如下列程式碼範例所概述：

```java
import com.ibm.iotf.client.api.APIClient;
....

GatewayClient gwClient = new GatewayClient(props);
gwClient.connect();

APIClient api = gwClient.api();
```
當您接收 API 用戶端的處理時，即可開始向閘道登錄裝置，如下列程式碼範例所概述：

```java
gwClient.connect();

  String deviceToBeAdded = "{\"deviceId\": \"" + DEVICE_ID +
					"\",\"authToken\": \"qwer123\"}";

    JsonParser parser = new JsonParser();
    JsonElement input = parser.parse(deviceToBeAdded);
    JsonObject response = this.gwClient.api().registerDeviceUnderGateway(DEVICE_TYPE, gwDeviceId, gwDeviceType, input);

```

登錄閘道後方的裝置時，裝置是透過 `gwDeviceId` 及 `gwDeviceType` 屬性的值與閘道相關聯。

## 發佈事件
{: #publish_events}

事件是閘道及裝置用來將資料發佈至 {{site.data.keyword.iot_short_notm}} 的機制。閘道或裝置會控制事件的內容，並指派名稱給它傳送的每一個事件。閘道可以發佈其本身的事件，也可以代表透過該閘道連接的任何裝置來發佈事件。

{{site.data.keyword.iot_short_notm}} 實例收到事件時，所收到事件的認證可識別傳送端閘道，這表示閘道無法假冒另一個裝置。

可使用三種[服務品質 (QoS) 水準](../../reference/mqtt/index.html#qos-levels)的任一種發佈事件，這些水準由 MQTT 通訊協定定義。依預設，事件是以 QoS=0 來發佈。

### 在預設 QoS 水準發佈閘道事件的程式碼

```java
gwClient.connect();
  JsonObject event = new JsonObject();
  event.addProperty("name", "foo");
  event.addProperty("cpu",  90);
  event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event);
```

### 提高事件預設 QoS 水準的程式碼

您可以為發佈的閘道事件提高 [QoS 水準](../../reference/mqtt/index.html#qos-levels)。QoS 水準大於零的事件可能需要較長的發佈時間，因為包含額外的確認接收資訊。


```java
gwClient.connect();
  JsonObject event = new JsonObject();
  event.addProperty("name", "foo");
  event.addProperty("cpu",  90);
  event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event, 2);
```

### 以自訂格式發佈事件的程式碼

事件可以透過不同的格式（例如，JSON、字串、二進位等）進行發佈。程式庫預設會以 JSON 格式發佈事件，但如果您想要，可以指定不同格式的資料。例如，若要以字串格式發佈資料，請使用下列程式碼 Snippet：

```java
gwClient.connect();
String data = "cpu:80";
boolean status = gwClient.publishGatewayEvent("load", data, "text", 2);
```

**附註：**在前一個程式碼範例中，事件的有效負載必須為字串格式。


XML 資料可以轉換為字串格式並進行發佈，如下列程式碼範例所概述：

```java
status = gwClient.publishGatewayEvent("load", xmlConvertedString, "xml", 2);
```

同樣地，若要以二進位格式發佈事件，請使用位元組陣列，如下列範例所概述：

```java
gwClient.connect();
byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = gwClient.publishGatewayEvent("blink", cpuLoad , "binary", 1);
```

### 發佈裝置事件的程式碼
{: #publishing_events_devices}

閘道可以代表透過閘道連接的任何裝置，透過傳遞原始事件的適當類型 ID 及裝置 ID 值來發佈事件，如下列範例所概述：

```java

gwClient.connect()

//Generate the event to be published
    JsonObject event = new JsonObject();
    event.addProperty("name", "foo");
    event.addProperty("cpu",  60);
    event.addProperty("mem",  40);

    // publish the event on behalf of device
gwClient.publishDeviceEvent(deviceType, deviceId, eventName, event);
```

使用超載的 `publishDeviceEvent()` 方法來發佈偏好服務品質水準的裝置事件。如需所使用主題結構的相關資訊，請參閱[閘道的 MQTT 連線功能](../mqtt.html)。

### 以自訂格式發佈裝置事件的程式碼

與閘道事件類似，也會以不同格式發佈裝置事件。程式庫預設會以 JSON 格式發佈裝置事件，但如果您想要，可以指定不同格式的資料。例如，若要以字串格式發佈資料，請使用下列程式碼範例：

```java
gwClient.connect();
String data = "cpu:80";
boolean status = gwClient.publishDeviceEvent(deviceType, deviceId, "load", data, "text", 2);
```

**附註：**事件的有效負載必須為字串格式。

任何 XML 資料都可以轉換為字串格式並進行發佈，如下列範例所示：

```java
status = gwClient.publishDeviceEvent(deviceType, deviceId, "load", xmlConvertedString, "xml", 2);
```

同樣地，若要以二進位格式發佈裝置事件，請使用位元組陣列，如下列範例所概述：
```java
gwClient.connect();
byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = gwClient.publishDeviceEvent(deviceType, deviceId, "blink", cpuLoad , "binary", 1);
```

## 處理指令
{: #handling_commands}

閘道可以訂閱導向閘道本身的指令，以及導向任何透過閘道連接的裝置的指令。閘道用戶端連接時，會自動訂閱此閘道的任何指令。但是，若要訂閱透過閘道連接的裝置的任何指令，請使用超載的 `subscribeToDeviceCommands()` 方法，如下列範例所概述：

```java
gwClient.connect()

// subscribe to commands on behalf of device
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

若要處理特定指令，您需要登錄 `Command` 回呼方法。會以 `Command` 類別的實例傳回訊息，並且包含下列內容：


| 內容     |資料類型     | 說明|
|----------------|----------------|---------------
|`deviceType`|字串| 收到指令的裝置類型。|
|`deviceId`|字串| 收到指令的裝置 ID，可以是閘道或透過閘道所連接的裝置。|
|`data`|物件| 指令有效負載。|
|`format`|字串| 指令有效負載的格式，可以是任何字串（例如，JSON、二進位、文字或其他）。|
|`command`|字串|指令的名稱。|
|`timestamp`|org.joda.time.DateTime|傳送指令時的日期和時間。|

下列程式碼範例概述如何實作 `Command` 回呼方法：

```java
import com.ibm.iotf.client.gateway.Command;
import com.ibm.iotf.client.gateway.GatewayCallback;

public class GatewayCommandCallback implements GatewayCallback, Runnable {
	// A queue to hold and process the commands
	private BlockingQueue<Command> queue = new LinkedBlockingQueue<Command>();

	public void processCommand(Command cmd) {
  	    queue.put(cmd);
  	}

  	public void run() {
  	    while(true) {
			Command cmd = queue.take();
  	        System.out.println("Command " + cmd.getData());

  	        // code to process the command
  	    }
  	}

  	/**
	 * If a gateway subscribes to a topic of a device or sends data on behalf of a device
	 * that the gateway does not have permission to connect to, the message or the subscription is ignored.
	 * This behavior is different compared with the behavior of applications, where the connection is terminated.
	 * The Gateway is notified on the the notification topic:
	 */
  	@Override
public void processNotification(Notification notification) {

}
  }

```
將 `Command` 回呼新增至閘道用戶端時，只要發佈任何具有訂閱準則的指令，就會呼叫 `processCommand()` 方法。

下列程式碼範例概述如何將 `Command` 回呼新增至閘道用戶端實例。

```java
gwClient.connect()
GatewayCommandCallback callback = new GatewayCommandCallback();
gwClient.setGatewayCallback(callback);
//Subscribe to a device that is connected to the gateway
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

超載方法可用來控制指令訂閱。

### 列出透過閘道連接的裝置
{: #list_devices_gw}


若要將透過指定閘道（typeId、deviceId）連接的所有裝置擷取至 {{site.data.keyword.iot_short_notm}}，請呼叫 `getDevicesConnectedThroughGateway()` 方法。

```java
gwClient.connect()
gwClient.api().getDevicesConnectedThroughGateway(gatewayType, gatewayId);
```

## 範例
{: #samples}

我們提供了數個範例，以協助您將閘道及閘道後方的裝置連接至 {{site.data.keyword.iot_short_notm}} 實例。這些範例使用 {{site.data.keyword.iot_short_notm}} Java 用戶端程式庫，並位於[閘道範例 GitHub 儲存庫](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples)。

## 秘訣
{: #recipes}

| 秘訣     | 說明|
|----------------|----------------
|[將裝置當作閘道連接至 {{site.data.keyword.iot_short_notm}}](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-gateway-to-watson-iot-platform/)| GitHub 專案及詳細指示，說明如何將 Raspberry Pi 閘道及閘道後方的 Arduino Uno 裝置連接至 {{site.data.keyword.iot_short_notm}}。
|[Raspberry Pi 在 {{site.data.keyword.iot_short_notm}} 中作為受管理閘道](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/)|前一個閘道秘訣的延伸，說明如何連接在 {{site.data.keyword.iot_short_notm}} 中當作受管理裝置的 Raspberry Pi 閘道以及如何執行裝置管理作業。
