---

copyright:
  years: 2016

---

# 设置 iOS Swift SDK
{: #getting-started-ios}

在 iOS 应用程序中安装 {{site.data.keyword.amashort}} SDK，初始化该 SDK，然后对受保护和不受保护的资源发起请求。

## 开始之前
{: #before-you-begin}
* 必须具有受 {{site.data.keyword.amashort}} 服务保护的移动后端的实例。有关如何创建移动后端的更多信息，请参阅[入门](getting-started.html)。
* 确保正确设置 Xcode。有关如何设置 iOS 开发环境的更多信息，请参阅 [Apple Developer Web 站点](https://developer.apple.com/support/xcode/)。


## 安装 {{site.data.keyword.amashort}} 客户端 SDK
{: #install-mca-sdk-ios}
{{site.data.keyword.amashort}} SDK 通过 CocoaPods 进行分发；CocoaPods 是用于 iOS 项目的依赖关系管理器。CocoaPods 会自动从存储库下载工件，并将其提供给 iOS 应用程序。


### 安装 CocoaPods
{: #install-cocoapods}
1. 打开终端并运行 **pod --version** 命令。如果已经安装了 CocoaPods，那么将显示版本号。可以跳至下一部分来安装 SDK。

1. 如果未安装 CocoaPods，请运行：
```
sudo gem install cocoapods```
有关更多信息，请参阅 [CocoaPods Web 站点](https://cocoapods.org/)。

### 使用 CocoaPods 安装 {{site.data.keyword.amashort}} 客户端 SDK
{: #install-sdk-cocoapods}

1. 在终端中，浏览到 iOS 项目的根目录。

1. 如果尚未针对 CocoaPods 初始化工作空间，请运行 `pod init` 命令。<br/>
 CocoaPods 会创建 `Podfile` 文件，用于为 iOS 项目定义依赖关系。

1. 编辑 `Podfile` 文件，并将以下行添加到所需目标：

	```
  use_frameworks!
	pod 'BMSSecurity'
	```
  **提示：**您可以将 `use_frameworks!` 添加到 Xcode 目标中，而不是置于 Podfile 中。

1. 保存 `Podfile` 文件，然后在命令行中运行 `pod install`。<br/>Cocoapods 将安装添加的依赖关系。您可以看到进度和添加的组件。<br/>
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

1. 初始化 {{site.data.keyword.amashort}} 客户端 SDK。将 `<applicationRoute>` 和 `<applicationGUID>` 替换为从 {{site.data.keyword.Bluemix_notm}} 仪表板中的**移动选项**获取的**路径**和**应用程序 GUID** 值。

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {


 // Initialize the Client SDK.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<application Bluemix region>)

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
 let callBack:MfpCompletionHandler = {(response: Response?, error: NSError?) in
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

## 后续步骤
{: #next-steps}
连接到受保护端点时，无需任何凭证。如果需要用户登录到您的应用程序，那么必须配置 Facebook、Google 或定制认证。
  * [Facebook](facebook-auth-ios-swift-sdk.html)
  * [Google](google-auth-ios-swift-sdk.html)
  * [定制](custom-auth-ios-swift-sdk.html)
