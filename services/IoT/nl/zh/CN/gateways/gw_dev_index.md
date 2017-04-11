---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 在 {{site.data.keyword.iot_short_notm}} 上开发网关
{: #gw_dev_index}

如果设备无法直接连接到因特网，那么可以构建网关设备来检索数据，并将数据发送到您 {{site.data.keyword.iot_full}} 组织中的应用程序。
提供的客户机库、样本和信息可帮助您将设备网关连接到 {{site.data.keyword.iot_short_notm}} 组织和应用程序。
{:shortdesc}

## 连接协议
网关通过 MQTT 消息传递协议连接到 {{site.data.keyword.iot_short_notm}}。不支持使用 HTTP 消息传递将网关连接至 {{site.data.keyword.iot_short_notm}}。使用 HTTP 消息传递仅可以连接设备。

## 客户机库
用于开发可连接到 {{site.data.keyword.iot_short_notm}} 的网关的客户机库现提供以下语言版本：

|客户机库 |库和更多文档的链接
|:---|:---
|C++|[https://github.com/ibm-watson-iot/iot-cpp ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-watson-iot/iot-cpp){: new_window}
|C#|[https://github.com/ibm-watson-iot/iot-csharp ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-watson-iot/iot-csharp){: new_window}
|Embedded C| [https://github.com/ibm-watson-iot/iot-embeddedc ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-watson-iot/iot-embeddedc){: new_window}
|Java™|[https://github.com/ibm-watson-iot/iot-java ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-watson-iot/iot-java){: new_window}
|mBed C++|[https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/ ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/){: new_window}
|Node.js|[https://github.com/ibm-watson-iot/iot-nodejs ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-watson-iot/iot-nodejs){: new_window}
|Node-RED|[https://github.com/ibm-watson-iot/iot-nodered ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-watson-iot/iot-nodered){: new_window}
|Python|[https://github.com/ibm-watson-iot/iot-python ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-watson-iot/iot-python){: new_window}
有关可用客户机库的更多信息和链接，另请参阅[用于开发 {{site.data.keyword.iot_short_notm}} 的客户机库](../iot_platform_client_lib.html)。

## 边缘分析
{: #eaa_community}

使用 {{site.data.keyword.iot_short_notm}} Edge Analytics 功能，可以在网关设备上运行 {{site.data.keyword.iot_short_notm}} Analytics。使用 Edge Analytics，可以引入分析功能，用于分析和响应在网络边缘收集的数据。您还可以将设备数据发送到 {{site.data.keyword.iot_short_notm}}，以进行额外的分析处理、仪表板可视化、作为其他分析的输入或者存储在基于云的历史存储库中。

可以从 [IBM Edge Analytics 社区页面 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/developerworks/community/groups/service/html/communitystart?communityUuid=3df173af-0c21-4b9c-9fd1-e8e5561ef460&ftHelpTip=true){: new_window} 下载 Edge Analytics SDK。SDK 包括 SDK JAR 文件、Javadoc、样本代码、诀窍链接和自述文件。在社区中，还可以观看视频，以快速入门和熟悉运用 Edge Analytics，可以使用社区论坛来问问题。
