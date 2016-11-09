---

copyright:
  years: 2016
lastupdated: "2016-10-18"

---
{:new_window: target="_blank"}

# Mobile 仪表板中的新功能
{: #what_is_new}

上次更新时间：2016 年 10 月 18 日
{: .last-updated}

{{site.data.keyword.Bluemix}} Mobile 仪表板 10 月的更新引进以下更改：

   * 现在，您可以直接从仪表板，向项目添加 Push Notifications 和 Analytics 功能。
   * [代码入门模板](starters.html#Code_Starter)现在可用。
   * 现在支持 Swift。


### Analytics
{: #analytics}

   * 当您添加 Analytics 功能时，默认情况下会启用演示模式。您可以在运行应用程序后关闭演示模式，以查看您的分析。


### UI 构建器
{: #ui_builder}

   * 现在，从项目可以访问 **Push Notifications** 功能。
   * **项目设置**选项卡已重命名为**设置**选项卡。
   * **认证**选项卡已重命名为**用户访问权**选项卡。


### 代码
{: #code}

   * 生成的适用于 iOS 的 Objective-C 和 Swift 代码现在使用 CocoaPods 来管理依赖关系。这表示您需要安装 CocoaPods。要安装它，请运行 `sudo gem install cocoapods`。安装 CocoaPods 之后，请运行 `pod setup` 以对其进行配置（如果尚未配置的话）。最后，运行 `pod install` 以下载并安装所需的项目依赖关系，然后在 Xcode 中打开 `.xcworkspace` 文件。在已下载代码归档的 `README.md` 文件中，可以找到其他详细信息。有关更多信息，请阅读[必备开发者工具](get_code.html#prereq-dev-tools)。

经常回顾以及时了解新更新。


# 相关链接
{: #rellinks}

<!-- links to internal services don't work
## {{site.data.keyword.Bluemix_notm}} Mobile services
{: #general}
* [Mobile Analytics (Beta)](../services/mobileanalytics/index.html){: new_window}
* [Mobile Client Access](../services/mobileaccess/index.html){: new_window}
* [Mobile Foundation](../services/mobilefoundation/index.html){: new_window}
* [Mobile Quality Assurance)](../services/MobileQualityAssurance/index.html){: new_window}
* [Push Notifications](../services/mobilepush/index.html){: new_window}
-->

## 博客帖子
{: #general}
* [博客帖子：Introducing the Bluemix Mobile dashboard](https://developer.ibm.com/bluemix/2016/07/08/new-bluemix-mobile-dashboard/){: new_window}
* [博客帖子：Introducing the next generation of the Bluemix Mobile dashboard](https://ibm.com/blogs/bluemix/2016/10/introducing-the-next-generation-of-the-bluemix-mobile-dashboard/){: new_window}
* [博客帖子：Introducing Bluemix Mobile Code Starters](https://www.ibm.com/blogs/bluemix/2016/10/rapid-dev-with-mobile-code-starters/){: new_window}
* [博客帖子：Bluemix Mobile, Part 1: Creating a Store Catalog application](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [博客帖子：Bluemix Mobile, Part 2: Integrating custom Bluemix backend into the Store Catalog app](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}

## 教程和样本
{: #samples}
* [Mobile Backend for Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
