---

copyright:
  years: 2016

---
{:new_window: target="_blank"}

# 在移动仪表板中创建移动项目
{: #mobile}
上次更新时间：2016 年 7 月 21 日
{: .last-updated} 

使用 {{site.data.keyword.Bluemix}} Mobile Services，可以在不依赖于 IT 人员参与的情况下，将预构建、受管理且可扩展的云服务合并到您的移动应用程序中。您可以专注于移动应用程序的构建，而不用担心管理后端基础架构的复杂性。

“移动”仪表板提供了对 {{site.data.keyword.Bluemix_notm}} 的完整体验。您可以在该仪表板中轻松创建新的移动项目。通过**项目**视图，可以在一个位置中管理所有项目。**服务**视图显示您现有的移动服务实例。

要查看“移动”仪表板，请单击 {{site.data.keyword.Bluemix_notm}} 主页中的**移动**类别。
<img src="images/mobile_dashboard.jpg" alt="{{site.data.keyword.Bluemix_notm}} 主页">

首先，在“移动”仪表板的**项目**视图中，单击**新建项目**。

## {{site.data.keyword.Bluemix_notm}} Mobile Services 概述。
{: #mobile_services_overview}

下表描述了可用的 {{site.data.keyword.Bluemix_notm}} Mobile Services。您可以使用 {{site.data.keyword.Bluemix_notm}}“目录”中的单个服务，也可以将这些服务集成到您的移动项目中。

<table summary="此表描述了 {{site.data.keyword.Bluemix_notm}} Mobile services，并提供了服务文档的链接">
<caption>表 1. {{site.data.keyword.Bluemix_notm}} Mobile Services</caption>
<th>{{site.data.keyword.Bluemix_notm}} Mobile Services</th>
<th>描述</th>
<tr>
<td> <img src="images/mobile_analytics_icon.png" alt="{{site.data.keyword.mobileanalytics_short}} 图标"><br/>{{site.data.keyword.mobileanalytics_short}}（试验性）</td>
<td valign="top">使用 {{site.data.keyword.mobileanalytics_full}} 服务可度量移动应用程序、移动用户和移动设备的状态、行为与上下文。<br/><br/>
请在 <a href="../services/mobileanalytics/index.html" alt="{{site.data.keyword.mobileanalytics_short}} 文档链接">{{site.data.keyword.mobileanalytics_short}} 文档</a>中阅读有关使用此服务的更多信息。
</td>
</tr>
<tr>
<td><img src="images/catalog_icons-05.png" alt="{{site.data.keyword.amashort}} 服务图标"><br/>{{site.data.keyword.amashort}}</td>
<td valign="top">使用 {{site.data.keyword.amafull}} 服务可向移动应用程序添加安全功能。您可以配置客户机认证和身份提供者，以便用户可以使用自己现有的 Google 或 Facebook 帐户登录到应用程序。<br/><br/>
请在 <a href="../services/mobileaccess/index.html" alt="{{site.data.keyword.amashort}} 文档链接">{{site.data.keyword.amashort}} 文档</a>中阅读有关使用此服务的更多信息。</td>
</tr>
<tr>
<td><img src="images/MFPFoundation_icon.png" alt="{{site.data.keyword.mobilefoundation_short}} 服务图标"><br/> {{site.data.keyword.mobilefoundation_short}}</td>
<td valign="top">使用 {{site.data.keyword.mobilefoundation_long}} 服务可加快设置 {{site.data.keyword.mfp_full}} 环境，在该环境中，可以开发、测试和使用企业移动应用程序。<br/><br/>
请在 <a href="../services/mobilefoundation/index.html" alt="{{site.data.keyword.mobilefoundation_short}} 文档链接">{{site.data.keyword.mobilefoundation_short}} 文档</a>中阅读有关使用此服务的更多信息。</td>
</tr>
<tr>
<td><img src="images/mqa_icon.png" alt="{{site.data.keyword.mqa}} 服务图标"><br/>{{site.data.keyword.mqa}}</td>
<td valign="top">使用 {{site.data.keyword.mqafull}} 服务可发现移动质量服务，并为您的应用程序设置这些服务。您可以查看移动应用程序的高级别质量度量值，以快速了解正在处理的应用程序的问题。这些度量值包括崩溃、错误、用户反馈和用户观点等信息。通过查看应用程序的这些信息，可以确定是否要进一步调查特定问题。<br/><br/>
请在 <a href="../services/MobileQualityAssurance/index.html" alt="{{site.data.keyword.mqa}} 文档链接">{{site.data.keyword.mqa}} 文档</a>中阅读有关使用此服务的更多信息。</td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="Push Notifications 服务图标"><br/>{{site.data.keyword.mobilepushshort}}</td>
<td valign="top">使用 {{site.data.keyword.mobilepushfull}} 服务可发送并管理发给 iOS 和 Android 平台的移动推送通知。此服务会管理您的应用程序用户与其设备和设备平台之间的映射，还会处理将推送通知派送给设备。使用此服务，可以向移动应用程序用户发送广播、单点广播（根据用户标识和设备标识）和基于标记（或基于主题）的推送通知。<br/><br/>
请在 <a href="../services/mobilepush/index.html" alt="{{site.data.keyword.mobilepushshort}} 文档链接">{{site.data.keyword.mobilepushshort}} 文档</a>中阅读有关使用此服务的更多信息。</td>
</table>

## 集成 Mobile Services
{: #services_integration}
您可以将现有的 {{site.data.keyword.Bluemix_notm}} Mobile Services（例如 {{site.data.keyword.mobilepushshort}} 和 {{site.data.keyword.cloudant}}）集成到您的项目中。

#### 集成 {{site.data.keyword.mobilepushshort}}
{: #push_integration}

要集成现有 {{site.data.keyword.mobilepushshort}} 服务，请执行以下步骤：

1. 单击 {{site.data.keyword.mobilepushshort}} 服务实例。
2. 单击**移动选项**，然后复制**路径**和 **AppGuid** 值。

   **注**：您的 {{site.data.keyword.mobilepushshort}} 服务必须绑定到应用程序后，才会显示**移动选项**。

3. 导航回“移动”仪表板的**项目**视图。
4. 单击项目以对其进行编辑。
5. 单击**推送**，然后启用通知。
6. 提供先前复制到**应用程序标识**中的 **AppGuid** 值。
7. 提供先前复制到**应用程序路径 URL** 中的**路径**值。

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


# 相关链接
{: #rellinks}

<!-- links to internal services don't work
## {{site.data.keyword.Bluemix_notm}} Mobile services
{: #general}
* [Mobile Analytics (Experimental)](../services/mobileanalytics/index.html){: new_window}
* [Mobile Client Access](../services/mobileaccess/index.html){: new_window}
* [Mobile Foundation](../services/mobilefoundation/index.html){: new_window}
* [Mobile Quality Assurance)](../services/MobileQualityAssurance/index.html){: new_window}
* [Push Notifications](../services/mobilepush/index.html){: new_window}
-->

## 博客帖子
{: #general}
* [博客帖子：Introducing the Bluemix Mobile dashboard](https://developer.ibm.com/bluemix/2016/07/08/new-bluemix-mobile-dashboard/){: new_window}
* [博客帖子：Bluemix Mobile, Part 1: Creating a Store Catalog application](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [博客帖子：Bluemix Mobile, Part 2: Integrating custom Bluemix backend into the Store Catalog app](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}
 
## 教程和样本
{: #samples}
* [Mobile Backend for Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}

