---

copyright:
  years: 2016

---

# 在 iOS 应用程序 (Swift SDK) 中启用 Facebook 认证
{: #facebook-auth-ios}

要在 iOS 应用程序中将 Facebook 用作身份提供者，请为 Facebook 应用程序添加并配置 iOS 平台。

## 开始之前
{: #facebook-auth-ios-before}

* 您必须具有受 {{site.data.keyword.amashort}} 保护的资源，并且具有安装了 {{site.data.keyword.amashort}} 客户端 SDK 的 iOS 项目。有关更多信息，请参阅 [{{site.data.keyword.amashort}} 入门](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)和[设置 iOS Swift SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html)。  
* 使用 {{site.data.keyword.amashort}} 服务器 SDK 手动保护后端应用程序。有关更多信息，请参阅[保护资源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。
* 创建 Facebook 应用程序标识。有关更多信息，请参阅[从 Facebook 开发者门户网站获取 Facebook 应用程序标识](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)。

## 针对 iOS 平台配置 Facebook 应用程序
{: #facebook-auth-ios-config}

1. 登录到 [Facebook 应用程序仪表板](https://developers.facebook.com/apps/)。

1. 记录应用程序的**应用程序标识**。配置 iOS 项目以进行 Facebook 认证时需要此值。

1. 单击**设置 > 添加平台 > iOS**。

1. 指定 iOS 应用程序的 *bundleId*。要找到 iOS 应用程序的 *bundleId*，请在 `info.plist` 文件或 Xcode 项目的**常规**选项卡中查找**捆绑软件标识**。
**提示**：如果计划使用 URL 方案后缀或单点登录，请考虑启用这些功能。

1. 单击**保存设置**。

## 配置 {{site.data.keyword.amashort}} 进行 Facebook 认证
{: #facebook-auth-ios-configmca}

配置了 Facebook 应用程序标识并将 Facebook 应用程序配置为向 iOS 客户端提供服务后，可以在 {{site.data.keyword.amashort}} 中启用 Facebook 认证。

1. 在 {{site.data.keyword.Bluemix}}“仪表板”中打开应用程序。

1. 单击**移动选项**，然后记录**路径** (*applicationRoute*) 和**应用程序 GUID** (*applicationGUID*)。初始化 SDK 时需要这些值。

1. 单击 {{site.data.keyword.amashort}} 磁贴。这将装入 {{site.data.keyword.amashort}}“仪表板”。

1. 单击 **Facebook** 磁贴。

1. 指定 Facebook 应用程序标识，然后单击**保存**。

## 针对 iOS 配置 {{site.data.keyword.amashort}} 客户端 SDK
{: #facebook-auth-ios-sdk}

### 安装 CocoaPods
{: #facebook-auth-cocoapods}

{{site.data.keyword.amashort}} 客户端 SDK 通过 CocoaPods 进行分发；CocoaPods 是用于 iOS 项目的依赖关系管理器。CocoaPods 会自动从存储库下载工件，并将其提供给 iOS 应用程序。

1. 打开终端并运行 `pod --version` 命令。如果已经安装了 CocoaPods，那么将显示版本号。可以跳至本教程的下一部分。

1. 通过运行 `sudo gem install cocoapods` 来安装 CocoaPods。如果需要其他指导信息，请参阅 [CocoaPods Web 站点](https://cocoapods.org/)。

1. 关闭 XCode。

1. 打开终端并运行 `cd` 进入项目目录。

1.  运行 `pod init`。

### 使用 CocoaPods 安装 {{site.data.keyword.amashort}} 客户端 Swift SDK
{: #facebook-auth-install-swift-cocoapods}

1. 在 iOS 项目中，编辑 `Podfile` 并添加以下行：

 ```
use_frameworks!
pod 'BMSFacebookAuthentication'
	```
 **提示：**您可以将 `use_frameworks!` 添加到 Xcode 目标中，而不是置于 Podfile 中。

1. 保存 `Podfile`，然后在命令行中运行 `pod install` 命令。CocoaPods 会安装依赖关系。这将显示进度和添加的组件。

 **重要信息**：您现在必须使用 CocoaPods 生成的 `xcworkspace` 文件来打开项目。通常该文件的名称为 `{your-project-name}.xcworkspace`。  

1. 在命令行中运行 `open {your-project-name}.xcworkspace` 以打开 iOS 项目工作空间。

### 配置 iOS 项目进行 Facebook 认证
{: #facebook-auth-ios-configproject}

1. 找到 `info.plist` 文件，该文件通常位于 Xcode 项目的 `Supporting files` 文件夹下。

1. 通过将以下属性添加到 `info.plist` 文件来配置 Facebook 集成：

   ![图像](images/ios-facebook-infoplist-settings.png)

   使用 Facebook 应用程序标识来更新 URL 方案和 FacebookappID 属性

   您还可以通过右键单击 `info.plist` 文件，选择**打开方式 > 源代码**，并添加以下 XML 来更新该文件：

   ```XML
	<key>CFBundleURLTypes</key>
	<array>
		<dict>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>fb{your-facebook-application-id}</string>
			</array>
		</dict>
	</array>
	<key>FacebookAppID</key>
	<string>{your-facebook-application-id}</string>
	<key>FacebookDisplayName</key>
	<string>{your-faceebook-application-name}</string>
	<key>LSApplicationQueriesSchemes</key>
	<array>
		<string>fbauth</string>
		<string>fbauth2</string>
	</array>
	<key>NSAppTransportSecurity</key>
	<dict>
	    <key>NSExceptionDomains</key>
	    <dict>
	        <key>facebook.com</key>
	        <dict>
	            <key>NSIncludesSubdomains</key>
	            <true/>                
	            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
	            <false/>
	        </dict>
	        <key>fbcdn.net</key>
	        <dict>
	            <key>NSIncludesSubdomains</key>
	            <true/>
	            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
	            <false/>
	        </dict>
	        <key>akamaihd.net</key>
	        <dict>
	            <key>NSIncludesSubdomains</key>
	            <true/>
	            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
	            <false/>
	        </dict>
	    </dict>
	</dict>
```
   使用 Facebook 应用程序标识更新 URL 方案和 FacebookappID 属性。将 FacebookDisplayName 更新为 Facebook 应用程序的名称。

    **重要信息**：确保您未覆盖 `info.plist` 文件中的任何现有属性。如果您有重叠属性，必须手动进行合并。有关更多信息，请参阅 [Configure Xcode Project](https://developers.facebook.com/docs/ios/getting-started/) 和 [Preparing Your Apps for iOS9](https://developers.facebook.com/docs/ios/ios9)。

## 初始化 {{site.data.keyword.amashort}} 客户端 Swift SDK
{: #facebook-auth-ios-initalize-swift}

通过传递 `applicationGUID` 和 `applicationRoute` 参数来初始化客户端 SDK。

通常会将初始化代码放置在应用程序代表的 `application:didFinishLaunchingWithOptions` 方法中，但这不是强制性的

1. 获取应用程序参数值。在 {{site.data.keyword.Bluemix_notm}}“仪表板”中打开应用程序。单击**移动选项**。**路径**和**应用程序 GUID** 字段中将显示 `applicationRoute` 和 `applicationGUID` 值。

1. 通过添加以下头，将所需框架导入要使用 {{site.data.keyword.amashort}} 客户端 SDK 的类中：

 ```swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```
2. 初始化客户端 SDK。将 `<applicationRoute>` 和 `<applicationGUID>` 替换为从 {{site.data.keyword.Bluemix_notm}} 仪表板中的**移动选项**获取的**路径**和**应用程序 GUID** 值。

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {


 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 FacebookAuthenticationManager.sharedInstance.register()
 ```

1. 通过将以下代码添加到应用程序代表中的 `application:didFinishLaunchingWithOptions` 方法，通知 Facebook SDK 有关应用程序激活的信息，并注册 Facebook 认证处理程序。初始化 BMSClient 实例并将 Facebook 注册为认证管理器后，立即添加以下代码。

 ```Swift
  return FacebookAuthenticationManager.sharedInstance.onFinishLaunching(application, withOptions: launchOptions)
 ```

1. 将 `FacebookAuthenticationManager.swift` 文件从 `BMSFacebookAuthentication` pod 源文件复制到项目目录中。

1. 将以下代码添加到应用程序代表中。

 ```Swift
	func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?,annotation: AnyObject) -> Bool {


		return FacebookAuthenticationManager.sharedInstance.onOpenURL(application, url: url, sourceApplication: sourceApplication, annotation: annotation)

	}
 ```

## 测试认证
{: #facebook-auth-ios-testing}

初始化客户端 SDK 并注册 Facebook 认证管理器后，可以开始对移动后端发起请求。

### 开始之前
{: #facebook-auth-ios-testing-before}

您必须使用的是 {{site.data.keyword.mobilefirstbp}} 样板，并且已经在 `/protected` 端点具有受 {{site.data.keyword.amashort}} 保护的资源。如果需要设置 `/protected` 端点，请参阅[保护资源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。

1. 尝试在浏览器中对新创建的移动后端的受保护端点发送请求。打开以下 URL：`{applicationRoute}/protected`。例如：`http://my-mobile-backend.mybluemix.net/protected`
<br/>使用 MobileFirst Services Starter 样板创建的移动后端的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护。浏览器中将返回 `Unauthorized` 消息。由于此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问，因此会返回此消息。

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

1. 运行应用程序。这将弹出 Facebook 登录屏幕。

   ![图像](images/ios-facebook-login.png)

   如果您当前未登录到 Facebook，那么此屏幕的外观可能略有不同。

1. 单击**确定**以授权 {{site.data.keyword.amashort}} 使用您的 Facebook 用户身份进行认证。

1. 	请求成功后，将在 Xcode 控制台中显示以下输出：

 ```
 "onAuthenticationSuccess info = Optional({
     attributes =     {
     };
     deviceId = 218227041863639;
     displayName = "Don+Lon";
     isUserAuthenticated = 1;
     userId = 218227041863639;
 })
 response:Optional("Hello, this is a protected resouce of the mobile backend application!"), no error
 ```

1. 通过添加以下代码，您还可以添加注销功能：

 ```
FacebookAuthenticationManager.sharedInstance.logout(callBack)
```

 如果您在用户登录 Facebook 之后调用此代码，并且用户尝试重新登录，那么系统将提示他们授予 {{site.data.keyword.amashort}} 权限，以使用 Facebook 进行认证。

 要切换用户，您必须调用此代码，并且用户必须在浏览器中注销 Facebook。

 您可以选择是否将 ```callBack``` 传递给注销功能。您还可以传递 `nil`。
