---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"
---
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# 启用 Cordova 应用程序的 Facebook 认证
{: #facebook-auth-cordova}


要配置 {{site.data.keyword.amafull}} Cordova 应用程序进行 Facebook 认证集成，使用 Cordova 应用程序的本机代码（即 Java、Objective-C 或 Swift）进行更改。请分别配置每个平台。此 Cordova 应用程序必须已安装 {{site.data.keyword.amashort}} SDK。 


在本机开发环境中使用本机代码进行更改，例如在 Android Studio 或 Xcode 中更改。
{:shortdesc}

## 开始之前
{: #facebook-auth-before}
您必须具有：
* 已安装 {{site.data.keyword.amashort}} 客户端 SDK 的 Cordova 项目，请参阅[设置 Cordova 插件](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)。
* 受 {{site.data.keyword.amashort}} 服务保护的 {{site.data.keyword.Bluemix_notm}} 应用程序实例。有关如何创建 {{site.data.keyword.Bluemix_notm}} 后端应用程序的更多信息，请参阅[入门](index.html)。
* Facebook 应用程序标识。有关更多信息，请参阅[从 Facebook 开发者门户网站获取 Facebook 应用程序标识](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)。



## 配置 Android 平台
{: #facebook-auth-cordova-android}

配置 Cordova 应用程序的 Android 平台进行 Facebook 认证集成所需的步骤，与本机 Android 应用程序所需的步骤非常类似。有关更多信息，请参阅[在 Android 应用程序中启用 Facebook 认证](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html)。请完成以下步骤：

* 针对 Android 平台配置 Facebook 应用程序
* 配置 {{site.data.keyword.amashort}} 进行 Facebook 认证

### 针对 Android 配置 {{site.data.keyword.amashort}} 客户端 SDK

在 Cordova 应用程序中针对 Android 配置 {{site.data.keyword.amashort}} 客户端 SDK。

1. 在 Android 项目文件夹，打开应用程序模块的 `build.gradle` 文件（**非**项目的 `build.gradle` 文件）。找到 dependencies 部分，并为客户端 SDK 添加新的编译依赖关系：

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
     		name:'facebookauthentication',
     		version: '1.+',
     		ext: 'aar',
     		transitive: true
     		// other dependencies  
		 }
	```
	
2. 通过单击**工具 > Android > 使用 Gradle 文件同步项目**来使用 Gradle 同步项目。

3. 打开 `android/res/values/strings.xml` 文件，然后添加包含您的 Facebook 应用程序标识的 `facebook_app_id` 字符串。

	```XML
	<resources>
		<string name="app_name">HelloCordova</string>
		<string name="launcher_name">@string/app_name</string>
		<string name="activity_name">@string/launcher_name</string>
		<string name="facebook_app_id">522733366802111</string>
	</resources>
	```
	
4. 在 Android 项目的 `AndroidManifest.xml` 文件中 (`android/manifests/AndroidManifest.xml`)：

	* 将 Facebook SDK 所需元数据添加到 <application> 元素：

	```XML
	<application .......>

		<meta-data
			android:name="com.facebook.sdk.ApplicationId"
			android:value="@string/facebook_app_id"/>

		<activity ...../>
		<activity ...../>
	</application>
	```

	* 将 Facebook Activity 元素添加到现有 Activity 下：

	```XML
	<application .....>
		<activity ...../>
		<activity ...../>
	<activity   android:name="com.facebook.FacebookActivity"
	              android:configChanges="keyboard|keyboardHidden|screenLayout|screenSize|orientation"
	              android:theme="@android:style/Theme.Translucent.NoTitleBar"
	              android:label="@string/app_name" 
			    />
	</application>
	```

2. 对于 Cordova 应用程序，请在 JavaScript 代码中（而不是 Java 代码）初始化 {{site.data.keyword.amashort}} 客户端 SDK。`FacebookAuthenticationManager` API 仍必须使用本机代码进行注册。将此代码添加到主活动 `onCreate` 方法：  

	```Java
	FacebookAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
	```

6. 将以下代码添加到您的 Activity：

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
```

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

1. 在 Xcode 中单击项目根目录，然后选择**构建阶段**。

1. 将 `FacebookSDK.framework` 文件添加到**将二进制文件与库链接**中已链接库的列表。

 请参阅[配置 iOS 平台以进行 Facebook 认证](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html)。使用本机代码注册 `IMFFacebookAuthenticationHandler` API，如“**初始化 {{site.data.keyword.amashort}} 客户端 SDK**”部分中所述。请不要使用本机代码初始化 `IMFClient`。

将以下行添加到应用程序代表的 `application:openURL:sourceApplication:annotation` 方法。此代码将确保向所有 Cordova 插件通知相应事件。

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];
```
{: codeblock}

## 初始化 {{site.data.keyword.amashort}} 客户端 SDK
{: #facebook-auth-cordova-init}

在 Cordova 应用程序中使用以下 JavaScript 代码来初始化 {{site.data.keyword.amashort}} 客户端 SDK。

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```
{: codeblock}

将 `applicationRoute` 和 `applicationGUID` 替换为从**移动选项**获取的**路径**和**应用程序 GUID** 值。
	



##初始化 {{site.data.keyword.amashort}} AuthorizationManager
在 Cordova 应用程序中使用以下 JavaScript 代码来初始化 {{site.data.keyword.amashort}} AuthorizationManager。
```JavaScript
  MFPAuthorizationManager.initialize("tenantId");
  ```
{: codeblock}

将 `tenantId` 值替换为 {{site.data.keyword.amashort}} 服务 `tenantId`。您可以通过单击 {{site.data.keyword.amashort}} 服务磁贴上的**显示凭证**按钮来获取此值。



## 测试认证
{: #facebook-auth-cordova-test}
初始化客户端 SDK 并注册 Facebook 认证管理器后，可以开始对移动后端应用程序发起请求。

### 开始之前
您必须使用的是 {{site.data.keyword.mobilefirstbp}} 样板，并且已经在 `/protected` 端点具有受 {{site.data.keyword.amashort}} 保护的资源。有关更多信息，请参阅[保护资源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。

1. 尝试从浏览器对新创建的移动后端应用程序的受保护端点发送请求。打开以下 URL：`{applicationRoute}/protected`。例如：`http://my-mobile-backend.mybluemix.net/protected`
<br/>使用 MobileFirst Services Starter 样板创建的移动后端应用程序的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护。浏览器中将返回 `Unauthorized` 消息。由于此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问，因此会返回此消息。

1. 使用 Cordova 应用程序对同一端点发起请求。初始化 `BMSClient` 后，添加以下代码：

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error){
    	console.log("failure", error);
    }
	var request = new MFPRequest("/protected", MFPRequest.GET);
	request.send(success, failure);
	```
{: codeblock}

1. 运行应用程序。这将弹出 Facebook 登录屏幕：

	![图像](images/android-facebook-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![图像](images/ios-facebook-login.png)

	如果设备上未安装 Facebook 应用程序，或者如果您当前未登录到 Facebook，那么此屏幕的外观可能略有不同。

1. 单击**确定**以授权 {{site.data.keyword.amashort}} 使用您的 Facebook 用户身份进行认证。

1. 	请求成功后，将在 LogCat 实用程序或 Xcode 控制台中显示以下输出：

	![针对 Android 的 Facebook 认证成功消息](images/android-facebook-login-success.png)

	![针对 iOS 的 Facebook 认证成功消息](images/ios-facebook-login-success.png)
