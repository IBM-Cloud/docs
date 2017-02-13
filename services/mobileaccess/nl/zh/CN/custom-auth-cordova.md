---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 针对 {{site.data.keyword.amashort}} Cordova 应用程序配置定制认证
{: #custom-cordova}

安装 Cordova 应用程序以使用定制认证和 {{site.data.keyword.amafull}} 客户端 SDK 来访问受保护应用程序。

## 开始之前
{: #before-you-begin}
* 资源，该资源受 {{site.data.keyword.amashort}} 服务的实例保护，而该服务已配置为使用定制的身份提供者（请参阅[配置定制认证](custom-auth-config-mca.html)）。  
* **TenantID** 值。在 {{site.data.keyword.amashort}}“仪表板”中打开服务。单击**移动选项**按钮。`tenantId`（也称为 `appGUID`）值会显示在**应用程序 GUID/TenantId** 字段中。您将需要此值来初始化授权管理器。
* **域名**。这是在 {{site.data.keyword.amashort}}“仪表板”的**管理**选项卡中**定制**部分的**域名**字段中指定的值。
* {{site.data.keyword.Bluemix_notm}} **区域**。您可以在**头像**图标 ![“头像”图标](images/face.jpg "“头像”图标") 旁边的头中找到当前 {{site.data.keyword.Bluemix_notm}} 区域。显示的区域值应该为以下某个值：`US South`、`United Kingdom` 或 `Sydney`。对应的 SDK 常量的准确语法在代码示例中提供。

有关更多信息，请参阅以下信息：

 * [配置 {{site.data.keyword.amashort}} 进行定制认证](custom-auth-config-mca.html)。这将显示如何设置 {{site.data.keyword.amashort}} 服务以进行定制认证。在此可定义**域**值。
 * [设置 Cordova SDK](getting-started-cordova.html)。有关设置 Cordova 客户端应用程序的信息。
 * [使用定制身份提供者](custom-auth.html)。如何使用定制身份提供者认证用户。
 * [创建定制身份提供者](custom-auth-identity-provider.html)。一些说明定制身份提供者如何工作的示例。

## 配置 Cordova WebView 代码
### 在 Cordova WebView 中初始化 {{site.data.keyword.amashort}} 客户端 SDK
{: #custom-cordova-sdk}
通过传递 `index.js` 文件中的 `<applicationBluemixRegion>` 参数来初始化 SDK。

```JavaScript
BMSClient.initialize("<applicationBluemixRegion>");
```
{: codeblock}

将 `<applicationBluemixRegion>` 替换为区域（请参阅[开始之前](#before-you-begin)）。


### 认证侦听器接口
{: #custom-cordva-auth}

{{site.data.keyword.amashort}} 客户端 SDK 提供认证侦听器接口，用于实现定制认证流程。必须添加以下方法，用于分别在认证过程的不同阶段进行调用。

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...},
	onAuthenticationSuccess: function(info){...},
	onAuthenticationFailure: function(info){...}
}
```
{: codeblock}

每种方法处理认证过程的不同阶段。

### onAuthenticationChallengeReceived 方法
{: #onAuthenticationChallengeReceived}
从 {{site.data.keyword.amashort}} 服务收到定制认证质询时，会调用此方法。

```JavaScript
onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...}
```
{: codeblock}

* `authenticationContext`：由 {{site.data.keyword.amashort}} 客户端 SDK 提供，以便开发者可以在凭证收集期间向客户端 SDK 报告认证质询回复或失败（例如，用户取消了认证请求）。
* `challenge`：包含定制身份提供者返回的定制认证质询的 JSON 对象。

调用 `onAuthenticationChallengeReceived` 方法可使 {{site.data.keyword.amashort}} 客户端 SDK 将控制权委派给开发者。{{site.data.keyword.amashort}} 会等待凭证。开发者必须使用以下其中一种 `authContext` 接口方法来收集凭证并向 {{site.data.keyword.amashort}} 客户端 SDK 报告这些凭证。

```JavaScript
onAuthenticationSuccess: function(info){...}
```
{: codeblock}

认证成功后会调用此方法。自变量包括可选的 JSON 对象（用于包含有关认证成功的扩展信息）。


```JavaScript
onAuthenticationFailure: function(info){...}
```
{: codeblock}

认证失败后会调用此方法。自变量包括可选的 JSON 对象（用于包含有关认证失败的扩展信息）。


### authenticationContext
{: #custom-cordova-authcontext}

`authenticationContext` 值作为自变量提供给定制认证侦听器的 `onAuthenticationChallengeReceived` 方法。开发者必须收集凭证并使用 `authenticationContext` 方法向 {{site.data.keyword.amashort}} 客户端 SDK 返回凭证或报告失败。请使用下列其中一种方法：

```JavaScript
authenticationContext.submitAuthenticationChallengeAnswer(challengeAnswer);

```
{: codeblock}

```JavaScript
authenticationContext.submitAuthenticationFailure(info);
```
{: codeblock}

以下代码演示了定制认证侦听器可如何收集凭证、处理质询以及提供认证响应。

## 定制认证侦听器工作流程的样本实现
{: #custom-cordova-authlisten-sample}

此认证侦听器样本设计用于处理定制身份提供者。您可以从[此 Github 存储库 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "外部链接图标"){: new_window} 下载定制身份提供者。

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {
		console.log("onAuthenticationChallengeReceived :: ", challenge);

		// In this sample the authentication listener immediatelly returns a hardcoded
		// set of credentials. In a real life scenario this is where developer would
		// show a login screen, collect credentials and invoke
		// authenticationContext.submitAuthenticationChallengeAnswer() API

		var challengeResponse = {
			username: "john.lennon",
			password: "12345"
		}

		authenticationContext.submitAuthenticationChallengeAnswer(challengeResponse);

		// In case there was a failure collecting credentials you need to report
		// it back to the authenticationContext. Otherwise Mobile Client
		// Access client SDK will remain in a waiting-for-credentials state
		// forever

	},

	onAuthenticationSuccess: function(info){
		console.log("onAuthenticationSuccess :: ", info);
	},

	onAuthenticationFailure: function(info){
		console.log("onAuthenticationFailure :: ", info);
	}
}
```
{: codeblock}

## 在 Cordova WebView 中注册定制认证侦听器
{: #custom-cordova-authreg}

创建定制认证侦听器后，在开始使用前，必须先向 `BMSClient` 注册该侦听器。将以下代码添加到应用程序中。对受保护资源发送任何请求之前，请先调用以下代码。

```Java
BMSClient.registerAuthenticationListener(<realmName>, customAuthenticationListener);
```
{: codeblock}
使用在 {{site.data.keyword.amashort}}“仪表板”中指定的 `realmName`。


## 使用本机代码设置授权管理器

{{site.data.keyword.amashort}} 授权管理器必须使用本机平台代码进行注册。

**Android**（添加到主活动中的 `onCreate`）

```
String tenantId = "<tenantId>";
MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
```
{: codeblock}

**iOS Objective-C**（添加到 `AppDelegate.m`）

根据 Xcode 的版本，注册授权管理器。

```
#import "<your_module_name>-Swift.h"

- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

{  

    //[CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];
 }
```
{: codeblock}

注：对于正确的 Swift 头文件名，将 `your_module_name` 替换为项目的模块名称，例如，如果模块名称为 `Cordova`，那么代码应为 `#import "Cordova-Swift.h"`。要查找模块名称，请转至**构建设置 > 打包 > 产品模块名称**。

**注：**将 `tenantId` 替换为在 {{site.data.keyword.amashort}} 服务仪表板上的**移动选项**按钮中找到的租户标识。


## 启用 iOS 的密钥链共享

通过转至`功能`选项卡，然后在 Xcode 项目中将“`密钥链共享`”切换为“`开启`”以启用“`密钥链共享`”。


## 测试认证
{: #custom-cordova-test}
初始化客户端 SDK 并注册定制 `AuthenticationListener` 后，可以开始对移动后端应用程序发起请求。

### 开始之前
{: #custom-cordova-testing-before}
您必须具有使用 {{site.data.keyword.mobilefirstbp}} 样板创建的应用程序，并且在 `/protected` 端点具有受 {{site.data.keyword.amashort}} 保护的资源。


1. 通过在浏览器中打开 `{applicationRoute}/protected`（例如，`http://my-mobile-backend.mybluemix.net/protected`），向移动后端应用程序的受保护端点发送请求。使用 {{site.data.keyword.mobilefirstbp}} 样板创建的移动后端应用程序的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护。此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问。因此，浏览器中会显示 `Unauthorized` 消息。

1. 使用 Cordova 应用程序对同一端点发起请求。初始化 `BMSClient` 并注册定制 AuthenticationListener 后，添加以下代码。

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

	将 `<your-application-route>` 替换为后端应用程序 URL（请参阅[开始之前](#before-you-begin)）。

1. 	请求成功后，将在 `LogCat` 或 Xcode 控制台中显示以下输出：

	![图像](images/android-custom-login-success.png)

	![图像](images/ios-custom-login-success.png)
