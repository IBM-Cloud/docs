---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---

{{site.data.keyword.amafull}} 服务已替换为 {{site.data.keyword.appid_full}} 服务。

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 针对 {{site.data.keyword.amashort}} Android 应用程序配置定制认证
{: #custom-android}


配置 Android 应用程序进行定制认证，以使用 {{site.data.keyword.amashort}} 客户端 SDK，并将该应用程序连接到 {{site.data.keyword.Bluemix}}。

## 开始之前
{: #before-you-begin}
开始之前，您必须具有：

* 资源，该资源受 {{site.data.keyword.amashort}} 服务的实例保护，而该服务已配置为使用定制的身份提供者（请参阅[配置定制认证](custom-auth-config-mca.html)）。  
* **TenantID** 值。在 {{site.data.keyword.amashort}}“仪表板”中打开服务。单击**移动选项**按钮。`tenantId`（也称为 `appGUID`）值会显示在**应用程序 GUID/TenantId** 字段中。您将需要此值来初始化授权管理器。
* **域名**。这是在 {{site.data.keyword.amashort}}“仪表板”的**管理**选项卡中**定制**部分的**域名**字段中指定的值。
* 后端应用程序的 URL（**应用程序路径**）。您将需要此值来向后端应用程序的受保护端点发送请求。
* {{site.data.keyword.Bluemix_notm}} **区域**。您可以在**头像**图标 ![“头像”图标](images/face.jpg "“头像”图标") 旁边的头中找到当前 {{site.data.keyword.Bluemix_notm}} 区域。显示的区域值应为以下某个值：`US South`、`United Kingdom` 或 `Sydney`，并对应于 WebView Javascript 代码中需要的 SDK 值：`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_UK` 或 `BMSClient.REGION_SYDNEY`。您将需要此值来初始化 {{site.data.keyword.amashort}} 客户端。

有关更多信息，请参阅以下信息：
 * [{{site.data.keyword.amashort}} 入门](getting-started.html)
 * [设置 Android SDK](getting-started-android.html)
 * [使用定制身份提供者](custom-auth.html)
 * [创建定制身份提供者](custom-auth-identity-provider.html)
 * [配置 {{site.data.keyword.amashort}} 进行定制认证](custom-auth-config-mca.html)



## 初始化 {{site.data.keyword.amashort}} 客户端 SDK
{: #custom-android-initialize}
如果您的 Android 应用程序已经安装了 {{site.data.keyword.amashort}} Android SDK，那么可以跳过这部分。
1. 在 Android Studio 中的 Android 项目中，打开应用程序模块的 `build.gradle` 文件（非项目的 `build.gradle`）。

1. 在 `build.gradle` 文件中，找到 `dependencies` 部分，然后检查是否存在以下依赖关系：

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'core',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```
	{: codeblock}

1. 使用 Gradle 同步项目。单击**工具 > Android > 使用 Gradle 文件同步项目**。

1. 打开 Android 项目的 `AndroidManifest.xml` 文件。
在 `<manifest>` 元素下添加因特网访问许可权：

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```
	{: codeblock}

1. 初始化 SDK。
  
	在 Android 应用程序中，通常会将初始化代码放置在主 Activity 的 `onCreate` 方法中，但这不是强制性的。

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

	```
	{: codeblock}

将 `BMSClient.REGION_UK` 替换为 {{site.data.keyword.amashort}} 区域。有关获取这些值的更多信息，请参阅[开始之前](#before-you-begin)。


## AuthenticationListener 接口
{: #custom-android-authlistener}

{{site.data.keyword.amashort}} 客户端 SDK 提供 `AuthenticationListener` 接口，以便您可以实现定制认证流程。`AuthenticationListener` 接口公开三种方法，分别在认证过程的不同阶段进行调用。

### onAuthenticationChallengeReceived 方法
{: #custom-onAuth}
从 {{site.data.keyword.amashort}} 服务收到定制认证质询时，调用此方法。

```Java
void onAuthenticationChallengeReceived(AuthenticationContext authContext, JSONObject challenge, Context context);
```
{: codeblock}


#### 自变量
{: #custom-android-onAuth-arg}

* `AuthenticationContext`：由 {{site.data.keyword.amashort}} 客户端 SDK 提供，以便您可以在凭证收集期间向客户端 SDK 报告认证质询回复或失败。例如，用户取消认证时。
* `JSONObject`：包含定制身份提供者返回的定制认证质询。
* `Context`：对发送请求时所用 Android 上下文的引用。通常此自变量表示 Android Activity。

通过调用 `onAuthenticationChallengeReceived` 方法，{{site.data.keyword.amashort}} 客户端 SDK 将控制权委派给开发者。该服务会等待凭证。开发者必须使用其中一种 `AuthenticationContext` 接口方法来收集凭证并向 {{site.data.keyword.amashort}} 客户端 SDK 报告这些凭证。

### onAuthenticationSuccess 方法
{: #custom-android-authlistener-onsuccess}
认证成功后调用此方法。自变量包括“Android 上下文”和可选的 JSONObject（用于包含有关认证成功的扩展信息）。

```Java
void onAuthenticationSuccess(Context context, JSONObject info);
```
{: codeblock}

### onAuthenticationFailure 方法
{: #custom-android-authlistener-onfail}
认证失败后调用此方法。自变量包括“Android 上下文”和可选的 `JSONObject`（用于包含有关认证失败的扩展信息）。

```Java
void onAuthenticationFailure(Context context, JSONObject info);
```
{: codeblock}

## AuthenticationContext 接口
{: #custom-android-authcontext}

`AuthenticationContext` 作为自变量提供给定制 `AuthenticationListener` 的 `onAuthenticationChallengeReceived` 方法。您必须收集凭证并使用 `IMFAuthenticationContext` 方法向 {{site.data.keyword.amashort}} 客户端 SDK 返回凭证或报告失败。请使用下列其中一种方法。

```Java
void submitAuthenticationChallengeAnswer(JSONObject answer);
```
{: codeblock}

```Java
void submitAuthenticationFailure (JSONObject info);
```
{: codeblock}

## 定制 AuthenticationListener 的样本实现
{: #custom-android-samplecustom}

此 AuthenticationListener 样本设计用于处理定制身份提供者。您可以从 [Github 存储库 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window} 下载此样本。

```Java
package com.ibm.helloworld;
import android.content.Context;
import android.util.Log;
import com.ibm.mobilefirstplatform.clientsdk.android.security.mca.api.AuthenticationContext;
import com.ibm.mobilefirstplatform.clientsdk.android.security.mca.api.AuthenticationListener;
import org.json.JSONException;
import org.json.JSONObject;

public class CustomAuthenticationListener implements AuthenticationListener {@Override
	public void onAuthenticationChallengeReceived (AuthenticationContext authContext,
											JSONObject challenge, Context context) {log("onAuthenticationChallengeResceived :: " + challenge.toString());// In this sample the AuthenticationListener immediatelly returns a hardcoded
		// set of credentials. In a real life scenario this is where developer would
		// show a login screen, collect credentials and invoke
		// authContext.submitAuthenticationChallengeAnswer() APIJSONObject challengeResponse = new JSONObject();
		try {
			challengeResponse.put("username", "john.lennon");
			challengeResponse.put("password", "12345");
			authContext.submitAuthenticationChallengeAnswer(challengeResponse);
		} catch (JSONException e){// In case there was a failure collecting credentials you need to report
			// it back to the AuthenticationContext. Otherwise Mobile Client
			// Access client SDK will remain in a waiting-for-credentials state
			// forever

			log("This should never happen...");
			authContext.submitAuthenticationFailure(null);
		}
	}

	@Override
	public void onAuthenticationSuccess (Context context, JSONObject info) {
		log("onAuthenticationSuccess :: " + info.toString());
	}@Override
	public void onAuthenticationFailure (Context context, JSONObject info) {
		log("onAuthenticationFailure :: " + info.toString());
	}

	private void log(String text){
		Log.d("CustomAuthListener", text);
	}
}
```
{: codeblock}

## 注册定制 AuthenticationListener
{: #custom-android-register}

创建定制 AuthenticationListener 后，在开始使用前，请先向 `BMSClient` 注册该侦听器。将以下代码添加到应用程序中。对受保护资源发送任何请求之前，必须先调用此代码。

```Java
MCAAuthorizationManager mcaAuthorizationManager = 
      MCAAuthorizationManager.createInstance(this.getApplicationContext(),"<MCAServiceTenantId>");
mcaAuthorizationManager.registerAuthenticationListener(realmName, new CustomAuthenticationListener());
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);

```
{: codeblock}


在代码中：
* 将 `MCAServiceTenantId` 替换为 **TenantId** 值（请参阅[开始之前](##before-you-begin)）。
* 使用在 {{site.data.keyword.amashort}}“仪表板”中指定的 `realmName`（请参阅[配置定制认证](custom-auth-config-mca.html)）。


## 测试认证
{: #custom-android-testing}
初始化客户端 SDK 并注册定制 AuthenticationListener 后，可以开始对移动后端应用程序发起请求。

### 测试之前
{: #custom-android-testing-before}
您必须有一个应用程序，并且该应用程序所具有的资源在 `/protected` 端点受 {{site.data.keyword.amashort}} 保护。


1. 通过浏览器向移动后端应用程序的受保护端点 (`{applicationRoute}/protected`) 发送请求，例如 `http://my-mobile-backend.mybluemix.net/protected`。有关获取 `{applicationRoute}` 值的信息，请参阅[开始之前](#before-you-begin)。

1. 使用 {{site.data.keyword.mobilefirstbp}} 样板创建的移动后端应用程序的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护。此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问。因此，浏览器中会显示 `Unauthorized` 消息。

1. 使用 Android 应用程序对包含 `{applicationRoute}` 的同一受保护端点发起请求。初始化 `BMSClient` 并注册定制 AuthenticationListener 后，添加以下代码。

	```Java
	Request request = new Request("{applicationRoute}/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp",  MCAAuthorizationManager.getInstance().getUserIdentity().toString());
		}
		@Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
			if (null != t) {
				Log.d("Myapp", "onFailure :: " + t.getMessage());
			} else if (null != extendedInfo) {
				Log.d("Myapp", "onFailure :: " + extendedInfo.toString());
			} else {
				Log.d("Myapp", "onFailure :: " + response.getResponseText());
			}
		}
	});
	```
	{: codeblock}

1. 	请求成功后，将在 LogCat 工具中显示以下输出：

	![图像](images/android-custom-login-success.png)

 通过添加以下代码，您还可以添加注销功能：

 ```Java
 MCAAuthorizationManager.getInstance().logout(getApplicationContext(), listener);
 ```
 {: codeblock}


 如果您在用户登录之后调用此代码，那么用户将注销。用户在尝试重新登录时，必须重新回答服务器发出的质询。

 传递给注销功能的 `listener` 值可以为 `null`。
