---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Note to writers - index.md and iot4egettingstarted.md are (almost) duplicates and a change to one should be made to both. index.md appears within the product app as the getting started page. iot4egettingstarted.md appears as the top level topic in the docs toc. -->

# 使用 {{site.data.keyword.iotelectronics}} Starter 创建应用程序

{{site.data.keyword.iotelectronics_full}} 是集成的端到端解决方案，通过该解决方案，您的应用程序可以与连接的设备进行通信，并控制、分析和更新连接的设备。该入门模板包括一个可用于创建模拟设备的入门模板应用程序，以及一个可用于通过移动设备控制这些设备的样本移动应用程序。
{:shortdesc}

## 开始之前

开始之前，您必须在 {{site.data.keyword.Bluemix_notm}} 组织中部署 {{site.data.keyword.iotelectronics}} 的实例。部署实例会自动部署入门模板的组件应用程序和服务。

 您可以在 {{site.data.keyword.Bluemix_notm}} 目录的“样板”部分中，[查找 {{site.data.keyword.iotelectronics}} Starter](https://console.{DomainName}/catalog/starters/iot-for-electronics-starter/)。

## {{site.data.keyword.iotelectronics}} 入门
首先，请完成以下任务：

1. 使用 {{site.data.keyword.iotelectronics}} Starter Web 应用程序[创建模拟设备](iot4ecreatingappliances.html)。出于演示目的，洗衣机将用作 {{site.data.keyword.iotelectronics}} Starter 内的模拟设备。选择连接的设备可以是任何类型的智能电子设备。
2. [下载并连接](iotelectronics_config_mobile.html)样本移动应用程序。


## 后续工作
查看使用 {{site.data.keyword.iotelectronics}} 可以执行的操作。

- [浏览入门模板应用程序](iot4ecreatingappliances.html)，以了解企业制造商可以如何监视连接到 {{site.data.keyword.iot_short_notm}} 的设备。
- [浏览样本移动应用程序](iotelectronics_config_mobile.html)，以了解设备所有者可以如何注册其设备并与之交互。
- 在 {{site.data.keyword.iot_short_notm}} 中为已注册的设备[浏览和管理数据](iotelectronics_dashboard.html)。
- [浏览 API ![外部链接图标](../../icons/launch-glyph.svg)](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html){:new_window}，以了解可以如何定制和扩展自己的 {{site.data.keyword.iotelectronics}} 应用程序。

# 相关链接
{: #rellinks}
<!-- Related Links last updated 23 October 2016 - new API source -->
## API 文档
{: #api}
* [{{site.data.keyword.iotelectronics}} API ![外部链接图标](../../icons/launch-glyph.svg)](https://broker-uss-iot4e.electronics.internetofthings.ibmcloud.com/public/iot4eregistrationapi.html){:new_window}
* [{{site.data.keyword.iot_short}} API ![外部链接图标](../../icons/launch-glyph.svg)](https://developer.ibm.com/iotfoundation/recipes/api-documentation/){:new_window}
* [IBM Watson IoT Service Health Dashboard ![外部链接图标](../../icons/launch-glyph.svg)](https://status.internetofthings.ibmcloud.com){: new_window}

## 组件
{: #general}

* [{{site.data.keyword.iotelectronics}} 文档](iotelectronics_overview.html){:new_window}
* [{{site.data.keyword.iot_full}} 文档](https://console.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [{{site.data.keyword.sdk4nodefull}} 文档](https://console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime){:new_window}

## 样本
{: #samples}
* [样本移动应用程序](https://console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html){:new_window}
