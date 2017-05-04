---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

**重要信息：{{site.data.keyword.amafull}} 服务已替换为 {{site.data.keyword.appid_full}} 服务。**

# 启用 iOS 应用程序 (Swift SDK) 的 Google 认证
{: #google-auth-ios}

使用 Google 登录，在 {{site.data.keyword.amafull}} iOS Swift 应用程序上认证用户。


## 开始之前
{: #before-you-begin}

您必须具有：

* {{site.data.keyword.amafull}} 服务和 {{site.data.keyword.Bluemix_notm}} 应用程序的实例。有关如何创建 {{site.data.keyword.Bluemix_notm}} 后端应用程序的更多信息，请参阅[入门](index.html)。
* 后端应用程序的 URL（**应用程序路径**）。您将需要此值来向后端应用程序的受保护端点发送请求。
* **TenantID** 值。在 {{site.data.keyword.amashort}}“仪表板”中打开服务。单击**移动选项**按钮。`tenantId`（也称为 `appGUID`）值会显示在**应用程序 GUID/TenantId** 字段中。您将需要此值来初始化授权管理器。
* {{site.data.keyword.Bluemix_notm}} **区域**。您可以在**头像**图标 ![“头像”图标](images/face.jpg "“头像”图标") 旁边的头中找到当前 {{site.data.keyword.Bluemix_notm}} 区域。显示的区域值应为以下某个值：**美国南部**、**英国**或**悉尼**，并对应于代码中需要的值：`BMSClient.Region.usSouth`、`BMSClient.Region.unitedKingdom` 或 `BMSClient.Region.sydney`。
* Xcode 中的 iOS 项目。它不需要安装 {{site.data.keyword.amashort}} 客户端 SDK。  


## 准备应用程序以进行 Google 登录
{: #google-sign-in-ios}

按照 Google 在[针对 iOS 的 Google 登录 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developers.google.com/identity/sign-in/ios/start-integrating){: new_window} 中提供的指示信息，做好应用程序进行 Google 登录的准备。

此过程会：

* 在 Google 开发者网站上准备新项目，
* 创建 `GoogleService-Info.plist` 文件和 `REVERSE_CLIENT_ID` 值，以添加到 Xcode 项目，以及
* 创建 **Google 客户端标识**，以添加到 {{site.data.keyword.Bluemix_notm}} 后端应用程序。

以下步骤提供了准备应用程序而必须执行的任务的简要概述。

**注：**并非一定要添加 Google Sign-In CocoaPod。`BMSGoogleAuthentication` CocoaPod 会添加必要的 SDK。

1. 记录 Xcode 项目中来自主要目标**常规**选项卡**身份**部分的**捆绑软件标识**。您需要它创建 Google 登录项目。

1. 在 [Google Developer 站点 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developers.google.com/mobile/add?platform=ios){: new_window} 上，为针对 iOS 的 Google 登录创建项目。

1. 向您的项目添加 Google 登录 API。

1. 检索 `GoogleService-Info.plist`。

   **重要信息：**获取 `GoogleService-Info.plist` 文件时，请打开该文件，并记录 `CLIENT_ID` 值。您稍后配置 {{site.data.keyword.amashort}} 后端应用程序时需要此值。

1. 将 `GoogleService-Info.plist` 文件添加到 Xcode 项目。有关更多信息，请参阅[为项目添加配置文件 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config){: new_window}。

1. 在 Xcode 项目中，使用 `REVERSE_CLIENT_ID` 和捆绑软件标识更新 URL 方案。有关更多信息，请参阅[为项目添加 URL 方案 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developers.google.com/identity/sign-in/ios/start-integrating#add_a_url_scheme_to_your_project){: new_window}。

1. 使用以下代码更新应用程序的 `project-Bridging-Header.h` 文件：

	```
	#import <Google/SignIn.h>
	```
	{: codeblock}

	有关更新桥接头文件的更多信息，请参阅[启用登录 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developers.google.com/identity/sign-in/ios/sign-in#enable_sign-in){: new_window}。

## 配置 Mobile Client Access 进行 Google 认证
{: #google-auth-ios-config}

现在，您已经有 iOS 客户端标识，可以在 {{site.data.keyword.amashort}} 服务中启用 Google 认证。

1. 在 {{site.data.keyword.amashort}}“仪表板”中打开服务。
1. 在**管理**选项卡中，将**授权**切换为“开启”。
1. 展开 **Google** 部分。
1. 在 **iOS 的应用程序标识**中，指定从 `GoogleService-Info.plist` 文件获取的 `CLIENT_ID` 值。
1. 单击**保存**。

## 针对 iOS 配置客户端 SDK
{: #google-auth-ios-sdk}

### 安装 CocoaPods
{: #install-cocoapods}

1. 打开终端并运行 **pod --version** 命令。如果已经安装了 CocoaPods，那么将显示版本号。可以跳至下一部分来安装 SDK。

1. 如果未安装 CocoaPods，请运行：

	```
	sudo gem install cocoapods
```
	{: codeblock}

有关更多信息，请参阅 [CocoaPods Web 站点 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cocoapods.org/){: new_window}。

### 使用 CocoaPods 安装 {{site.data.keyword.amashort}} 客户端 Swift SDK
{: #facebook-auth-install-swift-cocoapods}

1. 如果 iOS 项目中没有 `Podfile`，请运行 `pod init`，以创建该文件。

1. 编辑 `Podfile` 并向相关目标添加以下行：

	```
	use_frameworks!
	pod 'BMSGoogleAuthentication'
	```
	{: codeblock}

	**注：**如果已安装 {{site.data.keyword.amashort}} 核心 SDK，那么您可以除去此行：`pod 'BMSSecurity'`。`BMSGoogleAuthentication` Pod 会安装所有必要的框架。

	**提示：**您可以将 `use_frameworks!` 添加到 Xcode 目标中，而不是置于 Podfile 中。

1. 保存 `Podfile`，然后在命令行中运行 `pod install`。CocoaPods 会安装依赖关系。您将看到进度和添加的组件。

	**重要信息**：您现在必须使用 CocoaPods 生成的 `xcworkspace` 文件来打开项目。通常该文件的名称为 `{your-project-name}.xcworkspace`。  

1. 在命令行中运行 `open {your-project-name}.xcworkspace` 以打开 iOS 项目工作空间。

1. 将 `GoogleAuthenticationManager.swift` 文件从 `BMSGoogleAuthentication` pod 源文件复制到项目目录中。

### 启用 iOS 的密钥链共享
{: #enable_keychain}

启用`密钥链共享`。转至`功能`选项卡，然后在 Xcode 项目中将`密钥链共享`切换为`开启`。


## 初始化 {{site.data.keyword.amashort}} 客户端 Swift SDK
{: #google-auth-ios-initialize}

要使用 {{site.data.keyword.amashort}} 客户端 SDK，请通过传递 `tenantID` 参数来初始化该 SDK。

通常会将初始化代码放置在应用程序代表的 `application:didFinishLaunchingWithOptions` 方法中，但这不是强制性的。

1. 将所需框架导入要使用 {{site.data.keyword.amashort}} 客户端 SDK 的类中。添加以下头：

	```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
let mcaAuthManager = MCAAuthorizationManager.sharedInstance
		mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
		//the regionName should be one of the following: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney   
		BMSClient.sharedInstance.authorizationManager = mcaAuthManager
		GoogleAuthenticationManager.sharedInstance.register()
		return true
	}

	// [START openurl]
	    func application(_ application: UIApplication,
			     open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
		return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, sourceApplication: sourceApplication, annotation: annotation)
      }

 @available(iOS 9.0, *)
 func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any]) -> Bool {
		return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, options: options)
  }
 ```
	{: codeblock}

	在代码中：

      * 将 `<serviceTenantID>` 替换为从**移动选项**中检索到的值。
      * 将 `<applicationBluemixRegion>` 替换为 {{site.data.keyword.Bluemix_notm}} **区域**。

	有关获取这些值的更多信息，请参阅[开始之前](#before-you-begin)。


## 测试认证
{: #google-auth-ios-testing}

初始化客户端 SDK 并注册 Google 认证管理器后，可以开始对移动后端应用程序发起请求。

### 开始之前
{: #google-auth-ios-testing-before}

您必须使用的是 {{site.data.keyword.mobilefirstbp}} 样板，并且已经在 `/protected` 端点具有受 {{site.data.keyword.amashort}} 保护的资源。如果需要设置 `/protected` 端点，请参阅[保护资源](protecting-resources.html)。

1. 尝试通过在桌面浏览器中打开 `{applicationRoute}/protected`，向移动后端应用程序的受保护端点发送请求。例如，`http://my-mobile-backend.mybluemix.net/protected`。

1. 使用 MobileFirst Services 样板创建的移动后端应用程序的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护，所以它只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问。因此，您会在桌面浏览器中看到 `Unauthorized`。

1. 使用 iOS 应用程序对同一端点发起请求。

	```Swift
	let protectedResourceURL = "<your protected resource absolute path>"
	let request = Request(url: protectedResourceURL, method: HttpMethod.GET)

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

1. 运行应用程序。您将看到 Google 登录屏幕弹出窗口

 ![图像](images/ios-google-login.png)

1. 登录并单击**确定**后，您将授权 {{site.data.keyword.amashort}} 使用您的 Google 用户身份进行认证。

1. 您的请求应该会成功。日志中会显示以下输出。

	```
	 response:Optional("Hello, this is a protected resource of the mobile backend application!"), no error
 ```
	{: screen}

1. 通过添加以下代码，您还可以添加注销功能：

	```
	GoogleAuthenticationManager.sharedInstance.logout(callBack)
 ```
	{: codeblock}

	如果您在用户登录 Google 之后调用此代码，并且用户尝试重新登录，那么系统将提示他们授权 {{site.data.keyword.amashort}} 使用 Google 进行认证。此时，用户可以单击<!--in the upper-right corner of the screen-->用户名，以选择其他用户并登录。

	您可以选择是否将 `callBack` 传递给注销功能。您还可以传递 `nil`。
