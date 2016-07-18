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

如果想要从新的 iOS 应用程序开始操作，可以使用 HelloWorld 应用程序。此应用程序演示了如何在不认证的情况下，从移动应用程序连接到 {{site.data.keyword.Bluemix}} 后端。该应用程序已经安装有 SDK。准备就绪后，可以获取要在应用程序中使用的特定库。

1. 在 {{site.data.keyword.Bluemix_notm}} 中创建移动后端。
    1. 在 {{site.data.keyword.Bluemix_notm}}“目录”的“样板”部分中，单击 MobileFirst Services Starter。
    2. 输入应用程序的名称和主机，并单击**创建**。
    3. 单击**完成**。
2. 从 GitHub 获取项目。您可以选择使用 git clone 命令获取项目。从您的计算机打开终端，然后输入以下命令：
```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld.git
    ```

3. 初始化项目。要初始化 SDK，请将以下代码复制到应用程序代表中的 `didFinishLaunchingWithOptions` 方法内。

	###Ojbective-C
	{: initializeobjc}

	**重要**：虽然 Objective-C SDK 仍然完全受支持，且仍被视为 {{site.data.keyword.Bluemix}} Mobile Services 的主要 SDK，但是计划本年度稍后停用，将使用新的 Swift SDK 替代。

	Objective-C SDK 会将监视数据报告给 {{site.data.keyword.amashort}} 服务的监视控制台。如果您依赖于 {{site.data.keyword.amashort}} 服务的监视功能，请继续使用 Objective-C SDK。

	```
	// initialize SDK with IBM Bluemix application ID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<insert route>" backendGUID:@"<insertGUID>"];
return YES;
```

	###Swift
	{: initializeswift}
	```
	// initialize SDK with IBM Bluemix application ID and route
IMFClient.sharedInstance().initializeWithBackendRoute("<insert route>", backendGUID: "<insertGUID>")
return true
```

4. 在开发环境中运行样本。在 Xcode 中，单击**产品&gt;运行**。这将启动 iOS 模拟器。

5. 在模拟器中，单击**对 {{site.data.keyword.Bluemix_notm}} 执行 Ping 操作**。样本应用程序会从 Mobile Client Access 服务获取 Authorization 头。如果 ping 操作成功，模拟器中的文本将更新。

  在 Xcode 中从移动应用程序成功连接到 {{site.data.keyword.Bluemix_notm}} 后，将显示以下消息：

  `恭喜！您已建立连接`
  {: screen}

  ![Hello World 应用程序已成功连接到 {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "图 1. Hello World 应用程序已成功连接到 Bluemix")

  如果连接失败，您会看到：`糟糕，出错了`
  {: screen}

  ![Hello World 应用程序未连接到 Bluemix](images/bummer_android.jpg "图 2. Hello World 应用程序未连接到 Bluemix")

	您可以按如下所示对失败的连接进行故障诊断：
	* 验证是否正确地粘贴了路径和 GUID 值。
		####Objective-C
		{: #objcvals}
		```
		[imfClient initializeWithBackendRoute:@"https://hellotest.mybluemix.net"
  backendGUID:@"9d48d73a-0878-4254-test-bdcbe6c79c31"];
  ```

		####Swift
		{: #swiftvals}
		```
		IMFClient.sharedInstance().initializeWithBackendRoute("https://hellotest.mybluemix.net", backendGUID: "9d48d73a-0878-4254-test-bdcbe6c79c31")
  ```

	* 查看调试日志以获取更多信息。


## 后续步骤：
{: #next}
有关如何获取 SDK 并将其集成到移动应用程序中的信息，请参阅有关设置 Bluemix 服务的信息。
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# 相关链接

## 样本
   * [Hello Bluemix 样本](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld)

## sdk
   * [Core SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## api
   * [Core API](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
