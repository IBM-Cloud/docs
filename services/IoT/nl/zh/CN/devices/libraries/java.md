---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-10-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 针对设备开发者的 Java
{: #java}

您可以使用 Java™ 来构建和定制设备，以用于在 {{site.data.keyword.iot_full}} 上与您的组织进行交互。提供的 {{site.data.keyword.iot_short_notm}} Java 客户机库、文档和示例可帮助您开始进行设备开发。
{:shortdesc}

## 下载 Java 客户机和资源
{: #java_client_download}

要访问 {{site.data.keyword.iot_short_notm}} 的 Java 客户机库和样本，请转至 GitHub 中的 [iot-java](https://github.com/ibm-watson-iot/iot-java) 存储库，并完成安装指示信息。

## 构造方法
{: #constructor}

构造方法用于构建客户机实例，并接受包含以下定义的 `Properties` 对象：

|定义 |描述 |
|:----|:----|
|`org` |必需值，必须设置为组织标识。如果使用的是 Quickstart 流，请指定 `quickstart`。|
|`type`  |必需值，用于指定设备的类型。|
|`id`  |必需值，用于指定设备的唯一标识。|
|`auth-method`  |要使用的认证方法。支持的唯一方法是 `token`。|
|`auth-token`   |用于将设备安全连接到 {{site.data.keyword.iot_short_notm}} 的认证令牌。|
|`clean-session`|true 或 false 值，仅当要以持久预订方式连接应用程序时是必需的。缺省情况下，`clean-session` 设置为 true。|
|`Port`|要连接到的端口号。指定 8883 或 443。如果未指定端口号，缺省情况下客户机将通过端口号 8883 连接到 {{site.data.keyword.iot_short_notm}}。|
|`MaxInflightMessages`  |设置连接的最大未完成消息数。缺省值为 100。|
|`Automatic-Reconnect`  |true 或 false 值，要自动将处于断开连接状态的设备重新连接到 {{site.data.keyword.iot_short_notm}} 时是必需的。缺省值为 false。|
|`Disconnected-Buffer-Size`|客户机处于断开连接状态时可以存储在内存中的最大消息数。缺省值为 5000。|
|`WebSocket`|true 或 false 值，仅当要使用与 {{site.data.keyword.iot_short_notm}} 的 websocket 连接时是必需的。缺省值为 false。|

**注：**要以持久预订方式连接设备，请将 `clean-session` 设置为 `false`。有关干净会话的更多信息，请参阅 [MQTT 文档](../../reference/mqtt/index.html#subscription-buffers-and-clean-session)的“预订缓冲区和干净会话”部分。

`Properties` 对象创建用于与 {{site.data.keyword.iot_short_notm}} 模块进行交互的定义。

以下代码样本显示了设备可以如何以 Quickstart 方式发布事件。

```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class QuickstartDeviceEventPublish {

    public static void main(String[] args) {

        //使用 Properties 类提供特定于设备的数据
        Properties options = new Properties();
        options.setProperty("org", "quickstart");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");

        DeviceClient myClient = null;
        try {
            //通过传递属性文件对类进行实例化
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //连接到 {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //生成要发布的事件的 JSON 对象
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Quickstart 流仅允许 QoS = 0
        myClient.publishEvent("status", event, 0);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

以下代码样本显示了设备如何在注册流中发布事件。


```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class RegisteredDeviceEventPublish {

    public static void main(String[] args) {

        //使用 Properties 类提供特定于设备的数据以及认证密钥和令牌
        Properties options = new Properties();

        options.setProperty("org", "uguhsp");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");
        options.setProperty("auth-method", "token");
        options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");

        DeviceClient myClient = null;
        try {
            //通过传递属性文件对类进行实例化
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //连接到 {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //生成要发布的事件的 JSON 对象
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //注册流允许 QoS 为 0、1 和 2
        myClient.publishEvent("status", event);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

### 使用配置文件

您可以不直接使用 `Properties` 对象，而改为使用包含 Properties 的名称/值对的配置文件。如果要使用包含 `Properties` 对象的配置文件，请使用以下代码格式：

```
package com.ibm.iotf.sample.client.device;

import java.io.File;
import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class RegisteredDeviceEventPublishPropertiesFile {

    public static void main(String[] args) {
        //使用 Properties 类提供特定于设备的数据以及认证密钥和令牌
        Properties options = DeviceClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));

        DeviceClient myClient = null;
        try {
            //通过传递属性文件对类进行实例化
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //连接到 {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //生成要发布的事件的 JSON 对象
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //注册流允许 QoS 为 0、1 和 2
        myClient.publishEvent("status", event, 1);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

配置文件的内容必须为以下格式：

```
    [device]
    org=$orgId
    typ=$myDeviceType
    id=$myDeviceId
    auth-method=token
    auth-token=$token
```

## 连接到 {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}


要连接到 {{site.data.keyword.iot_short_notm}}，请使用 `connect()` 函数。`connect()` 函数包含名为 `autoRetry` 的可选布尔值参数，用于确定在发生 MqttException 连接失败时，库是否尝试重新连接。缺省情况下，`autoRetry` 设置为 true。如果由于传递了不正确的设备注册详细信息而导致 MqttSecurityException 连接失败，那么库不会尝试重新连接，即便 `autoRetry` 设置为 true 也不例外。

要为 MQTT 设置“保持活动”时间间隔，可以选择在调用 `connect()` 函数之前，先使用 `setKeepAliveInterval(int)` 方法。`setKeepAliveInterval(int)` 值以秒为测量单位，用于定义发送或接收消息的最长间隔时间。使用此参数时，客户机可以检测到服务器何时不再可用，而无需等待 TCP/IP 超时时间段结束。客户机将确保在每个“保持活动”时间间隔时间段内，至少有一条消息在网络上传递。如果在超时时间段内未接收到与数据相关的消息，那么客户机会发送一条简短的 `ping` 消息，服务器将确认此消息。缺省情况下，`setKeepAliveInterval(int)` 设置为 60 秒。要禁用客户机上的“保持活动”处理功能，请将 `setKeepAliveInterval(int)` 值设置为 0。


```
DeviceClient myClient = new DeviceClient(options);
myClient.setKeepAliveInterval(120);
myClient.connect(true);
```

要控制在连接失败时执行的重试次数，请使用重载的 connect(int numberOfTimesToRetry) 函数。


```
DeviceClient myClient = new DeviceClient(options);
myClient.setKeepAliveInterval(120);
myClient.connect(10);
```

设备成功连接到 {{site.data.keyword.iot_short_notm}} 后，可以通过应用程序发布事件和预订设备命令。


## 发布事件
{: #publishing_events}

事件是设备将数据发布到 {{site.data.keyword.iot_short_notm}} 时所采用的机制。设备控制事件内容，并为其发送的每个事件指定名称。

{{site.data.keyword.iot_short_notm}} 实例接收到事件时，所接收事件的凭证会识别发送设备，这意味着一台设备无法冒充其他设备。

可以在 MQTT 协议定义的三个[服务质量 (QoS) 级别](../../reference/mqtt/index.html#qos-levels)中的任一级别发布事件。缺省情况下，事件在 QoS=0 级别发布。

### 在缺省 QoS 级别发布事件

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

myClient.publishEvent("status", event);
```


### 提高事件的 QoS 级别

可以提高已发布事件的 [QoS 级别](../../reference/mqtt/index.html#qos-levels)。QoS 级别大于零的事件发布所用时间可能更长，因为包含额外的接收确认信息。

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

//注册流允许 QoS 为 0、1 和 2
myClient.publishEvent("status", event, 2);
```

### 以定制格式发布事件

事件可以使用不同的格式（例如，JSON、字符串、二进制等）进行发布。缺省情况下，库会以 JSON 格式发布事件，但您可以根据需要指定其他格式的数据。例如，要以字符串格式发布数据，请使用以下代码片段。

```
myClient.connect();

String data = "cpu:"+getProcessCpuLoad();
status = myClient.publishEvent("load", data, "text", 2);
```

**注：**在先前的代码示例中，事件的有效内容必须为字符串格式。



任何 XML 数据都可以转换为字符串格式，并按如下所示进行发布：

```
status = myClient.publishEvent("load", xmlConvertedString, "xml", 2);
```

与此类似，要以二进制格式发布事件，请使用以下示例中所概述的字节数组：

```
myClient.connect();

byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = myClient.publishEvent("blink", cpuLoad , "binary", 1);
```

### 使用 HTTP 发布事件
{: #publishing_events_http}


除了使用 MQTT 外，还可以将设备配置为通过 HTTP 将事件发布到 {{site.data.keyword.iot_short_notm}}。以下步骤概述了通过 HTTP 发布事件的序列：

1. 使用属性文件构造 `DeviceClient` 实例。
2. 构造需要发布的事件。
3. 指定事件名称，然后使用 `publishEventOverHTTP()` 方法发布事件，如以下代码样本中所示：

``` sourceCode
DeviceClient myClient = new DeviceClient(deviceProps);

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

boolean response  = myClient.api().publishDeviceEventOverHTTP("blink", event, ContentType.json);
```

要查看完整代码，请参阅 [HttpDeviceEventPublish] 设备示例。

根据属性文件中的设置，`publishEventOverHTTP()` 方法会以 Quickstart 方式或注册流方式发布事件。当属性文件中的“组织标识”设置为 `quickstart` 时，`publishEventOverHTTP()` 方法会将事件发布到设备示例 Quickstart 服务，并以纯 HTTP 格式发布事件。如果在属性文件中指定了有效的已注册组织，那么会通过 HTTPS 来安全地发布事件。

HTTP 协议提供“至多一次”传递，这类似于 MQTT 协议的“至多一次”(QoS 0) 服务质量级别。使用“至多一次”传递来发布事件时，应用程序必须实现任何出错情况下的重试逻辑。

[HttpDeviceEventPublish]: https://github.com/ibm-messaging/iot-device-samples/blob/master/java/device-samples/src/main/java/com/ibm/iotf/sample/client/device/HttpDeviceEventPublish.java

## 处理命令
{: #handling_commands}

设备客户机进行连接时，会自动预订此设备的所有命令。要处理特定命令，需要注册命令回调方法。
消息将作为 `Command` 类的实例返回，此类包含以下属性：

| 属性     |数据类型     | 描述|
|----------------|----------------|
|`payload` |java.lang.String| 消息有效内容的数据。|
|`format`  |java.lang.String| 格式可以为任意字符串，例如 JSON。|
|`command`   |java.lang.String|标识命令。|
|`timestamp`   |org.joda.time.DateTime|事件的日期和时间。|


``` sourceCode
package com.ibm.iotf.sample.client.device;

import java.util.Properties;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.LinkedBlockingQueue;


import com.ibm.iotf.client.device.Command;
import com.ibm.iotf.client.device.CommandCallback;
import com.ibm.iotf.client.device.DeviceClient;


//实现 CommandCallback 类，以提供希望的命令处理方法
class MyNewCommandCallback implements CommandCallback, Runnable {

    // 用于保留和处理命令以顺利处理 MQTT 消息的队列
    private BlockingQueue<Command> queue = new LinkedBlockingQueue<Command>();

    /**
    * 每当有与预订条件相匹配的命令时，都会由库来调用此方法 */
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
                //在此样本中，只显示了命令
                cmd = queue.take();
                System.out.println("COMMAND RECEIVED = '" + cmd.getCommand() + "'\twith Payload = '" + cmd.getPayload() + "'");
            } catch (InterruptedException e) {}
        }
    }
}

public class RegisteredDeviceCommandSubscribe {


    public static void main(String[] args) {

        //使用 Properties 类提供特定于设备的数据以及认证密钥和令牌
        Properties options = new Properties();

        options.setProperty("org", "uguhsp");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");
        options.setProperty("auth-method", "token");
        options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");

        DeviceClient myClient = null;
        try {
            //通过传递属性文件对类进行实例化
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //将上面实现的 CommandCallback 作为自变量传递到此设备客户机
        myClient.setCommandCallback(new MyNewCommandCallback());

        //连接到 {{site.data.keyword.iot_short_notm}}
        myClient.connect();
    }
}
```

## 样本
{: #samples}

有关使用 {{site.data.keyword.iot_short_notm}} Java 客户机库开发的设备和设备管理样本的列表，请参阅 [iot-device-samples GitHub 存储库](https://github.com/ibm-messaging/iot-device-samples/tree/master/java)。
