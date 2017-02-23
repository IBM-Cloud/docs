----

copyright:
  years: 2015, 2016, 2017

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 在 {{site.data.keyword.iot_short_notm}} 上开发设备
{: #device_dev_index}

上次更新时间：2016 年 11 月 26 日
{: .last-updated}

设备是连接到因特网并且要向云发送数据或从云接收数据的任何对象。可以使用设备将事件信息（例如，传感器读数）发送到云，也可以使用设备接受来自云中应用程序的命令。

设备使用事件将数据发布到 {{site.data.keyword.iot_short_notm}}。设备控制事件内容，并为发送的每个事件指定名称。{{site.data.keyword.iot_short_notm}} 从设备接收到事件时，会使用用于接收事件的连接的凭证来确定事件是哪个设备发送的。此体系结构可防止设备互相冒充。

有关关键概念（包括设备）的更多信息，请参阅[关于 Watson IoT Platform](https://console.ng.bluemix.net/docs/services/IoT/iotplatform_overview.html#watsoniotplatform_importantconcepts)。


# 将设备连接到 {{site.data.keyword.iot_short_notm}}
{: #device_connect}
可以使用 HTTP 或 MQTT 协议将设备连接到 {{site.data.keyword.iot_short_notm}}。如果要配置请求/响应场景（例如，有人进行采购并接收确认时），请使用 HTTP。如果要配置事件场景（例如，有人按门铃，使得移动设备触发警报时），请使用 MQTT。

设备必须向组织注册后，才能连接到 {{site.data.keyword.iot_full}}。要安全连接到 {{site.data.keyword.iot_short_notm}}，您必须注册 Bluemix 帐户，并创建您自己的 {{site.data.keyword.iot_short_notm}} 组织。然后，可以使用此组织的标识来注册设备。已注册的设备会使用唯一设备标识（例如，MAC 地址）和仅针对该设备接受的认证令牌向 {{site.data.keyword.iot_short_notm}} 标识自身。一旦您已安全连接后，即可使用 Bluemix 来构建自己的应用程序。请尝试使用 Node-RED 将您的应用程序连线在一起。

如果要连接未注册的设备（例如，要运行概念验证），那么可以使用特殊组织标识 `QuickStart` 来连接设备。`QuickStart` 是在云中运行的 {{site.data.keyword.iot_short_notm}} 的公共沙箱实例。如果无需安全连接，那么可以使用 `QuickStart` 来测试设备连接并试验 {{site.data.keyword.iot_short_notm}}。完成试验后，请使用 TLS 和您的认证令牌，以安全方式将设备重新连接到您自己的特定组织标识实例。

有关使用 HTTP 协议将设备连接到 {{site.data.keyword.iot_short_notm}} 的更多信息，请参阅[针对设备的 HTTP REST API](https://console.ng.bluemix.net/docs/services/IoT/devices/api.html)。
有关使用 MQTT 协议将设备连接到 {{site.data.keyword.iot_short_notm}} 的更多信息，请参阅[设备的 MQTT 连接](https://console.ng.bluemix.net/docs/services/IoT/devices/mqtt.html)。


# 设备开发入门
{: #get_started}
如果您有已经针对 {{site.data.keyword.iot_short_notm}} 启用的设备，那么可以直接开始使用该设备。

如果您的设备尚未启用，请查看 [developerWorks](https://developer.ibm.com/recipes/) 上提供的诀窍。浏览现有诀窍以了解是否有适合您设备的诀窍，然后使用相应诀窍来帮助您着手开发。您甚至可以根据需要发布自己的诀窍。

如果找不到适合您特定设备的诀窍，IBM 还提供有若干编程指南和 API，可供您用于入门。这些指南包含客户机库、样本和信息，可帮助您构建和开发代码，以用于将设备和应用程序集成并连接到 {{site.data.keyword.iot_short_notm}}。目前提供了以下编程指南：

- Java
- Node.js
- Embedded C
- ARM mBed C++
- Python
- C#
- Node-RED

有关可用编程指南的更多信息和链接，请参阅[用于开发 {{site.data.keyword.iot_short_notm}} 的客户机库](../iot_platform_client_lib.html)。

如果找不到合适的 {{site.data.keyword.iot_short_notm}} 编程指南，您可以自行编写程序，并使用 MQTT 或 HTTP 协议将设备连接到 {{site.data.keyword.iot_short_notm}}。

MQTT 是一种开放标准，由 OASIS 标准化组织进行管理，并通过了 ISO 国际认证。有关更多信息，请参阅 [OASIS Message Queuing Telemetry Transport](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=mqtt)。

提供有各种各样的 MQTT 客户机库，适用于众多不同的系统，包括以下环境：
- http://www.eclipse.org/paho/
- https://github.com/mqtt/mqtt.github.io/wiki/software?id=software

有关 MQTT 的更多信息，请参阅 [MQTT 消息传递](https://console.ng.bluemix.net/docs/services/IoT/reference/mqtt/index.html?pos=3)。
