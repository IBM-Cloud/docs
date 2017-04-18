---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-01"

---

{:screen: .screen}
{:shortdesc: .shortdesc}


# 启用 iOS Objective C 应用程序的 Google 认证
{: #google-auth-ios}


使用 Google 登录，在 {{site.data.keyword.amafull}} iOS 应用程序上认证用户。

**注：**虽然 Objective-C SDK 仍受到完全支持，且仍视为 {{site.data.keyword.Bluemix_notm}} Mobile Services 的主 SDK，但是有计划要在今年晚些时候停止使用此 SDK，以支持新的 Swift SDK。有关我们强烈建议使用 Swift SDK 的新应用程序。本页面中的指示信息适用于 {{site.data.keyword.amashort}} 客户端 Objective-C SDK。有关使用 Swift SDK 的指示信息，请参阅[在 iOS 应用程序 (Swift SDK) 中启用 Google 认证](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html)。

## 开始之前
{: #before-you-begin}
您必须具有：
* {{site.data.keyword.amafull}} 服务和 {{site.data.keyword.Bluemix_notm}} 应用程序的实例。有关如何创建 {{site.data.keyword.Bluemix_notm}} 后端应用程序的更多信息，请参阅[入门](index.html)。




* 后端应用程序的 URL（**应用程序路径**）。您将需要此值来向后端应用程序的受保护端点发送请求。
* **TenantID** 值。在 {{site.data.keyword.amashort}}“仪表板”中打开服务。单击**移动选项**按钮。`tenantId`（也称为 `appGUID`）值会显示在**应用程序 GUID/TenantId** 字段中。您将需要此值来初始化授权管理器。

## 针对 iOS 平台配置 Google 项目
{: #google-auth-ios-project}
要开始将 Google 用作身份提供者，请在 Google 开发者控制台中创建项目以获取 Google 客户端标识。此客户端标识是供 Google 用于确定哪个应用程序正在尝试进行连接的唯一标识。   

1. 如果尚未创建 Google iOS 项目，请在 [Google 开发者控制台](https://console.developers.google.com)站点上按照以下步骤执行操作。

1. 从**社交 API** 列表中，选择 **Google+ API**，然后单击**启用**。

1. 从**凭证**列表中，单击**创建凭证**按钮，然后选择 **OAuth 客户端标识**。

1. 此时，将向您显示应用程序类型选项。请选择 **iOS**。

1. 为 iOS 客户端提供有意义的名称。指定 iOS 应用程序的捆绑软件标识。要找到 iOS 应用程序的捆绑软件标识，请在 `info.plist` 文件或 Xcode 项目的**常规**选项卡中查找**捆绑软件标识**。

1. 记录新的 Google iOS 客户端标识。在 {{site.data.keyword.Bluemix}} 中设置应用程序时需要此值。




## 配置 {{site.data.keyword.amashort}} 进行 Google 认证
{: #google-auth-ios-config}

现在，您已经有 Google iOS 客户端标识，可以在 {{site.data.keyword.Bluemix_notm}}“仪表板”中启用 Google 认证。

1. 在 {{site.data.keyword.amashort}}“仪表板”中打开服务。
1. 在**管理**选项卡中，将**授权**切换为“开启”。
1. 展开 **Google** 部分。
1. 在 **iOS 的应用程序标识**中，指定 iOS 的 Google 客户端标识。
1. 单击**保存**。


## 针对 iOS 配置 {{site.data.keyword.amashort}} Google 客户端 SDK
{: #google-auth-ios-sdk}

### 使用 CocoaPods 安装 {{site.data.keyword.amashort}} 客户端 SDK
{: #google-auth-ios-sdk-cocoapods}

1. 浏览到您的 iOS 项目。

1. 编辑 `Podfile` 以添加以下行：

	```
	pod 'IMFGoogleAuthentication'
	```
{: codeblock}

1. 保存 `Podfile`，然后在命令行中运行 `pod install`。CocoaPods 会安装依赖关系。您将看到进度和添加的组件。

  **重要信息**：您现在必须使用 CocoaPods 生成的 `xcworkspace` 文件来打开项目。通常该文件的名称为 `{your-project-name}.xcworkspace`。  

1. 在命令行中运行 `open {your-project-name}.xcworkspace` 以打开 iOS 项目工作空间。

### 配置 iOS 项目进行 Google 认证
{: #google-auth-ios-googleauth}
更新 `info.plist` 文件来配置 Google 集成。`info.plist` 文件通常位于 Xcode 项目的 `Supporting files` 文件夹中。您可以在属性列表编辑器或在文本编辑器中编辑该文件。

* 通过将以下 URL 方案添加到 `info.plist` 文件来配置 Google 集成。
 ![info.plist 文件](images/ios-google-infoplist-settings.png)

	第一个 URL 方案是从 Google 开发者控制台获得的反序客户端标识版本。例如，如果客户端标识为 `123123-abcabc.apps.googleusercontent.com`，那么 URL 方案为：`com.googleusercontent.apps.123123-abcabc`。

	第二个 URL 方案是应用程序的捆绑软件标识。

* 使用文本编辑器。右键单击 `info.plist`，然后选择**打开方式 > 源代码
**。将以下 XML 添加到文件中：

	```XML
	<key>CFBundleURLTypes</key>
	<array>
		<dict>
			<key>CFBundleTypeRole</key>
			<string>Editor</string>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>com.googleusercontent.apps.123123-abcabc</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeRole</key>
			<string>Editor</string>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>com.ibm.HelloWorld</string>
			</array>
		</dict>
	</array>

	```
{: codeblock}

	更新这两个 URL 方案。

	**重要信息**：请不要覆盖 `info.plist` 文件中的任何现有属性。如果您有重叠属性，那么需要手动合并属性。有关更多信息，请参阅[尝试针对 iOS 执行登录](https://developers.google.com/identity/sign-in/ios/start)。


## 初始化 {{site.data.keyword.amashort}} 客户端 SDK
{: #google-auth-ios-initialize}

要使用 {{site.data.keyword.amashort}} 客户端 SDK，请通过传递 TenantID 和“应用程序路径”参数来对其进行初始化。

通常会将初始化代码放置在应用程序代表的 `application:didFinishLaunchingWithOptions` 方法中，但这不是强制性的。

1. 将所需框架导入要使用 {{site.data.keyword.amashort}} 客户端 SDK 的类中。添加以下头：

	#### Objective-C：

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```
{: codeblock}

	#### Swift：

	{{site.data.keyword.amashort}} 客户端 SDK 将通过 Objective-C 实现。您可能需要将桥接头添加到 Swift 项目才能使用 SDK。

	1. 在 Xcode 中右键单击项目，并选择**新建文件...**。

	2. 在 **iOS 源**类别中，选取**头文件**。

	3. 将其命名为 `BridgingHeader.h`。

	4. 将以下 import 添加到桥接头：
		
	   `#import <IMFCore/IMFCore.h>`
		
	   `#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>`
	
	5. 在 Xcode 中单击项目，然后选择**构建设置**选项卡。

	6. 搜索 `Objective-C Bridging Header`。

	7. 将值设置为您的 `BridgingHeader.h` 文件的位置，例如：`$(SRCROOT)/MyApp/BridgingHeader.h`。

	8. 通过构建项目来确保 Xcode 选取了您的桥接头。

3. 使用以下代码来初始化客户端 SDK。将 `<applicationRoute>` 和 `<TenantID>` 替换为您的**路径**和 **TenantID**。

	#### Objective-C：

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"<applicationRoute>"
			backendGUID:@"<TenantID>"];
	```
{: codeblock}

	#### Swift：

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("<applicationRoute>",
	 							backendGUID: "<TenantID>")
	```
{: codeblock}

1. 通过传递 {{site.data.keyword.amashort}} 服务 `tenantId` 参数来初始化 `AuthorizationManager`。 
  ####Objective-C
	
  ```Objective-C
     [[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"tenantId"];
  ```
 {: codeblock}

  ####Swift

  ```Swift
  IMFAuthorizationManager.sharedInstance().initializeWithTenantId("tenantId")
 ```
 {: codeblock}

1. 通过将以下代码添加到应用程序代表中的 `application:didFinishLaunchingWithOptions` 方法，注册 Google 认证处理程序。初始化 IMFClient 后，立即添加以下代码：

	#### Objective-C：

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```
{: codeblock}

	#### Swift：

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```
{: codeblock}

1. 将以下代码添加到应用程序代表中。

	#### Objective-C：

	```Objective-C
	- (void)applicationDidBecomeActive:(UIApplication *)application {
		[[IMFGoogleAuthenticationHandler sharedInstance] handleDidBecomeActive];
	}

- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url
					sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {

		BOOL shouldHandleGoogleURL = [GPPURLHandler handleURL:url
					sourceApplication:sourceApplication annotation:annotation];

[[IMFGoogleAuthenticationHandler sharedInstance] handleOpenURL:shouldHandleGoogleURL];
		return  shouldHandleGoogleURL;
	}
	```
{: codeblock}

	#### Swift：

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		let shouldHandleGoogleURL = GPPURLHandler.handleURL(url,
				sourceApplication: sourceApplication, annotation: annotation)

IMFGoogleAuthenticationHandler.sharedInstance()
							.handleOpenURL(shouldHandleGoogleURL)

return shouldHandleGoogleURL;
	}
```
{: codeblock}

## 测试认证
{: #google-auth-ios-testing}
初始化客户端 SDK 后，可以开始对移动后端发起请求。

### 开始之前
{: #google-auth-ios-testing-before}
您必须使用的是 {{site.data.keyword.mobilefirstbp}} 样板，并且已经在 `/protected` 端点具有受 {{site.data.keyword.amashort}} 保护的资源。如果需要设置 `/protected` 端点，请参阅[保护资源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。


1. 尝试通过在桌面浏览器中打开 `{applicationRoute}/protected`（例如，`http://my-mobile-backend.mybluemix.net/protected`），向移动后端的受保护端点发送请求。

1. 使用 MobileFirst Services 样板创建的移动后端的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护，所以它只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问。因此，您会在桌面浏览器中看到 `Unauthorized`。

1. 使用 iOS 应用程序对同一端点发起请求。

	#### Objective-C：

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
{: codeblock}

	#### Swift：

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
{: codeblock}

1. 运行应用程序。您将看到 Google 登录屏幕弹出窗口

	![图像](images/ios-google-login.png)

	如果设备上未安装 Facebook 应用程序，或者如果您当前未登录到 Facebook，那么此屏幕的外观可能略有不同。

1. 通过单击**确定**，您将授权 {{site.data.keyword.amashort}} 使用您的 Google 用户身份进行认证。

1. 	您的请求应该会成功。您应该会在 LogCat 中看到以下输出

	![图像](images/ios-google-login-success.png)
		
	通过添加以下代码，您还可以添加注销功能：

	#### Objective C：

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] logout : callBack]
	```
{: codeblock}

	#### Swift：

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().logout(callBack)
	```
{: codeblock}

	如果您在用户登录 Google 之后调用此代码，并且用户尝试重新登录，那么系统将提示他们授权 {{site.data.keyword.amashort}} 使用 Google 进行认证。此时，用户可以单击<!--in the upper-right corner of the screen-->用户名，以选择其他用户并登录。

	您可以选择是否将 `callBack` 传递给注销功能。您还可以传递 `nil`。
