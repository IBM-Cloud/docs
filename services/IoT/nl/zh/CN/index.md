---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}} 入门
{: #gettingstartedtemplate}
上次更新时间：2016 年 8 月 26 日
{: .last-updated}

{{site.data.keyword.iot_full}} for {{site.data.keyword.Bluemix_notm}} 为您提供多功能工具箱，其中包括网关设备、设备管理和强大的应用程序访问。通过使用 {{site.data.keyword.iot_short_notm}}，您可以从组织收集已连接的设备数据，并对实时数据执行分析。
{:shortdesc}

## 开始之前
{: #byb}

连接设备并利用数据之前，您的 {{site.data.keyword.Bluemix_notm}} 组织中必须有 {{site.data.keyword.iot_short_notm}} 服务的实例。可以直接从 [Bluemix Services Catalog 中的 {{site.data.keyword.iot_short_notm}} 页面](https://console.{DomainName}/catalog/services/internet-of-things-platform/)创建此实例。  

## 步骤 1：连接设备
{: #up_and_running}

要快速入门和熟悉运用此服务，请根据具体情况研究以下选项：

   |   已部署此服务 | 未部署此服务
  ------------- | -------------
  **我有要连接的设备** | [将设备连接到 {{site.data.keyword.iot_short_notm}}](iotplatform_task.html#iotplatform_task)。| 在[播放组织演示](http://discover-iot.eu-gb.mybluemix.net/?cm_mc_uid=44491599487314618721024&cm_mc_sid_50200000=1462798151#/play){:new_window}中研究设备连接。**我没有要连接的设备** | [创建并连接 Node-RED 设备模拟器](nodereddevice_sample.html){:new_window}。 | 开始使用 [Watson IoT Platform 入门模板](https://new-console.stage1.ng.bluemix.net/docs/starters/IoT/iot500.html){:new_window}。
有关如何将特定设备类型连接到 {{site.data.keyword.iot_short_notm}} 的更多信息，请参阅 [developerWorks 诀窍](https://developer.ibm.com/recipes/?post_type=tutorials&s=iot){:new_window}。  

有关设备连接开发者文档，请参阅：
- [设备的 MQTT 连接](devices/mqtt.html)。
- [网关的 MQTT 连接](gateways/mqtt.html)。

## 步骤 2：分析设备数据
{: #analyzing_data}

开始浏览设备正在向 {{site.data.keyword.iot_short_notm}} 发送的实时数据。

{{site.data.keyword.iot_short_notm}} 包括以下分析工具：  
- 用于可视化实时设备数据的[板和卡](data_visualization.html)。
- 由实时设备数据触发的[规则和操作](analytics.html)。

有关快速入门示例，请参阅[将规则和操作与 IBM Watson IoT Platform Cloud Analytics 配合使用](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/){:new_window} developerWorks 诀窍。

## 步骤 3：创建应用程序以使用设备数据
{: #develop_applications}

通过创建并连接您自己的应用程序以使用实时和历史设备数据，从而扩展 {{site.data.keyword.iot_short_notm}} 的数据分析功能。

有关更多信息，请参阅以下主题：   
- 浏览[应用程序开发者文档](applications/api.html)和 [{{site.data.keyword.iot_short_notm}} API 文档](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#/){:new_window}。
- 浏览 [{{site.data.keyword.iot_short_notm}} 客户机库](iot_platform_client_lib.html)，此库提供了工具和文件来构建和开发代码，从而集成和连接设备及应用程序。
- [连接 {{site.data.keyword.cloudantfull}} 服务](cloudant_connector.html)到 {{site.data.keyword.iot_short_notm}} 以存储历史设备数据。




# 相关链接
{: #rellinks}
## 教程和样本
{: #samples}
* [连接设备的诀窍](https://developer.ibm.com/recipes/?post_type=tutorials&s=iot){:new_window}
* [{{site.data.keyword.iot_short_notm}} Play 组织](https://play.internetofthings.ibmcloud.com/){:new_window}
* [将 Intel Galileo 连接到 {{site.data.keyword.iot_short_notm}}](https://developer.ibm.com/recipes/tutorials/connect-an-intel-galileo-to-the-internet-of-things-foundation-connect/){:new_window}
* [连接 ARM® mbed™ IoT 入门模板套件](https://developer.ibm.com/recipes/tutorials/arm-mbed-iot-starter-kit-part-1/){:new_window}
* [将 Raspberry Pi 连接到 {{site.data.keyword.iot_short_notm}}](https://developer.ibm.com/recipes/tutorials/raspberry-pi-4/){:new_window}

## API 参考
{: #api}
* [{{site.data.keyword.iot_short_notm}} API 文档](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#/){:new_window}
* [开发者文档](developer_doc_overview.html)
