---

copyright:
  years: 2015, 2016

---

# 针对 iOS 配置 {{site.data.keyword.amashort}} 客户端 SDK
{: #custom-ios}

将要使用定制认证的 iOS 应用程序配置为使用 {{site.data.keyword.amashort}} 客户端 SDK，并将该应用程序连接到 {{site.data.keyword.Bluemix}}。

**提示：**如果要使用 Swift 开发 iOS 应用程序，请考虑使用 {{site.data.keyword.amashort}} 客户端 Swift SDK。本页面中的指示信息适用于 {{site.data.keyword.amashort}} 客户端 Objective-C SDK。有关使用 Swift SDK 的指示信息，请参阅[针对 iOS (Swift SDK) 配置 {{site.data.keyword.amashort}} 客户端 SDK](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-ios-swift-sdk.html)。

## 开始之前
{: #before-you-begin}
您必须具有受配置为使用定制身份提供者的 {{site.data.keyword.amashort}} 服务实例保护的资源。您的移动应用程序还必须安装 {{site.data.keyword.amashort}} 客户端 SDK。有关更多信息，请参阅以下信息：
 * [{{site.data.keyword.amashort}} 入门](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [设置 iOS Objective-C SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html)
 * [使用定制身份提供者](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [创建定制身份提供者](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [配置 {{site.data.keyword.amashort}} 进行定制认证](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)



## 使用 CocoaPods 安装客户端 SDK
{: #custom-ios-sdk-cocoapods}
使用 CocoaPods 依赖关系管理器来安装 {{site.data.keyword.amashort}} 客户端 SDK。

1. 打开终端，并浏览到 iOS 项目的根目录。

1. 编辑 `Podfile` 并添加以下行。

	```
	pod 'IMFCore'
	```

1. 在命令行中，运行 `pod install`。
CocoaPods 会安装添加的依赖关系。这将显示进度和添加的组件。

**重要信息**：您现在必须使用 CocoaPods 生成的 xcworkspace 文件来打开项目。通常该文件的名称为 `{your-project-name}.xcworkspace`。

1. 在命令行中运行 `open {your-project-name}.xcworkspace` 以打开 iOS 项目工作空间。



### 初始化客户端 SDK
{: #custom-ios-sdk-initialize}

传递应用程序路径 (`applicationRoute`) 和 GUID (`applicationGUID`) 参数，以初始化 SDK。通常会将初始化代码放置在应用程序代表的 `application:didFinishLaunchingWithOptions` 方法中，但这不是强制性的

1. 获取应用程序参数值。在 {{site.data.keyword.Bluemix_notm}}“仪表板”中打开应用程序。单击**移动选项**，以查看**路径** (`applicationRoute`) 和**应用程序 GUID** (`applicationGUID`) 的值。

1. 将 `IMFCore` 框架导入要使用客户端 SDK 的类中。

	Objective-C:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	```

	Swift:

	{{site.data.keyword.amashort}} 客户端 SDK 将通过 Objective-C 实现。您可能需要将桥接头添加到 Swift 项目才能使用 SDK。

	* 在 Xcode 中右键单击项目，并选择**新建文件...**
	* 在 **iOS 源**类别中，选取**头文件**。将文件命名为 `BridgingHeader.h`。
	* 将 `#import <IMFCore/IMFCore.h>` 添加到桥接头。
	* 在 Xcode 中单击项目，然后选择**构建设置**选项卡。
	* 搜索 `Objective-C Bridging Header`。
	* 将值设置为您的 `BridgingHeader.h` 文件的位置，例如：`$(SRCROOT)/MyApp/BridgingHeader.h`
	* 通过构建项目来验证 Xcode 是否选取了您的桥接头。

1. 初始化客户端 SDK。将 applicationRoute 和 applicationGUID 替换为从**移动选项**获取的**路径** (`applicationRoute`) 和**应用程序 GUID** (`applicationGUID`) 值。

	Objective-C:

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	Swift:

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```


## IMFAuthenticationHandler 代表
{: #custom-ios-sdk-authhandler}


{{site.data.keyword.amashort}} 客户端 SDK 提供 `IMFAuthenticationHandler` 接口，用于实现定制认证流程。`IMFAuthenticationHandler` 公开三种方法，分别在认证过程的不同阶段进行调用。

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
 						didReceiveAuthenticationChallenge:(NSDictionary*)challenge;
```

从 {{site.data.keyword.amashort}} 服务收到定制认证质询时，会调用此方法。自变量包括：

* `IMFAuthenticationContext` 协议由 {{site.data.keyword.amashort}} 客户端 SDK 提供，以便开发者可以在凭证收集期间向客户端 SDK 报告认证质询回复或失败（例如，用户已取消）
* `NSDictionary` 包含定制身份提供者返回的定制认证质询

通过调用 `authenticationContext:didReceiveAuthenticationChallenge` 方法，{{site.data.keyword.amashort}} 客户端 SDK 会将控制权委派给开发者，并将其自身置于“正在等待凭证”方式。开发者负责使用其中一种 `IMFAuthenticationContext` 协议方法来收集凭证并向 {{site.data.keyword.amashort}} 客户端 SDK 报告这些凭证；下面将描述这些协议方法。

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationSuccess:(NSDictionary *)userInfo;
```

认证成功后会调用此方法。自变量包括 IMFAuthenticationContext 和可选的 NSDictionary（用于包含有关认证成功的扩展信息）。

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationFailure:(NSDictionary*)userInfo;
```

认证失败后会调用此方法。自变量包括 IMFAuthenticationContext 和可选的 NSDictionary（用于包含有关认证失败的扩展信息）。

## IMFAuthenticationContext 协议
{: #custom-ios-sdk-authcontext}


`IMFAuthenticationContext` 作为自变量提供给定制 `IMFAuthenticationHandler` 的 `authenticationContext:didReceiveAuthenticationChallenge` 方法。开发者负责收集凭证并使用 `IMFAuthenticationContext` 方法向 {{site.data.keyword.amashort}} 客户端 SDK 返回凭证或报告失败。请使用下列其中一种方法：

```
-(void) submitAuthenticationChallengeAnswer:(NSDictionary*) answer;

-(void) submitAuthenticationFailure:(NSDictionary*) userInfo;
```

## 定制 IMFAuthenticationDelegate 的样本实现
{: #custom-ios-sdk-sample}


IMFAuthenticationDelegate 样本旨在处理定制身份提供者样本。您可以从 [Github 存储库](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)下载此样本。

Objective-C:

``` Objective-C
CustomAuthenticationDelegate.h
-----------------------------------
#import <Foundation/Foundation.h>

@import IMFCore;
@interface CustomAuthenticationDelegate : NSObject <IMFAuthenticationDelegate>
@end


CustomAuthenticationDelegate.m
-----------------------------------
#import "CustomAuthenticationDelegate.h"

@implementation CustomAuthenticationDelegate

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationChallenge:(NSDictionary *)challenge{

	NSLog(@"didReceiveAuthenticationChallenge :: %@", challenge);

	// In this sample the IMFAuthenticationDelegate immediately returns a hardcoded
	// set of credentials. In a real life scenario this is where developer would
	// show a login screen, collect credentials and invoke
	// [context submitAuthenticationChallengeAnswer:] API

	NSDictionary *challengeAnswer = [NSDictionary dictionaryWithObjectsAndKeys:
									 @"john.lennon", @"username",
									 @"12345", @"password", nil];

	[context submitAuthenticationChallengeAnswer:challengeAnswer];

	// In case there was a failure collecting credentials you need to report
	// it back to the IMFAuthenticationContext. Otherwise Mobile Client
	// Access Client SDK will remain in a waiting-for-credentials state
	// forever
}

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationSuccess:(NSDictionary *)userInfo{
	NSLog(@"didReceiveAuthenticationSuccess");


}

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationFailure:(NSDictionary *)userInfo{
	NSLog(@"didReceiveAuthenticationFailure");

}

@end
```

Swift 实现：

```Swift
import Foundation

class CustomAuthenticationDelegate : NSObject, IMFAuthenticationDelegate{

	func authenticationContext(context: IMFAuthenticationContext!,
					didReceiveAuthenticationChallenge challenge: [NSObject : AnyObject]!) {

		NSLog("didReceiveAuthenticationChallenge :: %@", challenge)

		// In this sample the IMFAuthenticationDelegate immediately returns a hardcoded
		// set of credentials. In a real life scenario this is where developer would
		// show a login screen, collect credentials and invoke
		// context.submitAuthenticationChallengeAnswer() API

		let challengeAnswer: [String:String] = [
			"username":"john.lennon",
			"password":"12345"
		]

		context.submitAuthenticationChallengeAnswer(challengeAnswer)

		// In case there was a failure collecting credentials you need to report
		// it back to the IMFAuthenticationContext. Otherwise Mobile Client
		// Access Client SDK will remain in a waiting-for-credentials state
		// forever
	}


	func authenticationContext(context: IMFAuthenticationContext!,
					didReceiveAuthenticationSuccess userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationSuccess")
	}

	func authenticationContext(context: IMFAuthenticationContext!,
					didReceiveAuthenticationFailure userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationFailure")
	}
}
```

## 注册定制 IMFAuthenticationDelegate

创建定制 IMFAuthenticationDelegate 后，向 `IMFClient` 注册。对受保护资源发送任何请求之前，请先在应用程序中调用以下代码。使用在 {{site.data.keyword.amashort}}“仪表板”中指定的 realmName。

Objective-C 应用程序：

```Objective-C
[[IMFClient sharedInstance]
				registerAuthenticationDelegate:[CustomAuthenticationDelegate new]
										forRealm:realmName];
```

Swift 应用程序：
```Swift
IMFClient.sharedInstance().registerAuthenticationDelegate(CustomAuthenticationDelegate(),
									forRealm: realmName)
```




## 测试认证
{: #custom-ios-testing}
初始化客户端 SDK 并注册定制 `IMFAuthenticationDelegate` 后，可以开始对移动后端发起请求。

### 开始之前
{: #custom-ios-testing-before}
必须具有使用 {{site.data.keyword.mobilefirstbp}} 样板创建的应用程序，并且在 `/protected` 端点具有受 {{site.data.keyword.amashort}} 保护的资源。

1. 通过在浏览器中打开 `{applicationRoute}/protected`（例如，`http://my-mobile-backend.mybluemix.net/protected`），向移动后端的受保护端点发送请求。使用 {{site.data.keyword.mobilefirstbp}} 样板创建的移动后端的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护。此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问。因此，浏览器中会显示 `Unauthorized` 消息。
1. 使用 iOS 应用程序对同一端点发起请求。初始化 `BMSClient` 并注册定制 `IMFAuthenticationDelegate` 后，添加以下代码：

	Objective-C:

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

	Swift:

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
1. 	请求成功后，将在 Xcode 控制台中看到以下输出：

	![图像](images/ios-custom-login-success.png)
	
	
	
	通过添加以下代码，您还可以添加注销功能：

	Objective C: 

	```Objective-C
	[[IMFAuthorizationManager sharedInstance] logout : callBack]
	```
	Swift: 

	```Swift
	IMFAuthorizationManager.sharedInstance().logout(callBack)
	```

如果您在用户登录之后调用此代码，那么用户将注销。用户在尝试重新登录时，必须重新回答服务器发出的质询。您可以选择是否将 `callBack` 传递给注销功能。您还可以传递 `nil`。

