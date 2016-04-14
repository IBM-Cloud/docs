---

copyright:
  years: 2015, 2016

---

# 设置 iOS Objective-C SDK
{: #getting-started-ios}

在 iOS 应用程序中安装 {{site.data.keyword.amashort}} SDK，初始化该 SDK，然后对受保护和不受保护的资源发起请求。

**提示：**如果要使用 Swift 开发 iOS 应用程序，请考虑使用 {{site.data.keyword.amashort}} 客户端 Swift SDK。有关详细信息，请参阅[设置 iOS Swift SDK](getting-started-ios-swift-sdk.html)

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
	pod 'IMFCore'
	```

1. 保存 `Podfile` 文件，然后在命令行中运行 `pod install`。<br/>Cocoapods 将安装添加的依赖关系。您可以看到进度和添加的组件。<br/>
**重要信息**：CocoaPods 会生成 `xcworkspace` 文件。必须打开此文件才能继续处理项目。

1. 打开 iOS 项目工作空间。打开 CocoaPods 生成的 `xcworkspace` 文件。例如：`{your-project-name}.xcworkspace`。运行 `open {your-project-name}.xcworkspace`。

## 初始化 {{site.data.keyword.amashort}} 客户端 SDK
{: #init-mca-sdk-ios}

要使用 {{site.data.keyword.amashort}} 客户端 SDK，您必须通过传递**路径** (`applicationRoute`) 和**应用程序 GUID** (`applicationGUID`) 参数来初始化 SDK。


1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”的主页中，单击您的应用程序。单击**移动选项**。您需要**路径**和**应用程序 GUID** 值来初始化 SDK。

1. 通过添加以下头，将 `IMFCore` 框架导入要使用 {{site.data.keyword.amashort}} 客户端 SDK 的类中：

	**Objective-C：**
	 ```Objective-C
	#import <IMFCore/IMFCore.h>
	```

	**Swift:**

	{{site.data.keyword.amashort}} 客户端 SDK 将通过 Objective-C 实现。您可能需要将桥接头添加到 Swift 项目：

	1. 在 Xcode 中右键单击项目，并选择**新建文件...**。
	1. 在 **iOS 源**类别中，单击**头文件**。将文件命名为 `BridgingHeader.h`。
	1. 将以下行添加到桥接头：`#import <IMFCore/IMFCore.h>`
	1. 在 Xcode 中单击项目，然后选择**构建设置**选项卡。
	1. 搜索 `Objective-C Bridging Header`。
	1. 将值设置为您的 `BridgingHeader.h` 文件的位置，例如 `$(SRCROOT)/MyApp/BridgingHeader.h`。
	1. 通过构建项目来确保 Xcode 选取了您的桥接头。您应该不会看到任何失败消息。

1. 使用以下代码来初始化 {{site.data.keyword.amashort}} 客户端 SDK。通常会将初始化代码放置在应用程序代表的 `application:didFinishLaunchingWithOptions` 方法中，但这不是强制性的。<br/>
将 *applicationRoute* 和 *applicationGUID* 替换为 {{site.data.keyword.Bluemix_notm}}“仪表板”中**移动选项**中的值。

	**Objective-C:**

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	**Swift:**

	```Swift
IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",backendGUID: "applicationGUID")
	```

## 对移动后端发起请求
{: #request}

初始化 {{site.data.keyword.amashort}} 客户端 SDK 后，可以开始对移动后端发起请求。

1. 尝试在浏览器中对移动后端上的受保护端点发送请求。打开以下 URL：`{applicationRoute}/protected`。例如：`http://my-mobile-backend.mybluemix.net/protected`
<br/>使用 MobileFirst Services Starter 样板创建的移动后端的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护。由于此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问，因此会在浏览器中返回 `Unauthorized` 消息。

1. 使用 iOS 应用程序对同一端点发起请求。初始化 `IMFClient` 后，添加以下代码：

	**Objective-C:**

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

	**Swift:**

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
