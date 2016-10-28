---

copyright:
  years: 2015, 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# MQTT 消息传递
{: #ref-mqtt}
上次更新时间：2016 年 9 月 13 日
{: .last-updated}

MQTT 是设备和应用程序用于与 {{site.data.keyword.iot_full}} 通信的主要协议。MQTT 是一种发布和预订消息传递传输协议，用于在传感器和移动设备之间高效交换实时数据。
{:shortdesc}

MQTT 通过 TCP/IP 运行，并且在可以直接对 TCP/IP 编码时，还可选择使用库来处理 MQTT 协议的详细信息。提供了范围非常广泛的各种 MQTT 客户机库。IBM 致力于开发和支持多种客户机库，包括以下站点上提供的客户机库：

- [MQTT 社区 Wiki](https://github.com/mqtt/mqtt.github.io/wiki)
- [Eclipse Paho 项目](http://eclipse.org/paho/)

## 版本支持
{: #version-support}

{{site.data.keyword.iot_short_notm}} 支持以下 MQTT 消息传递协议版本：

MQTT 版本 | 偏差 | 注释
--- | --- | ---
[3.1.1](https://www.oasis-open.org/standards#mqttv3.1.1)（推荐） | 不支持保留消息，例如，共享的预订。 | <ul><li>OASIS 标准。<li>ISO 标准 (ISO/IEC PRF 20922) <li>相比 V3.1，此标准对协议的定义更为精准，从而改善了各个客户机和服务器之间的互操作性。<li>最大 MQTT 客户机标识 (ClientId) 长度从 V3.1 实施的 23 个字符的限制增加到 256 个字符。</br>{{site.data.keyword.iot_short_notm}} 服务通常需要较长的客户机标识 (ClientId)。</br>不管是 MQTT 协议的哪个版本，都支持较长客户机标识，但是一些 V3.1 客户机库会检查 ClientId 值的长度并实施 23 个字符的限制。</ul>
3.1 | - | MQTT V3.1 是目前广泛使用的协议版本。

{{site.data.keyword.iot_short_notm}} 支持 MQTT 标准允许的任何内容。MQTT 独立于数据，因此无法发送图像、任何编码的文本、加密数据以及几乎每种类型的二进制格式数据。有关 MQTT 标准的更多信息，请参阅以下资源：
- [MQTT.org](http://mqtt.org/)
- [HiveMQ：MQTT 介绍](http://www.hivemq.com/blog/mqtt-essentials-part-1-introducing-mqtt)

## 应用程序、设备和网关客户机
{: #device-app-clients}

在 {{site.data.keyword.iot_short_notm}} 中，主要对象类为设备和应用程序。网关是设备的子类。

MQTT 客户机向服务标识其自身的对象类用于在处于连接状态时确定客户机的功能。对象类还确定客户机认证的机制。

应用程序和设备还可用于不同的 MQTT 主题空间。设备在限定了设备的主题空间中运行，而应用程序对整个组织的主题空间具有完全访问权。有关更多信息，请参阅以下主题：

- [设备](../../devices/mqtt.html)
- [应用程序](../../applications/mqtt.html)
- [网关](../../gateways/mqtt.html)

## 服务质量级别
{: #qos-levels}

MQTT 协议为客户机和服务器之间的消息传递提供了三种服务质量：“最多一次”、“至少一次”和“恰好一次”。
虽然可使用任何服务质量级别发送事件和命令，但必须仔细考虑哪个合适的服务级别满足您的需求。服务质量级别 2 选项并不总是优于级别 0。

### 最多一次 (QoS0)

“最多一次”服务质量级别 (QoS0) 是最快的传输方式，有时称为“触发并忘记”。消息将最多传递一次，或者可能完全不会传递。网络中的传递不会得到确认，并且不会存储消息。如果客户机断开连接或者服务器发生故障，那么消息可能会丢失。

MQTT 协议不需要服务器将服务质量级别为 0 的发布内容转发到客户机。如果客户机在服务器收到发布内容时断开连接，根据服务器实施，可能会废弃此发布内容。

**提示：**以某个时间间隔发送实时数据时，请使用服务质量级别 0。丢失单条消息实际上不会产生很大影响，因为之后很快将发送包含较新数据的另一条消息。在此场景中，使用较高服务质量会带来额外成本，却不会获得任何实际优势。

### 至少一次 (QoS1)

使用服务质量级别 1 (QoS1)，消息会始终至少传递一次。如果发送者收到应答之前消息传递失败，那么一条消息可能会传递多次。该消息必须存储在发送者本地，直到发送者收到关于接收者已发布此消息的确认为止。存储此消息是为了以防必须再次发送此消息。

### 恰好一次 (QoS2)

“恰好一次”服务质量级别 (QoS2) 是最安全也是最慢的传输方式。消息始终传递恰好一次，并且必须存储在发送者本地，直到发送者收到关于接收者已发布此消息的确认为止。存储此消息是为了以防必须再次发送此消息。使用服务质量级别 2，会采用比级别 1 更复杂的握手和应答序列，以确保消息不会重复。

**提示：**发送命令时，如果需要确认将仅执行指定命令且仅执行一次，请使用服务质量级别 2。此示例说明了级别 2 产生的额外开销比其他级别更为有利的情况。

## 预订缓冲区和 clean session
{: #subscription-buffers-and-clean-session}

将为来自设备或应用程序的每个预订分配一个可容纳 5000 条消息的缓冲区。使用缓冲区，任何应用程序或设备可滞后于其正在处理的实时数据，还可为其做出的每个预订积压最多 5000 条暂挂消息。缓冲区已满时，会在收到新消息时废弃最旧消息。

使用 MQTT clean session 选项可访问预订缓冲区。当 clean session 设置为 false 时，订户会收到来自缓冲区的消息。当 clean session 设置为 true 时，会重置缓冲区。

**注：**无论使用什么服务质量设置，预订缓冲区限制都适用。如果应用程序无法与其做出的预订的消息速率保持同步，以级别 1 或 2 发送的消息有可能无法传递到该应用程序。

## 消息有效内容限制
{: #message-payload}

{{site.data.keyword.iot_short_notm}} 支持发送和接收 MQTT 标准允许的任何格式的消息。MQTT 独立于数据，因此无法发送图像、任何编码的文本、加密数据以及几乎每种类型的二进制格式数据。但是，对于特定用例，存在一些限制。   

对于 {{site.data.keyword.iot_short_notm}} 上的消息有效内容，也存在大小限制。

### 消息有效内容格式限制

消息有效内容可包含任何有效字符串，但是，JSON（“json”）、文本（“text”）和二进制（“bin”）格式比其他格式类型更常用。

下表概述了不同格式类型的消息有效内容限制：

有效内容格式  | 特定用例的准则
--------- | ----------  
JSON | JSON 是 {{site.data.keyword.iot_short_notm}} 的标准格式。如果计划使用内置 {{site.data.keyword.iot_short_notm}} 仪表板、板和卡以及分析，请确保消息有效内容格式符合格式正确的 JSON 文本。
文本 | 使用有效 UTF-8 字符编码。
二进制 | 无限制。


### 最大消息有效内容大小

**重要信息：**{{site.data.keyword.iot_short_notm}} 上的最大有效内容大小为 131072 字节。将拒绝其有效内容超出限制的消息。正在连接的客户机也会断开连接，并且会在诊断日志中显示一条消息，如以下设备消息示例中所示：

`Closed connection from x.x.x.x. The message size is too large for this endpoint.`
