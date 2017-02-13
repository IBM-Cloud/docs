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

# 设置 Android SDK
{: #getting-started-android}

在 Android 应用程序中安装 {{site.data.keyword.amafull}} 客户端 SDK，初始化该 SDK，然后对受保护和不受保护的资源发起请求。
{: shortdesc}

## 开始之前
{: #before-you-begin}

您必须具有：

* {{site.data.keyword.Bluemix_notm}} 应用程序的实例。
* {{site.data.keyword.amafull}} 服务的实例。
* **TenantID**。在 {{site.data.keyword.amafull}}“仪表板”中打开服务。单击**移动选项**按钮。`tenantId`（也称为 `appGUID`）值会显示在**应用程序 GUID/TenantId** 字段中。您将需要此值来初始化授权管理器。
* **应用程序路径**。这是后端应用程序的 URL。您将需要此值来向其受保护端点发送请求。
* {{site.data.keyword.Bluemix_notm}} **区域**。您可以在**头像**图标 ![“头像”图标](images/face.jpg "“头像”图标") 旁边的头中找到当前 {{site.data.keyword.Bluemix_notm}} 区域。显示的区域值应为以下某个值：`US South`、`Sydney` 或 `United Kingdom`，并对应于代码中需要的 SDK 值：`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_SYDNEY` 或 `BMSClient.REGION_UK`。您将需要此值来初始化 {{site.data.keyword.amashort}} 客户端。
* Android Studio 项目，设置为使用 Gradle。有关如何设置 Android 开发环境的更多信息，请参阅 [Google 开发者工具![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://developer.android.com/sdk/index.html "外部链接图标"){: new_window}。

## 安装 {{site.data.keyword.amashort}} 客户端 SDK
{: #install-mca-sdk}

{{site.data.keyword.amashort}} 客户端 SDK 通过 Gradle 进行分发；Gradle 是用于 Android 项目的依赖关系管理器。Gradle 会自动从存储库下载工件，并将其提供给 Android 应用程序。

1. 创建 Android Studio 项目或打开现有项目。

1. 打开应用程序的 `build.gradle` 文件（**非** 项目的 `build.gradle` 文件）。

1. 找到 `build.gradle` 文件的 **dependencies** 部分。添加 {{site.data.keyword.amashort}} 客户端 SDK 的编译依赖关系：

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

1. 使用 Gradle 同步项目。单击**工具 &gt; Android &gt; 使用 Gradle 文件同步项目**。

1. 打开 Android 项目的 `AndroidManifest.xml` 文件。
在 `<manifest>` 元素下添加因特网访问许可权：

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```
	{: codeblock}

## 初始化 {{site.data.keyword.amashort}} 客户端 SDK
{: #initalize-mca-sdk}

通过将 **context** 和 **region** 传递到 `initialize` 方法来初始化客户端 SDK。在 Android 应用程序中，通常会将初始化代码放置在主 Activity 的 `onCreate` 方法中，但这不是强制性的。

```Java
  BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);
					
  BMSClient.getInstance().setAuthorizationManager(
					MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));
						
	```
{: codeblock}

* 将 `<applicationBluemixRegion>` 替换为托管 {{site.data.keyword.Bluemix_notm}} 服务的区域。
* 将 `<MCAServiceTenantId>` 替换为 **tenantId** 

。
有关这些值的更多信息，请参阅[开始之前](#before-you-begin)。

## 对移动后端应用程序发起请求
{: #request}

初始化 {{site.data.keyword.amashort}} 客户端 SDK 后，可以开始对移动后端应用程序发起请求。

1. 尝试对移动后端应用程序的受保护端点发送请求。在浏览器中，打开以下 URL：`{applicationRoute}/protected`（例如，`http://my-mobile-backend.mybluemix.net/protected`）。   

	使用 MobileFirst Services Starter 样板创建的移动后端应用程序的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护。由于此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问，因此会在浏览器中返回 `Unauthorized` 消息。



1. 使用 Android 应用程序对同一端点发起请求。初始化 `BMSClient` 后，添加以下代码：

	```Java
	Request request = new Request("http://my-mobile-backend.mybluemix.net/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
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

1. 请求成功后，将在 LogCat 实用程序中看到以下输出：


	![图像](images/getting-started-android-success.png)

## 后续步骤
{: #next-steps}

连接到受保护端点时，无需任何凭证。如果需要用户登录到您的应用程序，那么必须配置 Facebook、Google 或定制认证。

* [Facebook](facebook-auth-android.html)
* [Google](google-auth-android.html)
* [定制](custom-auth-android.html)
