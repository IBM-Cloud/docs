---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 使用 {{site.data.keyword.messagehub}} 连接并配置历史服务  
{: #messagehub_main}

将 {{site.data.keyword.messagehub_full}} 连接到 {{site.data.keyword.iot_short}} 为历史数据存储提供了可扩展的高吞吐量消息传递总线。{{site.data.keyword.messagehub}} 基于 Apache Kafka 构建，这是一种高吞吐量的开放式源代码消息传递系统，提供了等待时间短的平台，用于处理实时数据订阅源。

## 开始之前  
{: #byb}

在将 {{site.data.keyword.messagehub}} 连接到 {{site.data.keyword.iot_short}} 服务之前，请完成以下任务：

- 使用 {{site.data.keyword.Bluemix_notm}}“目录”，在 {{site.data.keyword.iot_short_notm}} 所在的 {{site.data.keyword.Bluemix_notm}} 空间中设置 {{site.data.keyword.messagehub}}。有关 {{site.data.keyword.messagehub}} 的更多信息，请参阅 [{{site.data.keyword.messagehub}}入门](https://console.{DomainName}/docs/services/MessageHub/index.html)。

- 确保您在已通过 {{site.data.keyword.Bluemix_notm}} 登录的 {{site.data.keyword.Bluemix_notm}} 组织中具有开发者特权。如果您未通过 {{site.data.keyword.Bluemix_notm}} 登录，或者在此 {{site.data.keyword.Bluemix_notm}} 组织中不具有开发者特权，那么您无法授权绑定 {{site.data.keyword.messagehub}} 和 {{site.data.keyword.iot_short_notm}}。

## Connect

要连接 {{site.data.keyword.messagehub}} 用于历史数据存储，请执行以下操作：

1. 在 {{site.data.keyword.iot_short}} 仪表板上，单击导航栏中的**扩展**。
2. 在“历史数据存储”磁贴中，单击**设置**。
4. 选择要连接的 {{site.data.keyword.messagehub}} 服务。
  
{{site.data.keyword.iot_short}} 服务所在的 {{site.data.keyword.Bluemix_notm}} 空间中的所有可用 {{site.data.keyword.messagehub}} 服务都会列在“配置历史数据存储”部分中。
5. 选择 {{site.data.keyword.messagehub}} 配置选项：
 1. 选择时区。
   
发送到 {{site.data.keyword.messagehub}} 的设备数据上的时间戳记会转换为所选时区。
 2. 选择缺省主题。
   
如果此处已定义缺省主题，那么设备事件会发送到该主题。要使用更详细的主题分配，请将缺省主题保留为空白，并添加定制转发规则。
 3. 可选：指定定制转发规则。
   
指定用于转发设备事件的其他规则。仅会转发与定制转发规则匹配的事件。  
 **注：**一个事件可能会与多个转发规则相匹配，从而转发到多个 {{site.data.keyword.messagehub}} 主题。
 4. 可选：配置主题。
   
要使用两个缺省分区以及更多分区来创建主题，可以指定分区配置。
 5. 单击**完成**。
5. 单击**授权**。
6. 在“授权”对话框中，单击**确认**。

现在，您的设备数据会存储在 {{site.data.keyword.messagehub}} 中。
