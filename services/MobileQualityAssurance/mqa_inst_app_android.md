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


# Instrumenting MQA with an Android app (Deprecated)
{: #instrumentAnd}


To use {{site.data.keyword.mqafull}} with your Android app, you must download the SDK and instrument it by making some changes using the Android Studio development environment. 
{: shortdesc}

Before you can instrument an app with {{site.data.keyword.mqa}}, you must have a {{site.data.keyword.Bluemix}} account and the correctly installed version of the development environment for the platforms of the app that you are instrumenting.

To instrument {{site.data.keyword.mqa}} to work with your Android app, complete the following tasks:

1. Add the required permissions and downloaded SDK to your Android project.

	1. Open your project in Android Studio.
	
	2. Select **File** > **New** > **New Module**.
	
	3. In the *Create New Module* wizard, under *More Modules*, select **Import .JAR or .AAR Package**, and then click **Next**.
	
	4. In the File name field, enter the name of the {{site.data.keyword.mqa}} SDK .aar file that you downloaded and click **Finish**.
	
	5. Begin adding {{site.data.keyword.mqa}} to your mobile app in your Android Studio project by selecting **File** > **Project Structure**.
	
	6. Select the module for your app in the Project Structure window, and select the *Dependencies* tab.
	
	7. Select **+**, and then select **Module Dependency**.
	
	8. In the Choose Modules window, select the {{site.data.keyword.mqa}} Android module that you imported, and then click **OK**.
	
	9. Select **OK** to close the Project Structure window.
	
	10. Update the Android manifest file by ensuring that the following activities are included in an `<application>` entry:
	    
		```
		<activity android:name="com.ibm.mqa.ui.ProblemActivity" />
		<activity android:name="com.ibm.mqa.ui.FeedbackActivity" />
		<activity android:name="com.ibm.mqa.ui.ScreenshotEditorActivity" />
		```
		{: codeblock}
	   
	11. Ensure that the following required permissions are listed in the manifest file:
	
		```
		<uses-permission android:name="android.permission.INTERNET" /> 
		<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
		<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
		```
		{: codeblock}
   
	The following code shows a possible sample of your `AndroidManifest.xml` file:

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

2. Configure a new session to start with each log in.

	1. Add the following code snippet to the `MainActivity` class of your app, which is in the `MainActivity.java` file. It uses your application key to send data to {{site.data.keyword.mqa}}.
		 
		```
		public static final String APP_KEY = "Your_Application_Key_Goes_Here";
		```
		{: codeblock}
		
		Replace *Your_Application_Key_Goes_Here* with your application key from the App Settings page of {{site.data.keyword.mqa}}.
	
	2. To use the {{site.data.keyword.mqa}} configuration builder, first import the following items by adding them to the `MainActivity.java` file of your app: 
		
		```
		import com.ibm.mqa.MQA;
		import com.ibm.mqa.MQA.Mode;
		import com.ibm.mqa.config.Configuration;
		```
		{: codeblock}
		
	3. Create a configuration object in the onCreate event of your MainActivity class. This object provides several methods that you can use to specify configuration items. At the conclusion of configuring the object, you call a build() method to finalize the object. An example of a complete configuration follows:
	
		```
		Configuration configuration = new Configuration.Builder(this)
		.withAPIKey(APP_KEY) //Provides the quality assurance application APP_KEY
		.withMode(Mode.QA) //Selects the quality assurance application mode
		.build();
		```
		{: codeblock}
	
	4. In the Application class of your app, add code to configure and start {{site.data.keyword.mqa}} sessions by calling the `MQA.startNewSession()` method in the `onCreate` event of your Application class.
	
	    For example: 
		   
		```
		MQA.startNewSession(this, configuration);
		```
		{: codeblock}

        Extended example:

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

3. Continue with the steps on the [Getting started with {{site.data.keyword.mqa}}](index.html) page.


# Related Links
{: #rellinks notoc}

## Related Links
{: #general notoc}
* [Getting started with {{site.data.keyword.mqa}}](index.html){:new_window}