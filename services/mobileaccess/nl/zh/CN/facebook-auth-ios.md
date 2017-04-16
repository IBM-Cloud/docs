---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-03"

---
{:shortdesc: .shortdesc}

# 启用 iOS 应用程序 (Objective-C SDK) 的 Facebook 认证
{: #facebook-auth-ios}

要在 {{site.data.keyword.amafull}} iOS 应用程序中将 Facebook 用作身份提供者，请为 Facebook 应用程序添加并配置 iOS 平台。

{:shortdesc}

**注：**虽然 Objective-C SDK 仍受到完全支持，且仍视为 {{site.data.keyword.Bluemix}} Mobile Services 的主 SDK，但是有计划要在今年晚些时候停止使用此 SDK，以支持新的 Swift SDK（请参阅[设置 iOS Swift SDK](facebook-auth-ios-swift-sdk.html)）。

## 开始之前
{: #before-you-begin}

您必须具有：
* 设置为使用 CocoaPods 的 iOS 项目。有关更多信息，请参阅[设置 iOS SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html) 中的**安装 CocoaPods**。
**注：**继续之前，您无需安装核心 {{site.data.keyword.amashort}} 客户端 SDK。
* 受 {{site.data.keyword.amashort}} 服务保护的 {{site.data.keyword.Bluemix_notm}} 应用程序实例。有关如何创建 {{site.data.keyword.Bluemix_notm}} 后端的更多信息，请参阅[入门](index.html)。
* **AppGUID** 值。在 {{site.data.keyword.amashort}}“仪表板”中打开服务。单击**移动选项**按钮。`AppGUID`（也称为 `tenantId`）值会显示在**应用程序 GUID/TenantId** 字段中。您将需要此值来初始化授权管理器。
* Facebook 应用程序和应用程序标识。有关更多信息，请参阅[在 Facebook for Developers Web 站点上创建应用程序](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)。

## 针对 iOS 平台配置 Facebook 应用程序
{: #facebook-auth-ios-config}
在 Facebook for Developers 站点上：

1. 在 [Facebook for Developers](https://developers.facebook.com) 上登录到您的帐户。 

1. 确保 iOS 平台已添加到应用程序。添加或配置 iOS 平台时，需要提供 iOS 应用程序的 **bundleId**。要找到 iOS 应用程序的 **bundleId**，请在 `info.plist` 文件或 Xcode 项目的**常规**选项卡中查找**捆绑软件标识**。

1. 单击**保存设置**。

	**提示**：如果计划使用 URL 方案后缀或单点登录，请考虑启用这些功能。

1. 单击**保存设置**。

## 配置 {{site.data.keyword.amashort}} 进行 Facebook 认证
{: #facebook-auth-ios-configmca}

配置了 Facebook 应用程序标识并将 Facebook 应用程序配置为向 iOS 客户端提供服务后，可以在 {{site.data.keyword.amashort}} 中启用 Facebook 认证。

1. 在 {{site.data.keyword.amashort}}“仪表板”中打开服务。
1. 在**管理**选项卡中，将**授权**切换为“开启”。
	1. 展开 **Facebook** 部分。
	1. 添加 **Facebook 应用程序标识**，然后单击**保存**。

## 针对 iOS 配置 {{site.data.keyword.amashort}} Facebook 客户端 SDK
{: #facebook-auth-ios-sdk}

### 安装 CocoaPods
{: #facebook-auth-cocoapods}

{{site.data.keyword.amashort}} 客户端 SDK 通过 CocoaPods 进行分发；CocoaPods 是用于 iOS 项目的依赖关系管理器。CocoaPods 会自动从存储库下载工件，并将其提供给 iOS 应用程序。

1. 打开终端并运行 `pod --version` 命令。如果已经安装了 CocoaPods，那么将显示版本号。可以跳至本教程的下一部分。

1. 通过运行 `sudo gem install cocoapods` 来安装 CocoaPods。如果需要其他指导信息，请参阅 [CocoaPods Web 站点](https://cocoapods.org/)。

### 使用 CocoaPods 安装 {{site.data.keyword.amashort}} Facebook 客户端 SDK
{: #facebook-auth-install-cocoapods}

1. 在 iOS 项目中，编辑 `Podfile` 中的以下行：

	```
	pod 'IMFFacebookAuthentication'
	```
{: codeblock}

1. 保存 `Podfile`，然后在命令行中运行 `pod install` 命令。CocoaPods 会安装依赖关系。这将显示进度和添加的组件。
**重要信息**：您现在必须使用 CocoaPods 生成的 `xcworkspace` 文件来打开项目。通常该文件的名称为 `{your-project-name}.xcworkspace`。  

1. 在命令行中运行 `open {your-project-name}.xcworkspace` 以打开 iOS 项目工作空间。

### 配置 iOS 项目进行 Facebook 认证
{: #facebook-auth-ios-configproject}

1. 找到 `info.plist` 文件，该文件通常位于 Xcode 项目的 `Supporting files` 文件夹下。

1. 通过将以下属性添加到 `info.plist` 文件来配置 Facebook 集成：

	![图像](images/ios-facebook-infoplist-settings.png)

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
<string>MyApp</string>
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
{: codeblock}

使用 **Facebook 应用程序标识**更新 URL 方案和 `FacebookappID` 属性。

  **重要信息**：确保您未覆盖 `info.plist` 文件中的任何现有属性。如果您有重叠属性，必须手动进行合并。有关更多信息，请参阅 [Configure Xcode Project](https://developers.facebook.com/docs/ios/getting-started/) 和 [Preparing Your Apps for iOS9](https://developers.facebook.com/docs/ios/ios9)。


## 初始化 {{site.data.keyword.amashort}} 客户端 SDK
{: #facebook-auth-ios-initalize}

传递应用程序路径 (`applicationRoute`) 和应用程序 GUID (`applicationGUID`)，以初始化客户端 SDK。



通常会将初始化代码放置在应用程序代表的 `application:didFinishLaunchingWithOptions` 方法中，但这不是强制性的。


1. 通过添加以下头，将所需框架导入要使用 {{site.data.keyword.amashort}} 客户端 SDK 的类中：

	####Objective-C
	{: #framework-objc}

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFFacebookAuthentication/IMFFacebookAuthenticationHandler.h>
	#import <FacebookSDK/FacebookSDK.h>
	```	

	####Swift
	{: #bridgingheader-swift}

	{{site.data.keyword.amashort}} 客户端 SDK 是使用 Objective-C 实现的，因此可能需要向 Swift 项目添加桥接头。

	1. 在 Xcode 中右键单击项目，并选择**新建文件...**
		1. 在 **iOS 源**类别中，选取`头文件`。
		1. 将其命名为 `BridgingHeader.h`。
		1. 将 import 添加到桥接头：

			```Objective-C
			#import <IMFCore/IMFCore.h>
			#import <IMFFacebookAuthentication/IMFFacebookAuthenticationHandler.h>
			#import <FacebookSDK/FacebookSDK.h>
			```

	1. 在 Xcode 中单击项目，然后选择**构建设置**选项卡。
		1. 搜索 **Objective-C Bridging Header**。
		1. 将值设置为您的 `BridgingHeader.h` 文件的位置，例如：`$(SRCROOT)/MyApp/BridgingHeader.h`。
		1. 通过构建项目来确保 Xcode 选取了您的桥接头。您应该不会看到任何失败消息。

2. 初始化客户端 SDK。有关获取 `applicationRoute` 和 `applicationGUID` 的信息，请参阅[开始之前](#before-you-begin)。

	####Objective-C
	{: #approute-objc}

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	####Swift
	{: #approute-swift}

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
                               backendGUID: "applicationGUID")
	```

1. 通过传递 {{site.data.keyword.amashort}} 服务 `tenantId` 参数来初始化 `AuthorizationManager`。请参阅[开始之前](#before-you-begin)。

	####Objective-C
	{: #authman-objc}

	```Objective-C
     [[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"tenantId"];
  ```

	####Swift
	{: #authman-swift}

	```Swift
  IMFAuthorizationManager.sharedInstance().initializeWithTenantId("tenantId")
 ```

1. 通过将以下代码添加到应用程序代表中的 `application:didFinishLaunchingWithOptions` 方法，通知 Facebook SDK 有关应用程序激活的信息，并注册 Facebook 认证处理程序。
初始化 IMFClient 实例后，请添加以下代码。 	

	####Objective-C
	{: #activate-objc}

	```Objective-C
		[FBAppEvents activateApp];
		[[IMFFacebookAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```

	####Swift
	{: #activate-swift}

	```Swift
		FBAppEvents.activateApp()
		IMFFacebookAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```

1. 将以下代码添加到应用程序代表中。

	####Objective-C
	{: #appdelegate-objc}

	```Objective-C
	- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url
			sourceApplication:(NSString *)sourceApplication annotation:(id)annotation {

		return [FBAppCall handleOpenURL:url sourceApplication:sourceApplication];
	}
	```

	####Swift
	{: #appdelegate-swift}

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		return FBAppCall.handleOpenURL(url, sourceApplication: sourceApplication)

	}
```


## 测试认证
{: #facebook-auth-ios-testing}
初始化客户端 SDK 并注册 Facebook 认证管理器后，可以开始对移动后端发起请求。

### 开始之前
{: #facebook-auth-ios-testing-before}
您必须使用的是 {{site.data.keyword.mobilefirstbp}} 样板，并且已经在 `/protected` 端点具有受 {{site.data.keyword.amashort}} 保护的资源。如果需要设置 `/protected` 端点，请参阅[保护资源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。

1. 尝试在浏览器中对新创建的移动后端的受保护端点发送请求。打开以下 URL：`{applicationRoute}/protected`。
例如：`http://my-mobile-backend.mybluemix.net/protected`
<br/>使用 MobileFirst Services Starter 样板创建的移动后端的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护。浏览器中将返回 `Unauthorized` 消息。由于此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问，因此会返回此消息。

1. 使用 iOS 应用程序对同一端点发起请求。

	####Objective-C
	{: #requestpath-objc}

	```Objective-C
	NSString *requestPath = [NSString stringWithFormat:@"%@/protected",
								[[IMFClient sharedInstance] backendRoute]];

	IMFResourceRequest *request =  [IMFResourceRequest requestWithPath:requestPath
																method:@"GET"];

	[request sendWithCompletionHandler:^(IMFResponse *response, NSError *error) {
		if (error){
			NSLog(@"Error :: %@", [error description]);
		} else {
			NSLog(@"Response :: %@", [response responseText]);
			NSLog(@"%@", [[IMFAuthorizationManager sharedInstance] userIdentity]);
		}
	}];
	```

	####Swift
	{: #requestpath-swift}

	```Swift
	let requestPath = IMFClient.sharedInstance().backendRoute + "/protected"

	let request = IMFResourceRequest(path: requestPath, method: "GET");
	request.sendWithCompletionHandler { (response, error) -> Void in
		if (nil != error){
			NSLog("Error :: %@", error.description)
		} else {
			NSLog("Response :: %@", response.responseText)
			NSLog("%@", IMFAuthorizationManager.sharedInstance().userIdentity)
		}
	};
 ```

1. 运行应用程序。这将弹出 Facebook 登录屏幕。

	![图像](images/ios-facebook-login.png)

	如果设备上未安装 Facebook 应用程序，或者如果您当前未登录到 Facebook，那么此屏幕的外观可能略有不同。

1. 单击**确定**以授权 {{site.data.keyword.amashort}} 使用您的 Facebook 用户身份进行认证。

1. 	请求成功后，将在 Xcode 控制台中显示以下输出：
	![图像](images/ios-facebook-login-success.png)

		通过添加以下代码，您还可以添加注销功能：

	####Objective-C
	{: #logout-objc}

	```Objective-C
	[[IMFFacebookAuthenticationHandler sharedInstance] logout : callBack]
	```
{: codeblock}

	####Swift
	{: #logout-swift}

	```Swift
	IMFFacebookAuthenticationHandler.sharedInstance().logout(callBack)
	```
{: codeblock}

	如果您在用户登录 Facebook 之后调用此代码，并且用户尝试重新登录，那么系统将提示他们授权 {{site.data.keyword.amashort}} 使用 Facebook 进行认证。

	要切换用户，您必须调用此代码，并且用户必须在浏览器中注销 Facebook。

  您可以选择是否将 `callBack` 传递给注销功能。您还可以传递 `nil`。
