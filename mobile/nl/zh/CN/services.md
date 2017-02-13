---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-11"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# 服务
{: #services}

从 {{site.data.keyword.Bluemix}} Mobile 仪表板**服务**视图中，您可以查看现有的服务或创建新服务。Mobile 仪表板提供单一位置，用于查看项目所管理的所有 Bluemix 服务。  

如果从**服务**视图删除服务，那么您将从与之相关联的项目断开服务连接。如果您想要将服务重新连接到项目，请创建新服务实例。

## {{site.data.keyword.Bluemix_notm}} Mobile Services 概述。
{: #mobile_services_overview}

下表描述了 {{site.data.keyword.Bluemix_notm}} Mobile Services。您可以使用 {{site.data.keyword.Bluemix_notm}}“目录”中的单个服务，也可以将这些服务集成到您的移动项目中。

<table summary="此表描述了 {{site.data.keyword.Bluemix_notm}} Mobile Services，并提供了服务文档的链接">
<caption>表 1. {{site.data.keyword.Bluemix_notm}} Mobile Services</caption>
<th>{{site.data.keyword.Bluemix_notm}} Mobile Services</th>
<th>描述</th>
<tr>
<td> <img src="images/mobile_analytics_icon.png" alt="{{site.data.keyword.mobileanalytics_short}} 图标"><br/>{{site.data.keyword.mobileanalytics_short}}</td>
<td valign="top">使用 {{site.data.keyword.mobileanalytics_full}} 服务，可深入了解您的移动应用程序的性能如何，以及如何使用它们。<br/><br/>
请阅读 <a href="/docs/services/mobileanalytics/index.html" alt="{{site.data.keyword.mobileanalytics_short}} 文档链接">{{site.data.keyword.mobileanalytics_short}} 文档</a>中有关操作此服务的更多信息。
</td>
</tr>
<tr>
<td><img src="images/authentication_icon
.png" alt="{{site.data.keyword.amashort}} 服务图标"><br/>{{site.data.keyword.amashort}}</td>
<td valign="top">使用 {{site.data.keyword.amafull}} 服务可向移动应用程序添加安全功能。您可以配置客户机认证和身份提供者，以便用户可以使用自己现有的 Google 或 Facebook 帐户登录到应用程序。<br/><br/>
请在 <a href="/docs/services/mobileaccess/index.html" alt="{{site.data.keyword.amashort}} 文档链接">{{site.data.keyword.amashort}} 文档</a>中阅读有关使用此服务的更多信息。</td>
</tr>
<tr>
<td><img src="images/MFPFoundation_icon.png" alt="{{site.data.keyword.mobilefoundation_short}} 服务图标"><br/> {{site.data.keyword.mobilefoundation_short}}</td>
<td valign="top">使用 {{site.data.keyword.mobilefoundation_long}} 服务可加快设置 {{site.data.keyword.mfp_full}} 环境，在该环境中，可以开发、测试和使用企业移动应用程序。<br/><br/>
请在 <a href="/docs/services/mobilefoundation/index.html" alt="{{site.data.keyword.mobilefoundation_short}} 文档链接">{{site.data.keyword.mobilefoundation_short}} 文档</a>中阅读有关使用此服务的更多信息。</td>
</tr>
<tr>
<td><img src="images/mqa_icon.png" alt="{{site.data.keyword.mqa}} 服务图标"><br/>{{site.data.keyword.mqa}}</td>
<td valign="top">使用 {{site.data.keyword.mqafull}} 服务可发现移动质量服务，并为您的应用程序设置这些服务。您可以查看移动应用程序的高级别质量度量值，以快速了解正在处理的应用程序的问题。这些度量值包括崩溃、错误、用户反馈和用户观点等信息。通过查看应用程序的这些信息，可以确定是否要进一步调查特定问题。<br/><br/>
请在 <a href="/docs/services/MobileQualityAssurance/index.html" alt="{{site.data.keyword.mqa}} 文档链接">{{site.data.keyword.mqa}} 文档</a>中阅读有关使用此服务的更多信息。</td>
</tr>
<tr>
<td><img src="images/push_icon.png" alt="{{site.data.keyword.mobilepushshort}} 服务图标"><br/>{{site.data.keyword.mobilepushshort}}</td>
<td valign="top">{{site.data.keyword.mobilepushfull}} 服务提供一个统一平台来发送和管理针对平台的移动和 Web 推送通知。
<br/><br/>
{{site.data.keyword.mobilepushshort}} 会管理您的应用程序用户与其设备、设备平台和浏览器之间的映射，还会处理将推送通知派送给用户。您可以作为推送通知，向移动和Web 浏览器应用程序用户发送广播、单点广播（基于设备标识和用户标识）和标记（或主题）。还可以使用 SDK 和 REST API 来进一步开发您的客户机应用程序。<br/><br/>
在 <a href="/docs/services/mobilepush/index.html" alt="{{site.data.keyword.mobilepushshort}} 文档链接">{{site.data.keyword.mobilepushshort}} 文档链接</a>中阅读有关操作此服务的更多信息。</td>
</table>

## 集成 Mobile Services
{: #services_integration}
您可以将现有的 {{site.data.keyword.Bluemix_notm}} Mobile Services（例如 {{site.data.keyword.cloudant}}）集成到项目中。


#### 集成 {{site.data.keyword.cloudant}}
{: #cloudant_integration}

要集成现有 {{site.data.keyword.cloudant}} 服务，请执行以下步骤：

1. 单击 {{site.data.keyword.cloudant}} 服务实例。
2. 单击**启动**。
3. 在**数据库**视图中，单击“数据库名称”。
4. 单击 **API**，然后复制 **API 密钥**值的内容直至数据库名称（包括该名称）。

   **注**：请勿复制数据库名称之后的内容。

5. 单击**许可权** > **生成 API 密钥**，然后复制**密钥**和**密码**值。
6. 导航回“移动”仪表板的**项目**视图。
7. 单击项目以对其进行编辑。
8. 单击**数据** > **+ 数据源** > **Cloudant**，提供数据源名称，然后单击**添加**。
9. 单击 **Cloudant 配置**。
10. 提供先前复制到 **API URL** 中的 **API 密钥**值。
11. 提供先前复制到**用户**中的**密钥**值。
12. 提供先前复制到**密码**中的**密码**值。
13. 单击**确定**。
