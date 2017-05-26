---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-02"
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
- 在 {{site.data.keyword.Bluemix_notm}} 组织中，必须提供不少于 2GB 的可用内存，才能启用部署功能。如果您是从前版本进行升级，那么应至少具有 2.5 GB。

## 部署所需的服务和应用程序
{: #deploying_services}

1. 要部署需要的所有服务和应用程序，请在 [{{site.data.keyword.Bluemix_notm}} 控制台](https://console.ng.bluemix.net/#all-items)上，单击 {{site.data.keyword.iotinsurance_short}} 服务，然后单击**部署**。

  {{site.data.keyword.iotinsurance_short}} 部署其所需的所有服务和 Node.js 应用程序。它会自动地将应用程序绑定到服务。

  每个服务实例使用缺省服务计划。您可以稍后通过转至服务控制台来升级任何服务计划。您还可以通过删除新实例并将现有实例手动绑定到 {{site.data.keyword.iotinsurance_short}} 服务来使用服务的现有实例。有关应用程序的更多信息，请参阅[关于 {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html)。

  **重要信息：**部署 {{site.data.keyword.iotinsurance_short}} 试用版时，请注意同时部署的其他服务和应用程序的免费版本功能有限。{{site.data.keyword.iot_short_notm}} 限制为最多 500 个设备，而 {{site.data.keyword.cloudant_short_notm}} 限制为一个 GB 的数据，并且具有有限的读写线程功能。

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

（可选）要启用现有移动应用程序的推送通知，您可以选择创建 {{site.data.keyword.mobilepushshort}} 服务的实例，将其绑定到 {{site.data.keyword.iotinsurance_short}} API，并添加公用密钥密码术标准 (PKCS) 12 文件。有关移动应用程序的信息，请参阅[安装和连接样本移动
应用程序](iotinsurance_mobile_app.html)。有关 {{site.data.keyword.mobilepushshort}} 的信息，请参阅[推送通知入门](https://console.ng.bluemix.net/docs/services/mobilepush/index.html)。

要在创建后配置服务，请执行以下步骤：

  1. 打开 {{site.data.keyword.mobilepushshort}} 服务。
  2. 单击**配置**。
  3. 在“Apple 推送通知证书”部分中，上传移动应用程序的 PKCS 12 文件并输入密码。

## 使用 Weather Company 数据
{: #weather_company}

（可选）{{site.data.keyword.iotinsurance_short}} 提供了一组 Weather Company 的静态数据，您可以进行查看以演示。您还可以选择创建 [{{site.data.keyword.weatherfull}} 服务](../Weather/index.html)实例并将其绑定到 {{site.data.keyword.iotinsurance_short}} 天气应用程序，从而访问 Weather Company 的实时数据。

**重要信息：**{{site.data.keyword.weather_short}} 服务的免费版本限制为 10,000 个请求。如果需要更多请求，您可以升级为付费版本。

后续步骤
{: #whats_next}
了解使用 {{site.data.keyword.iotinsurance_short}} 可以执行的操作。

- 使用“保障工具包”中的指令和 API 来创建[用户和保障关联](iotinsurance_shield_toolkit.html)。
<!-- - Install and connect the [sample mobile app](iotinsurance_mobile_app.html). -->
- 下载或查看所有 [GitHub 站点上的 API 示例 ![外部链接图标](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}。
