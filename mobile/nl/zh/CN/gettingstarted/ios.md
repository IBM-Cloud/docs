<!-- Attribute definitions -->
{:codeblock: .codeblock}
{:screen: .screen}

# HelloWorld 样本入门
{: #gettingstarted-ios}
*上次更新时间：2016 年 1 月 28 日*
如果想要从新的 iOS 应用程序开始操作，可以使用 HelloWorld 应用程序。此应用程序演示了如何在不认证的情况下，从移动应用程序连接到 {{site.data.keyword.Bluemix}} 后端。该应用程序已经安装有 SDK。准备就绪后，可以获取要在应用程序中使用的特定库。

1. 在 {{site.data.keyword.Bluemix_notm}} 中创建移动后端。
<ol>
	<li>在 {{site.data.keyword.Bluemix_notm}}“目录”的“样板”部分中，单击 **MobileFirst Services Starter**。</li>
    <li>输入应用程序的名称和主机，并单击**创建**。</li>
    <li>单击**完成**。</li>
</ol>
2. 从 GitHub 获取项目。从计算机，打开终端并输入以下命令：
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld
```

3. 初始化项目。要初始化 SDK，请将以下代码复制到应用程序代表中的 `didFinishLaunchingWithOptions` 方法内。
   * Objective-C：
```
// initialize SDK with IBM Bluemix application ID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<insert route>" backendGUID:@"<insertGUID>"];
return YES;
```{: codeblock}
   * Swift：
```
// initialize SDK with IBM Bluemix application ID and route
IMFClient.sharedInstance().initializeWithBackendRoute("<insert route>", backendGUID: "<insertGUID>")
return true
```{: codeblock}

4. 在开发环境中运行样本。在 Xcode 中，单击**产品&gt;运行**。这将启动 iOS 模拟器。
在模拟器中，单击**对 {{site.data.keyword.Bluemix_notm}} 执行 Ping 操作**。样本应用程序会从 Mobile Client Access 服务获取 Authorization 头。如果 ping 操作成功，模拟器中的文本将更新。
<br/>在 Xcode 中从移动应用程序成功连接到 {{site.data.keyword.Bluemix_notm}} 后，将显示消息“Yay! You are connected”：<br/>
![Hello World 应用程序已成功连接到 {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "图 1. Hello World 应用程序已成功连接到 {{site.data.keyword.Bluemix_notm}}")
<br/>
如果连接成功，调试登录 Xcode 会包含以下消息：
`您已成功连接到 {{site.data.keyword.Bluemix_notm}}`
5. 解决任何问题。连接失败时，将显示消息“Bummer Something went wrong”。此外，还会提供有关该错误的更多信息。<br/>
![Hello World 应用程序未连接到 {{site.data.keyword.Bluemix_notm}}](images/bummer_android.jpg "图 2. Hello World 应用程序未连接到 Bluemix")
<br/>请验证是否正确地粘贴了路径和 GUID 值：
   * Objective-C：
  ```
  [imfClient initializeWithBackendRoute:@"https://hellotest.mybluemix.net"
  backendGUID:@"9d48d73a-0878-4254-test-bdcbe6c79c31"];
  ``` {: codeblock}
   * Swift：
  ```
  IMFClient.sharedInstance().initializeWithBackendRoute("https://hellotest.mybluemix.net", backendGUID: "9d48d73a-0878-4254-test-bdcbe6c79c31")
  ```{: codeblock}


您还可以检查调试日志以获取更多信息。

## 后续步骤：
{: #next}
有关如何获取 SDK 并将其集成到移动应用程序中的信息，请参阅有关设置 {{site.data.keyword.Bluemix}} 服务的信息。
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# 相关链接

## 样本
   * [HelloWorld 样本](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld)

## sdk
   * [Core SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-ios-core)

## api
*
[Core API](https://classicdocs.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)
