---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-04"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# {{site.data.keyword.iotinsurance_short}} 入门
{: #gettingstarted}

{{site.data.keyword.iotinsurance_full}} 是一项 {{site.data.keyword.Bluemix_notm}} 服务，可用于收集、管理和分析所连接的保单持有者的数据。通过 {{site.data.keyword.iotinsurance_short}}，可以提供个性化的风险评估、实时保护并降低保单成本。
{:shortdesc}

要快速入门和熟悉运用本服务，必须部署所需的服务和应用程序，然后配置服务。在[关于 {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html) 中可以找到服务和应用程序的概述以及体系结构图。

**先决条件：**开始之前，请确保满足以下先决条件：
- 您的 {{site.data.keyword.Bluemix_notm}} 空间中必须有 [{{site.data.keyword.iotinsurance_short}} 服务](https://console.ng.bluemix.net/catalog/services/iot-for-insurance/)的实例。 
- 在 {{site.data.keyword.Bluemix_notm}} 组织中，必须提供不少于 2GB 的可用内存，才能启用部署功能。

## 部署所需的服务和应用程序
{: #deploying_services}

1. 要部署需要的所有服务和应用程序，请在 [{{site.data.keyword.Bluemix_notm}} 控制台](https://console.ng.bluemix.net/#all-items)上，单击 {{site.data.keyword.iotinsurance_short}} 服务，然后单击**部署**。

  {{site.data.keyword.iotinsurance_short}} 部署其所需的所有服务和 Node.js 应用程序。它会自动地将应用程序绑定到服务。

  每个服务实例使用缺省服务计划。您可以稍后通过转至服务控制台来升级任何服务计划。您还可以通过删除新实例并将现有实例手动绑定到 {{site.data.keyword.iotinsurance_short}} 服务来使用服务的现有实例。有关应用程序的更多信息，请参阅[关于 {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html)。

  **注**：{{site.data.keyword.iotinsurance_short}} 不再部署 {{site.data.keyword.amafull}} 或 {{site.data.keyword.mobilepushfull}}。{{site.data.keyword.iotinsurance_short}} 的较早版本使用 {{site.data.keyword.amashort}} 服务处理移动应用程序的响应。此处理会针对所有现有 {{site.data.keyword.iotinsurance_short}} 实例继续运作。但是，您必须创建定制验证流程，以使用移动应用程序和新 {{site.data.keyword.iotinsurance_short}} 实例。您还可以选择[创建 {{site.data.keyword.mobilepushshort}} 实例](https://console.ng.bluemix.net/docs/services/mobilepush/index.html)、对其进行配置并将其绑定到 {{site.data.keyword.iotinsurance_short}} API。

2. 验证 {{site.data.keyword.iotinsurance_short}} 仪表板是否可用，并且您是否可以访问 API。
  1. 单击**打开**以打开 {{site.data.keyword.iotinsurance_short}} 仪表板。单击**登录**以接受预填充的凭证。
  2. 单击 **API** 以返回到 {{site.data.keyword.iotinsurance_short}} 服务控制台并查看 API。

  **注：**部署后，可以通过直接在浏览器中输入仪表板或 API 的 URL 来访问仪表板和 API。使用此方法时，必须输入 {{site.data.keyword.iotinsurance_short}} 服务凭证。要找到凭证，请返回到 {{site.data.keyword.iotinsurance_short}} 服务控制台。单击**服务凭证**选项卡，然后单击**查看凭证**。记下用户标识和密码。


<!--
## Configuring
{: #iot4i_configservices}



### Configuring {{site.data.keyword.amashort}}
{: #config_ama}
1. Return to your Bluemix console. All apps and services that were deployed by {{site.data.keyword.iotinsurance_short}} are displayed.

2. Copy the URL of the {{site.data.keyword.iotinsurance_short}} API application. Right-click the API application and select **Copy Link Location**.

3. Open the {{site.data.keyword.amashort}} service. The service is available in the Services section of your {{site.data.keyword.Bluemix_notm}} console.

4. Enable authentication by clicking **On**.

5. In the **Custom** section, enter the following authentication credentials:

  - **Realm name**: `IoT4I`

  - **Custom Identity Provider Url**: Paste the URL of the API application that you copied in a previous step.

  - **Your Web Application Redirect URIs**: Leave this field blank.

6. Save your settings. You can now return to the {{site.data.keyword.iotinsurance_short}} service console or your {{site.data.keyword.Bluemix_notm}} console.
-->


## 创建和配置 {{site.data.keyword.mobilepushshort}}
{: #config_push}
要启用现有移动应用程序的推送通知，您可以选择创建 {{site.data.keyword.mobilepushshort}} 服务的实例，将其绑定到 {{site.data.keyword.iotinsurance_short}} API，并添加公用密钥密码术标准 (PKCS) 12 文件。有关移动应用程序的信息，请参阅[安装和连接样本移动
应用程序](iotinsurance_mobile_app.html)。有关 {{site.data.keyword.mobilepushshort}} 的信息，请参阅[推送通知入门](https://console.ng.bluemix.net/docs/services/mobilepush/index.html)。

要在创建后配置服务，请执行以下步骤：

  1. 打开 {{site.data.keyword.mobilepushshort}} 服务。
  2. 单击**配置**。
  3. 在“Apple 推送通知证书”部分中，上传移动应用程序的 PKCS 12 文件并输入密码。


后续步骤
{: #whats_next}
了解使用 {{site.data.keyword.iotinsurance_short}} 可以执行的操作。

- 使用“保障工具包”中的指令和 API 来创建[用户和保障关联](iotinsurance_shield_toolkit.html)。
<!-- - Install and connect the [sample mobile app](iotinsurance_mobile_app.html). -->
- 下载或查看所有 [GitHub 站点上的 API ![外部链接图标](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}。

# 相关链接
{: #rellinks}

## 教程和样本
{: #samples}
* [{{site.data.keyword.iotinsurance_short}} 保障库 ![外部链接图标](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-shields){: new_window}
* [GitHub 上的样本移动应用程序代码 ![外部链接图标](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## API 参考
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API ![外部链接图标](../../icons/launch-glyph.svg)](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [{{site.data.keyword.iotinsurance_short}}API 示例 ![外部链接图标](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}


## 相关链接
{: #general}
* [{{site.data.keyword.iot_full}}文档](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [开发人员支持论坛 ![外部链接图标](../../icons/launch-glyph.svg)](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix]){:new_window}
* [堆栈溢出支持论坛 ![外部链接图标](../../icons/launch-glyph.svg)](http://stackoverflow.com/questions/tagged/ibm-bluemix){:new_window}
