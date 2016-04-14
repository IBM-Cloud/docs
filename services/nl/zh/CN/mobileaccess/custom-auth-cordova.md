---

copyright:
  years: 2015, 2016

---

# 针对 Cordova 配置 {{site.data.keyword.amashort}} 客户端 SDK
{: #custom-cordova}
将要使用定制认证的 Cordova 应用程序配置为使用 {{site.data.keyword.amashort}} 客户端 SDK，并将该应用程序连接到 {{site.data.keyword.Bluemix}}。


## 开始之前
{: #before-you-begin}
您必须具有受配置为使用定制身份提供者的 {{site.data.keyword.amashort}} 服务实例保护的资源。您的移动应用程序还必须安装 {{site.data.keyword.amashort}} 客户端 SDK。有关更多信息，请参阅以下信息：
 * [{{site.data.keyword.amashort}} 入门](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [设置 Cordova SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)
 * [使用定制身份提供者](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [创建定制身份提供者](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [配置 {{site.data.keyword.amashort}} 进行定制认证](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)

## 初始化 {{site.data.keyword.amashort}} 客户端 SDK
{: #custom-cordova-sdk}
通过传递 applicationGUID 和 applicationRoute 参数来初始化 SDK。

1. 获取应用程序参数值。在 {{site.data.keyword.Bluemix_notm}}“仪表板”中打开应用程序。单击**移动选项**。这会显示**路径** (`applicationRoute`) 和**应用程序 GUID** (`applicationGUID`) 值。
1. 初始化客户端 SDK。

	```JavaScript
	BMSClient.initialize(applicationRoute, applicationGUID);

	```
 将 *applicationRoute* 和 *applicationGUID* 替换为 {{site.data.keyword.Bluemix_notm}} 仪表板上应用程序的**移动选项**面板中的**路径**和**应用程序 GUID** 值。

## 认证侦听器接口
{: #custom-cordva-auth}

{{site.data.keyword.amashort}} 客户端 SDK 提供认证侦听器接口，用于实现定制认证流程。必须添加以下方法，用于分别在认证过程的不同阶段进行调用。

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...},
	onAuthenticationSuccess: function(info){...},
	onAuthenticationFailure: function(info){...}
}
```

每种方法处理认证过程的不同阶段。

### onAuthenticationChallengeReceived 方法
{: #onAuthenticationChallengeReceived}
从 {{site.data.keyword.amashort}} 服务收到定制认证质询时，会调用此方法。
```JavaScript
onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...}
```

#### 自变量
{: #onAuthenticationChallengeReceived-args}
* `authenticationContext`：由 {{site.data.keyword.amashort}} 客户端 SDK 提供，以便开发者可以在凭证收集期间向客户端 SDK 报告认证质询回复或失败（例如，用户取消了认证请求）。
* `challenge`：包含定制身份提供者返回的定制认证质询的 JSON 对象。

调用 `onAuthenticationChallengeReceived` 方法可使 {{site.data.keyword.amashort}} 客户端 SDK 将控制权委派给开发者。{{site.data.keyword.amashort}} 会等待凭证。开发者必须使用以下其中一种 `authContext` 接口方法来收集凭证并向 {{site.data.keyword.amashort}} 客户端 SDK 报告这些凭证。

```JavaScript
onAuthenticationSuccess: function(info){...}
```

认证成功后会调用此方法。自变量包括可选的 JSONObject（用于包含有关认证成功的扩展信息）。


```JavaScript
onAuthenticationFailure: function(info){...}
```

认证失败后会调用此方法。自变量包括可选的 JSONObject（用于包含有关认证失败的扩展信息）。


## authenticationContext
{: #custom-cordova-authcontext}

`authenticationContext` 值作为自变量提供给定制认证侦听器的 `onAuthenticationChallengeReceived` 方法。开发者必须收集凭证并使用 `authenticationContext` 方法向 {{site.data.keyword.amashort}} 客户端 SDK 返回凭证或报告失败。请使用下列其中一种方法：

```JavaScript
authenticationContext.submitAuthenticationChallengeAnswer(challengeAnswer);

authenticationContext.submitAuthenticationFailure(info);
```

## 定制认证侦听器的样本实现
{: #custom-cordova-authlisten-sample}

此认证侦听器样本旨在处理定制身份提供者。可以从[此 Github 存储库](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)下载定制身份提供者。

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
		// Access Client SDK will remain in a waiting-for-credentials state
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

## 注册定制认证侦听器
{: #custom-cordova-authreg}

创建定制认证侦听器后，在开始使用前，请先向 `BMSClient` 注册该侦听器。将以下代码添加到应用程序中。对受保护资源发送任何请求之前，请先调用以下代码。

```Java
BMSClient.registerAuthenticationListener(realmName, customAuthenticationListener);
```
 使用在 {{site.data.keyword.amashort}}“仪表板”中指定的 *realmName*。


## 测试认证
{: #custom-cordova-test}
初始化客户端 SDK 并注册定制 AuthenticationListener 后，可以开始对移动后端发起请求。

### 开始之前
{: #custom-cordova-testing-before}
必须具有使用 {{site.data.keyword.mobilefirstbp}} 样板创建的应用程序，并且在 `/protected` 端点具有受 {{site.data.keyword.amashort}} 保护的资源。


1. 通过在浏览器中打开 `{applicationRoute}/protected`（例如，`http://my-mobile-backend.mybluemix.net/protected`），向移动后端的受保护端点发送请求。使用 {{site.data.keyword.mobilefirstbp}} 样板创建的移动后端的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护。此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问。因此，浏览器中会显示 `Unauthorized` 消息。

1. 使用 Cordova 应用程序对同一端点发起请求。初始化 `BMSClient` 并注册定制 AuthenticationListener 后，添加以下代码。

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

1. 	请求成功后，将在 LogCat 或 Xcode 控制台中显示以下输出：

	![图像](images/android-custom-login-success.png)

	![图像](images/ios-custom-login-success.png)
