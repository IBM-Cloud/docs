---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 设备的 MQTT 连接
{: #mqtt}

MQTT 是设备和应用程序用于与 {{site.data.keyword.iot_full}} 通信的主要协议。提供的客户机库、信息和样本可帮助您将设备与 {{site.data.keyword.iot_short_notm}} 连接并集成。
{:shortdesc}

## 客户机连接
{: #client_connections}

有关客户机安全性以及如何将 MQTT 客户机连接到 {{site.data.keyword.iot_short_notm}} 中设备的信息，请参阅[将应用程序、设备和网关连接到 {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html)。


## 将设备连接到 Quickstart 服务
{: #connecting_devices}

Quickstart 服务是速度最快的服务级别。它无需确认接收，也不支持大于零的 MQTT 服务质量 (QoS) 级别。连接到 Quickstart 服务时，无需认证或注册，并且 `orgId` 必须设置为 `quickstart`。

如果要编写设备代码以用于 Quickstart，请注意在 Quickstart 方式下，不支持以下 {{site.data.keyword.iot_short_notm}} 服务功能：

-  预订命令
-  设备管理协议
-  干净会话或可持续会话

**重要信息：**如果设备发送消息的速度超过每秒一条，那么可能会废弃这些消息。


## MQTT 认证
{: #mqtt_authentication}

对于网关和设备，{{site.data.keyword.iot_short_notm}} 将使用 MQTT 基于令牌的认证。

要启用 MQTT 认证，请在进行 MQTT 连接时提交用户名和密码。

### 用户名

用户名的值对于所有设备都相同：`use-token-auth`。此值会使 {{site.data.keyword.iot_short_notm}} 使用指定为密码的设备认证令牌。

### 密码

每个设备的密码都是在设备向 {{site.data.keyword.iot_short_notm}} 注册时生成的唯一认证令牌。

## 发布事件
{: #publishing_events}

设备以下列格式发布到事件主题：

<pre class="pre"><code class="hljs">iot-2/evt/<var class="keyword varname">event_id</var>/fmt/<var class="keyword varname">format_string</var></code></pre>
{: codeblock}

其中：

-  **event_id** 是事件的标识，例如 `status`。事件标识可以是在 MQTT 中有效的任何字符串。如果未使用通配符，那么订户应用程序必须在其预订主题中使用此字符串，才能接收在其主题上发布的事件。
-  **format_string** 是一个字符串，用于定义消息有效内容的内容类型，以便消息接收方可以确定如何解析内容。常见的内容类型值包括但不限于“json”、“xml”、“txt”和“csv”。值可以是在 MQTT 中有效的任何字符串。

**重要信息：**消息有效内容限制为最大 131072 字节。大于此限制的消息将被拒绝。

### 保留消息
{{site.data.keyword.iot_short_notm}} 组织无权发布保留的 MQTT 消息。如果设备发送保留消息，{{site.data.keyword.iot_short_notm}} 服务将覆盖已设置为 true 的保留消息标志，并将消息当作保留消息标志设置为 false 进行处理。


## 预订命令
{: #subscribing_to_commands}

设备可以使用以下格式预订命令主题：

<pre class="pre"><code class="hljs">iot-2/cmd/<var class="keyword varname">command_id</var>/fmt/<var class="keyword varname">format_string</var></code></pre>
{: codeblock}

其中：
 - **command_id** 是命令的标识，例如 `update`。命令标识可以是在 MQTT 协议中有效的任何字符串。如果未使用通配符，那么设备必须在其预订主题中使用此字符串，才能接收在其主题上发布的命令。
 - **format_string** 是一个字符串，用于定义命令有效内容的内容类型，以便命令接收方可以确定如何解析内容。常见的内容类型值包括但不限于“json”、“xml”、“txt”和“csv”。值可以是在 MQTT 中有效的任何字符串。

设备无法预订来自其他设备的事件。设备只能接收向其自己的设备发布的命令。

## 受管设备
{: #managed-devices}

对设备生命周期管理的支持是可选的。设备管理协议使用的 MQTT 连接与设备已经用于事件和命令控制的 MQTT 连接相同。

### 服务质量级别和干净会话

受管设备可以发布服务质量 (QoS) 级别为 0 或 1 的消息。

QoS 为 0 的消息可以废弃，并且在消息传递服务器重新启动后不会持久存储。QoS 为 1 的消息可以排队，并且在消息传递服务器重新启动后会持久存储。预订的持久性将确定请求是否排队。进行预订的连接的 `cleansession` 参数将确定预订的持久性。  

{{site.data.keyword.iot_short_notm}} 发布 QoS 级别为 1 的请求，以支持消息排队。要对未连接受管设备期间发送的消息排队，请通过将 `cleansession` 参数设置为 false，将设备配置为不使用干净会话。

**警告：**
  受管设备使用持久预订时，如果在设备脱机的情况下向其发送任何命令，那么若在请求超时之前设备未能重新连接到服务，就会将所有这些命令报告为失败操作。但是，设备重新连接后，设备将处理这些请求。持久预订由 `cleansession=false` 参数指定。

### 主题

受管设备需要预订以下主题，才可处理来自 {{site.data.keyword.iot_short_notm}} 服务的请求和响应：

```
iotdm-1/#
```


受管设备会发布到特定于要执行的管理请求类型的主题：

- 受管设备在 `iotdevice-1/response` 上发布设备管理响应。
- 有关受管设备可以发布到哪些其他主题，请参阅[设备管理协议](device_mgmt/index.html)和[设备管理请求](device_mgmt/requests.html)。



### 消息格式

所有消息都以 JSON 格式进行发送。

**请求**  
请求的格式如以下代码样本中所示：

<pre class="pre"><code class="hljs">{  "d": {...}, "<var class="keyword varname">reqId</var>": "b53eb43e-401c-453c-b8f5-94b73290c056" }</code></pre>
{: codeblock}

其中：

 - **d** 包含与请求相关的任何数据。
 - **reqId** 为请求的标识，必须复制到响应中。如果无需响应，那么可以省略 *reqId* 字段。

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
 - **rc** 为原始请求的结果代码。
 - **message** 为具有响应代码文本描述的可选元素。
 - **d** 为对响应进行补充的可选数据元素。
 - **reqId** 为原始请求的请求标识，用于将响应与请求相关联。设备必须确保所有请求标识唯一。对 {{site.data.keyword.iot_short_notm}} 请求的响应必须包含正确的 **reqId** 值。

有关特定请求和响应消息的更多信息，请参阅[设备管理协议](device_mgmt/index.html)和[设备管理请求](device_mgmt/requests.html)。
