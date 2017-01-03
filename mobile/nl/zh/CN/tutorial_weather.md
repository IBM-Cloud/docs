---

copyright:
  years: 2016
lastupdated: "2016-10-21"

---
{:new_window: target="_blank"}

# 教程 - Weather Code Starter
{: #tutorial_weather}

{{site.data.keyword.Bluemix}} Mobile Code Starter for Weather 显示某个 Scaffold 项目，以利用 Swift 开始使用 Weather，并包括 Push 和 Analytics 集成点。


## 需求
{: #tutorial_requirements}

* [Bluemix](http://bluemix.net) 帐户
* 从 [Bluemix 目录](https://console.{DomainName}/catalog/)获得的 [Weather Company Data](https://console.{DomainName}/catalog/services/weather-company-data/) 服务实例


## 入门
{: #tutorial_gs}

要快速入门和熟悉运用 Weather Code Starter，请遵循以下步骤：

1. 在 {{site.data.keyword.Bluemix_notm}} 中创建 Mobile 仪表板项目。

   1. 从 Mobile 仪表板的**入门**页面中，单击**创建项目**。

      或者，您可以从**项目**页面单击**新建项目**。

   2. 单击**代码入门模板**。

   3. 选择 **Weather** 并单击**创建项目**。

   4. 输入项目名称并单击**创建**。

2. 可选：添加 Push Notifications 功能。

   1. 在**项目概述**页面上，针对 **Push Notifications** 单击**添加**。

      或者，您可以在 **Push Notifications** 页面上单击**创建**。

   2. 输入服务名称并单击**创建**。

   3. 对于 iOS，[配置 Apple Push Notification 服务](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}。

   4. 对于 Android，[配置 Google Cloud Messaging](/docs/services/mobilepush/t_push_provider_android.html){: new_window}。
   
3. 可选：添加 Analytics 功能。

   1. 在**项目概述**页面上，针对 **Analytics** 单击**添加**。

      或者，您可以在 **Analytics** 页面上单击**创建**。

   2. 输入服务名称并单击**创建**。
   
   3. 您可以在运行应用程序后关闭**演示模式**，以查看您的分析数据。

4. 可选：添加 Authentication 功能。

   1. 在**项目概述**页面上，针对 **Authentication** 单击**添加**。

      或者，您可以在 **Authentication** 页面上选择**创建**。

   2. 输入服务名称并单击**创建**。
   
   3. 打开 **Authentication**。
   
   4. 选择身份提供者，并输入必需的信息以对其进行配置。只能启用一个身份提供者。

   5. 请参阅 [Mobile Client Access 入门](/docs/services/mobileaccess/index.html){: new_window}，以获取有关配置 Authentication 的更多信息。

5. 下载项目。

   1. 单击**代码**并选择首选语言。

   2. 单击**下载代码**。

5. 解压缩归档文件并遵循 `README.md` 文件中的指示信息。


## 接下来执行的操作
{: #tutorial_next}

[立即试用！](http://console.{DomainName}/mobile/create-project?starter=fad1d49e-f7b6-3aff-9b53-14673fca4399){: new_window}
