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

#在 {{site.data.keyword.iot_short_notm}} 上使用 Java 开发网关
{: #java_cli_gw}

如果设备无法直接连接到 {{site.data.keyword.iot_full}} 上的组织，那么可以使用 Java™ 来构建并定制网关。提供的 {{site.data.keyword.iot_short_notm}} Java 客户机库、文档和示例可帮助您开始进行网关开发。
{:shortdesc}

## 下载 Java 客户机和资源
{: #java_client_download}

要访问 {{site.data.keyword.iot_short_notm}} 的 Java 客户机库和样本，请转至 GitHub 中的 [iot-java](https://github.com/ibm-watson-iot/iot-java) 存储库，并完成安装指示信息。

## 构造方法
{: #constructor}

构造方法用于构建网关客户机实例，并接受包含以下定义的 `Properties` 对象：

|定义 |描述 |
|:----|:----|
|`org`|必需值，必须设置为组织标识。如果使用的是 Quickstart 流，请指定 `quickstart`。|
|`domain`|消息传递端点 URL，这是可选项。如果未指定 domain 的值，那么 URL 将缺省为 `internetofthings.ibmcloud.com`，这是 {{site.data.keyword.iot_short_notm}} 生产服务器。|
|`type`|必需值，用于指定网关的类型。|
|`id` |必需值，用于指定网关的唯一标识。|
|`auth-method`|要使用的认证方法。支持的唯一方法是 `token`。|
|`auth-token`|用于将网关安全连接到 {{site.data.keyword.iot_short_notm}} 的 API 密钥认证令牌。|
|`clean-session`|true 或 false 值，仅当要以持久预订方式连接网关时是必需的。缺省情况下，`clean-session` 设置为 true。|
|`WebSocket`|true 或 false 值，仅当要使用 WebSocket 连接网关时是必需的。|
|`Port`|要连接到的端口号。指定 8883 或 443。如果未指定端口号，缺省情况下客户机将通过端口号 8883 连接到 {{site.data.keyword.iot_short_notm}}。|
|`MaxInflightMessages`|设置连接的最大未完成消息数。缺省值为 100。|
|`Automatic-Reconnect`|true 或 false 值，要自动将处于断开连接状态的网关重新连接到 {{site.data.keyword.iot_short_notm}} 时是必需的。缺省值为 false。|
|`Disconnected-Buffer-Size`|客户机处于断开连接状态时可以存储在内存中的最大消息数。缺省值为 5000。|

**注：**要以持久预订方式连接网关，请将 `clean-session` 设置为 `false`。有关干净会话的更多信息，请参阅 [MQTT 文档](../../reference/mqtt/index.html#subscription-buffers-and-clean-session)的“预订缓冲区和干净会话”部分。

`Properties` 对象创建用于与 {{site.data.keyword.iot_short_notm}} 模块进行交互的定义。

以下代码样本显示了如何构造网关客户机实例：

```java
Properties options = new Properties();
options.setProperty("org", "<Your organization ID>");
options.setProperty("type", "<The gateway device type>");
options.setProperty("id", "The gateway device ID");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "API token");
GatewayClient gwClient = new GatewayClient(options);

```


### 使用配置文件

您可以不直接使用 `Properties` 对象来创建网关实例，而改为使用包含网关属性的名称/值对的配置文件。要使用配置文件来构建网关的 `Properties` 对象，请使用以下代码格式：

```Java
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
...
```

配置文件的内容必须为以下格式：

```java
[Gateway]
org=$orgId
domain=$domain
typ=$myGatewayDeviceType
id=$myGatewayDeviceId
auth-method=token
auth-token=$token

```

## 连接到 {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

要连接到 {{site.data.keyword.iot_short_notm}}，请使用 `connect()` 函数。`connect()` 函数包含名为 `autoRetry` 的可选布尔值参数，用于确定在连接因 MQTT 异常 (MqttException) 而失败时，库是否尝试重新连接。缺省情况下，`autoRetry` 设置为 true。如果由于传递了不正确的设备注册详细信息而导致 MqttSecurityException 连接失败，那么库不会尝试重新连接，即便 `autoRetry` 设置为 true 也不例外。

要为 MQTT 设置保持活动时间间隔，可以选择在调用 `connect()` 函数之前，先使用 `setKeepAliveInterval(int)` 方法。`setKeepAliveInterval(int)` 值以秒为测量单位，用于定义发送或接收消息的最长间隔时间。指定了 `setKeepAliveInterval(int)` 值时，客户机无需等待 TCP/IP 超时时间段结束即可检测到服务器不再可用。客户机将确保在每个保持活动时间间隔时间段内，至少有一条消息在网络上传递。如果在超时时间段内未接收到与数据相关的消息，那么客户机会发送一条简短的 `ping` 消息，服务器将确认此消息。缺省情况下，`setKeepAliveInterval(int)` 设置为 60 秒。要禁用客户机上的保持活动处理功能，请将 `setKeepAliveInterval(int)` 值设置为 0。

```java
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
gwClient.setKeepAliveInterval(80);
gwClient.connect();
```

要控制在连接失败时执行的重试次数，请使用重载的 connect(int numberOfTimesToRetry) 函数。

```java
GatewayClient gwClient = new GatewayClient(props);
gwClient.setKeepAliveInterval(80);
gwClient .connect(10);
```

网关客户机成功连接到 {{site.data.keyword.iot_short_notm}} 后，网关可以为自己以及代表连接到该网关的设备发布事件并预订命令。

## 注册位于网关后面的设备
{: #register_device_gateway}

可以注册位于自动或通过使用 API 开发代码来连接到 {{site.data.keyword.iot_short_notm}} 实例的网关后面的设备。

### 自动设备注册
每当网关为连接到自己的设备发布任何事件或预订任何命令时，都可以在 {{site.data.keyword.iot_short_notm}} 上自动注册设备。

### API 设备注册
此外，还可以使用 {{site.data.keyword.iot_short_notm}} API 将位于网关后面的设备注册到 {{site.data.keyword.iot_short_notm}} 实例。

要简化使用 {{site.data.keyword.iot_short_notm}} API 进行开发的工作，请通过调用 api() 方法来启动 API 客户机实例，如以下代码样本中所概述：

```java
import com.ibm.iotf.client.api.APIClient;
....

GatewayClient gwClient = new GatewayClient(props);
gwClient.connect();

APIClient api = gwClient.api();
```
接收到 API 客户机的句柄时，可以开始向网关注册设备，如以下代码样本中所概述：
```java
gwClient.connect();

  String deviceToBeAdded = "{\"deviceId\": \"" + DEVICE_ID +
					"\",\"authToken\": \"qwer123\"}";

    JsonParser parser = new JsonParser();
    JsonElement input = parser.parse(deviceToBeAdded);
    JsonObject response = this.gwClient.api().registerDeviceUnderGateway(DEVICE_TYPE, gwDeviceId, gwDeviceType, input);

```

注册位于网关后面的设备时，该设备会通过 `gwDeviceId` 和 `gwDeviceType` 属性的值与该网关相关联。

## 发布事件
{: #publish_events}

事件是网关和设备用于将数据发布到 {{site.data.keyword.iot_short_notm}} 的机制。网关或设备控制事件内容，并为其发送的每个事件指定名称。网关可以从自身发布事件，也可以代表通过该网关连接的任何设备发布事件。

{{site.data.keyword.iot_short_notm}} 实例接收到事件时，所接收事件的凭证会识别发送网关，这意味着一个网关无法冒充其他设备。

可以在 MQTT 协议定义的三个[服务质量 (QoS) 级别](../../reference/mqtt/index.html#qos-levels)中的任一级别发布事件。缺省情况下，事件在 QoS=0 级别发布。

### 用于在缺省 QoS 级别发布网关事件的代码

```java
gwClient.connect();
  JsonObject event = new JsonObject();
  event.addProperty("name", "foo");
  event.addProperty("cpu",  90);
  event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event);
```

### 用于提高事件的缺省 QoS 级别的代码

可以提高已发布网关事件的 [QoS 级别](../../reference/mqtt/index.html#qos-levels)。QoS 级别大于零的事件发布所用时间可能更长，因为包含额外的接收确认信息。


```java
gwClient.connect();
  JsonObject event = new JsonObject();
  event.addProperty("name", "foo");
  event.addProperty("cpu",  90);
  event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event, 2);
```

### 用于以定制格式发布事件的代码

事件可以使用不同的格式（例如，JSON、字符串、二进制等）进行发布。缺省情况下，库会以 JSON 格式发布事件，但您可以根据需要指定其他格式的数据。例如，要以字符串格式发布数据，请使用以下代码片段：

```java
gwClient.connect();
String data = "cpu:80";
boolean status = gwClient.publishGatewayEvent("load", data, "text", 2);
```

**注：**在先前的代码示例中，事件的有效内容必须为字符串格式。



XML 数据可以转换为字符串格式并发布，如以下代码样本中所概述：

```java
status = gwClient.publishGatewayEvent("load", xmlConvertedString, "xml", 2);
```

与此类似，要以二进制格式发布事件，请使用以下示例中所概述的字节数组：

```java
gwClient.connect();
byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = gwClient.publishGatewayEvent("blink", cpuLoad , "binary", 1);
```

### 用于发布来自设备的事件的代码
{: #publishing_events_devices}

网关可以代表经由该网关连接的任何设备，通过传递原始事件的相应类型标识和设备标识值来发布事件，如以下样本中所概述：

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

使用重载的 `publishDeviceEvent()` 方法在首选服务质量级别发布设备事件。有关使用的主题结构的更多信息，请参阅[网关的 MQTT 连接](../mqtt.html)。

### 用于发布定制格式的设备事件的代码

与网关事件类似，设备事件也可以采用不同格式发布。缺省情况下，库会以 JSON 格式发布设备事件，但您可以根据需要采用不同格式指定数据。例如，要以字符串格式发布数据，请使用以下代码样本：

```java
gwClient.connect();
String data = "cpu:80";
boolean status = gwClient.publishDeviceEvent(deviceType, deviceId, "load", data, "text", 2);
```

**注：**事件的有效内容必须为字符串格式。

任何 XML 数据都可以转换为字符串格式并发布，如以下示例中所示：

```java
status = gwClient.publishDeviceEvent(deviceType, deviceId, "load", xmlConvertedString, "xml", 2);
```

与此类似，要以二进制格式发布设备事件，请使用以下示例中所概述的字节数组：
```java
gwClient.connect();
byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = gwClient.publishDeviceEvent(deviceType, deviceId, "blink", cpuLoad , "binary", 1);
```

## 处理命令
{: #handling_commands}

网关可以预订针对该网关本身以及在网关后面连接的任何设备的命令。网关客户机进行连接时，会自动预订针对此网关的所有命令。但要预订针对通过网关连接的设备的任何命令，请使用重载的 `subscribeToDeviceCommands()` 方法，如以下示例中所概述：

```java
gwClient.connect()

// subscribe to commands on behalf of device
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

要处理特定命令，需要注册 `Command` 回调方法。消息将作为 `Command` 类的实例返回，并包含以下属性：


| 属性     |数据类型     | 描述|
|----------------|----------------|---------------
|`deviceType`|字符串| 为其接收命令的设备类型。|
|`deviceId`|字符串| 为其接收命令的设备标识，可以为网关或通过网关连接的设备。|
|`data`|对象| 命令有效内容。|
|`format`|字符串| 命令有效内容的格式，可以为任意字符串，例如 JSON、二进制、文本或其他。|
|`command`|字符串|命令的名称。|
|`timestamp`|org.joda.time.DateTime|发送命令的日期和时间。|

以下代码样本概述了可以如何实现 `Command` 回调方法：

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
`Command` 回调添加到网关客户机后，每当发布具有所预订条件的任何命令时，都会调用 `processCommand()` 方法。

以下代码样本概述了如何将 `Command` 回调添加到网关客户机实例中。

```java
gwClient.connect()
GatewayCommandCallback callback = new GatewayCommandCallback();
gwClient.setGatewayCallback(callback);
//Subscribe to a device that is connected to the gateway
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

重载方法可用于控制命令预订。

### 列出通过网关连接的设备
{: #list_devices_gw}


要检索通过指定网关 (typeId, deviceId) 连接到 {{site.data.keyword.iot_short_notm}} 的所有设备，请调用 `getDevicesConnectedThroughGateway()` 方法。

```java
gwClient.connect()
gwClient.api().getDevicesConnectedThroughGateway(gatewayType, gatewayId);
```

## 样本
{: #samples}

有多个样本可帮助您将网关和位于网关后面的设备连接到您的 {{site.data.keyword.iot_short_notm}} 实例。这些样本使用 {{site.data.keyword.iot_short_notm}} Java 客户机库，并位于[网关样本 GitHub 存储库 ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples){: new_window} 中。

## 诀窍
{: #recipes}

| 诀窍     | 描述|
|----------------|----------------
|[Connecting your device as a gateway to {{site.data.keyword.iot_short_notm}} ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-gateway-to-watson-iot-platform/){: new_window}| 一个 GitHub 项目和详细指示信息，说明了如何将 Raspberry Pi 网关和位于该网关后面的 Arduino Uno 设备连接到 {{site.data.keyword.iot_short_notm}}。
|[RaspberryPi as a managed gateway in {{site.data.keyword.iot_short_notm}} ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/){: new_window}|上一个网关诀窍的扩展，说明了如何将 Raspberry Pi 网关作为 {{site.data.keyword.iot_short_notm}} 中的受管设备进行连接以及如何执行设备管理操作。
