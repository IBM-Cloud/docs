---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Hello Bluemix for iOS 样本入门
{: #gettingstarted-android}
*上次更新时间：2016 年 6 月 1 日*
{: .last-updated}  

如果想要从新的 iOS 应用程序开始操作，可以使用 Hello Bluemix 应用程序。此应用程序演示了如何在不认证的情况下，从移动应用程序连接到 {{site.data.keyword.Bluemix}} 后端。准备就绪后，可以获取要在应用程序中使用的特定库。

1. 在 {{site.data.keyword.Bluemix_notm}} 中创建移动后端。
    1. 在 {{site.data.keyword.Bluemix_notm}}“目录”的“样板”部分中，单击 MobileFirst Services Starter。
    2. 输入应用程序的名称和主机，并单击**创建**。
    3. 单击**完成**。
2. 运行 Hello Bluemix 样本应用程序：
	1. 从 GitHub 获取项目。您可以选择使用 git clone 命令获取项目。从您的计算机打开终端，然后输入以下命令：
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellobluemix.git
    ```
	2. 从克隆了项目的 `bms-samples-swift-hellobluemix` 目录运行 `pod install` 命令。如果没有安装 Cocoapods，请从 [https://cocoapods.org](https://cocoapods.org) 获取 CocoaPods。
	3. 使用 `open HelloBluemix.xcworkspace` 命令打开 Xcode 工作空间。
	4. 在 `AppDelegate.swift` 文件中，将 appRoute 和 appGuid 值更新为从 Bluemix 后端中获取的早先创建的 appRoute 和 appGuid 值。

3. 在开发环境中运行样本。在 Xcode 中，单击**产品&gt;运行**。这将启动 iOS 模拟器。


	**重要信息**：appRoute 必须使用 `https` 协议，而不能使用 `http`，否则可能会因为应用程序传输安全性设置而发生连接失败。您可以在 [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/) 博客帖子中阅读有关这些设置的更多信息。

4. 在模拟器中，单击**对 {{site.data.keyword.Bluemix_notm}} 执行 Ping 操作**。样本应用程序会从 Mobile Client Access 服务获取 Authorization 头。如果 ping 操作成功，模拟器中的文本将更新。

  在 Xcode 中从移动应用程序成功连接到 {{site.data.keyword.Bluemix_notm}} 后，您会看到：`哇！您已建立连接`
  {: screen}

  <!--
  ![Hello World application successfully connected to {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figure 1. Hello World application successfully connected to Bluemix")
-->

  如果连接失败，您会看到：`糟糕，出错了`
  {: screen}

 <!--
  ![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")
  -->

	您可以按如下所示对失败的连接进行故障诊断：
	* 验证是否正确地粘贴了路径和 GUID 值。
	* 查看调试日志以获取更多信息。


## 后续步骤：
{: #next}
有关如何获取 SDK 并将其集成到移动应用程序中的信息，请参阅有关设置 Bluemix 服务的信息。
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# 相关链接

## 样本
   * [Hello Bluemix 样本 (iOS)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellobluemix)

## sdk
   * [Core SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## api
   * [Core API](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
