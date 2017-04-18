---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"

---
{:shortdesc: .shortdesc}

# 设置 iOS Objective-C SDK
{: #getting-started-ios}

在 iOS 应用程序中安装 {{site.data.keyword.amafull}} SDK，初始化该 SDK，然后对受保护和不受保护的资源发起请求。


{:shortdesc}

**重要信息：**虽然 Objective-C SDK 仍受到完全支持，且仍视为 {{site.data.keyword.Bluemix_notm}} Mobile Services 的主 SDK，但是有计划要在今年晚些时候停止使用此 SDK，以支持新的 Swift SDK。有关我们强烈建议使用 Swift SDK 的新应用程序的信息，请参阅[设置 iOS Swift SDK](getting-started-ios-swift-sdk.html)。

## 开始之前
{: #before-you-begin}
您必须具有：
* 受 {{site.data.keyword.amashort}} 服务保护的 {{site.data.keyword.Bluemix_notm}} 应用程序实例。有关如何创建 {{site.data.keyword.Bluemix_notm}} 后端应用程序的更多信息，请参阅[入门](index.html)。
* **TenantID**。在 {{site.data.keyword.amashort}}“仪表板”中打开服务。单击**移动选项**。`tenantId`（也称为 `appGUID`）值会显示在**应用程序 GUID/TenantId** 字段中。您将需要此值来初始化 {{site.data.keyword.amashort}} 授权管理器。
* **应用程序路径**。这是后端应用程序的 URL。您将需要此值来向其受保护端点发送请求。
* Xcode 项目。  


## 安装 {{site.data.keyword.amashort}} 客户端 SDK
{: #install-mca-sdk-ios}
{{site.data.keyword.amashort}} SDK 通过 CocoaPods 进行分发；CocoaPods 是用于 iOS 项目的依赖关系管理器。CocoaPods 会自动从存储库下载工件，并将其提供给 iOS 应用程序。


### 安装 CocoaPods
{: #install-cocoapods}

1. 打开终端并运行 **pod --version** 命令。如果已经安装了 CocoaPods，那么将显示版本号。跳至下一部分来安装 SDK。

1. 如果未安装 CocoaPods，请运行：

```
sudo gem install cocoapods
```

有关更多信息，请参阅 [CocoaPods Web 站点](https://cocoapods.org/)。



### 使用 CocoaPods 安装 {{site.data.keyword.amashort}} 客户端 SDK
{: #install-sdk-cocoapods}

1. 在终端中，浏览到 iOS 项目的根目录。

1. 如果尚未针对 CocoaPods 初始化工作空间，请运行 `pod init` 命令。<br/>
 CocoaPods 会创建 `Podfile` 文件，用于为 iOS 项目定义依赖关系。

1. 编辑 `Podfile` 文件，并将以下行添加到所需目标：


	`pod 'IMFCore'`

1. 保存 `Podfile` 文件，然后在命令行中运行 `pod install`。<br/>Cocoapods 将安装添加的依赖关系并显示添加的组件。<br/>

	**重要信息**：CocoaPods 会生成 `xcworkspace` 文件。必须打开此文件才能继续处理项目。

1. 打开 iOS 项目工作空间。打开 CocoaPods 生成的 `xcworkspace` 文件。例如：`{your-project-name}.xcworkspace`。运行 `open {your-project-name}.xcworkspace`。

## 初始化 {{site.data.keyword.amashort}} 客户端 SDK
{: #init-mca-sdk-ios}

1. 通过添加以下头，将 `IMFCore` 框架导入要使用 {{site.data.keyword.amashort}} 客户端 SDK 的类中：

	####Objective-C
	{: #imfcore-objc}

	```Objective-C
	  #import <IMFCore/IMFCore.h>
	
	```

	####Swift
	{: #sdk-swift}

	{{site.data.keyword.amashort}} 客户端 SDK 将通过 Objective-C 实现。您可能需要将桥接头添加到 Swift 项目：
	1. 在 Xcode 中右键单击项目，并选择**新建文件**。
	1. 在 **iOS 源**类别中，单击**头文件**。将文件命名为 `BridgingHeader.h`。
	1. 将此行添加到桥接头中：`#import <IMFCore/IMFCore.h>`。
	1. 在 Xcode 中单击项目，然后选择**构建设置**选项卡。
	1. 搜索 `Objective-C Bridging Header`。
	1. 将值设置为您的 `BridgingHeader.h` 文件的位置，例如 `$(SRCROOT)/MyApp/BridgingHeader.h`。
	1. 通过构建项目来确保 Xcode 选取了您的桥接头。您应该不会看到任何失败消息。

1. 使用以下代码来初始化 {{site.data.keyword.amashort}} 客户端 SDK。通常会将初始化代码放置在应用程序代表的 `application:didFinishLaunchingWithOptions` 方法中，但这不是强制性的。<br/>
有关获取 `applicationRoute` 和 `applicationGUID` 的信息，请参阅[开始之前](#before-you-begin)。 

	####Objective-C
	{: #sharedinstance-objc}

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	####Swift
	{: #sharedinstance-swift}
	```Swift
 		MFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",backendGUID: "applicationGUID")
	```

## 初始化 AuthorizationManager
通过传递 {{site.data.keyword.amashort}} 服务 `tenantId` 参数来初始化 `AuthorizationManager`。有关获取这些值的信息，请参阅[开始之前](#before-you-begin)。 

####Objective-C

```Objective-C
[[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"<tenantId>"];
```

####Swift

```Swift
IMFAuthorizationManager.sharedInstance().initializeWithTenantId("<tenantId>")
```

	
## 对移动后端应用程序发起请求
{: #request}

初始化 {{site.data.keyword.amashort}} 客户端 SDK 后，可以开始对移动后端应用程序发起请求。

1. 尝试在浏览器中对移动后端应用程序上的受保护端点发送请求。打开以下 URL：`{applicationRoute}/protected`。例如：`http://my-mobile-backend.mybluemix.net/protected`
<br/>使用 MobileFirst Services Starter 样板创建的移动后端应用程序的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护。由于此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问，因此会在浏览器中返回 `Unauthorized` 消息。

1. 使用 iOS 应用程序对同一端点发起请求。初始化 `IMFClient` 后，添加以下代码：

	####Objective-C
	{: #nsstring-objc}

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
		}
	}];
	```

	####Swift
	{: #imfclientrequestpath-swift}

	```Swift
	let requestPath = IMFClient.sharedInstance().backendRoute + "/protected"

	let request = IMFResourceRequest(path: requestPath, method: "GET");
	request.sendWithCompletionHandler { (response, error) -> Void in
		if (nil != error){
			NSLog("Error :: %@", error.description)
		} else {
			NSLog("Response :: %@", response.responseText)
		}
	};

	```

1.  请求成功后，将在 Xcode 控制台中看到以下输出：

	![图像](images/getting-started-ios-success.png)

## 后续步骤
{: #next-steps}
连接到受保护端点时，无需任何凭证。如果需要用户登录到您的应用程序，那么必须配置 Facebook、Google 或定制认证。
  * [Facebook](facebook-auth-ios.html)
  * [Google](google-auth-ios.html)
  * [定制](custom-auth-ios.html)
