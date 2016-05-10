---

copyright:
  years: 2015, 2016

---

# 在 Android 应用程序中启用 Facebook 认证
{: #facebook-auth-android}
要在 Android 应用程序中将 Facebook 用作身份提供者，请为 Facebook 应用程序添加并配置 Android 平台。

## 开始之前
{: #facebook-auth-android-before}
 * 您必须具有受 {{site.data.keyword.amashort}} 保护的资源，并且具有安装了 {{site.data.keyword.amashort}} 客户端 SDK 的 Android 项目。有关更多信息，请参阅 [{{site.data.keyword.amashort}} 入门](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)和[设置 Android SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-android.html)。  
 * 使用 {{site.data.keyword.amashort}} 服务器 SDK 手动保护后端应用程序。有关更多信息，请参阅[保护资源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。
 * 创建 Facebook 应用程序标识。有关更多信息，请参阅[从 Facebook 开发者门户网站获取 Facebook 应用程序标识](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)。


## 针对 Android 平台配置 Facebook 应用程序
{: #facebook-auth-android-config}
要在 Android 应用程序中将 Facebook 用作身份提供者，必须为 Facebook 应用程序添加并配置 Android 平台。

1. 在 Facebook 开发者门户网站中打开 Facebook 应用程序。

1. 单击**设置 &gt; 添加平台 &gt; Android**。

1. 在“Google Play 软件包名称”提示中，指定 Android 应用程序的软件包名称。要找到 Android 应用程序的软件包名称，请在 Android Studio 中打开 `AndroidManifest.xml` 文件，然后查找 `<manifest ..... package="{your-package-name}">`。

1. 在**类名**提示中，指定主 Activity 的类名。要找到 Android 应用程序的主 Activity 类名，请打开 `AndroidManifest.xml` 文件，然后使用类似于以下代码片段的意向过滤器来查找 Activity 声明：

	```XML
	<activity
		android:name=".MainActivity"
		android:label="@string/app_name">
		<intent-filter>
			<action android:name="android.intent.action.MAIN"/>
			<category android:name="android.intent.category.LAUNCHER"/>
		</intent-filter>
	</activity>
	```

1. 要使 Facebook 确保您的应用程序真实性，必须指定开发者证书 SHA1 的散列。

	**关于 Android 安全性的更多信息：**Android 操作系统需要安装在 Android 设备上的所有应用程序都使用开发者证书进行签署。Android 应用程序可以通过两种方式进行构建：调试和发布。<br/>
对于调试和发布方式使用不同的证书。用于在调试方式下签署 Android 应用程序的证书会与 Android SDK 捆绑在一起，Android SDK 通常由 Android Studio 自动安装。当您希望将应用程序发布到 Google Play 商店时，必须使用通常由您自行生成的其他证书来签署应用程序。<br/>您可以使用 Facebook 输入两组密钥散列：一组密钥散列用于在调试方式下通过调试证书构建的应用程序，另一组密钥散列用于在发布方式下通过发布证书构建的应用程序。有关更多信息，请参阅 [signing your Android applications](http://developer.android.com/tools/publishing/app-signing.html)。

1. 包含要用于开发环境的证书的密钥库会存储在 `~/.android/debug.keystore` 文件中。缺省密钥库密码为：`android`。使用此证书可在调试方式下构建应用程序。

1. 检索调试方式证书的密钥散列：

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore | openssl sha1 -binary | openssl base64
	```

	**提示**：可以使用相同的语法来检索发布方式证书的密钥散列。请替换命令中的别名和密钥库路径。

1. 复制使用 **keytool** 命令获取的密钥散列，并将其粘贴到 Facebook 开发者门户网站中的“开发/发布密钥散列”提示中。

	**提示**：如果计划使用单点登录，请考虑启用此功能。

1. 单击**保存设置**。

## 配置 {{site.data.keyword.amashort}} 进行 Facebook 认证
{: #facebook-auth-android-mca}
已拥有 Facebook 应用程序标识并且将 Facebook 应用程序配置为向 Android 客户端提供服务后，可以在 {{site.data.keyword.amashort}}“仪表板”中启用 Facebook 认证。

1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”中打开应用程序。

1. 单击**移动选项**，然后记录**路径** (`applicationRoute`) 和**应用程序 GUID** (`applicationGUID`)。初始化 SDK 时需要这些值。

1. 单击 {{site.data.keyword.amashort}} 磁贴。这将装入 {{site.data.keyword.amashort}}“仪表板”。

1. 单击 **Facebook** 磁贴。

1. 指定 Facebook 应用程序标识，然后单击**保存**。

## 针对 Android 配置 {{site.data.keyword.amashort}} 客户端 SDK
{: #facebook-auth-android-sdk}
要针对 Android 配置客户端 SDK，请在 Android Studio 中使用 Gradle 依赖关系管理器。

1.  打开应用程序模块的 `build.gradle` 文件。
Android 项目可能具有两个 `build.gradle` 文件：一个用于项目，一个用于应用程序模块。请使用应用程序模块文件。

1. 找到 `build.gradle` 文件的 dependencies 部分，并为客户端 SDK 添加新的编译依赖关系：

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

	您可以除去对 `com.ibm.mobilefirstplatform.clientsdk.android` 组的 `core` 模块的依赖关系（如果存在于文件中）。`facebookauthentication` 模块会自动下载 `core` 模块。

  保存更新后，`facebookauthentication` 模块会在 Android 项目中下载并安装 Facebook SDK。


1. 使用 Gradle 同步项目。单击**工具 > Android > 使用 Gradle 文件同步项目**。

1. 打开 `res/values/strings.xml` 文件，然后添加包含您的 Facebook 应用程序标识的 `facebook_app_id` 字符串：

	```XML
	<resources>
		<string name="app_name">HelloWorld</string>
		<string name="action_settings">Settings</string>
		<string name="facebook_app_id">522733366802111</string>
	</resources>
```

1. 在 Android 项目的 `AndroidManifest.xml` 文件中：
   1. 在 `<manifest>` 元素下添加因特网访问许可权：

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
```
  2. 将 Facebook SDK 所需元数据添加到 `<application>` 元素：

	```XML
	<application .......>

		<meta-data
			android:name="com.facebook.sdk.ApplicationId"
			android:value="@string/facebook_app_id"/>

		<activity ...../>
		<activity ...../>
	</application>
```

   1. 将 Facebook Activity 元素添加到现有 Activity 下：

	```XML
	<application .....>
		<activity ...../>
		<activity ...../>

		<activity 	android:name="com.facebook.FacebookActivity"
					android:configChanges=
						"keyboard|keyboardHidden|screenLayout|screenSize|orientation"
					android:theme="@android:style/Theme.Translucent.NoTitleBar"
					android:label="@string/app_name" />

	</application>
```

1. 初始化客户端 SDK，然后注册 Facebook 认证管理器。通过传递 context、应用程序 GUID (`applicationGUID`) 和路径 (`applicationRoute`) 参数来初始化 {{site.data.keyword.amashort}} 客户端 SDK。<br/>
 通常会将初始化代码放置在 Android 应用程序中主 Activity 的 `onCreate` 方法中，但这不是强制性的。<br/>
 将 *applicationRoute* 和 *applicationGUID* 替换为 Bluemix 仪表板中应用程序主页上**移动选项**菜单中的**路径**和**应用程序 GUID** 值。

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");

	FacebookAuthenticationManager.getInstance().register(this);
```


1. 将以下代码添加到您的 Activity：

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
```

## 测试认证
初始化客户端 SDK 并注册 Facebook 认证管理器后，可以开始对移动后端发起请求。

### 开始之前
{: #facebook-auth-android-testing-before}
您必须使用的是 {{site.data.keyword.mobilefirstbp}} 样板，并且已经在 `/protected` 端点具有受 {{site.data.keyword.amashort}} 保护的资源。如果需要设置 `/protected` 端点，请参阅[保护资源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。

1. 尝试在浏览器中对新创建的移动后端的受保护端点发送请求。打开以下 URL：`{applicationRoute}/protected`。例如：`http://my-mobile-backend.mybluemix.net/protected`
<br/>使用 MobileFirst Services Starter 样板创建的移动后端的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护。浏览器中将返回 `Unauthorized` 消息。由于此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问，因此会返回此消息。

1. 使用 Android 应用程序对同一端点发起请求。初始化 `BMSClient` 并注册 `FacebookAuthenticationManager` 后，添加以下代码。

	```Java
	Request request = new Request("/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp", AuthorizationManager.getInstance().getUserIdentity().toString());
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

1. 运行应用程序。这将显示 Facebook 登录屏幕。

	![图像](images/android-facebook-login.png)

	如果设备上未安装 Facebook 应用程序，或者如果您当前未登录到 Facebook，那么此屏幕的外观可能略有不同。

1. 单击**确定**以授权 {{site.data.keyword.amashort}} 使用您的 Facebook 用户身份进行认证。

1. 	请求成功后，将在 LogCat 实用程序中显示以下输出：

	![图像](images/android-facebook-login-success.png)

1. 通过添加以下代码，您还可以添加注销功能：

 ```
FacebookAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
 ```

 如果您在用户登录 Facebook 之后调用此代码，那么用户将从 Facebook 注销。当用户尝试重新登录时，系统将提示他们输入 Facebook 凭证。

 传递给注销功能的 `listener` 值可以为空值。
