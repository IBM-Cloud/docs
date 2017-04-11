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

# 针对应用程序开发者的 Java
{: #java}


您可以使用 Java™ 来构建和定制应用程序，以用于在 {{site.data.keyword.iot_full}} 上与您的组织进行交互。提供的 {{site.data.keyword.iot_short_notm}} Java 客户机库、文档和示例可帮助您开始进行应用程序开发。

{:shortdesc}

## 下载 Java 客户机和资源
{: #java_client_download}

上次更新时间：2016 年 10 月 25 日
{: .last-updated}

要访问 {{site.data.keyword.iot_short_notm}} 的 Java 客户机库和样本，请转至 GitHub 中的 [iot-java ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-watson-iot/iot-java){: new_window} 存储库，并完成安装指示信息。


## 构造方法
{: #constructor}

构造方法用于构建客户机实例，并接受包含以下定义的 `Properties` 对象：

| 定义     |描述     |
|----------------|----------------|
|`org` |必需值，必须设置为组织标识。如果使用的是 Quickstart 流，请指定 `quickstart`。|
|`id` |组织中应用程序的唯一标识。|
|`auth-method`  |认证方法。支持的唯一方法是 `apikey`。|
|`auth-key`   |可选的 API 密钥，将 auth-method 的值设置为 `apikey` 时必须指定。|
|`auth-token`   |API 密钥令牌，将 auth-method 的值设置为 `apikey` 时，此参数也是必需的。 |
|`clean-session`|true 或 false 值，仅当要以持久预订方式连接应用程序时是必需的。缺省情况下，`clean-session` 设置为 `true`。|
|`Port`|要连接到的端口号。指定 8883 或 443。如果未指定端口号，缺省情况下客户机将通过端口号 8883 连接到 {{site.data.keyword.iot_short_notm}}。|
|`MaxInflightMessages`  |设置连接的最大未完成消息数。缺省值为 100。|
|`Automatic-Reconnect`  |true 或 false 值，要自动将处于断开连接状态的设备重新连接到 {{site.data.keyword.iot_short_notm}} 时是必需的。缺省值为 false。|
|`Disconnected-Buffer-Size`|客户机处于断开连接状态时可以存储在内存中的最大消息数。缺省值为 5000。|
|`shared-subscription`|布尔值，如果要构建可扩展应用程序，用于在应用程序的多个实例之间均衡消息负载，必须将此参数设置为 true。有关更多信息，请参阅[可扩展应用程序](../mqtt.html#scalable_apps)。`Properties` 对象创建用于与 {{site.data.keyword.iot_short_notm}} 模块进行交互的定义。如果未指定此对象的属性，或者如果指定了 `quickstart`，那么客户机将作为未注册设备连接到 {{site.data.keyword.iot_short_notm}} Quickstart 服务。

以下代码样本显示了可以如何以 `quickstart` 方式构造应用程序客户机 (`ApplicationClient`) 实例：

```
    import com.ibm.iotf.client.app.ApplicationClient;
    import java.util.Properties;

    Properties options = new Properties();
    options.put("org", "quickstart");

    ApplicationClient myClient = new ApplicationClient(options);
```

以下代码样本显示了可以如何以注册流方式构造应用程序客户机 (`ApplicationClient`) 实例：

```
    Properties options = new Properties();
    options.put("org", "uguhsp");
    options.put("id", "app" + (Math.random() * 10000));
    options.put("Authentication-Method","apikey");
    options.put("API-Key", "<API-Key>");
    options.put("Authentication-Token", "<Authentication-Token>");

    ApplicationClient myClient = new ApplicationClient(options);
```

### 使用配置文件

您可以不直接包含 `Properties` 对象，而改为使用包含 `Properties` 对象的名称/值对的配置文件，如以下代码样本中所概述：

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    ...
```
指定的应用程序配置文件必须为以下格式：

```
    [application]
    org=$orgId
    id=$myApplication
    auth-method=apikey
    auth-key=$key
    auth-token=$token
    enable-shared-subscription=true|false
```

## 连接到 {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

要连接到 {{site.data.keyword.iot_short_notm}}，请使用 `connect()` 函数。`connect()` 函数包含名为 `autoRetry` 的可选布尔值参数，用于确定在发生 MqttException 连接失败时，库是否尝试重新连接。缺省情况下，`autoRetry` 设置为 true。如果由于传递了不正确的设备注册详细信息而导致 MqttSecurityException 连接失败，那么库不会尝试重新连接，即便 `autoRetry` 设置为 true 也不例外。

要为 MQTT 设置“保持活动”时间间隔，可以选择在调用 `connect()` 函数之前，先使用 `setKeepAliveInterval(int)` 方法。`setKeepAliveInterval(int)` 值以秒为测量单位，用于定义发送或接收消息的最长间隔时间。使用此参数时，客户机可以检测到服务器何时不再可用，而无需等待 TCP/IP 超时时间段结束。客户机将确保在每个“保持活动”时间间隔时间段内，至少有一条消息在网络上传递。如果在超时时间段内未接收到与数据相关的消息，那么客户机会发送一条简短的 `ping` 消息，服务器将确认此消息。缺省情况下，`setKeepAliveInterval(int)` 设置为 60 秒。要禁用客户机上的“保持活动”处理功能，请将 `setKeepAliveInterval(int)` 值设置为 0。

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    myClient.setKeepAliveInterval(120);
    myClient.connect();
```

要控制在连接失败时执行的重试次数，请在 myClient.connect() 函数中指定一个整数，如以下代码片段中所概述：

```
    DeviceClient myClient = new DeviceClient(options);
    myClient.setKeepAliveInterval(120);
    myClient.connect(10);
```

应用程序客户机成功连接到 {{site.data.keyword.iot_short_notm}} 服务后，可以预订设备事件和状态，还可以发布设备事件和命令。

## 预订设备事件
{: #subscribing_device_events}

事件是设备将数据发布到 {{site.data.keyword.iot_short_notm}} 时所采用的机制。设备控制事件内容，并为其发送的每个事件指定名称。

{{site.data.keyword.iot_short_notm}} 实例接收到事件时，所接收事件的凭证会识别发送设备，这意味着一台设备无法冒充其他设备。


缺省情况下，应用程序会预订来自所有已连接设备的所有事件。使用设备类型、设备标识、事件和消息格式参数可控制预订的范围。以下代码样本显示了可以如何使用这些参数来定义预订范围：

### 预订来自所有设备的所有事件


```
    myClient.connect();
    myClient.subscribeToDeviceEvents();
```
### 预订来自特定类型的所有设备的所有事件


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino");
```

### 预订来自特定设备的所有事件


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee");
```
### 预订来自两个或更多不同设备的特定事件

```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee", "myEvent");
    myClient.subscribeToDeviceEvents("iotsample-arduino", "10aabbccddee", "myEvent");
```
### 预订以 JSON 格式发布的事件


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee", "myEvent", "json", 0);
```

**注**：单个客户机可支持多个预订。

## 处理来自设备的事件
{: #handling_device_events}

要处理预订接收到的事件，请注册事件回调方法。消息将作为 Event 类的实例返回，此类具有以下参数：

|参数|数据类型|描述|
|:---|:---|
|`event.device`|字符串|在组织内所有类型的设备中作为该设备的唯一标识。|
|`event.deviceType`|字符串|标识设备类型。通常，deviceType 是对执行特定任务的设备的一种分组，例如，“weatherballoon”可能是一种设备类型。|
|`event.deviceId`|字符串|表示设备的标识。通常，对于特定设备类型，deviceId 是该设备的唯一标识，例如序列号或 MAC 地址。|
|`event.event`|字符串|通常用于对特定事件分组，例如“status”、“warning”和“data”。|
|`event.format`|字符串|格式可以为任意字符串，例如 JSON。  |
|`event.data`|字典|消息有效内容的数据。最大长度为 131072 字节。|
|`event.timestamp`|日期和时间|事件的日期和时间|


以下代码提供了实现事件回调的样本：

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

事件回调添加到 ApplicationClient 后，每当发布与预订匹配的事件时，都会调用 `processEvent()` 方法。以下片段显示了如何将事件回调添加到 ApplicationClient 实例：



```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToDeviceEvents();
```

与预订设备事件类似，应用程序可以预订发送到设备的命令。以下代码样本显示了如何为组织中的所有设备预订所有命令：

```

    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToDeviceCommands();
```

重载方法可用于控制命令预订。向与命令预订匹配的设备发送命令时，会调用 `processCommand()` 方法。


## 预订设备状态
{: #subscribing_device_status}

与预订设备事件类似，应用程序也可以预订设备状态，例如设备与 {{site.data.keyword.iot_short_notm}} 建立或断开连接。缺省情况下，此预订会预订所有已连接设备的状态更新。使用设备类型和设备标识参数可控制预订范围。以下代码样本显示了可以如何使用这些参数来定义预订范围：

### 预订所有设备的状态更新

```
    myClient.connect();
    myClient.subscribeToDeviceStatus();
```

### 预订特定类型的所有设备的状态更新


```

    myClient.connect();
    myClient.subscribeToDeviceStatus("iotsample-arduino");
```

### 预订两个不同设备的状态更新


```

    myClient.connect();
    myClient.subscribeToDeviceStatus("iotsample-arduino", "00aabbccddee");
    myClient.subscribeToDeviceStatus("iotsample-arduino", "10aabbccddee");
```

**注**：单个客户机可支持多个预订。

## 处理来自设备的状态更新
{: #handling_device_status_updates}

要处理预订接收到的状态更新，需要注册状态事件回调方法。对于 `Connect` 和 `Disconnect` 状态事件，消息将作为 Status 类的实例返回，此类包含以下参数：


| 参数     |数据类型     |
|----------------|----------------|
|`status.clientAddr` |字符串|
|`status.protocol`  |字符串|
|`status.clientId`   |字符串|
|`status.user`   |字符串|
|`status.time`   |java.util.Date|
|`status.action` |字符串|
|`status.connectTime`   |java.util.Date|
|`status.port`|整数|

仅当状态事件为 `Disconnect` 时，才可设置以下属性：

| 属性     |数据类型     |
|----------------|----------------|
|`status.writeMsg` |整数|
|`status.readMsg`  |整数|
|`status.reason`   |字符串|
|`status.readBytes`   |整数|
|`status.writeBytes`   |整数|


以下代码样本提供了实现状态回调的示例：

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

将状态回调添加到应用程序客户机后，每当匹配条件的设备与 {{site.data.keyword.iot_short_notm}} 建立或断开连接时，都会调用 `processDeviceStatus()` 方法。以下代码样本显示了可以如何将状态回调实例添加到应用程序客户机：

```

    myClient.connect()
    myClient.setStatusCallback(new MyStatusCallback());
    myClient.subscribeToDeviceStatus();
```
应用程序可以预订其他任何应用程序状态，例如应用程序与 {{site.data.keyword.iot_short_notm}} 建立或断开连接。以下代码片段显示了如何预订 {{site.data.keyword.iot_short_notm}} 组织的应用程序状态：

```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToApplicationStatus();
```
重载方法可用于控制对特定应用程序的状态预订。每当匹配条件的应用程序与 {{site.data.keyword.iot_short_notm}} 建立或断开连接时，都会调用 `processApplicationStatus()` 方法。


## 发布来自设备的事件
{: #publishing_events_devices}

以下代码样本显示了应用程序如何发布事件以使其看起来是源自设备的事件。

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


事件可以使用不同的格式（例如，JSON、字符串、二进制等）进行发布。缺省情况下，库会以 JSON 格式发布事件，但您可以根据需要指定其他格式的数据。例如，要以字符串格式发布数据，请使用以下代码片段。

```
    myClient.connect();
    String data = "cpu:"+60;
    status = myClient.publishEvent("load", data, "text", 2);
```
**注：**在先前的代码示例中，事件的有效内容必须为字符串格式。

任何 XML 数据都可以转换为字符串，并按如下所示进行发布：

```
    status = myClient.publishEvent("load", xmlConvertedString, "xml", 2);
```

与此类似，要以二进制格式发布事件，请使用字节数组，如以下示例中所概述：

```
    myClient.connect();
    byte[] cpuLoad = new byte[] {60, 35, 30, 25};
    status = myClient.publishEvent("blink", cpuLoad , "binary", 1);
```

### 使用 HTTP 发布事件
{: #publishing_events_http}

除了使用 MQTT 外，还可以配置应用程序，以通过 HTTP 将设备事件发布到 {{site.data.keyword.iot_short_notm}}。以下步骤概述了通过 HTTP 发布设备事件的序列：

1. 使用属性文件构造 ApplicationClient 实例。
2. 构造需要发布的事件。
3. 指定事件名称、设备类型和设备标识。
4. 使用 `publishEventOverHTTP()` 方法发布事件，如以下代码示例中所示：

```
    	ApplicationClient myClient = new ApplicationClient(props);

    	JsonObject event = new JsonObject();
    	event.addProperty("name", "foo");
    	event.addProperty("cpu",  90);
    	event.addProperty("mem",  70);

    	boolean status = myClient.publishApplicationEventforDeviceOverHTTP(deviceId, deviceType, "blink", event, ContentType.json);
```

有关完整的代码样本，请参阅 [HttpApplicationDeviceEventPublish ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpApplicationDeviceEventPublish.java){: new_window} 应用程序示例。

根据属性文件中的设置，`publishEventOverHTTP()` 方法会在 Quickstart 或注册流中发布事件。如果 `quickstart` 在属性文件中指定为组织标识，那么 `publishEventOverHTTP()` 方法会将事件以纯 HTTP 格式发布到 {{site.data.keyword.iot_short_notm}} Quickstart 服务。如果在属性文件中指定的已注册组织有效，那么会始终使用 HTTPS 来发布事件以确保所有通信的安全。

HTTP 协议提供“至多一次”传递，这类似于 MQTT 协议的“至多一次”(QoS 0) 服务质量级别。使用“至多一次”传递来发布事件时，应用程序必须实现出错情况下的重试逻辑。


## 将命令发布到设备
{: #publishing_commands_devices}

应用程序可以将命令发布到已连接设备，如以下示例中所示：

```

    myClient.connect()

    //Generate the event to be published
    JsonObject data = new JsonObject();
    data.addProperty("name", "stop-rotation");
    data.addProperty("delay",  0);

    //Registered flow allows 0, 1 and 2 QoS
    myAppClient.publishCommand(deviceType, deviceId, "stop", data);
```

### 使用 HTTP 发布命令
{: #publishing_commands_http}

除了使用 MQTT 外，还可以将应用程序配置为通过 HTTP 将命令发布到连接的设备。以下步骤概述了使用 HTTP 发布设备事件的序列：

1. 使用属性文件构造 ApplicationClient 实例
2. 构造需要发布的命令
3. 指定命令名、设备类型和设备标识
4. 使用 `publishCommandOverHTTP` 方法发布命令，如以下代码中所示：

```

    	ApplicationClient myClient = new ApplicationClient(props);

    	// Generate a JSON object of the event to be published
	JsonObject event = new JsonObject();
	event.addProperty("reboot", 5);

	boolean response = myClient.publishCommandOverHTTP("execute", event);
```

要查看完整的代码样本，请参阅 [HttpCommandPublish ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpCommandPublish.java){: new_window} 应用程序示例。

HTTP 协议提供“至多一次”传递，这类似于 MQTT 协议的“至多一次”(QoS 0) 服务质量级别。使用“至多一次”传递来发布命令时，应用程序必须实现出错情况下的重试逻辑。有关更多信息，请参阅[针对应用程序的 HTTP REST API](../api.html)。


## 样本
{: #samples}

-  [MQTTApplicationDeviceEventPublish![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/MQTTApplicationDeviceEventPublish.java){: new_window} - 显示如何发布设备事件的样本应用程序。
-   [RegisteredApplicationCommandPublish![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationCommandPublish.java){: new_window} - 显示如何向设备发布命令的样本应用程序。
-  [RegisteredApplicationSubscribeSample ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationSubscribeSample.java){: new_window} - 显示如何预订不同事件（例如，设备事件、设备命令、设备状态和应用程序状态）的样本应用程序。
-   [SharedSubscriptionSample ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/SharedSubscriptionSample.java){: new_window} - 显示如何构建可扩展应用程序以便在应用程序的多个实例之间进行消息负载均衡的样本应用程序。
-  [Backup-restore-sample ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-messaging/iot-backup-restore-sample){: new_window} - 显示可以如何备份和恢复 {{site.data.keyword.cloudant}} 中的设备配置的样本。
