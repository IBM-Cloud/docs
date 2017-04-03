---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

{{site.data.keyword.amafull}} 服务已替换为 {{site.data.keyword.appid_full}} 服务。

# 启用 Android 应用程序的 Google 认证
{: #google-auth-android}

使用 Google 在 {{site.data.keyword.amafull}} Android 应用程序上认证用户。添加 {{site.data.keyword.amashort}} 安全功能。

## 开始之前
{: #before-you-begin}

您必须具有：

* {{site.data.keyword.amafull}} 服务和 {{site.data.keyword.Bluemix_notm}} 应用程序的实例。有关如何创建 {{site.data.keyword.Bluemix_notm}} 后端应用程序的更多信息，请参阅[入门](index.html)。
* 后端应用程序的 URL（**应用程序路径**）。您将需要此值来向后端应用程序的受保护端点发送请求。
* **TenantID** 值。在 {{site.data.keyword.amashort}}“仪表板”中打开服务。单击**移动选项**按钮。`tenantId`（也称为 `appGUID`）值会显示在**应用程序 GUID/TenantId** 字段中。您将需要此值来初始化授权管理器。
* {{site.data.keyword.Bluemix_notm}} **区域**。您可以在**头像**图标 ![“头像”图标](images/face.jpg "“头像”图标") 旁边的头中找到当前 {{site.data.keyword.Bluemix_notm}} 区域。显示的区域值应为以下某个值：`US South`、`United Kingdom` 或 `Sydney`，并对应于 WebView Javascript 代码中需要的 SDK 值：`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_UK` 或 `BMSClient.REGION_SYDNEY`。您将需要此值来初始化 {{site.data.keyword.amashort}} 客户端。
* 配置为使用 Gradle 的 Android 项目。该项目不需要安装 {{site.data.keyword.amashort}} 客户端 SDK。  

设置 {{site.data.keyword.amashort}} Android 应用程序的 Google 认证需要对以下各项进行进一步配置：

* {{site.data.keyword.Bluemix_notm}} 应用程序
* Android Studio 项目

## 在 Google 开发者控制台上创建项目
{: #create-google-project}

要开始将 Google 用作身份提供者，请在 [Google 开发者控制台 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.developers.google.com){: new_window} 中创建项目。创建项目的步骤之一是获取 Google 客户端标识。Google 客户端标识是 Google 认证针对您的应用程序使用的唯一标识，设置 {{site.data.keyword.amashort}} 服务时需要该标识。

从控制台中：

1. 使用 **Google+** API 创建项目。
2. 添加 **OAuth** 用户访问权。
3. 添加凭证之前，您必须选择平台 (Android)。
4. 添加凭证。

要完成凭证的创建，您需要添加**签署证书指纹**。


### 设置签署证书
{: #signing_cert}

为了让 Google 验证您的应用程序真实性，必须指定签署证书指纹。

Android 操作系统需要安装在 Android 设备上的所有应用程序都使用开发者证书进行签署。Android 应用程序可以通过两种方式进行构建：调试和发布。通常建议对于调试和发布方式使用不同的证书。用于在调试方式下签署 Android 应用程序的证书会与 Android SDK 捆绑在一起。Android SDK 通常由 Android Studio 自动安装。当您希望将应用程序发布到 Google Play 时，必须使用通常由您自行生成的其他证书来签署应用程序。有关更多信息，请参阅[签署 Android 应用程序 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://developer.android.com/tools/publishing/app-signing.html){: new_window}。

包含用于开发环境的证书的密钥库存储在 `~/.android/debug.keystore` 文件中。缺省密钥库密码为 `android`。此证书用于在调试方式下构建应用程序。

1. 从客户端开发环境中检索签署证书指纹：

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore -list -v
	```
	{: codeblock}

	还可以使用相同的语法来检索发布方式证书的密钥散列。请替换命令中的别名和密钥库路径。

1. 在“Google 控制台凭证”对话框的**证书指纹**下，找到以 `SHA1` 开头的行。将通过运行 **keytool** 命令获得的指纹值复制到文本框。

###软件包名称

1. 在“凭证”对话框中，输入 Android 应用程序的软件包名称。

	要找到 Android 应用程序的软件包名称，请在 Android Studio 中打开 `AndroidManifest.xml` 文件，然后查找：

	```
	<manifest package="{your-package-name}">
	```
	{: codeblock}

1. 完成后，单击**创建**。这将完成凭证创建。

###Google 客户端标识
{: #google-client-id}

成功创建凭证之后，凭证页面会显示 Google 客户端标识。请记录此值。您需要在 {{site.data.keyword.Bluemix}} 应用程序中注册此值。


## 配置 {{site.data.keyword.amashort}} 进行 Google 认证
{: #google-auth-android-config}

现在，您已经具有 Android 的 Google 客户端标识，可以在 {{site.data.keyword.amashort}}“仪表板”中启用 Google 认证。

1. 在 {{site.data.keyword.amashort}}“仪表板”中打开服务。
1. 在**管理**选项卡中，将**授权**切换为“开启”。
1. 展开 **Google** 部分。
1. 在 **Android 的客户端标识**中，指定 Android 的 Google 客户端标识，然后单击**保存**。

## 针对 Android 配置 {{site.data.keyword.amashort}} 客户端 SDK
{: #google-auth-android-sdk}

从 Android Studio 项目中。

1. 打开应用程序模块的 `build.gradle` 文件。

	Android 项目可能具有两个 `build.gradle` 文件：一个用于项目，另一个用于应用程序模块。请使用用于应用程序模块的文件。

	找到 dependencies 部分，并为客户端 SDK 添加新的编译依赖关系：

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

	**注：**您可以除去对 `com.ibm.mobilefirstplatform.clientsdk.android` 组的 `core` 模块的依赖关系（如果有的话）。`googleauthentication` 模块会自动下载此依赖关系。`googleauthentication` 模块会下载 Google+ SDK 并将其安装在 Android 项目中。



1. 通过单击**工具 > Android > 使用 Gradle 文件同步项目**来使用 Gradle 同步项目。

1. 打开 Android 项目的 `AndroidManifest.xml` 文件。

1. 在 `<manifest>` 元素下添加因特网访问许可权：

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
<uses-permission android:name="android.permission.USE_CREDENTIALS" />
```
	{: codeblock}

1. 要使用 {{site.data.keyword.amashort}} 客户端 SDK，您必须通过传递 **context** 和 **region** 参数来对其进行初始化。

	在 Android 应用程序中，通常会将初始化代码放置在主 Activity 的 `onCreate` 方法中，但这不是强制性的。

1. 初始化客户端 SDK，然后注册 Google 认证管理器。

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

	BMSClient.getInstance().setAuthorizationManager(
					MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));

	GoogleAuthenticationManager.getInstance().register(this);
```
	{: codeblock}

	* 将 `BMSClient.REGION_UK` 替换为 {{site.data.keyword.Bluemix_notm}} **区域**。
	* 将 `<MCAServiceTenantId>` 替换为 **TenantId** 值。

	有关获取这些值的更多信息，请参阅[开始之前](##before-you-begin)。

	**注：**如果您的 Android 应用程序是针对 Android V6.0（API 级别 23
）或更高版本的，那么必须确保该应用程序具有 `android.permission.GET_ACCOUNTS`
调用，然后才能调用 `register`。有关更多信息，请参阅[在 Android 上请求许可权 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.android.com/training/permissions/requesting.html){: new_window}。

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

## 测试认证
{: #google-auth-android-test}

初始化客户端 SDK 并注册 Google 认证管理器后，可以开始对后端应用程序发起请求。

开始测试之前，您必须具有使用 **MobileFirst Services Starter** 样板创
建的移动后端应用程序，并且必须已经具有受
{{site.data.keyword.amashort}} `/protected` 端点保护的资源。有关更多信息，请参阅[保护资源](protecting-resources.html)。

1. 尝试通过在桌面浏览器中打开 `{applicationRoute}/protected`（例如，`http://my-mobile-backend.mybluemix.net/protected`），向移动后端应用程序的受保护端点发送请求。有关获取 `{applicationRoute}` 值的信息，请参阅[开始之前](#before-you-begin)。

	使用 MobileFirst Services 样板创建的移动后端应用程序的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护。所以此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问。因此，您会在桌面浏览器中看到 `Unauthorized`。

1. 使用 Android 应用程序对同一受保护端点发起请求。初始化 `BMSClient` 实例并注册 `GoogleAuthenticationManager` 后，添加以下代码。

	```Java
	Request request = new Request("{applicationRoute}/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp", MCAAuthorizationManager.getInstance().getUserIdentity().toString());
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

1. 运行应用程序。这将弹出 Google 登录屏幕。登录之后，应用程序将请求授予许可权以访问资源：

	![图像](images/android-google-login.png)

	根据您的 Android 设备以及您当前是否登录到 Google，您看到的 UI 可能会不同。

	通过单击**确定**，您将授权 {{site.data.keyword.amashort}} 使用您的 Google 用户身份进行认证。

1. 	请求成功后，可在 LogCat 工具中看到以下输出：

	![图像](images/android-google-login-success.png)

	通过添加以下代码，您还可以添加注销功能：

	```Java
 GoogleAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
 ```
	{: codeblock}

	如果您在用户登录 Google 之后调用此代码，那么用户将从 Google 注销。当用户尝试重新登录时，他们必须重新选择将要登录的 Google 帐户。如果他们尝试登录先前所登录的 Google 标识，那么不再提示用户输入凭证。如果要重新提示输入登录凭证，用户必须从 Android 设备除去其 Google 帐户。

	传递给注销功能的 `listener` 值可以为 `null`。
