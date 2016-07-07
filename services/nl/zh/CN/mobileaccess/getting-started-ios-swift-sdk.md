---

copyright:
  years: 2016

---
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# 设置 iOS Swift SDK
{: #getting-started-ios}

*上次更新时间：2016 年 6 月 14 日*
{: .last-updated}

Mobile Client Access 已发行新的 Swift SDK，其为现有 Mobile Client Access Objective-C SDK 提供的功能增添了新功能，同时也改进了现有功能，使得认证应用程序变得更加轻松，并为您的后端资源提供更好地保护。在 iOS Swift 应用程序中安装 {{site.data.keyword.amashort}} SDK，初始化该 SDK，然后对受保护和不受保护的资源发起请求。
{:shortdesc}

**注：**Objective-C SDK 会将监视数据报告给 Mobile Client Access 服务的监视控制台。如果您依赖于 Mobile Client Access 服务的监视功能，那么您需要继续使用 Objective-C SDK。

**注：**虽然 Objective-C SDK 仍受到完全支持，且仍视为 {{site.data.keyword.Bluemix_notm}} Mobile Services 的主 SDK，但是有计划要在今年晚些时候停止使用 Objective-C SDK，以支持此新的 Swift SDK。 






## 开始之前
{: #before-you-begin}
您必须具有：
* 受 {{site.data.keyword.amashort}} 服务保护的 {{site.data.keyword.Bluemix_notm}} 应用程序实例。有关如何创建 {{site.data.keyword.Bluemix_notm}} 后端的更多信息，请参阅[入门](index.html)。
* Xcode 项目。有关如何设置 iOS 开发环境的更多信息，请参阅 [Apple Developer Web 站点](https://developer.apple.com/support/xcode/)。


## 安装 {{site.data.keyword.amashort}} 客户端 SDK
{: #install-mca-sdk-ios}
{{site.data.keyword.amashort}} SDK 通过 CocoaPods 进行分发；CocoaPods 是用于 iOS 项目的依赖关系管理器。CocoaPods 会自动从存储库下载工件，并将其提供给 iOS 应用程序。


### 安装 CocoaPods
{: #install-cocoapods}
1. 打开终端并运行 **pod --version** 命令。如果已经安装了 CocoaPods，那么将显示版本号。可以跳至下一部分来安装 SDK。

1. 如果未安装 CocoaPods，请运行：
```
sudo gem install cocoapods
```
有关更多信息，请参阅 [CocoaPods Web 站点](https://cocoapods.org/)。

### 使用 CocoaPods 安装 {{site.data.keyword.amashort}} 客户端 SDK
{: #install-sdk-cocoapods}

1. 在终端窗口中，浏览到 iOS 项目的根目录。

1. 如果尚未针对 CocoaPods 初始化工作空间，请运行 `pod init` 命令。<br/>
 CocoaPods 会创建 `Podfile` 文件，用于为 iOS 项目定义依赖关系。

1. 编辑 `Podfile` 文件，并将以下行添加到所需目标：

	```
  use_frameworks!
  pod 'BMSSecurity'
	```
  **提示：**您可以将 `use_frameworks!` 添加到 Xcode 目标中，而不是置于 Podfile 中。

1. 保存 `Podfile` 文件，然后在命令行中运行 `pod install`。<br/>Cocoapods 会安装相关依赖项，并显示添加的依赖项和 Pods。<br/>
**重要信息**：CocoaPods 会生成 `xcworkspace` 文件。必须打开此文件才能继续处理项目。

1. 打开 iOS 项目工作空间。打开 CocoaPods 生成的 `xcworkspace` 文件。例如：`{your-project-name}.xcworkspace`。运行 `open {your-project-name}.xcworkspace`。

## 初始化 {{site.data.keyword.amashort}} 客户端 SDK
{: #init-mca-sdk-ios}

 通过传递 `applicationRoute` 和 `applicationGUID` 参数来初始化 SDK。通常会将初始化代码放置在应用程序代表的 `application:didFinishLaunchingWithOptions` 方法中，但这不是强制性的。

1. 获取应用程序参数值。在 {{site.data.keyword.Bluemix_notm}}“仪表板”中打开应用程序。单击**移动选项**。**路径**和**应用程序 GUID** 字段中将显示 `applicationRoute` 和 `applicationGUID` 值。

1. 将所需框架导入要使用 {{site.data.keyword.amashort}} 客户端 SDK 的类中。

 ```Swift
 import BMSCore
 import BMSSecurity
 ```  

1. 初始化 {{site.data.keyword.amashort}} 客户端 SDK。将 `<applicationRoute>` 和 `<applicationGUID>` 替换为从 {{site.data.keyword.Bluemix_notm}} 仪表板中的**移动选项**获取的**路径**和**应用程序 GUID** 值。将 `<applicationBluemixRegion>` 替换为托管 {{site.data.keyword.Bluemix_notm}} 应用程序的区域。要查看 {{site.data.keyword.Bluemix_notm}} 区域，请单击仪表板左上角的人脸图标 (![人脸](/face.png "人脸"))。 


 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 // Initialize the client SDK.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<applicationBluemixRegion>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 return true
 }
 ```

## 对移动后端发起请求
{: #request}

初始化 {{site.data.keyword.amashort}} 客户端 SDK 后，可以开始对移动后端发起请求。

1. 尝试在浏览器中对移动后端上的受保护端点发送请求。打开以下 URL：`{applicationRoute}/protected`。例如：`http://my-mobile-backend.mybluemix.net/protected`
<br/>使用 MobileFirst Services Starter 样板创建的移动后端的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护。由于此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问，因此会在浏览器中返回 `Unauthorized` 消息。

1. 使用 iOS 应用程序对同一端点发起请求。初始化 `BMSClient` 后，添加以下代码：

 ```Swift
 let customResourceURL = "<your protected resource's path>"
 let request = Request(url: customResourceURL, method: HttpMethod.GET)
 let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) in
     if error == nil {
         print ("response:\(response?.responseText), no error")
     } else {
         print ("error: \(error)")
     }
 }

 request.sendWithCompletionHandler(callBack)
 ```

1.  请求成功后，将在 Xcode 控制台中看到以下输出：

 ```
 response:Optional("Hello, this is a protected resouce of the mobile backend application!"), no error
 ```
{: screen}
 
## 后续步骤
{: #next-steps}
连接到受保护端点时，无需任何凭证。如果需要用户登录到您的应用程序，那么必须配置 Facebook、Google 或定制认证。
  * [Facebook](facebook-auth-ios-swift-sdk.html)
  * [Google](google-auth-ios-swift-sdk.html)
  * [定制](custom-auth-ios-swift-sdk.html)
