---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# 使用 API 扩展服务
{: #iot4i_extending_service}
{{site.data.keyword.iotinsurance_full}} 提供了多个 API，可用于定制并扩展 {{site.data.keyword.iotinsurance_short}} 解决方案。
{:shortdesc}

{{site.data.keyword.iotinsurance_short}} 随附对 Wink 漏水传感器的内置支持。通过使用提供的 API，可以定制 {{site.data.keyword.iotinsurance_short}} 解决方案以支持新的设备类型和供应商。{{site.data.keyword.iotinsurance_short}} 依赖云到云通信从设备获取传感器数据。通过创建新的转换微服务，可以定制 {{site.data.keyword.iotinsurance_short}} 以从新设备读取传感器数据，通过 {{site.data.keyword.iot_short_notm}} 服务将数据传递到系统其余部分，然后根据需要采取操作。

有关完整的示例代码集，请参阅 [API 示例 GitHub 存储库 ![外部链接图标](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){: new_window}。

有关 API 的完整信息，请参阅 [API 文档 ![外部链接图标](../../icons/launch-glyph.svg)](https://iot4i-api-docs.mybluemix.net/){: new_window}。
