---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 针对设备开发者的 Python
{: #python}
上次更新时间：2016 年 7 月 29 日
{: .last-updated}

您可以使用 Python 来构建和开发设备代码，以用于与 {{site.data.keyword.iot_full}} 上的组织进行交互。{{site.data.keyword.iot_short_notm}} 的 Python 客户机提供了 API，通过剥离底层协议（例如，MQTT 和 HTTP）来帮助与 {{site.data.keyword.iot_short_notm}} 功能进行简单交互。
{:shortdesc}

使用提供的信息和示例通过 Python 开始开发设备。

## 下载 Python 客户机和资源
{: #python_client_download}

要访问 {{site.data.keyword.iot_short_notm}} 的 Python 客户机和其他可用资源，请转至 GitHub 中的 [iot-python](https://github.com/ibm-watson-iot/iot-python) 存储库，并完成安装指示信息。

## 构造方法
{: #constructor}

选项字典创建用于与 {{site.data.keyword.iot_short_notm}} 模块进行交互的定义。构造方法用于构建客户机实例，并接受包含以下定义的选项字典：

|定义|描述 |
|:---|:---|
|`orgId`|组织标识。|
|`type`|设备类型。通常，deviceType 是一组执行特定任务的设备，例如“weatherballoon”。|
|`id`|设备的标识。通常，对于给定设备类型，deviceId 是该设备的唯一标识，例如序列号或 MAC 地址。|
|`auth-method`|要使用的认证方法。当前支持的唯一值是 `token`。|
|`auth-token`|用于将设备安全连接到 Watson IoT Platform 的认证令牌。|

如果未提供选项字典，那么客户机将作为未注册的设备连接到 Watson IoT 平台 Quickstart 服务。

```python

import ibmiotf.device
try:
  options = {
    "org": orgId,
    "type": deviceType,
    "id": deviceId,
    "auth-method": authMethod,
    "auth-token": authToken
  }
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

### 使用配置文件

您还可以在配置文件中单独定义选项字典，而不直接定义选项字典，如以下代码样本中所概述：

```python

import ibmiotf.device
try:
  options = ibmiotf.device.ParseConfigFile(configFilePath)
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

包含选项字典的配置文件必须为以下格式：

```python

[device]
org=orgID
type=deviceType
id=deviceId
auth-method=token
auth-token=token

```

## 发布事件
{: #publishing_events}

事件是设备用于将数据发布到 {{site.data.keyword.iot_short_notm}} 的机制。设备控制事件内容，并为其发送的每个事件指定名称。

{{site.data.keyword.iot_short_notm}} 实例接收到事件时，所接收事件的凭证会识别发送设备，这意味着一台设备无法冒充其他设备。

可以在 MQTT 协议定义的三个服务质量 (QoS) 级别中的任一级别发布事件。缺省情况下，事件在 QoS 级别 `0` 发布。

### 使用缺省服务质量发布事件

```
client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData)
```

### 提高事件的 QoS 级别

可以提高已发布事件的[服务质量 (QoS) 级别](../../reference/mqtt/index.html#qos-levels)。QoS 级别大于 `0` 的事件可能所用发布时间更长，因为包含额外的接收确认信息。

**注：**Quickstart 流方式仅支持 QoS 级别 `0`。

```
client.connect()
myQosLevel=2
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData, myQosLevel)
```
## 处理命令
{: #handling_commands}

设备客户机连接时，会自动预订为此设备指定的任何命令。要处理特定命令，需要注册命令回调方法。消息将作为 Command 类的实例返回，此类包含以下参数：

|属性|数据类型|描述|
|:---|:---|
|`command`|字符串|标识命令。|
|`format`|字符串|格式可以为任意字符串，例如 JSON。|
|`data`|字典|有效内容的数据。最大长度为 131072 字节。|
|`timestamp`|日期和时间|事件的日期和时间。|


```python

def myCommandCallback(cmd):
  print("Command received: %s" % cmd.data)
  if cmd.command == "setInterval":
    if 'interval' not in cmd.data:
      print("Error - command is missing required information: 'interval'")
    else:
      interval = cmd.data['interval']
  elif cmd.command == "print":
    if 'message' not in cmd.data:
      print("Error - command is missing required information: 'message'")
    else:
      print(cmd.data['message'])

...
client.connect()
client.commandCallback = myCommandCallback
```

## 定制消息格式支持
{: #custom_message_format}

缺省情况下，消息格式设置为 `json`，这意味着库支持对 JSON 格式的 Python 字典对象进行编码和解码。消息格式设置为 `json-iotf` 时，会根据 {{site.data.keyword.iot_short_notm}} JSON 有效内容规范对消息编码。要添加对自己定制消息格式的支持，请参阅 GitHub 中的 [Custom Message Format sample](https://github.com/ibm-watson-iot/iot-python/tree/master/samples/customMessageFormat)。

创建定制编码器模块后，必须在设备客户机中注册该模块，如以下示例中所概述：

```python

import myCustomCodec

client.setMessageEncoderModule("custom", myCustomCodec)
client.publishEvent("status", "custom", myData)
```
如果事件以未知格式发送，或者设备无法识别该格式，那么设备库会返回 `MissingMessageDecoderException` 条件。
