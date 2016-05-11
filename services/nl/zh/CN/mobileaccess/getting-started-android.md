---

copyright:
  years: 2015, 2016
  
---

# 设置 Android SDK
{: #getting-started-android}

在 Android 应用程序中安装 {{site.data.keyword.amashort}} 客户端 SDK，初始化该 SDK，然后对受保护和不受保护的资源发起请求。

## 开始之前
{: #before-you-begin}
* 必须具有受 {{site.data.keyword.amashort}} 服务保护的移动后端的实例。有关如何创建移动后端的更多信息，请参阅[入门](getting-started.html)。
* 设置 Android Studio 和 Android Studio SDK。有关如何设置 Android 开发环境的更多信息，请参阅 [Google Developer Tools](http://developer.android.com/sdk/index.html)。


## 安装 {{site.data.keyword.amashort}} 客户端 SDK
{: #install-mca-sdk}

{{site.data.keyword.amashort}} 客户端 SDK 通过 Gradle 进行分发；Gradle 是用于 Android 项目的依赖关系管理器。Gradle 会自动从存储库下载工件，并将其提供给 Android 应用程序。

1. 创建 Android Studio 项目或打开现有项目。

1. 打开 `build.gradle` 文件。
**提示：**Android 项目可能具有两个 `build.gradle` 文件：一个用于项目，一个用于应用程序模块。请使用应用程序模块文件。

1. 找到 `build.gradle` 文件的 **Dependencies** 部分。添加 {{site.data.keyword.amashort}} 客户端 SDK 的编译依赖关系：

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'core',
        version: '1.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
}
```

1. 使用 Gradle 同步项目。单击**工具 &gt; Android &gt; 使用 Gradle 文件同步项目**。

1. 打开 Android 项目的 `AndroidManifest.xml` 文件。在 `<manifest>` 元素下添加因特网访问许可权：

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
```

## 初始化 {{site.data.keyword.amashort}} 客户端 SDK
{: #initalize-mca-sdk}

通过将 context、applicationGUID 和 applicationRoute 参数传递到 `initialize` 方法来初始化 SDK。


1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”的主页中，单击您的应用程序。单击**移动选项**。您需要**应用程序路径**和**应用程序 GUID** 值来初始化 SDK。

2. 初始化 Android 应用程序中的 {{site.data.keyword.amashort}} 客户端 SDK。在 Android 应用程序中，通常会将初始化代码放置在主 Activity 的 `onCreate` 方法中，但这不是强制性的。
<br/>将 *applicationRoute* 和 *applicationGUID* 替换为 {{site.data.keyword.Bluemix_notm}}“仪表板”中**移动选项**中的值。

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");
```


## 对移动后端发起请求
{: #request}

初始化 {{site.data.keyword.amashort}} 客户端 SDK 后，可以开始对移动后端发起请求。

1. 尝试对新移动后端的受保护端点发送请求。在浏览器中，打开以下 URL：`{applicationRoute}/protected`。例如：`http://my-mobile-backend.mybluemix.net/protected`
<br/>使用 MobileFirst Services Starter 样板创建的移动后端的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护。由于此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问，因此会在浏览器中返回 `Unauthorized` 消息。

1. 使用 Android 应用程序对同一端点发起请求。初始化 `BMSClient` 后，添加以下代码：

	```Java
	Request request = new Request("/protected", Request.GET);
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

1. 请求成功后，将在 LogCat 实用程序中看到以下输出：

	![图像](images/getting-started-android-success.png)

## 后续步骤
{: #next-steps}

连接到受保护端点时，无需任何凭证。如果需要用户登录到您的应用程序，那么必须配置 Facebook、Google 或定制认证。
* [Facebook](facebook-auth-android.html)
* [Google](google-auth-android.html)
* [定制](custom-auth-android.html)
