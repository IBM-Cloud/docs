---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
# 标准和需求
{: #standards_and_requirements}

{{site.data.keyword.iot_full}} 支持许多有关消息传递、常规设备和应用程序开发的标准和需求。
{:shortdesc}


<!-- ## Blockchain
{: #blockchain}

{{site.data.keyword.iot_short_notm}} supports the following versions of the Hyperledger fabric:
- 0.5

## Python
{: #python}

Support for MQTT over SSL requires at least Python v2.7.9 or v3.4, and OpenSSL v1.0.1.
-->

## MQTT
{: #mqtt}

{{site.data.keyword.iot_short_notm}} 支持以下 MQTT 消息传递协议版本：

MQTT 版本 | 注释
--- | --- | ---
[3.1.1 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.oasis-open.org/standards#mqttv3.1.1){: new_window}（建议）  | <ul><li>OASIS 标准。<li>ISO 标准 (ISO/IEC PRF 20922) <li>相比 V3.1，此标准对协议的定义更为精准，从而改善了各个客户机和服务器之间的互操作性。<li>最大 MQTT 客户机标识 (ClientId) 长度从 V3.1 实施的 23 个字符的限制增加到 256 个字符。</br>{{site.data.keyword.iot_short_notm}} 服务通常需要较长的客户机标识。</br>不管是 MQTT 协议的哪个版本，都支持较长的客户机标识。但是，一些 V3.1 客户机库会检查 ClientId 值的长度并实施 23 个字符的限制。</ul>
3.1 | MQTT V3.1 是目前广泛使用的协议版本。

{{site.data.keyword.iot_short_notm}} 支持 MQTT 标准允许的任何内容。MQTT 独立于数据，因此无法发送图像、任何编码的文本、加密数据以及几乎每种类型的二进制格式数据。有关 MQTT 标准的更多信息，请参阅以下资源：
- [MQTT.org ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://mqtt.org/){: new_window}
- [HiveMQ：MQTT 介绍 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://www.hivemq.com/blog/mqtt-essentials-part-1-introducing-mqtt){: new_window}

有关 {{site.data.keyword.iot_short_notm}} 特定用例的消息有效内容大小限制和格式限制的信息，请参阅 [MQTT 消息传递](mqtt/index.html)。
