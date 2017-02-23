---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-22"

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
|C++| https://github.com/ibm-watson-iot/iot-cpp
|C#| https://github.com/ibm-watson-iot/iot-csharp
|Embedded C| https://github.com/ibm-watson-iot/iot-embeddedc
|Java™|https://github.com/ibm-watson-iot/iot-java
|mBed C++|https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/
|Node.js|https://github.com/ibm-watson-iot/iot-nodejs
|Node-RED|https://github.com/ibm-watson-iot/iot-nodered
|Python|https://github.com/ibm-watson-iot/iot-python

有关可用客户机库的更多信息和链接，另请参阅[用于开发 {{site.data.keyword.iot_short_notm}} 的客户机库](../iot_platform_client_lib.html)。
