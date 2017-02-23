---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-07-28"

---

  {:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 针对应用程序开发者的 C#
{: #c_sharp}


您可以使用 C# 来构建和定制应用程序，以用于在 {{site.data.keyword.iot_full}} 上与您的组织进行交互。使用提供的信息和示例通过 C# 开始开发应用程序。
{:shortdesc}

## 下载 C# 客户机和资源
{: #csharp_client_download}

要访问 {{site.data.keyword.iot_short_notm}} 的 C# 客户机库和样本，请转至 GitHub 中的 [iot-csharp](https://github.com/ibm-watson-iot/iot-csharp) 存储库，并完成安装指示信息。


## 构造方法
{: #constructor}

构造方法用于构建客户机实例，并接受包含以下定义的自变量：

|定义 |描述 |
|:---|:---|
|`orgId`   |组织标识。|
|`appId`   |组织中应用程序的唯一标识。|
|`auth-key`   |用于将应用程序安全连接到 Watson IoT Platform 的 API 密钥。|
|`auth-token`   |用于将应用程序安全连接到 Watson IoT Platform 的 API 密钥令牌。|

如果 `appId` 是提供的唯一自变量，那么客户机将作为未注册的设备连接到 {{site.data.keyword.iot_short_notm}} Quickstart 服务。自变量列表定义客户机如何连接到 {{site.data.keyword.iot_short_notm}} 模块。

```
ApplicationClient applicationClient = new ApplicationClient(orgId, appId, apiKey, authToken);  
applicationClient.connect();
```


## 预订设备事件
{: #subscribe_device_events}

设备使用事件将数据发布到 {{site.data.keyword.iot_short_notm}} 实例。设备控制事件内容，并为其发送的每个事件指定名称。

{{site.data.keyword.iot_short_notm}} 实例接收到事件时，所接收事件的凭证会识别发送设备，这意味着一台设备无法冒充其他设备。

缺省情况下，应用程序会预订来自所有已连接设备的所有事件。使用设备类型、设备标识、事件和消息格式参数可控制预订的范围。以下代码样本显示了可以如何使用这些参数来定义预订范围：

### 预订来自所有设备的所有事件

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents();
```

### 预订来自特定类型的所有设备的所有事件

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType);
```

### 预订来自所有设备的特定事件

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(evt);
```

###  预订来自两个或更多不同设备的特定事件：

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt);
```

### 预订以 JSON 格式发布的所有事件

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt, "json", 0);
```

**注**：单个客户机实例可支持多个预订。

### 处理来自设备的事件

要处理您的预订接收到的事件，请注册事件回调方法，如以下示例中所示：

```
public static void processEvent(String eventName, string eventFormat, string eventData) {
// Do something
}
applicationClient.connect();
applicationClient.eventCallback += processEvent;
applicationClient.subscribeToDeviceEvents();
```
下表描述了事件回调方法的参数：

|参数|数据类型|描述|
|:---|:---|
|`eventName`|字符串|标识事件。 |
|`eventFormat`|字符串| 格式可以为任意字符串，例如 JSON。|
|`eventData`|字典| 消息有效内容的数据。最大长度为 131072 字节。|


## 预订设备状态
{: #subscribe_device_status}

缺省情况下，预订会设置为接收所有已连接设备的状态更新。使用设备类型和设备标识参数可控制预订范围。以下代码样本显示了可以如何使用这些参数来定义预订范围：

### 预订所有设备的状态更新

```
applicationClient.connect();
applicationClient.subscribeToDeviceStatus += processDeviceStatus;
applicationClient.subscribeToDeviceStatus();
```

### 预订两种不同设备的状态更新

```
applicationClient.connect();
applicationClient.subscribeToDeviceStatus += processDeviceStatus;
applicationClient.subscribeToDeviceStatus(deviceType, deviceId);
```

**注**：单个客户机实例可支持多个预订。

### 处理来自设备的状态更新

要处理您的预订接收到的状态更新，请注册事件回调方法，如以下示例中所示：

```
public static void processDeviceStatus(String deviceType, string deviceId, string data)
        {
           //
        }
applicationClient.connect();
applicationClient.appStatusCallback += processAppStatus;
applicationClient.subscribeToApplicationStatus();
```

## 发布来自设备的事件
{: #publish_events_devices}

应用程序可以将事件当作源自设备的事件进行发布。

```
applicationClient.connect();
applicationClient.publishEvent(deviceType, deviceId, evt, data, 0);

```

下表描述了 `publishEvent()` 方法中指定的参数：

|参数|数据类型|描述|
|:---|:---|
|`deviceType`|字符串| 设备类型。通常，deviceType 是对执行特定任务的设备的一种分组，例如“weatherballoon”。|
|`deviceId`|字符串| 设备的标识。通常，对于给定设备类型，deviceId 是该设备的唯一标识，例如序列号或 MAC 地址。|
|`evt`|字符串| 事件的名称。|
|`format`|字符串| 格式可以为任意字符串，例如 JSON。|
|`data`|字典| 消息有效内容的数据。最大长度为 131072 字节。|
|`QoS`|整数| 服务质量。有效值为 `0`、`1` 和 `2`。 |


## 将命令发布到设备
{: #publish_commands_devices}

应用程序可以将命令发布到已连接设备。

```
applicationClient.connect();
applicationClient.publishCommand(deviceType, deviceId, "testcmd", "json", data, 0);
```
下表描述了 `publishCommand()` 方法中指定的参数：

|参数|数据类型|描述|
|:---|:---|
|`deviceType`|字符串| 设备类型。通常，deviceType 是对执行特定任务的设备的一种分组，例如“weatherballoon”。|
|`deviceId`|字符串| 设备的标识。通常，对于给定设备类型，deviceId 是该设备的唯一标识，例如序列号或 MAC 地址。|
|`command`|字符串| 命令的名称。|
|`format`|字符串| 格式可以为任意字符串，例如 JSON。|
|`data`|字典| 消息有效内容的数据。最大长度为 131072 字节。|
|`QoS`|整数| 服务质量。有效值为 `0`、`1` 和 `2`。 |
