---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

{{site.data.keyword.amafull}} 服务已替换为 {{site.data.keyword.appid_full}} 服务。

# 设置 iOS Swift SDK
{: #getting-started-ios}

在 iOS Swift 应用程序中安装 {{site.data.keyword.amashort}} SDK，初始化该 SDK，然后对受保护和不受保护的资源发起请求。


{:shortdesc}


## 开始之前
{: #before-you-begin}
您必须具有：

* {{site.data.keyword.Bluemix_notm}} 应用程序的实例。
* {{site.data.keyword.amafull}} 服务的实例。
* **TenantID**。在 {{site.data.keyword.amashort}}“仪表板”中打开服务。单击**移动选项**。`tenantId`（也称为 `appGUID`）值会显示在**应用程序 GUID/TenantId** 字段中。您将需要此值来初始化 {{site.data.keyword.amashort}} 授权管理器。
* **应用程序路径**。这是后端应用程序的 URL。您将需要此值来向其受保护端点发送请求。
* {{site.data.keyword.Bluemix_notm}} **区域**。您可以在**头像**图标 ![“头像”图标](images/face.jpg "“头像”图标") 旁边的头中找到当前 {{site.data.keyword.Bluemix_notm}} 区域。显示的区域值应为以下某个值：`US South`、`United Kingdom` 或 `Sydney`，并对应于代码中需要的 SDK 值：`BMSClient.Region.usSouth`、`BMSClient.Region.unitedKingdom` 或 `BMSClient.Region.sydney`。您将需要此值来初始化 {{site.data.keyword.amashort}} SDK。
* Xcode 项目。有关如何设置 iOS 开发环境的更多信息，请参阅 [Apple Developer Web 站点 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.apple.com/support/xcode/){: new_window}。


## 安装 {{site.data.keyword.amashort}} 客户端 SDK
{: #install-mca-sdk-ios}
{{site.data.keyword.amashort}} SDK 通过 CocoaPods 进行分发；CocoaPods 是用于 iOS 项目的依赖关系管理器。CocoaPods 会自动从存储库下载工件，并将其提供给 iOS 应用程序。


### 安装 CocoaPods
{: #install-cocoapods}

1. 在终端窗口中，运行 **pod --version** 命令。如果已经安装了 CocoaPods，那么将显示版本号，且您可以跳到下一个部分来安装 SDK。

1. 如果未安装 CocoaPods，请运行：

```
sudo gem install cocoapods
```
{: codeblock}

有关更多信息，请参阅 [CocoaPods Web 站点 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cocoapods.org/){: new_window}。

### 使用 CocoaPods 安装 {{site.data.keyword.amashort}} 客户端 SDK
{: #install-sdk-cocoapods}

1. 在终端窗口中，浏览到 iOS 项目的根目录。

1. 如果尚未针对 CocoaPods 初始化工作空间，请运行 `pod init` 命令。<br/>
 CocoaPods 会为您创建 `Podfile` 文件，可在此文件中定义 iOS 项目的依赖关系。

1. 编辑 `Podfile` 文件，并将以下行添加到所需目标：

	```
use_frameworks!
 pod 'BMSSecurity'
	```
	{: codeblock}

  **提示：**您可以将 `use_frameworks!` 添加到 Xcode 目标中，而不是置于 Podfile 中。

1. 保存 `Podfile` 文件，然后在命令行中运行 `pod install`。CocoaPods 会安装相关依赖项，并显示添加的依赖项和 Pods。<br/>

   **重要信息**：CocoaPods 会生成 `xcworkspace` 文件。必须打开此文件才能继续处理项目。

1. 打开 iOS 项目工作空间。打开 CocoaPods 生成的 `xcworkspace` 文件。例如，对于 `{your-project-name}.xcworkspace`，请运行：

	`open {your-project-name}.xcworkspace`

### 启用 iOS 的密钥链共享
{: #enable_keychain}

启用`密钥链共享`。转至`功能`选项卡，然后在 Xcode 项目中将`密钥链共享`切换为`开启`。

## 初始化 {{site.data.keyword.amashort}} 客户端 SDK
{: #init-mca-sdk-ios}

 通过传递 `tenantId` 参数来初始化 SDK。通常会将初始化代码放置在应用程序代表的 `application:didFinishLaunchingWithOptions` 方法中，但这不是强制性的。

1. 将所需框架导入要使用 {{site.data.keyword.amashort}} 客户端 SDK 的类中。

 ```Swift
 import BMSCore
 import BMSSecurity
 ```

1. 初始化 {{site.data.keyword.amashort}} 客户端 SDK。

 ```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

	func application(_ application: UIApplication, 
	    didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
let mcaAuthManager = MCAAuthorizationManager.sharedInstance
    mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
      // possible values for regionName: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, BMSClient.Region.sydney
	BMSClient.sharedInstance.authorizationManager = mcaAuthManager	
	return true
	}
 ```
  {: codeblock}

* 将 `tenantId` 值替换为从**移动选项**获取的值。
* 将 `<applicationBluemixRegion>` 替换为托管 {{site.data.keyword.Bluemix_notm}} 应用程序的区域。

有关这些值的信息，请参阅[开始之前](#before-you-begin)。


## 对移动后端应用程序发起请求
{: #request}

初始化 {{site.data.keyword.amashort}} 客户端 SDK 后，可以开始对移动后端应用程序发起请求。

1. 尝试在浏览器中对移动后端应用程序上的受保护端点发送请求。打开以下 URL：`{applicationRoute}/protected`，将 `{applicationRoute}` 替换为从**移动选项**中检索到的 **applicationRoute** 值（请参阅[初始化 Mobile Client Access 客户端 SDK](#init-mca-sdk-ios)）。例如：


	`http://my-mobile-backend.mybluemix.net/protected
	`

	由于此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问，因此会在浏览器中返回 `Unauthorized` 消息。



1. 使用 iOS 应用程序对同一端点发起请求。初始化 `BMSClient` 后，添加以下代码：

 ```Swift
	let customResourceURL = "<your protected resource absolute path>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
  if error == nil {
      print ("response:\(response?.responseText), no error")
     } else {
         print ("error: \(error)")
  }
  }
	request.send(completionHandler: callBack)
 ```
 {: codeblock}

1.  请求成功后，将在 Xcode 控制台中显示以下输出：

 ```
 response:Optional("Hello, this is a protected resource of the mobile backend application!"), no error
 ```
{: screen}

## 后续步骤
{: #next-steps}
连接到受保护端点时，无需任何凭证。如果需要用户登录到您的应用程序，那么必须配置 Facebook、Google 或定制认证。

  * [Facebook](facebook-auth-ios-swift-sdk.html)
  * [Google](google-auth-ios-swift-sdk.html)
  * [定制](custom-auth-ios-swift-sdk.html)
