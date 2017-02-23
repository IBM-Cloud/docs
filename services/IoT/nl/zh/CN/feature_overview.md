---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-12"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}} 功能概述
{: #feature_overview}

{{site.data.keyword.iot_full}} 基于以下关键方面进行构建：

  1. Connect - 连接设备并开发应用程序。
  2. 信息管理 - 存储和查看设备数据，并将 {{site.data.keyword.iot_short_notm}} 与其他服务集成。
  3. 分析 - 通过使用 {{site.data.keyword.iot_short_notm}} 仪表板可视化实时设备数据。
  4. 风险管理 - 通过对用户和应用程序的访问控制来配置安全的连接和体系结构。

## Connect
{: #connect}

{{site.data.keyword.iot_short_notm}} Connect 是任何 {{site.data.keyword.iot_short_notm}} 服务的起始点。连接设备、创建应用程序、控制设备以及与第三方服务交互全部通过 {{site.data.keyword.iot_short_notm}} Connect 实现。

### 网关设备

通过使用网关，可将设备连接到 {{site.data.keyword.iot_short_notm}}，在不使用网关的情况下，设备无法连接到因特网。网关具有设备的所有功能，还可以代表所连接的设备进行发布或预订。利用网关设备，那些无法连接互联网的传感器组可以通过将数据发送到网关来连接 {{site.data.keyword.iot_short_notm}}。有关更多信息，请参阅[开发网关](https://console.ng.bluemix.net/docs/services/IoT/gateways/gw_dev_index.html)。

### 设备管理

通过设备管理 API 以及设备上安装的设备管理代理程序，提供了设备管理功能。安装了设备管理代理程序的设备可执行设备管理操作，这些操作可通过主 {{site.data.keyword.iot_short_notm}} 仪表板或设备管理 API 触发。设备管理操作包括重新引导、下载和安装固件更新，以及将设备重置为出厂设置。同时，设备管理还可以扩展，以包括定制的设备管理操作。有关更多信息，请参阅[设备管理文档](https://console.ng.bluemix.net/docs/services/IoT/devices/device_mgmt/index.html)。

### 扩展和服务集成

扩展和服务集成支持将外部服务和核心服务的用户定义扩展添加到 {{site.data.keyword.iot_short_notm}} 实例。可以与 {{site.data.keyword.iot_short_notm}} 集成的外部服务包括 The Weather Company 天气位置服务（可用于查找设备所在位置的当前天气）、Jasper SIM 数据以及 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.ssoshort}}。有关第三方服务集成和扩展的更多信息，请参阅[集成外部服务](https://console.ng.bluemix.net/docs/services/IoT/reference/extensions/index.html)。

---

## 信息管理
{: #information_management}

{{site.data.keyword.iot_short_notm}} 信息管理在设备所发送的数据到达 {{site.data.keyword.iot_short_notm}} 服务后对其进行控制。信息管理包括数据存储和转换。

### 设备上次事件高速缓存

通过使用 {{site.data.keyword.iot_short_notm}} 上次事件高速缓存 API，可检索设备上次所发送的事件。这在设备联机或脱机的情况下都适用，这样不管设备的物理位置或使用状态如何，您都可检索设备状态。对于最多 365 天之前发生的任何特定事件，可检索设备的上次事件数据。

### 设备事件数据存储

可以存储 {{site.data.keyword.iot_short_notm}} 服务中的设备事件数据以供将来使用。要执行深度分析以获取对该数据的洞察，数据存储是非常关键的第一步。例如，您可跟踪较长时间段内的更改，存储数据集，以用于功能强大的分析工具（包括用于 Watson API 和认知计算）。有关更多信息，请参阅[连接 {{site.data.keyword.cloudant_short_notm}} 历史服务](https://console.ng.bluemix.net/docs/services/IoT/cloudant_connector.html)或[连接 {{site.data.keyword.messagehub}} 历史服务](https://console.ng.bluemix.net/docs/services/IoT/message_hub.html)。

---

## 分析
{: #analytics}

### 可视化实时设备数据

您可以通过使用仪表板卡，可视化和显示实时设备数据。仪表板卡实时监视和显示设备数据，这样您可以跟踪关键设备或设备数据。这些可视化内容显示在主 {{site.data.keyword.iot_short_notm}} 仪表板上，便于您快速访问实时设备数据的上下文和状态。有关更多信息，请参阅[可视化实时数据](https://console.ng.bluemix.net/docs/services/IoT/data_visualization.html)。

### 边缘与云分析

通过使用 {{site.data.keyword.iot_short_notm}} 云分析，可指定基于实时设备数据并且在满足条件时将触发警报和可选操作的规则条件。例如，可以创建一条规则，用于确保在设备中断或设备温度达到峰值时，向用户设备上的仪表板发送警报，并向管理员发送电子邮件。有关更多信息，请参阅[云分析文档](https://console.ng.bluemix.net/docs/services/IoT/cloud_analytics.html)。

通过边缘分析，可将分析规则触发过程从云移至支持边缘分析的网关，通过执行靠近设备的分析处理，可显著降低上传到云的设备数据流量。
有关更多信息，请参阅[边缘分析文档](https://console.ng.bluemix.net/docs/services/IoT/edge_analytics.html)。

---

## 风险管理
{: #risk_management}

### 安全的连接和体系结构

{{site.data.keyword.iot_short_notm}} 的体系结构旨在防止设备冒充其他设备，以维护设备数据的完整性。设备通过使用只有您自己知道的客户机标识和认证令牌组合来连接到 {{site.data.keyword.iot_short_notm}}。注册设备或生成 API 密钥后，认证令牌将使用加密盐 (Salt) 进行加密并散列化以维护凭证的安全性。

使用风险与安全管理附加组件，您可以增强 {{site.data.keyword.iot_short_notm}} 安全性，确保服务器和设备之间的所有连接点都可以通过经验证的凭证进行认证。有了这个附加组件，就会在 {{site.data.keyword.iot_short_notm}} 使用的用户标识和令牌之上，再使用证书和传输层安全 (TLS) 进行认证。在设备和服务器通信期间，根据在风险与安全管理附加组件上的配置，任何设备如果没有访问服务器的有效证书，那么即使使用了有效的用户标识和密码，也都会被拒绝访问。

---
