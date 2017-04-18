---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-07"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# 服务工作方式
{{site.data.keyword.iotinsurance_full}} 可创建流来收集、管理和分析所连接的保单持有者的数据。
{:shortdesc}

保险提供者在 {{site.data.keyword.Bluemix_notm}} 组织内创建 {{site.data.keyword.iotinsurance_short}} 的实例。承保人的客户在家中有传感器，可连接到传感器提供者的云。客户从移动设备授权 {{site.data.keyword.iotinsurance_short}} 服务接收传感器数据。{{site.data.keyword.iotinsurance_short}} Transformer 连接到传感器提供者的云，拉取每个用户的数据并将其发送给 {{site.data.keyword.iot_short_notm}} 服务器。如果传感器显示客户家中可提供在承保
人保障中指定的参数，那么将向承保人仪表板和客户设备发送通知。

连接的传感器会检测事件（例如，漏水），并向智能住宅供应商（例如，Wink）发送信息。{{site.data.keyword.iotinsurance_short}} 使用其与智能住宅供应商的云建立的连接来检测信号，并创建警报有效内容。有效内容通过 MQTT 发送给 {{site.data.keyword.iotinsurance_short}} 保障引擎进行处理。保障引擎会分析有效内容是否与保障规则定义的条件相匹配。如果匹配，保障引擎将通过 MQTT 向 {{site.data.keyword.iotinsurance_short}} 操作引擎发出危险有效内容。操作引擎会针对该类型的危险执行保障定义的操作，例如向房主发送短信。

{{site.data.keyword.iotinsurance_short}} 依赖 {{site.data.keyword.iot_full}} 在其组件之间传递警报和危险有效内容。完整的工作系统需要用户、保障以及用户与保障之间的关联。

![{{site.data.keyword.iotinsurance_short}} 过程。本主题的正文部分对此图进行了具体描述。](images/IoT4I_process.svg "{{site.data.keyword.iotinsurance_short}} 过程")
