---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 针对应用程序开发者的 Java
{: #java}

上次更新时间：2016 年 9 月 7 日
{: .last-updated}

您可以使用 Java 来构建和定制应用程序，以用于与 {{site.data.keyword.iot_full}} 上的组织进行交互。使用提供的信息和示例通过 Java 开始开发应用程序。
{:shortdesc}

## 下载 Java 客户机和资源
{: #java_client_download}

要访问 {{site.data.keyword.iot_short_notm}} 的 Java 客户机库和样本，请转至 GitHub 中的 [iot-java](https://github.com/ibm-watson-iot/iot-java) 存储库，并完成安装指示信息。


## 构造方法
{: #constructor}

构造方法用于构建客户机实例，并接受包含以下定义的 `Properties` 对象：

| 定义     |描述     |
|----------------|----------------|
|`org` |组织标识。这是必需值。如果使用的是 Quickstart 流，请指定 `quickstart`。|
|`id` |组织中应用程序的唯一标识。|
|`auth-method`  |认证方法，当前支持的唯一值是 `apikey`|
|`auth-key`   |可选的 API 密钥，auth-method 设置为 `apikey` 时是必需的。  |
|`auth-token`   |API 密钥令牌，auth-method 设置为 `apikey` 时是必需的。 |
|`clean-session`|true 或 false 值，仅当要以持久预订方式连接应用程序时是必需的。缺省情况下，`clean-session` 设置为 `true`。|
|`shared-subscription`|布尔值。如果要构建可扩展应用程序，用于跨应用程序的多个实例均衡消息负载，请设置为 `true`。有关更多信息，请参阅[可扩展应用程序](mqtt.html#/scalable-applications#scalable-applications)。`Properties` 对象创建用于与 {{site.data.keyword.iot_short_notm}} 模块进行交互的定义。如果未指定此对象的属性，或者如果指定了 `quickstart`，那么客户机将作为未注册设备连接到 {{site.data.keyword.iot_short_notm}} Quickstart 服务。

以下代码样本显示了可以如何以 `quickstart` 方式构造 ApplicationClient 实例：

```
    import com.ibm.iotf.client.app.ApplicationClient;
    import java.util.Properties;

    Properties options = new Properties();
    options.put("org", "quickstart");

    ApplicationClient myClient = new ApplicationClient(options);
```

以下代码样本显示了可以如何以注册流方式构造 ApplicationClient 实例：

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

您可以不直接包含 `Properties` 对象，而改为使用包含以下格式的 `Properties` 对象名称/值对的配置文件：

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    ...
```
应用程序配置文件必须为以下格式：

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

要连接到 {{site.data.keyword.iot_short_notm}}，请使用 `connect()` 函数。`connect()` 函数包含名为 `autoRetry` 的可选布尔值参数，用于确定发生 MqttException 连接失败时，库是否尝试重新连接。缺省情况下，`autoRetry` 设置为 true。如果由于传递了不正确的设备注册详细信息而导致 MqttSecurityException 连接失败，那么库不会尝试重新连接，即便 `autoRetry` 设置为 `true` 也不例外。

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);

    myClient.connect();
```

成功连接到 {{site.data.keyword.iot_short_notm}} 服务后，应用程序客户机可以预订设备事件，预订设备状态以及发布设备事件和命令。

## 预订设备事件
{: #subscribing_device_events}

事件是设备用于将数据发布到 {{site.data.keyword.iot_short_notm}} 的机制。设备控制事件内容，并为其发送的每个事件指定名称。

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
|`event.device`|字符串|在组织中的所有类型设备中唯一标识设备。|
|`event.deviceType`|字符串|标识设备类型。通常，deviceType 是一组执行特定任务的设备，例如“weatherballoon”。|
|`event.deviceId`|字符串|表示设备的标识。通常，对于给定设备类型，deviceId 是该设备的唯一标识，例如序列号或 MAC 地址。|
|`event.event`|字符串|通常用于对特定事件分组，例如“status”、“warning”和“data”。|
|`event.format`|字符串|格式可以为任意字符串，例如 JSON。  |
|`event.data`|字典|消息有效内容的数据。最大长度为 131072 字节。|
|`event.timestamp`|日期和时间|事件的日期和时间|


以下代码是事件回调的样本实现：

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

与预订设备事件类似，应用程序可以预订发送到设备的命令。以下代码样本显示了如何预订组织中所有设备的所有命令：

```

    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToDeviceCommands();
```

重载方法可用于控制命令预订。向与命令预订匹配的设备发送命令时，会调用 `processCommand()` 方法。


## 预订设备状态
{: #subscribing_device_status}

与预订设备事件类似，应用程序可以预订设备状态，例如设备连接到 {{site.data.keyword.iot_short_notm}} 以及从其断开连接。缺省情况下，此预订会预订所有已连接设备的状态更新。使用设备类型和设备标识参数可控制预订范围。以下代码样本显示了可以如何使用这些参数来定义预订范围：

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

### 预订两种不同设备的状态更新


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

仅当状态事件设置为 `Disconnect` 时，才可设置以下属性：

| 属性     |数据类型     |
|----------------|----------------|
|`status.writeMsg` |整数|
|`status.readMsg`  |整数|
|`status.reason`   |字符串|
|`status.readBytes`   |整数|
|`status.writeBytes`   |整数|


以下代码样本是状态回调的示例实施：

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

状态回调添加到 ApplicationClient 后，每当与条件匹配的设备连接到 {{site.data.keyword.iot_short_notm}} 或从其断开连接时，都会调用 `processDeviceStatus()` 方法。以下代码样本显示了可以如何将状态回调实例添加到 ApplicationClient：

```

    myClient.connect()
    myClient.setStatusCallback(new MyStatusCallback());
    myClient.subscribeToDeviceStatus();
```
应用程序可以预订其他任何应用程序状态，例如应用程序连接到 Watson IoT Platform 以及应用程序从其断开连接。以下代码片段显示了如何预订组织中的应用程序状态：                                              

```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToApplicationStatus();
```
重载方法可用于控制对特定应用程序的状态预订。每当与条件匹配的应用程序连接到 {{site.data.keyword.iot_short_notm}} 或从其断开连接时，都会调用 processApplicationStatus() 方法。

## 发布来自设备的事件
{: #publishing_events_devices}

以下代码样本显示了应用程序可以如何把事件当作源自设备的事件进行发布。

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

### 使用 HTTP 发布事件
{: #publishing_events_http}

除了 MQTT，还可以通过完成以下步骤使用 HTTP 来配置应用程序，以将设备事件发布到 {{site.data.keyword.iot_short_notm}}：

* 使用属性文件构造 ApplicationClient 实例
* 构造需要发布的事件
* 指定事件名称、设备类型和设备标识
* 使用 `publishEventOverHTTP()` 方法发布事件，如以下代码中所示：

```

    	ApplicationClient myClient = new ApplicationClient(props);

    	JsonObject event = new JsonObject();
    	event.addProperty("name", "foo");
    	event.addProperty("cpu",  90);
    	event.addProperty("mem",  70);

    	code = myClient.publishEventOverHTTP(deviceType, deviceId, "blink", event);
```

有关完整的代码样本，请参阅以下应用程序示例：

[HttpApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpApplicationDeviceEventPublish.java)

根据属性文件中的设置，`publishEventOverHTTP()` 方法会在 Quickstart 或注册流中发布事件。`quickstart` 是属性文件中指定的组织标识时，`publishEventOverHTTP()` 方法会将事件以纯文本格式发布到 {{site.data.keyword.iot_short_notm}} Quickstart 服务。在属性文件中指定有效的已注册组织时，事件始终会使用 HTTPS 进行发布，以便所有通信都安全。

HTTP 协议提供了“至多一次”传递，这类似于 MQTT 协议的“至多一次”(QoS 0) 服务质量级别。使用“至多一次”传递来发布事件时，如果发生错误，应用程序必须实现重试逻辑。


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


## 示例
{: #examples}


-  [MQTTApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/MQTTApplicationDeviceEventPublish.java) - 显示可以如何发布设备事件的样本应用程序。
-   [RegisteredApplicationCommandPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationCommandPublish.java) - 显示可以如何向设备发布命令的样本应用程序。
-  [RegisteredApplicationSubscribeSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationSubscribeSample.java) - 显示可以如何预订不同事件（例如，设备事件、设备命令、设备状态和应用程序状态）的样本应用程序。
-   [SharedSubscriptionSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/SharedSubscriptionSample.java) - 显示可以如何构建可扩展应用程序，用于跨应用程序的多个实例均衡消息负载的样本应用程序。
-  [备份和恢复样本](https://github.com/ibm-messaging/iot-backup-restore-sample) - 显示可以如何备份和恢复 NoSQL 数据库中设备配置的样本。
