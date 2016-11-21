---

copyright:
  years: 2016
lastupdated: "2016-10-26"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# {{site.data.keyword.iotinsurance_short}} 入门

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

2. 验证 {{site.data.keyword.iotinsurance_short}} 仪表板是否可用，并且您是否可以访问 API。
  1. 单击**打开**以打开 {{site.data.keyword.iotinsurance_short}} 仪表板。单击**登录**以接受预填充的凭证。
  2. 单击 **API** 以返回到 {{site.data.keyword.iotinsurance_short}} 服务控制台并查看 API。

  **注：**部署后，可以通过直接在浏览器中输入仪表板或 API 的 URL 来访问仪表板和 API。使用此方法时，必须输入 {{site.data.keyword.iotinsurance_short}} 服务凭证。要找到凭证，请返回到 {{site.data.keyword.iotinsurance_short}} 服务控制台。单击**服务凭证**选项卡，然后单击**查看凭证**。记下用户标识和密码。

## 配置服务
{: #iot4i_configservices}
执行以下任务以配置服务：

### 配置 {{site.data.keyword.amashort}}
{: #config_ama}
1. 返回到 Bluemix 控制台。这将显示 {{site.data.keyword.iotinsurance_short}} 部署的所有应用程序和服务。

1. 复制 {{site.data.keyword.iotinsurance_short}} API 应用程序的 URL。右键单击该 API 应用程序，然后选择**复制链接位置**。

2. 打开 {{site.data.keyword.amashort}} 服务。该服务在 {{site.data.keyword.Bluemix_notm}} 控制台的“服务”部分中提供。

3. 单击**打开**以启用认证。

4. 在**定制**部分中，单击**配置**，然后输入以下认证凭证：

  - **域名**：`IoT4I`

  - **定制身份提供者 URL**：粘贴您在第一步中复制的 API 应用程序的 URL。

  - **您的 Web 应用程序重定向 URI**：将此字段留空。

5. 保存设置。现在，您可以返回到 {{site.data.keyword.iotinsurance_short}} 服务控制台或 {{site.data.keyword.Bluemix_notm}} 控制台。

### 配置 {{site.data.keyword.mobilepushshort}}
{: #config_push}
要启用现有移动应用程序的推送通知，必须配置 {{site.data.keyword.mobilepushshort}} 服务并添加公用密钥密码术标准 (PKCS) 12 文件。有关移动应用程序的信息，请参阅[安装和连接样本移动
应用程序](iotinsurance_mobile_app.html)。有关 {{site.data.keyword.mobilepushshort}} 的信息，请参阅[推送通知入门](https://console.stage1.ng.bluemix.net/docs/services/mobilepush/index.html)。

  1. 打开 {{site.data.keyword.mobilepushshort}} 服务。
  2. 单击**配置**。
  3. 在“Apple 推送通知证书”部分中，上传移动应用程序的 PKCS 12 文件并输入密码。


后续步骤
{: #whats_next}
了解使用 {{site.data.keyword.iotinsurance_short}} 可以执行的操作。

- 使用“保障工具包”中的指令和 API 来创建[用户和保障关联](iotinsurance_shield_toolkit.html)。
- 安装并连接[样本移动应用程序](iotinsurance_mobile_app.html)。
- 下载或查看所有 [GitHub 站点上的 API](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples)。

# 相关链接
{: #rellinks}

## 教程和样本
{: #samples}
* [GitHub 上的样本移动应用程序代码](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## API 参考
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [{{site.data.keyword.iotinsurance_short}} API 示例](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}


## 相关链接
{: #general}
* [{{site.data.keyword.iot_full}}文档](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [开发人员支持论坛](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [堆栈溢出支持论坛](http://stackoverflow.com/questions/tagged/ibm-bluemix)
