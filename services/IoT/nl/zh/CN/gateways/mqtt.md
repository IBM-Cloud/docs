---

copyright:
  years: 2015, 2017
lastupdated: "2016-11-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 针对网关的 MQTT 连接
{: #mqtt}

MQTT 是设备和应用程序用于与 {{site.data.keyword.iot_full}} 通信的主要协议。提供的客户机库、信息和样本可帮助您将 MQTT 客户机用作网关，以将设备连接到 {{site.data.keyword.iot_short_notm}}。
{:shortdesc}

## 客户机连接
{: #client_connections}

有关客户机安全性以及如何将 MQTT 客户机作为网关进行连接的信息，请参阅[将应用程序、设备和网关连接到 {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html)。

## MQTT 认证
{: #authentication}
对于网关和设备，{{site.data.keyword.iot_short_notm}} 将使用 MQTT 基于令牌的认证。

要启用 MQTT 认证，请在进行 MQTT 连接时提交用户名和密码。

### 用户名
{: #username}

用户名对于所有网关都是相同的值：`use-token-auth`。此值会使 {{site.data.keyword.iot_short_notm}} 使用指定为密码的网关认证令牌。

### 密码
{: #password}

每个网关的密码都是在网关向 {{site.data.keyword.iot_short_notm}} 注册时生成的唯一认证令牌。

## 发布事件
{: #pub_events}

网关可以从自身发布事件，也可以代表通过该网关连接的任何设备发布事件。要发布事件，请使用以下主题，并根据计划使用的事件源替换相应的 `typeId` 和 `deviceId`：

<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/evt/<var class="keyword varname">eventId</var>/fmt/<var class="keyword varname">formatString</var></pre>
{: codeblock}


**示例**


|    |“typeID”|“deviceID”|
|:---|:---|:---|
|Gateway 1 |mygateway |gateway1 |
|Device 1 |mydevice |device1 |

-   Gateway 1 可以发布其自己的状态事件：  
    `iot-2/type/mygateway/id/gateway1/evt/status/fmt/json`
-   Gateway 1 可以代表 Device 1 发布状态事件：  
    `iot-2/type/mydevice/id/device1/evt/status/fmt/json`

**重要信息：**消息有效内容限制为最大 131072 字节。大于此限制的消息将被拒绝。

### 保留消息
{{site.data.keyword.iot_short_notm}} 组织无权发布保留的 MQTT 消息。如果网关发送保留消息，{{site.data.keyword.iot_short_notm}} 服务将覆盖已设置为 true 的保留消息标志，并将消息当作保留消息标志设置为 false 进行处理。

## 预订命令
{: #subscribing_cmds}

网关可以预订针对网关本身以及组织中任何设备（包括其他网关）的命令。要预订命令，请使用以下主题，并替换相应的 `typeId` 和 `deviceId`：

<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/cmd/<var class="keyword varname">commandId</var>/fmt/<var class="keyword varname">formatString</var></pre>
{: codeblock}

MQTT `+` 通配符可用于 `typeId`、`deviceId`、`commandId` 和 `formatString` 来预订多个命令源。

**示例：
**

|设备 |`typeId`|`deviceId`|
|:---|:---|
|Gateway 1| mygateway   | gateway1   |
|Device 1 | mydevice    | device1    |


-   Gateway 1 可以预订针对该网关的命令：  
    `iot-2/type/mygateway/id/gateway1/cmd/+/fmt/+`
-   Gateway 1 可以预订发送到 Device 1 的命令：  
    `iot-2/type/mydevice/id/device1/cmd/+/fmt/+`
-   Gateway 1 可以预订发送到类型为 `mydevice` 的设备的任何命令：  
     `iot-2/type/mydevice/id/+/cmd/+/fmt/+`

**重要信息：**指定为 `cleansession=false` 的 MQTT 持久会话不会搜索连接到网关的设备。如果设备先连接到网关 A，以后又连接到网关 B，那么该设备在断开连接后不会接收发布到该设备的网关 A 的任何消息。网关拥有 MQTT 客户机和预订，但并不拥有连接到网关的设备。

## 网关自动注册
{: #auto-reg}

网关设备可以自动注册所连接的设备。网关代表未注册的设备发布消息或预订主题时，会自动注册该设备。

来自网关设备的注册请求数限制为最多同时有 128 个暂挂请求。尝试连接大量新设备可能会导致通过网关注册设备时发生延迟。

**警告**

如果网关未能自动注册设备，那么网关在一段很短的时间内不会重试注册该设备。在该时间段期间，将废弃来自发生故障的设备的任何消息或预订。

## 网关通知
{: #notification}

验证发布或预订主题期间或者自动注册期间发生错误时，将向网关设备发送通知。网关可以通过预订以下主题并替换 `typeId` 和 `deviceId` 值来接收这些通知：

```
iot-2/type/**typeId**/id/**deviceId**/notify
```
<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/notify</pre>
{: codeblock}

在 notify 主题上接收到的消息会使用以下格式：

```   
{
   "Request": "<Request_Type>",
   "Time": "<Timestamp>",
   "Topic": "<Topic>",
   "Type": "<Device_Type>",
   "Id": "<Device_Id>",
   "Client": "<Client_ID>",
   "RC": "<Return_Code>",
   "Message": "<Message>"
}
```
其中：
-   `Request_Type` 值为 `publish` 或 `subscribe`
-   `Timestamp` 为 ISO 8601 格式的时间
-   `Topic` 为来自网关的请求主题
-   `Device_Type` 为主题中的设备类型
-   `Device_Id` 为主题中的设备标识
-   `Client_ID` 为请求的客户机标识
-   `Return_Code` 为返回码
-   `Message` 为错误消息

网关可以接收以下通知：

-   主题与任何允许的主题规则都不匹配。
-   设备类型无效。
-   设备标识无效。
-   已达到每个网关的最大设备数。
-   已达到每个组织的最大设备数。
-   由于内部错误而未能创建设备。

## 受管网关
{: #managed_gateways}

对设备生命周期管理的支持是可选的。{{site.data.keyword.iot_short_notm}} 所用设备管理协议使用的 MQTT 连接与网关用于事件和命令控制的 MQTT 连接相同。

### 服务质量级别和干净会话
{: #quality_service}

受管网关可以发布服务质量 (QoS) 级别为 0 或 1 的消息。

QoS 为 0 的消息可以废弃，并且在消息传递服务器重新启动后不会持久存储。QoS 为 1 的消息可以排队，并且在消息传递服务器重新启动后会持久存储。预订的持久性将确定请求是否排队。进行预订的连接的 `cleansession` 参数将确定预订的持久性。  

{{site.data.keyword.iot_short_notm}} 发布 QoS 级别为 1 的请求，以支持消息排队。要对未连接受管网关期间发送的消息排队，请通过将 `cleansession` 参数设置为 false，将设备配置为不使用干净会话。

**警告**

受管网关使用持久预订时，如果网关未在请求超时之前重新连接到服务，那么在该网关脱机时向其发送的设备管理命令会报告为失败操作。网关重新连接后，将处理这些请求。持久预订由 `cleansession=false` 参数指定。

网关拥有 MQTT 会话，与网关背后的设备无关。设备通过网关提交预订请求时，不管是否设置了 `cleansession=false` 选项，该请求都不会流转到其他网关。

### 主题
{: #topics}

受管网关必须预订以下主题，才可处理来自 {{site.data.keyword.iot_short_notm}} 的请求和响应：

-   受管网关预订以下主题上的设备管理响应：  
<pre class="pre">iotdm-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/response/+</pre>
{: codeblock}
-   受管网关预订以下主题上的设备管理请求：  
<pre class="pre">iotdm-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/+</pre>
{: codeblock}

受管网关发布以下响应和请求：

- 设备管理响应在以下主题上发布：  
<pre class="pre">iotdevice-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/response/</pre>
{: codeblock}
- 设备管理请求在以下主题上发布：  
<pre class="pre">iotdevice-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/</pre>
{: codeblock}

网关可以使用相关的 **typeId** 和 **deviceId** 为自身以及代表其他已连接设备处理设备管理协议消息。

### 消息格式
{: #msg_format}

所有消息都以 JSON 格式进行发送。

**请求**

请求的格式如以下代码样本中所示：

```   
    {  "d": {...}, "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056" }
```

-   `d` 包含与请求相关的任何数据
-   `reqId` 是请求的标识，必须复制到响应中。如果无需响应，那么不会使用此字段。

**响应**

响应的格式如以下代码样本中所示：

```
    {
        "rc": 0,
        "message": "success",
        "d": {...},
        "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056"
    }
```
其中：
-   `rc` 为原始请求的结果代码。
-   `message` 为具有响应代码文本描述的可选元素。
-   `d` 为响应随附的可选数据元素。
-   `reqId` 为原始请求的请求标识。请求标识用于将响应与请求相关联，并且设备需要确保所有请求标识都是唯一的。对 {{site.data.keyword.iot_short_notm}} 请求的响应必须包含正确的 `reqId` 值。
