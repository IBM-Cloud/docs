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


# 针对设备开发者的 C#
{: #c_sharp}

您可以使用 C# 来构建和定制设备，以用于在 {{site.data.keyword.iot_full}} 上与您的组织进行交互。使用提供的信息和示例通过 C# 开始开发设备。
{:shortdesc}

## 下载 C# 客户机和资源
{: #csharp_client_download}

要访问 {{site.data.keyword.iot_short_notm}} 的 C# 客户机和资源，请转至 GitHub 中的 [iot-csharp ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-watson-iot/iot-csharp){: new_window} 存储库，并完成安装指示信息。


## 构造方法
{: #constructor}

构造方法用于构建客户机实例，并接受包含以下定义的自变量：

|定义 |描述 |
|:---|:---|
|`orgId`|组织标识。|
|`deviceType`|设备类型。|
|`deviceId` |设备的标识。|
|`auth-method`   |要使用的认证方法。当前支持的唯一值是 `token`。|
|`auth-token`   |用于将设备安全连接到 Watson IoT Platform 的认证令牌。|


如果只提供了 `deviceId` 和 `deviceType` 自变量，那么客户机将作为未注册的设备连接到 {{site.data.keyword.iot_short_notm}} Quickstart 服务。自变量列表定义了客户机如何连接到 {{site.data.keyword.iot_short_notm}} 模块。


```
namespace com.ibm.iotf.client

public DeviceClient(string orgId, string deviceType, string deviceID, string auth-method, string auth-token)
        : base(orgId, "d" + CLIENT_ID_DELIMITER + orgId + CLIENT_ID_DELIMITER + deviceType + CLIENT_ID_DELIMITER + deviceID, "use-token-auth", auth-token)
    {

    }
```

## 发布事件
{: #publishing-events}

设备使用事件将数据发布到 {{site.data.keyword.iot_short_notm}} 实例。设备控制事件内容，并为其发送的每个事件指定名称。

{{site.data.keyword.iot_short_notm}} 实例接收到事件时，入局事件的凭证会识别发送设备，这意味着一台设备无法冒充其他设备。

可以在 MQTT 协议定义的三个[服务质量 (QoS) 级别](../mqtt.html#managed-devices)中的任一级别发布事件。缺省情况下，事件在 QoS 0 级别发布。


## 使用缺省服务质量级别发布事件
{: #publish_event_default_qos}

```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}");
```


## 使用用户定义的服务质量级别发布事件
{: #publish_event_user_qos}

在大于 `0` 的 MQTT QoS 级别发布的事件包含额外的接收确认信息，因此发布所用时间可能要比 QoS 级别为 `0` 的事件更长。


```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}", 2);
```

## 处理命令
{: #handling_commands}

设备客户机进行连接时，会自动预订此设备的任何命令。要处理特定命令，必须注册命令回调方法，如以下示例中所示：

```
public static void processCommand(string cmdName, string cmdFormat, string cmdData) {
...
 }
```

```
deviceClient.connect();
deviceClient.commandCallback += processCommand;
```
下表描述了 commandCallback 方法的参数：

|参数|数据类型|描述|
|:---|:---|
|`cmdName`|字符串|标识命令。 |
|`cmdFormat`|字符串|格式可以为任意字符串，例如 JSON。|
|`cmdData`|字典|有效内容的数据。最大长度为 131072 字节。|
