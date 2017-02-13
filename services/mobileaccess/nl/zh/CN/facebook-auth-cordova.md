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


# 启用 Cordova 应用程序的 Facebook 认证
{: #facebook-auth-cordova}

要配置 {{site.data.keyword.amafull}} Cordova 应用程序进行 Facebook 认证集成，请分别配置每个平台。Cordova 应用程序必须已安装 {{site.data.keyword.amashort}} SDK。

本机平台和 Cordova WebView Javascript 代码都需要进行更改才能支持 Facebook 认证。

在本机开发环境中使用本机代码进行更改，例如在 Android Studio 或 Xcode 中更改。
{:shortdesc}

## 开始之前
{: #facebook-auth-before}

您必须具有：
* 已安装 {{site.data.keyword.amashort}} 客户端 SDK 的 Cordova 项目（Android 或 iOS），请参阅[设置 Cordova 插件](getting-started-cordova.html#getting-started-cordova-plugin)。
* 受 {{site.data.keyword.amashort}} 服务保护的 {{site.data.keyword.Bluemix_notm}} 应用程序实例。有关如何创建 {{site.data.keyword.Bluemix_notm}} 后端服务的更多信息，请参阅[入门](index.html)。
* 应用程序路径。这是后端应用程序的 URL。
* `tenantId` 值。打开 {{site.data.keyword.amashort}} 服务仪表板。单击**移动选项**。`tenantId`（也称为 `appGUID`）值会显示在**应用程序 GUID/TenantId** 字段中。您将需要这些值来初始化 SDK，并将请求发送到后端服务。
*  找到托管 {{site.data.keyword.Bluemix_notm}} 服务的区域。您可以在菜单栏中的**头像**图标 ![“头像”图标](images/face.jpg "“头像”图标") 旁边的头中找到当前 {{site.data.keyword.Bluemix_notm}} 区域。区域值应为以下某个值：**美国南部**、**悉尼**或**英国**。对应于这些名称的准确 SDK 常量值如代码示例中所示。
* Facebook 应用程序和应用程序标识。有关更多信息，请参阅[从 Facebook 开发者门户网站获取 Facebook 应用程序标识](facebook-auth-overview.html#facebook-appID)。



## 配置 Android 平台
{: #facebook-auth-cordova-android}

配置 Cordova 应用程序的 Android 平台进行 Facebook 认证集成所需的步骤，与本机 Android 应用程序所需的步骤非常类似。有关更多信息，请参阅[在 Android 应用程序中启用 Facebook 认证](facebook-auth-android.html)。请完成以下步骤：

* [针对 Android 平台配置 Facebook 应用程序](facebook-auth-android.html#facebook-auth-android-config)。这将在 Facebook 开发者站点上为 Android 应用程序设置 Facebook 认证。
* [配置 MCA 进行 Facebook 认证](facebook-auth-android.html#facebook-auth-android-mca)。这将在 {{site.data.keyword.Bluemix}} 服务器上配置 {{site.data.keyword.amashort}} 服务进行 Android Facebook 认证。


### 针对 Android 平台配置 {{site.data.keyword.amashort}} Facebook 客户端 SDK
{: #configure_android}

在本机 Android 应用程序项目中，必须由 Gradle 添加 {{site.data.keyword.amashort}} Facebook 客户端 SDK。

1. 在 Android 项目文件夹，打开应用程序模块的 `build.gradle` 文件（**非**项目的 `build.gradle` 文件）。找到 dependencies 部分，并为客户端 SDK 添加新的编译依赖关系：

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'facebookauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
```
	{: codeblock}

2. 单击**工具 > Android > 使用 Gradle 文件同步项目**来使用 Gradle 同步项目。

3. 打开 `android/res/values/strings.xml` 文件，然后添加包含您的 Facebook 应用程序标识的 `<facebook_app_id>` 字符串。

	```XML
	<resources>
		<string name="app_name">HelloCordova</string>
		<string name="launcher_name">@string/app_name</string>
		<string name="activity_name">@string/launcher_name</string>
		<string name="facebook_app_id">"<facebook_app_id>"</string>
	</resources>
	```
	{: codeblock}

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
    {: codeblock}

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
    {: codeblock}

5. 将以下代码添加到 Activity Java 代码：

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}

### 使用本机 Android 代码初始化授权管理器
{: #initialize_android}

`FacebookAuthenticationManager` API 仍必须使用本机代码进行注册。使用 `<tenantId>` 将此代码添加到主活动 `onCreate` 方法（请参阅[开始之前](#before-you-begin)）。

```
String tenantId = "<tenantId>";
MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
FacebookAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
```
{: codeblock}


## 配置 iOS 平台
{: #facebook-auth-cordova-ios}

配置 Cordova 应用程序的 iOS 平台进行 Facebook 认证集成所需的步骤，与本机 iOS Swift 应用程序所需的步骤类似（使用 Objective-C 代码与 Swift SDK 需要头文件）。主要差别在于目前 Cordova CLI 不支持 CocoaPods 依赖关系管理器。必须手动添加集成使用 Facebook 认证的 {{site.data.keyword.amashort}} 客户端所需的文件。有关更多信息，请参阅[启用 iOS 应用程序的 Facebook 认证 (Swift SDK)](facebook-auth-ios-swift-sdk.html)。请完成以下步骤：

* [针对 iOS 平台配置 Facebook 应用程序](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-config)。这将在 Facebook 开发者站点上设置 Facebook 认证服务。
* [配置 MCA 进行 Facebook 认证](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-configmca)。这将在 {{site.data.keyword.Bluemix}} 服务器上配置 {{site.data.keyword.amashort}} 服务。
* [针对 iOS 配置 MCA Facebook 客户端 SDK](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-sdk)。这将使用 Cocoapods 安装 {{site.data.keyword.amashort}} iOS Swift SDK 进行 Facebook 授权。


### 启用 iOS 的密钥链共享
{: #enable_keychain}

启用`密钥链共享`。转至`功能`选项卡，然后在 Xcode 项目中将`密钥链共享`切换为`开启`。

### 使用 Objective-C 初始化 {{site.data.keyword.amashort}} 授权管理器
{: #initialize_objc}

授权管理器必须根据 Xcode 的版本，使用 `app-delegate.m` 文件中的本机 Objective-C 代码进行初始化。

```
	#import "<your_module_name>-Swift.h"

	- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

	{

	    [CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];

	    [[FacebookAuthenticationManager sharedInstance] register];

	    self.viewController = [[MainViewController alloc] init];

	    [[FacebookAuthenticationManager sharedInstance] onFinishLaunchingWithApplication:application withOptions:launchOptions];


	    return [super application:application didFinishLaunchingWithOptions:launchOptions];
}



- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url
					sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {

		return [[FacebookAuthenticationManager sharedInstance] onOpenURLWithApplication:application 
	   		url:url sourceApplication:sourceApplication annotation:annotation];
	}

```
{: codeblock}

**注：**导入的头文件名由合并到字符串 `-Swift.h` 的模块名称构成，例如，如果模块名称为 `Cordova`，那么 import 行应该为 `#import "Cordova-Swift.h"` 。要查找模块名称，请转至 `构建设置` > `打包` > `产品模块名称`。

将 `<tenantId>` 替换为租户标识（请参阅[开始之前](#facebook-auth-before)）。


##在 Cordova WebView 中初始化 {{site.data.keyword.amashort}} 客户端 SDK
{: #initialize_webview}

对于所有平台，都要在 Cordova Javascript WebView 中使用以下 JavaScript 代码来初始化 {{site.data.keyword.amashort}} 客户端 SDK。

```javascript
BMSClient.initialize(<applicationBluemixRegion>);
```
{: codeblock}

将 `<applicationBluemixRegion>` 替换为区域（请参阅[开始之前](#facebook-auth-before)）。

## 测试认证
{: #facebook-auth-cordova-test}

初始化客户端 SDK 并注册 Facebook 认证管理器后，可以开始对移动后端服务发起请求。

### 开始之前
{: #testing_auth_before}

您必须使用的是 {{site.data.keyword.mobilefirstbp}} 样板，并且已经在 `/protected` 端点具有受 {{site.data.keyword.amashort}} 保护的资源。有关更多信息，请参阅[保护资源](protecting-resources.html)。

1. 尝试从浏览器对移动后端应用程序的受保护端点发送请求。打开以下 URL：`{applicationRoute}/protected`。例如：`http://my-mobile-backend.mybluemix.net/protected`。

	`/protected` 端点值应该是通过 MobileFirst Services Starter 样板创建且通过 {{site.data.keyword.amashort}} 保护的移动后端服务的任意一个受保护的端点。浏览器中将返回 `Unauthorized` 消息。由于此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问，因此会返回此消息。



1. 使用 Cordova 应用程序对同一端点发起请求。初始化 `BMSClient` 后，添加以下代码：

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error){
    	console.log("failure", error);
    }
	var request = new BMSRequest("<applicationRoute}/protected>", BMSRequest.GET);
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
