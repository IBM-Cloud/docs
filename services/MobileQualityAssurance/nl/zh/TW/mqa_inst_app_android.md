---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 对 MQA 安装 Android 应用程序（已弃用）
{: #instrumentAnd}


要搭配使用 {{site.data.keyword.mqafull}} 和 Android 应用程序，必须下载 SDK，并使用 Android Studio 开发环境，进行一些更改，以对其执行安装操作。
{: shortdesc}

您必须具有 {{site.data.keyword.Bluemix}} 帐户并为执行安装操作的应用程序平台正确安装了开发环境版本，才能对应用程序安装 {{site.data.keyword.mqa}}。

要对 {{site.data.keyword.mqa}} 执行安装操作以使用 Android 应用程序，请完成以下任务：

1. 将所需许可权和已下载的 SDK 添加到 Android 项目。

	1. 在 Android Studio 中打开项目。
	
	2. 选择**文件** > **新建** > **新建模块**。
	
	3. 在*创建新模块*向导的*更多模块*下，选择**导入 .JAR 或 .AAR 包**，然后单击**下一步**。
	
	4. 在“文件名”字段中，输入所下载的 {{site.data.keyword.mqa}} SDK .aar 文件的名称，然后单击**完成**。
	
	5. 通过选择**文件** > **项目结构**，开始在 Android Studio 项目中，将 {{site.data.keyword.mqa}} 添加到移动应用程序。
	
	6. 在“项目结构”窗口中选择应用程序的模块，然后选择*依赖关系*选项卡。
	
	7. 选择 **+**，然后选择**模块依赖关系**。
	
	8. 在“选择模块”窗口中，选择导入的 {{site.data.keyword.mqa}} Android 模块，然后单击**确定**。
	
	9. 选择**确定**以关闭“项目结构”窗口。
	
	10. 确保 `<application>` 条目中包含以下活动，以更新 Android 清单文件：
	    
		```
		<activity android:name="com.ibm.mqa.ui.ProblemActivity" />
		<activity android:name="com.ibm.mqa.ui.FeedbackActivity" />
		<activity android:name="com.ibm.mqa.ui.ScreenshotEditorActivity" />
		```
		{: codeblock}
	   
	11. 确保清单文件中列出以下所需的许可权：
	
		```
		<uses-permission android:name="android.permission.INTERNET" /> 
		<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
		<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
		```
		{: codeblock}
   
	以下代码显示 `AndroidManifest.xml` 文件的可能示例：

		```
		<?xml version="1.0" encoding="utf-8"?>
        <manifest xmlns:android=
		  "http://schemas.android.com/apk/res/android"
        package="com.applause.android"
        android:versionCode="6"
        android:versionName="2.3" >

        <uses-sdk android:minSdkVersion="8" />

        <!-- Required permission -->
        <uses-permission android:name=
		  "android.permission.INTERNET" /> 
        <uses-permission android:name=
		  "android.permission.READ_EXTERNAL_STORAGE" />
        <uses-permission android:name=
		  "android.permission.SYSTEM_ALERT_WINDOW" /> 

        <!-- Optional permissions -->
  
        <uses-permission android:name=
		  "android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name=
		  "android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name=
		  "android.permission.READ_PHONE_STATE" />
        <uses-permission android:name=
		  "android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name=
		  "android.permission.ACCESS_FINE_LOCATION" />
        <uses-permission android:name=
		  "android.permission.BLUETOOTH" />
        <!-- ... rest of your application's 
		  permissions, if any -->

        <application
        android:icon="@drawable/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/AppTheme"
        android:name=".MyApplication' >

        <!-- ... rest of your application's components -->

        <!-- Quality assurance application activities -->
        <activity android:name=
		  "com.ibm.mqa.ui.ProblemActivity" />
        <activity android:name=
		  "com.ibm.mqa.ui.FeedbackActivity" />
        <activity android:name=
		  "com.ibm.mqa.ui.ScreenshotEditorActivity" /> 
        </application>

        </manifest>
		```
	    {: codeblock}

2. 配置新会话以开始执行每个登录。

	1. 将以下代码片段添加到应用程序的 `MainActivity` 类中，该类位于 `MainActivity.java` 文件中。它使用应用程序密钥，将数据发送到 {{site.data.keyword.mqa}}。
		 
		```
		public static final String APP_KEY = "Your_Application_Key_Goes_Here";
		```
		{: codeblock}
		
		将 *Your_Application_Key_Goes_Here* 替换为来自 {{site.data.keyword.mqa}}“应用程序设置”页面的应用程序密钥。
	
	2. 要使用 {{site.data.keyword.mqa}} 配置构建器，首先通过将以下项添加到应用程序的 `MainActivity.java` 文件中，以导入这些项： 
		
		```
		import com.ibm.mqa.MQA;
		import com.ibm.mqa.MQA.Mode;
		import com.ibm.mqa.config.Configuration;
		```
		{: codeblock}
		
	3. 在 MainActivity 类的 onCreate 事件中创建配置对象。此对象提供可用来指定配置项的几种方法。在完成配置对象时，调用 build() 方法，以最终完成对象。完整配置的示例如下所示：
	
		```
		Configuration configuration = new Configuration.Builder(this)
		.withAPIKey(APP_KEY) //Provides the quality assurance application APP_KEY
		.withMode(Mode.QA) //Selects the quality assurance application mode
		.build();
		```
		{: codeblock}
	
	4. 在应用程序的 Application 类中，添加代码以配置并启动 {{site.data.keyword.mqa}} 会话，方法是在 Application 类的 `onCreate` 事件中调用 `MQA.startNewSession()` 方法。
	
	    例如： 
		   
		```
		MQA.startNewSession(this, configuration);
		```
		{: codeblock}

        扩展示例：

		<pre><code>
		// import Android class
        import android.app.Application;

        // Make sure that you import the quality assurance 
		  application
        import com.ibm.mqa.MQA;
        import com.ibm.mqa.MQA.Mode;
        import com.ibm.mqa.config.Configuration;

        // Optionally import the quality assurance 
		  application's logging functions
        import com.ibm.mqa.Log;

        public class MyApplication extends Application {
 
	    public static final String APP_KEY = 
		  "Your_Application_Key_Goes_Here";
 
	    @Override
	    public void onCreate() {
		super.onCreate();
		 
		Configuration configuration = new 
		  Configuration.Builder(this)
		.withAPIKey(APP_KEY) //Provides the quality assurance 
		  application APP_KEY
		.withMode(Mode.QA) //Selects the quality assurance 
		  production mode.  This example is for preproduction mode, 
		//Use .withMode(Mode.MARKET) for production mode. 
		.build();
 
		MQA.startNewSession(this, configuration);
	       }
             }
		</code></pre>
		{: codeblock}

3. 继续 [{{site.data.keyword.mqa}} 入门](index.html)页面上的步骤。


# 相关链接
{: #rellinks notoc}

## 相关链接
{: #general notoc}
* [{{site.data.keyword.mqa}} 入门](index.html){:new_window}
