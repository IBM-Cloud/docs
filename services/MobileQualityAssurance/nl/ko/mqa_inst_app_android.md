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


# Android 앱을 사용하여 MQA 인스트루먼트(더 이상 사용되지 않음)
{: #instrumentAnd}


{{site.data.keyword.mqafull}}를 Android 앱과 함께 사용하려면, SDK를 다운로드하고 Android Studio 개발 환경에서 몇 가지 변경사항을 작성하여 이를 인스트루먼트해야 합니다.
{: shortdesc}

{{site.data.keyword.mqa}}를 사용하여 앱을 인스트루먼트할 수 있으려면 {{site.data.keyword.Bluemix}} 계정이 있어야 하며 인스트루먼트하는 앱의 플랫폼에 대한 배치 환경의 버전이 올바르게 설치되어 있어야 합니다. 

Android 앱과 작동하도록 {{site.data.keyword.mqa}}를 인스트루먼트하려면, 다음 태스크를 완료하십시오. 

1. 필수 권한 및 다운로드한 SDK를 Android 프로젝트에 추가하십시오. 

	1. Android Studio에서 프로젝트를 여십시오. 
	
	2. **파일** > **새로 작성** > **새 모듈**을 선택하십시오. 
	
	3. *새 모듈 작성* 마법사의 *추가 모듈* 아래에서 **.JAR 또는 .AAR 패키지 가져오기**를 선택한 후 **다음**을 클릭하십시오. 
	
	4. 파일 이름 필드에서 다운로드한 {{site.data.keyword.mqa}} SDK .aar 파일의 이름을 입력하고 **완료**를 클릭하십시오. 
	
	5. **파일** > **프로젝트 구조**를 선택하여 Android Studio 프로젝트의 모바일 앱에 {{site.data.keyword.mqa}}를 추가하십시오. 
	
	6. 프로젝트 구조 창에서 앱에 대한 모듈을 선택하고 *종속 항목* 탭을 선택하십시오. 
	
	7. **+**를 선택한 후 **모듈 종속 항목**을 선택하십시오. 
	
	8. 모듈 선택 창에서, 가져온 {{site.data.keyword.mqa}} Android 모듈을 선택한 후 **확인**을 클릭하십시오. 
	
	9. 프로젝트 구조 창을 닫으려면 **확인**을 선택하십시오. 
	
	10. 다음 활동이 `<application>` 항목에 포함되도록 Android Manifest 파일을 업데이트하십시오. 
	    
		```
		<activity android:name="com.ibm.mqa.ui.ProblemActivity" />
		<activity android:name="com.ibm.mqa.ui.FeedbackActivity" />
		<activity android:name="com.ibm.mqa.ui.ScreenshotEditorActivity" />
		```
		{: codeblock}
	   
	11. 다음 필수 권한이 Manifest 파일에 나열되어 있는지 확인하십시오. 
	
		```
		<uses-permission android:name="android.permission.INTERNET" /> 
		<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
		<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
		```
		{: codeblock}
   
	다음 코드는 `AndroidManifest.xml` 파일의 가능한 샘플을 표시합니다. 

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

2. 로그인할 때마다 시작하도록 새 세션을 구성하십시오. 

	1. `MainActivity.java` 파일에 있는 앱의 `MainActivity` 클래스에 다음 코드 스니펫을 추가하십시오. 데이터를 {{site.data.keyword.mqa}}에 전송하는 데 애플리케이션 키를 사용합니다. 
		 
		```
		public static final String APP_KEY = "Your_Application_Key_Goes_Here";
		```
		{: codeblock}
		
		*Your_Application_Key_Goes_Here*을 {{site.data.keyword.mqa}} 앱 설정 페이지의 애플리케이션 키로 대체하십시오. 
	
	2. {{site.data.keyword.mqa}} 구성 빌더를 사용하려면 먼저 다음 항목을 앱의 `MainActivity.java` 파일에 추가하여 항목을 가져오십시오.  
		
		```
		import com.ibm.mqa.MQA;
		import com.ibm.mqa.MQA.Mode;
		import com.ibm.mqa.config.Configuration;
		```
		{: codeblock}
		
	3. MainActivity 클래스의 onCreate 이벤트에서 구성 오브젝트를 작성하십시오. 이 오브젝트는 구성 항목을 지정하는 데 사용할 수 있는 몇 가지 메소드를 제공합니다. 오브젝트 구성의 끝부분에서 build() 메소드를 호출하여 오브젝트를 완료합니다. 전체 구성의 예는 다음과 같습니다. 
	
		```
		Configuration configuration = new Configuration.Builder(this)
		.withAPIKey(APP_KEY) //Provides the quality assurance application APP_KEY
		.withMode(Mode.QA) //Selects the quality assurance application mode
		.build();
		```
		{: codeblock}
	
	4. 앱의 애플리케이션 클래스에서, 애플리케이션 클래스의 `onCreate` 이벤트에 있는 `MQA.startNewSession()` 메소드를 호출하여 {{site.data.keyword.mqa}} 세션을 구성 및 시작하도록 코드를 추가하십시오. 
	
	    예제:  
		   
		```
		MQA.startNewSession(this, configuration);
		```
		{: codeblock}

        확장 예제: 

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

3. [{{site.data.keyword.mqa}} 시작하기](index.html) 페이지의 단계를 계속하십시오. 


# 관련 링크
{: #rellinks notoc}

## 관련 링크
{: #general notoc}
* [{{site.data.keyword.mqa}} 시작하기](index.html){:new_window}
