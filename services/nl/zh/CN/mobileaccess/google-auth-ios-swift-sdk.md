---

copyright:
  years: 2016

---

# 在 iOS 应用程序 (Swift SDK) 中启用 Google 认证
{: #google-auth-ios}

## 开始之前
{: #google-auth-ios-before}

* 您必须具有受 {{site.data.keyword.amashort}} 保护的资源，并且具有安装了 {{site.data.keyword.amashort}} 客户端 SDK 的 iOS 项目。有关更多信息，请参阅 [{{site.data.keyword.amashort}} 入门](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)和[设置 iOS Swift SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html)。  
* 使用 {{site.data.keyword.amashort}} 服务器 SDK 手动保护后端应用程序。有关更多信息，请参阅[保护资源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。

## 准备应用程序以登录 Google
{: #google-sign-in-ios}

遵循 Google 在[针对 iOS 的 Goolge 登录](https://developers.google.com/identity/sign-in/ios/start-integrating)中提供的指示信息准备应用程序以登录 Google。以下步骤为您提供了为准备应用程序而必须执行的任务的简要概述。

1. 为应用程序启用针对 iOS 的 Goolge 登录。有关更多信息，请参阅[尝试针对iOS 执行登录](https://developers.google.com/identity/sign-in/ios/start?ver=swift)。

1. 获取项目的配置文件 (`GoogleService-Info.plist`)。要获取该文件，请参阅[为应用程序启用 Google 服务](https://developers.google.com/mobile/add?platform=ios)。

 **重要信息：**获取 `GoogleService-Info.plist` 文件时，请打开该文件，并记录 `CLIENT_ID` 值。您稍后配置 {{site.data.keyword.amashort}} 时需要此值。

1. 将 `GoogleService-Info.plist` 文件添加到 Xcode 项目。有关更多信息，请参阅[将配置文件添加到项目](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config)。

1. 在 Xcode 项目中，使用 `REVERSE_CLIENT_ID` 和捆绑软件标识更新 URL 方案。有关更多信息，请参阅[将 URL 方案添加到项目](https://developers.google.com/identity/sign-in/ios/start-integrating#add_url_schemes_to_your_project)。

1. 使用以下代码更新应用程序的 project-Bridging-Header.h 文件：

 ```
 #import <Google/SignIn.h>
 ```

 有关更新桥接头文件的更多信息，请参阅[启用登录](https://developers.google.com/identity/sign-in/ios/sign-in#enable_sign-in)中的步骤 1。

## 配置 {{site.data.keyword.amashort}} 进行 Google 认证
{: #google-auth-ios-config}

现在，您已经有 iOS 客户端标识，可以在 {{site.data.keyword.Bluemix}}“仪表板”中启用 Google 认证。

1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”中打开应用程序。

1. 单击**移动选项**，然后记录**路径** (*applicationRoute*) 和**应用程序 GUID** (*applicationGUID*)。初始化 SDK 时需要这些值。

1. 单击 {{site.data.keyword.amashort}} 磁贴。这将装入 {{site.data.keyword.amashort}}“仪表板”。

1. 单击 **Google** 磁贴。

1. 在 **iOS 的应用程序标识**中，指定之前从 `GoogleService-Info.plist` 文件获取的 `CLIENT_ID` 值，然后单击**保存**。

## 针对 iOS 配置 {{site.data.keyword.amashort}} 客户端 SDK
{: #google-auth-ios-sdk}

### 安装 CocoaPods
{: #google-auth-cocoapods}

{{site.data.keyword.amashort}} 客户端 SDK 通过 CocoaPods 进行分发；CocoaPods 是用于 iOS 项目的依赖关系管理器。CocoaPods 会自动从存储库下载工件，并将其提供给 iOS 应用程序。

1. 打开终端并运行 `pod --version` 命令。如果已经安装了 CocoaPods，那么将显示版本号。可以跳至本教程的下一部分。

1. 通过运行 `sudo gem install cocoapods` 来安装 CocoaPods。如果需要其他指导信息，请参阅 [CocoaPods Web 站点](https://cocoapods.org/)。

1. 关闭 XCode。

1. 打开终端并运行 `cd` 进入项目目录。

1.  运行 `pod init`。

### 使用 CocoaPods 安装 {{site.data.keyword.amashort}} 客户端 SWift SDK
{: #google-auth-ios-sdk-cocoapods}

1. 浏览到您的 iOS 项目。

1. 编辑 `Podfile` 以添加以下行：

 ```
 use_frameworks!
 pod 'BMSGoogleAuthentication'
 ```
 **提示：**您可以将 `use_frameworks!` 添加到 Xcode 目标中，而不是置于 Podfile 中。

1. 保存 `Podfile`，然后在命令行中运行 `pod install`。CocoaPods 会安装依赖关系。您将看到进度和添加的组件。

 **重要信息**：您现在必须使用 CocoaPods 生成的 `xcworkspace` 文件来打开项目。通常该文件的名称为 `{your-project-name}.xcworkspace`。  

1. 在命令行中运行 `open {your-project-name}.xcworkspace` 以打开 iOS 项目工作空间。

1. 将 `GoogleAuthenticationManager.swift` 文件从 `BMSGoogleAuthentication` pod 源文件复制到项目目录中。

## 初始化 {{site.data.keyword.amashort}} 客户端 Swift SDK
{: #google-auth-ios-initialize}

要使用 {{site.data.keyword.amashort}} 客户端 SDK，请通过传递 `applicationGUID` 和 `applicationRoute` 参数来初始化该 SDK。

通常会将初始化代码放置在应用程序代表的 `application:didFinishLaunchingWithOptions` 方法中，但这不是强制性的。

1. 获取应用程序参数值。在 {{site.data.keyword.Bluemix_notm}}“仪表板”中打开应用程序。单击**移动选项**。**路径**和**应用程序 GUID** 字段中将显示 `applicationRoute` 和 `applicationGUID` 值。

1. 将所需框架导入要使用 {{site.data.keyword.amashort}} 客户端 SDK 的类中。添加以下头：

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```

1. 使用以下代码来初始化客户端 SDK。将 `<applicationRoute>` 和 `<applicationGUID>` 替换为从 {{site.data.keyword.Bluemix_notm}} 仪表板中的**移动选项**获取的**路径**和**应用程序 GUID** 值。

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {


 // Initialize the Client SDK.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUId, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 GoogleAuthenticationManager.sharedInstance.register()
      return true
      }

 // [START openurl]
      func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?,annotation: AnyObject) -> Bool {
return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, sourceApplication: sourceApplication, annotation: annotation)
      }

 @available(iOS 9.0, *)
 func application(app: UIApplication, openURL url: NSURL, options: [String : AnyObject]) -> Bool {
 return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, options: options)
  }
 ```

## 测试认证
{: #google-auth-ios-testing}

初始化客户端 SDK 并注册 Google 认证管理器后，可以开始对移动后端发起请求。

### 开始之前
{: #google-auth-ios-testing-before}

您必须使用的是 {{site.data.keyword.mobilefirstbp}} 样板，并且已经在 `/protected` 端点具有受 {{site.data.keyword.amashort}} 保护的资源。如果需要设置 `/protected` 端点，请参阅[保护资源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。


1. 尝试通过在桌面浏览器中打开 `{applicationRoute}/protected`（例如，`http://my-mobile-backend.mybluemix.net/protected`），向移动后端的受保护端点发送请求。

1. 使用 MobileFirst Services 样板创建的移动后端的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护，所以它只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问。因此，您会在桌面浏览器中看到 `Unauthorized`。

1. 使用 iOS 应用程序对同一端点发起请求。

 ```Swift
 let protectedResourceURL = "<Your protected resource URL>" // any protected resource
 let request = Request(url: protectedResourceURL , method: HttpMethod.GET)
 let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) in
 if error == nil {
    print ("response:\(response?.responseText), no error")
 } else {
    print ("error: \(error)")
 }
 }

 request.sendWithCompletionHandler(callBack)
	```

1. 运行应用程序。您将看到 Google 登录屏幕弹出窗口

 ![图像](images/ios-google-login.png)

1. 登录并单击**确定**后，您将授权 {{site.data.keyword.amashort}} 使用您的 Google 用户身份进行认证。

1. 	您的请求应该会成功。您应该会在日志中看到以下输出。

 ```
 onAuthenticationSuccess info = Optional({attributes = {};
     deviceId = 105747725068605084657;
     displayName = "donlonqwerty@gmail.com";
     isUserAuthenticated = 1;
     userId = 105747725068605084657;
 })
 response:Optional("Hello, this is a protected resource!"), no error
 ```

1. 通过添加以下代码，您还可以添加注销功能：

 ```
 GoogleAuthenticationManager.sharedInstance.logout(callBack)
 ```

  如果您在用户登录 Google 之后调用此代码，并且用户尝试重新登录，那么系统将提示他们授予 {{site.data.keyword.amashort}} 权限，以使用 Google 进行认证。此时，用户可以单击屏幕右上角的用户名，以选择其他用户并登录。

   您可以选择是否将 `callBack` 传递给注销功能。您还可以传递 `nil`。
