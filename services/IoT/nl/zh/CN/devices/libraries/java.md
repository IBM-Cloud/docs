---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 针对设备开发者的 Java
{: #java}

上次更新时间：2016 年 8 月 2 日
{: .last-updated}


您可以使用 Java 来构建和定制设备，以用于与 {{site.data.keyword.iot_full}} 上的组织进行交互。使用提供的信息和示例通过 Java 开始开发设备。
{:shortdesc}

## 下载 Java 客户机和资源
{: #java_client_download}

要访问 {{site.data.keyword.iot_short_notm}} 的 Java 客户机库和样本，请转至 GitHub 中的 [iot-java](https://github.com/ibm-watson-iot/iot-java) 存储库，并完成安装指示信息。


## 构造方法
{: #constructor}

构造方法用于构建客户机实例，并接受包含以下定义的 properties 对象：

|定义 |描述 |
|:---|:---|
|`org` |组织标识。此字段是必填的。如果使用的是 Quickstart 流，请指定 `quickstart`。|
|`type`  |设备类型。此字段是必填的。|
|`id`  |设备的标识。此字段是必填的。|
|`auth-method`   |要使用的认证方法。当前支持的唯一值是 `token`。|
|`auth-token`   |用于将设备安全连接到 Watson IoT Platform 的认证令牌。|
|`clean-session`|true 或 false 值，仅当要以持久预订方式连接应用程序时是必需的。缺省情况下，`clean-session` 设置为 `true`。|

**注：**要以持久预订方式连接设备，请将 `clean-session` 设置为 `false`。有关清除会话的更多信息，请参阅 [MQTT 文档](../../reference/mqtt/index.html#subscription-buffers-and-clean-session)的“预订缓冲区和清除会话”部分。

properties 对象创建用于与 {{site.data.keyword.iot_short_notm}} 模块进行交互的定义。

以下代码显示了以 Quickstart 方式发布事件的设备。

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

以下代码样本显示了设备可以如何在注册流中发布事件。


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

您可以不直接使用 properties 对象，而改为使用包含 properties 的名称/值对的配置文件：如果要使用包含 properties 对象的配置文件，请使用以下代码格式：

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

通过调用 connect 函数来连接到 {{site.data.keyword.iot_short_notm}}。connect 函数采用可选的布尔值参数 `autoRetry`，缺省情况下值为 `true`。`autoRetry` 参数允许库在发生 MqttException 错误时重新连接。请注意，因使用的设备注册详细信息不正确而发生 MqttSecurityException错误时，库不会尝试重新连接，即便 `autoRetry` 参数设置为 `true` 也不例外。

```
DeviceClient myClient = new DeviceClient(options);

myClient.connect(true);
```

成功连接到 {{site.data.keyword.iot_short_notm}} 服务后，设备客户机可以执行各种操作，例如发布事件以及预订来自应用程序的设备命令。


## 发布事件
{: #publishing_events}

事件是设备用于将数据发布到 {{site.data.keyword.iot_short_notm}} 的机制。设备控制事件内容，并为其发送的每个事件指定名称。

{{site.data.keyword.iot_short_notm}} 实例接收到事件时，所接收事件的凭证会识别发送设备，这意味着一台设备无法冒充其他设备。

可以在三个[服务质量 (QoS) 级别](../../reference/mqtt/index.html#qos-levels)中的任一级别发布事件，服务质量级别由 MQTT 协议进行定义。缺省情况下，事件在 QoS=0 级别发布。

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

可以提高已发布事件的 [QoS 级别](../../reference/mqtt/index.html#qos-levels)。QoS 级别大于零的事件可能所用发布时间更长，因为包含额外的接收确认信息。

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

//注册流允许 QoS 为 0、1 和 2
myClient.publishEvent("status", event, 2);
```

### 使用 HTTP 发布事件

除了 MQTT 外，还可以使用 HTTP 和以下步骤将设备事件发布到 {{site.data.keyword.iot_short_notm}}：

* 使用属性文件构造 DeviceClient 实例
* 构造需要发布的事件
* 指定事件名称，并使用 `publishEventOverHTTP()` 方法发布事件，如以下代码中所示：

``` sourceCode
DeviceClient myClient = new DeviceClient(deviceProps);

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

int httpCode = myClient.publishEventOverHTTP("blink", event);
```

可以在 [HttpDeviceEventPublish] 设备示例中找到整个代码。

根据属性文件中的设置，`publishEventOverHTTP()` 方法能以 Quickstart 方式或注册流方式发布事件。属性文件中的“组织标识”为 `quickstart` 时，`publishEventOverHTTP()` 方法可将事件发布到设备样本 Quickstart 服务，然后以纯 HTTP 格式发布事件。在属性文件中使用有效注册组织时，此方法将始终以 HTTPS（即基于 SSL的 HTTP）格式发布事件，所以全部通信都会受到保护。

HTTP 协议提供了“至多一次”传递，这类似于 MQTT 协议的“至多一次”(QoS 0) 服务质量级别。使用“至多一次”传递来发布事件时，如果发生错误，应用程序必须实现重试逻辑。

[HttpDeviceEventPublish]: https://github.com/ibm-messaging/iot-device-samples/blob/master/java/device-samples/src/main/java/com/ibm/iotf/sample/client/device/HttpDeviceEventPublish.java

## 处理命令
{: #handling_commands}

设备客户机进行连接时，会自动预订此设备的所有命令。要处理特定命令，需要注册命令回调方法。
消息将作为 Command 类的实例返回，此类具有以下参数：

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

    // 要保留和处理命令以顺利处理 MQTT 消息的队列
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

有关使用 {{site.data.keyword.iot_short_notm}} Java 客户机库开发的设备和设备管理样本的列表，请参阅 [GitHub 存储库](https://github.com/ibm-messaging/iot-device-samples/tree/master/java)。
