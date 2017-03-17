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


# Android アプリでの MQA の装備 (非推奨)
{: #instrumentAnd}


Android アプリで {{site.data.keyword.mqafull}} を使用するには、SDK をダウンロードし、Android Studio 開発環境を使用していくつかの変更を行って装備する必要があります。
{: shortdesc}

アプリに {{site.data.keyword.mqa}} を装備するには、事前に {{site.data.keyword.Bluemix}} アカウントを取得し、装備するアプリのプラットフォームに対応するバージョンの開発環境を正しくインストールしておく必要があります。

Android アプリと連携するように {{site.data.keyword.mqa}} を装備するには、以下のタスクを実行します。

1. 必要な許可、およびダウンロードした SDK を Android プロジェクトに追加します。

	1. Android Studio でプロジェクトを開きます。
	
	2. **「File」** > **「New」** > **「New Module」**を選択します。
	
	3. 「*Create New Module*」ウィザードの「*More Modules*」で、**「Import .JAR or .AAR Package」**を選択して、**「Next」**をクリックします。
	
	4. 「File name」フィールドに、ダウンロードした {{site.data.keyword.mqa}} SDK .aar ファイルの名前を入力して、**「Finish」**をクリックします。
	
	5. **「File」** > **「Project Structure」**を選択して、Android Studio プロジェクト内のモバイル・アプリへの {{site.data.keyword.mqa}} の追加を開始します。
	
	6. 「Project Structure」ウィンドウでアプリ用のモジュールを選択し、「*Dependencies*」タブを選択します。
	
	7. **「+」**を選択し、次に**「Module Dependency」**を選択します。
	
	8. 「Choose Modules」ウィンドウで、インポートした {{site.data.keyword.mqa}} Android モジュールを選択して、**「OK」**をクリックします。
	
	9. **「OK」**を選択して「Project Structure」ウィンドウを閉じます。
	
	10. 以下のアクティビティーが `<application>` エントリーに含まれていることを確認して、Android マニフェスト・ファイルを更新します。
	    
		```
		<activity android:name="com.ibm.mqa.ui.ProblemActivity" />
		<activity android:name="com.ibm.mqa.ui.FeedbackActivity" />
		<activity android:name="com.ibm.mqa.ui.ScreenshotEditorActivity" />
		```
		{: codeblock}
	   
	11. 以下の必須の許可がマニフェスト・ファイルにリストされていることを確認します。
	
		```
		<uses-permission android:name="android.permission.INTERNET" />
		<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
		<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
		```
		{: codeblock}
   
	以下のコードは、`AndroidManifest.xml` ファイルの可能なサンプルを示しています。

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

2. ログインごとに新規セッションを開始するように構成します。

	1. アプリの `MainActivity.java` ファイル内にある `MainActivity` クラスに、以下のコード・スニペットを追加します。これは、アプリケーション・キーを使用してデータを {{site.data.keyword.mqa}} に送信します。
		 
		```
		public static final String APP_KEY = "Your_Application_Key_Goes_Here";
		```
		{: codeblock}
		
		*Your_Application_Key_Goes_Here* を、{{site.data.keyword.mqa}} の「アプリの設定 (App Settings)」ページにあるアプリケーション・キーに置き換えます。
	
	2. {{site.data.keyword.mqa}} 構成ビルダーを使用するには、まず以下の項目をアプリの `MainActivity.java` ファイルに追加して、これらの項目をインポートします。 
		
		```
		import com.ibm.mqa.MQA;
		import com.ibm.mqa.MQA.Mode;
		import com.ibm.mqa.config.Configuration;
		```
		{: codeblock}
		
	3. MainActivity クラスの onCreate イベント内に構成オブジェクトを作成します。このオブジェクトは、構成項目の指定に使用できるいくつかのメソッドを提供します。オブジェクトの構成の終わりに、build() メソッドを呼び出して、オブジェクトをファイナライズします。完全な構成の例を以下に示します。
	
		```
		Configuration configuration = new Configuration.Builder(this)
		.withAPIKey(APP_KEY) //Provides the quality assurance application APP_KEY
		.withMode(Mode.QA) //Selects the quality assurance application mode
		.build();
		```
		{: codeblock}
	
	4. アプリの Application クラスで、Application クラスの `onCreate` イベント内の `MQA.startNewSession()` メソッドを呼び出すことにより {{site.data.keyword.mqa}} セッションを構成して開始するコードを追加します。
	
	    例: 
		   
		```
		MQA.startNewSession(this, configuration);
		```
		{: codeblock}

        拡張された例:

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

3. [{{site.data.keyword.mqa}} の開始](index.html)ページのステップを続けます。


# 関連リンク
{: #rellinks notoc}

## 関連リンク
{: #general notoc}
* [{{site.data.keyword.mqa}} の開始](index.html){:new_window}
