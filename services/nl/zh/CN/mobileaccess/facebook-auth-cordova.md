---

copyright:
  years: 2015, 2016

---

# 在 Cordova 应用程序中启用 Facebook 认证
{: #facebook-auth-cordova}
要配置 Cordova 应用程序进行 Facebook 认证集成，必须使用 Cordova 应用程序的本机代码（即 Java、Objective-C 或 Swift）进行更改。请分别配置每个平台。在本机开发环境中使用本机代码进行更改，例如在 Android Studio 或 Xcode 中更改。

## 开始之前
{: #facebook-auth-before}
* 您必须具有受 {{site.data.keyword.amashort}} 保护的资源，并且具有安装了 {{site.data.keyword.amashort}} 客户端 SDK 的 Cordova 项目。有关更多信息，请参阅 [{{site.data.keyword.amashort}} 入门](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)和[设置 Cordova 插件](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)。
* 使用 {{site.data.keyword.amashort}} 服务器 SDK 手动保护后端应用程序。有关更多信息，请参阅[保护资源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。
* 创建 Facebook 应用程序标识。有关更多信息，请参阅[从 Facebook 开发者门户网站获取 Facebook 应用程序标识](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)。
* （可选）请熟悉以下部分：
   * [在 Android 应用程序中启用 Facebook 认证](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html)
   * [在 iOS 应用程序中启用 Facebook 认证](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html)


## 配置 Android 平台
{: #facebook-auth-cordova-android}

配置 Cordova 应用程序的 Android 平台进行 Facebook 认证集成所需的步骤，与本机 Android 应用程序所需的步骤非常类似。有关更多信息，请参阅[在 Android 应用程序中启用 Facebook 认证](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html)。请完成以下步骤：

* 针对 Android 平台配置 Facebook 应用程序
* 配置 {{site.data.keyword.amashort}} 进行 Facebook 认证
* 针对 Android 配置 {{site.data.keyword.amashort}} 客户端 SDK

配置 Cordova 应用程序时的唯一差别在于，必须使用 JavaScript 代码（而不是 Java 代码）来初始化 {{site.data.keyword.amashort}} 客户端 SDK。`FacebookAuthenticationManager` API 仍必须使用本机代码进行注册。

## 配置 iOS 平台
{: #facebook-auth-cordova-ios}

配置 Cordova 应用程序的 iOS 平台进行 Facebook 认证集成所需的步骤，与本机 iOS 应用程序所需的步骤类似。主要差别在于目前 Cordova CLI 不支持 CocoaPods 依赖关系管理器。必须手动添加集成 Facebook 认证所需的文件。有关更多信息，请参阅[在 iOS 应用程序中启用 Facebook 认证](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html)。请完成以下步骤：

* 针对 iOS 平台配置 Facebook 应用程序
* 配置 {{site.data.keyword.amashort}} 进行 Facebook 认证

### 手动安装用于 Facebook 认证的 {{site.data.keyword.amashort}} SDK 以及 Facebook SDK
{: #facebook-auth-cordova-ios-sdk}
1. 下载包含 [{{site.data.keyword.Bluemix_notm}}Mobile Services SDK for iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master) 的归档。

1. 转至 `Sources/Authenticators/IMFFacebookAuthentication` 目录，并将所有文件复制（拖放）到 Xcode 中的 iOS 项目。复制以下文件：
	* IMFDefaultFacebookAuthenticationDelegate.h
  * IMFDefaultFacebookAuthenticationDelegate.m
	* IMFFacebookAuthenticationDelegate.h
	* IMFFacebookAuthenticationHandler.h
	* IMFFacebookAuthenticationHandler.m

	在 Xcode 提示时，选择**复制文件...**。

1. 下载并安装 [Facebook SDK V3.19](https://developers.facebook.com/resources/facebook-ios-sdk-3.19.pkg)。

1. Facebook SDK 会安装到 `~/Documents/FacebookSDK` 目录中。浏览到该目录并将 `FacebookSDK.framework` 文件复制（拖放）到 Xcode 中的 iOS 项目中。

1. 	单击 Xcode 左侧窗格中的项目根目录，然后选择**构建阶段**。

1. 将 `FacebookSDK.framework` 文件添加到**将二进制文件与库链接**中已链接库的列表。

 请参阅[配置 iOS 平台以进行 Facebook 认证](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html)。使用本机代码注册 `IMFFacebookAuthenticationHandler` API，如“**初始化 {{site.data.keyword.amashort}} 客户端 SDK**”部分中所述。请不要使用本机代码初始化 `IMFClient`。

将以下行添加到应用程序代表的 `application:openURL:sourceApplication:annotation` 方法。此代码将确保向所有 Cordova 插件通知相应事件。

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```

## 初始化 {{site.data.keyword.amashort}} 客户端 SDK
{: #facebook-auth-cordova-init}

在 Cordova 应用程序中使用以下 JavaScript 代码来初始化 {{site.data.keyword.amashort}} 客户端 SDK。

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```

将 *applicationRoute* 和 *applicationGUID* 替换为从**移动选项**获取的**路径**和**应用程序 GUID** 值。

## 测试认证
{: #facebook-auth-cordova-test}
初始化客户端 SDK 并注册 Facebook 认证管理器后，可以开始对移动后端发起请求。

### 开始之前
您必须使用的是 {{site.data.keyword.mobilefirstbp}} 样板，并且已经在 `/protected` 端点具有受 {{site.data.keyword.amashort}} 保护的资源。有关更多信息，请参阅[保护资源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。

1. 尝试在浏览器中对新创建的移动后端的受保护端点发送请求。打开以下 URL：`{applicationRoute}/protected`。例如：`http://my-mobile-backend.mybluemix.net/protected`
<br/>使用 MobileFirst Services Starter 样板创建的移动后端的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护。浏览器中将返回 `Unauthorized` 消息。由于此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问，因此会返回此消息。

1. 使用 Cordova 应用程序对同一端点发起请求。初始化 `BMSClient` 后，添加以下代码：

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new MFPRequest("/protected", MFPRequest.GET);
	request.send(success, failure);
	```

1. 运行应用程序。这将弹出 Facebook 登录屏幕：

	![图像](images/android-facebook-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![图像](images/ios-facebook-login.png)

	> 如果设备上未安装 Facebook 应用程序，或者如果您当前未登录到 Facebook，那么此屏幕的外观可能略有不同。

1. 单击**确定**以授权 {{site.data.keyword.amashort}} 使用您的 Facebook 用户身份进行认证。

1. 	请求成功后，将在 LogCat 实用程序或 Xcode 控制台中显示以下输出：

	![针对 Android 的 Facebook 认证成功消息](images/android-facebook-login-success.png)

	![针对 iOS 的 Facebook 认证成功消息](images/ios-facebook-login-success.png)
