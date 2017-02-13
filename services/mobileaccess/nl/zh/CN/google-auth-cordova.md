---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 启用 Cordova 应用程序的 Google 认证
{: #google-auth-cordova}

要集成 {{site.data.keyword.amafull}} Cordova 应用程序进行 Google 认证，必须在 Cordova 应用程序的本机平台代码（Java 或 Objective-C）中进行更改，还要在 Cordova WebView (Javascript) 中进行更改。每个平台必须分别进行配置。在本机开发环境中使用本机代码进行更改，例如在 Android Studio 或 Xcode 中更改。

## 开始之前
{: #before-you-begin}

您必须具有：

* 已安装 {{site.data.keyword.amashort}} 客户端 SDK 的 Cordova 项目。有关更多信息，请参阅[设置 Cordova 插件](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)。  
* 受 {{site.data.keyword.amashort}} 服务保护的 {{site.data.keyword.Bluemix_notm}} 应用程序实例。有关如何创建 {{site.data.keyword.Bluemix_notm}} 后端服务的更多信息，请参阅[入门](index.html)。
* 应用程序路径。这是后端应用程序的 URL。
* **TenantID**。在 {{site.data.keyword.Bluemix_notm}}“仪表板”中打开服务。单击**移动选项**。`tenantId`（也称为 `appGUID`）值会显示在**应用程序 GUID/TenantId** 字段中。您将需要此值来初始化授权管理器。
*  找到托管 {{site.data.keyword.Bluemix_notm}} 应用程序的区域。您可以在**头像**图标 ![“头像”图标](images/face.jpg "“头像”图标") 旁边的头中找到当前 Bluemix 区域。区域值应为以下某个值：**美国南部**、**悉尼**或**英国**。对应于这些名称的准确 SDK 常量值如代码示例中所示。
* （可选）请熟悉以下部分：
   * [启用 Android 应用程序的 Google 认证](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)
   * [在 iOS 应用程序中启用 Google 认证](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html)


## 配置 Android 平台
{: #google-auth-cordova-android}

配置 Cordova 应用程序的 Android 平台进行 Google 认证所需的步骤，与本机应用程序所需的步骤非常类似。请参阅[在 Android 应用程序中启用 Google 认证](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)并设置以下各项：

   * [在 Google 开发者控制台上创建项目](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html#create-google-project)。这将显示如何在 Google 开发者 Web 站点上设置认证服务。
   * [配置 MCA 进行 Google 认证](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html#google-auth-android-config)。这将显示如何设置 {{site.data.keyword.amashort}} 以使用 Google 授权。

### 针对 Android Cordova 配置 {{site.data.keyword.amashort}} 客户端 SDK

1. 在 Android 项目文件夹，打开应用程序模块的 `build.gradle` 文件（**非**项目的 `build.gradle` 文件）。找到 dependencies 部分，并为客户端 SDK 添加新的编译依赖关系：

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'googleauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```
	{: codeblock}

1. 通过单击**工具 > Android > 使用 Gradle 文件同步项目**来使用 Gradle 同步项目。

1. `GoogleAuthenticationManager` API 仍必须使用本机代码进行注册。将此代码添加到主活动 `onCreate` 方法：

	```Java
	String tenantId = "<tenantId>";
	MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
	BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
	GoogleAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
	```
	{: codeblock}

1. 将以下代码添加到您的 Activity：

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		GoogleAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}

## 配置 iOS 平台
{: #google-auth-cordova-ios}

配置 Cordova 应用程序的 iOS 平台进行 Google 认证集成所需的步骤，与本机应用程序所需的步骤类似。主要差别在于目前 Cordova CLI 不支持 CocoaPods 依赖关系管理器。必须手动添加与 Google 认证集成所需的文件。有关更多信息，请参阅[启用 iOS 应用程序的 Google 认证 (Swift SDK)](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html)。请完成以下步骤：

   * [为应用程序准备进行 Google 登录](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-sign-in-ios)：准备 Google 登录以认证 {{site.data.keyword.amashort}} iOS 应用程序。

   * [配置 MCA 进行 Google 认证](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-auth-ios-config)：配置 {{site.data.keyword.amashort}} 服务以使用 Google 登录。

   * [针对 iOS 配置 MCA 客户端 SDK](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-auth-ios-sdk)：配置 {{site.data.keyword.amashort}} 客户端以使用 Google 登录。


### 启用 iOS 的密钥链共享
{: #enable_keychain}

启用`密钥链共享`。转至`功能`选项卡，然后在 Xcode 项目中将`密钥链共享`切换为`开启`。


### 使用 iOS 代码初始化授权管理器

使用 `AppDelgate.m` 文件中的 Objective-C 初始化 {{site.data.keyword.amashort}} 授权管理器。

```
 #import "<your_module_name>-Swift.h" 
 
- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

{
	[CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];

	    [[GoogleAuthenticationManager sharedInstance] register];

    self.viewController = [[MainViewController alloc] init];

	    [[GoogleAuthenticationManager sharedInstance] onFinishLaunchingWithApplication:application withOptions:launchOptions];

	return [super application:application didFinishLaunchingWithOptions:launchOptions];
}



- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url
					sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {

		return [[GoogleAuthenticationManager sharedInstance] onOpenURLWithApplication:application url:url 
	sourceApplication:sourceApplication annotation:annotation];
}
```
{: codeblock}

**注：**

* 将 `<your_module_name>` 替换为项目的模块名称。例如，如果模块名称为 `Cordova`，那么 import 行应该为 `#import "Cordova-Swift.h"`。要查找模块名称，请转至`构建设置`选项卡，再转至`打包` > `产品模块名称`。
* 将 `<tenantId>` 替换为租户标识（请参阅[开始之前](#before-you-begin)）。


## 在 Cordova WebView 中初始化 {{site.data.keyword.amashort}} 客户端 SDK
{: #google-auth-cordova-initialize}

对于所有平台，在 Cordova 应用程序中使用以下 Javascript 代码来初始化 {{site.data.keyword.amashort}} 客户端 SDK。

```JavaScript
BMSClient.initialize("<applicationBluemixRegion>");
```
{: codeblock}

将 `<applicationBluemixRegion>` 替换为区域（请参阅[开始之前](#before-you-begin)）。

## 测试认证
{: #google-auth-cordova-test}

初始化客户端 SDK 后，可以开始对移动后端应用程序发起请求。

### 开始之前
{: #google-auth-cordova-testing-before}

必须在 `/protected` 端点具有受 {{site.data.keyword.amashort}} 保护的后端应用程序。如果需要设置 `/protected` 端点，请参阅[保护资源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。

1. 尝试通过在桌面浏览器中打开 `{applicationRoute}/protected`（例如，`http://my-mobile-backend.mybluemix.net/protected`），向移动后端应用程序的受保护端点发送请求。

1. 使用 MobileFirst Services 样板创建的移动后端应用程序的 `/protected` 端点受 {{site.data.keyword.amashort}} 的保护，所以它只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问。因此，您会在桌面浏览器中看到 `Unauthorized`。

1. 使用 Cordova 应用程序通过完整 URL（例如，`http://my-mobile-backend.mybluemix.net/protected`）对同一端点发起请求。初始化 `BMSClient` 后，添加以下代码。

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new BMSRequest("<your-application-route>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}

1. 运行应用程序。此时将显示 Google 登录屏幕。

	![Google 登录屏幕](images/android-google-login.png)

	![Google 登录屏幕](images/ios-google-login.png)

	如果设备上未安装 Facebook 应用程序，或者如果您当前未登录到 Facebook，那么此屏幕的外观可能略有不同。

1. 通过单击**确定**，您将授权 {{site.data.keyword.amashort}} 使用您的 Google 用户身份进行认证。

1. 您的请求应该会成功。根据使用的平台，应该会在 LogCat/Xcode 控制台中看到以下输出：

	![Android 上的代码片段](images/android-google-login-success.png)

	![iOS 上的代码片段](images/ios-google-login-success.png)
