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


# 使用 Android 應用程式檢測 MQA（已淘汰）
{: #instrumentAnd}


若要使用 {{site.data.keyword.mqafull}} 搭配 Android 應用程式，您必須下載 SDK 並使用 Android Studio 開發環境進行一些變更來加以檢測。
{: shortdesc}

使用 {{site.data.keyword.mqa}} 檢測應用程式之前，您必須有 {{site.data.keyword.Bluemix}} 帳戶，以及適合要檢測之應用程式平台的正確安裝開發環境版本。

若要檢測 {{site.data.keyword.mqa}} 以便搭配 Android 應用程式使用，請完成下列作業：

1. 將必要的許可權和已下載的 SDK 新增至您的 Android 專案。

	1. 在 Android Studio 中開啟專案。
	
	2. 選取 **File** > **New** > **New Module**。
	
	3. 在 *Create New Module* 精靈的 *More Modules* 下，選取 **Import .JAR or .AAR Package**，然後按一下 **Next**。
	
	4. 在檔名欄位中，輸入您下載之 {{site.data.keyword.mqa}} SDK .aar 檔案的名稱，然後按一下 **Finish**。
	
	5. 選取 **File** > **Project Structure**，在 Android Studio 專案中開始新增 {{site.data.keyword.mqa}} 至您的行動應用程式。
	
	6. 在 Project Structure 視窗中選取應用程式的模組，然後選取 *Dependencies* 標籤。
	
	7. 選取 **+**，然後選取 **Module Dependency**。
	
	8. 在 Choose Modules 視窗中，選取您匯入的 {{site.data.keyword.mqa}} Android 模組，然後按一下 **OK**。
	
	9. 選取 **OK** 以關閉 Project Structure 視窗。
	
	10. 更新 Android 資訊清單檔，確定下列活動已包含在 `<application>` 項目中：
	    
		```
		<activity android:name="com.ibm.mqa.ui.ProblemActivity" />
		<activity android:name="com.ibm.mqa.ui.FeedbackActivity" />
		<activity android:name="com.ibm.mqa.ui.ScreenshotEditorActivity" />
		```
		{: codeblock}
	   
	11. 確定下列必要的許可權已列在資訊清單檔中：
	
		```
		<uses-permission android:name="android.permission.INTERNET" /> 
		<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
		<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
		```
		{: codeblock}
   
	下列程式碼顯示 `AndroidManifest.xml` 檔案的可能範例：

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

2. 配置新的階段作業，以開始進行每個登入。

	1. 將下列程式碼 snippet 新增至您應用程式的 `MainActivity` 類別，它位於 `MainActivity.java` 檔案。它使用您的應用程式索引鍵傳送資料給 {{site.data.keyword.mqa}}。
		 
		```
		public static final String APP_KEY = "Your_Application_Key_Goes_Here";
		```
		{: codeblock}
		
		將 *Your_Application_Key_Goes_Here* 取代為來自 {{site.data.keyword.mqa}} App Settings 頁面的應用程式索引鍵。
	
	2. 若要使用 {{site.data.keyword.mqa}} 配置建置器，請先將下列項目新增至應用程式的 `MainActivity.java` 檔來匯入它們： 
		
		```
		import com.ibm.mqa.MQA;
		import com.ibm.mqa.MQA.Mode;
		import com.ibm.mqa.config.Configuration;
		```
		{: codeblock}
		
	3. 在 MainActivity 類別的 onCreate 事件中建立配置物件。這個物件提供數個方法，您可用來指定配置項目。在終結物件配置時，請呼叫 build() 方法來終結物件。完整配置的範例如下所示：
	
		```
		Configuration configuration = new Configuration.Builder(this)
		.withAPIKey(APP_KEY) //Provides the quality assurance application APP_KEY
		.withMode(Mode.QA) //Selects the quality assurance application mode
		.build();
		```
		{: codeblock}
	
	4. 在應用程式的 Application 類別，新增程式碼，以藉由呼叫 Application 類別的 `onCreate` 事件中的 `MQA.startNewSession()` 方法，配置並啟動 {{site.data.keyword.mqa}} 階段作業。
	
	    例如： 
		   
		```
		MQA.startNewSession(this, configuration);
		```
		{: codeblock}

        延伸的範例：

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

3. 繼續執行[開始使用 {{site.data.keyword.mqa}}](index.html) 頁面上的步驟。


# 相關鏈結
{: #rellinks notoc}

## 相關鏈結
{: #general notoc}
* [開始使用 {{site.data.keyword.mqa}}](index.html){:new_window}
