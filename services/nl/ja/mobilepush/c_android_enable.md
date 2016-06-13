---

copyright:
 years: 2015 2016

---


# Android アプリケーションによるプッシュ通知受け取りの可能化
{: #tag_based_notifications}


Android アプリケーションによるプッシュ通知の受け取りとデバイスへのプッシュ通知の送信を可能にします。

## Gradle を使用したクライアント Push SDK のインストール
{: #android_install}

このセクションでは、Android アプリケーションをさらに開発するためにクライアント Push SDK をインストールして使用する方法について説明します。

Bluemix® モバイル・サービスの Push SDK は、Gradle を使用して追加できます。Gradle は自動的に成果物をリポジトリーからダウンロードして、Android アプリケーションで使用できるようにします。Android Studio および Android Studio SDK を正しくセットアップしてください。システムのセットアップ方法について詳しくは、[Android Studio 概要](https://developer.android.com/tools/studio/index.html)を参照してください。Gradle については、[Configuring Gradle Builds](http://developer.android.com/tools/building/configuring-gradle.html) を参照してください。

1. Android Studio で、モバイル・アプリケーションを作成して開いてから、アプリケーションの **build.gradle** ファイルを開きます。次に、以下の依存関係をモバイル・アプリケーションに追加します。これらの import ステートメントは、コード・スニペットに必要です。

	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```


1. 以下の依存関係をモバイル・アプリケーションに追加します。以下のコード行により、Bluemix™ Mobile Services Push クライアント SDK と Google Play サービス SDK をコンパイル有効範囲の依存関係に追加します。

	```
	dependencies {
	  compile 'com.ibm.mobilefirstplatform.clientsdk.android:push:1.+' 
compile 'com.google.android.gms:play-services:7.8.0' 
}  
	```
1. **AndroidManifest.xml** ファイルに、以下のアクセス権を追加します。サンプル・マニフェストを表示するには、[Android helloPush Sample Application (Android helloPush サンプル・アプリケーション)](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml)を参照してください。 サンプル Gradle ファイルを表示するには、[Sample Build Gradle file (サンプル Build Gradle ファイル)](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle) を参照してください。

	```
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="com.ibm.clientsdk.android.app.permission.C2D_MESSAGE" />
	<uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
<uses-permission android:name="android.permission.GET_ACCOUNTS" />
<uses-permission android:name="android.permission.USE_CREDENTIALS" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
	```

	ここに、[Android のアクセス権](http://developer.android.com/guide/topics/security/permissions.html)の詳しい説明があります。

1. アクティビティーの通知インテント設定を追加します。この設定により、ユーザーが通知エリアで受信した通知をクリックすると、アプリケーションが開始します。

	```
	<intent-filter>  
		<action android:name="<Your_Android_Package_Name.IBMPushNotification"/>   
		<category  android:name="android.intent.category.DEFAULT"/>
	</intent-filter>
	```
	**注**: 上記のアクション内の *Your_Android_Package_Name* を、アプリケーションで使用されているアプリケーション・パッケージ名に置き換えてください。

1. RECEIVE イベント通知のための Google Cloud Messaging (GCM) インテント・サービスおよびインテント・フィルターを追加します。

	```
	service android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushIntentService" />

	<receiver
	    android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.internal.MFPPushBroadcastReceiver"
	    android:permission="com.google.android.c2dm.permission.SEND">
	    <intent-filter>
	        <action android:name="com.google.android.c2dm.intent.RECEIVE" />

	        <category android:name="com.ibm.mobilefirstplatform.clientsdk.android.app" />
	    </intent-filter>
	    <intent-filter>
	        <action android:name="android.intent.action.BOOT_COMPLETED" />

	        <category android:name="com.ibm.mobilefirstplatform.clientsdk.android.app" />
	    </intent-filter>
	</receiver>
	```


## Android アプリ用の Push SDK の初期化
{: #android_initialize}

初期化コードを配置する一般的な場所は、Android アプリケーション内のメインアクティビティーの onCreate メソッド内です。

Bluemix アプリケーション・ダッシュボード内の**「モバイル・オプション」**リンクをクリックして、アプリケーション経路とアプリケーション GUID を取得します。これらの値を、経路とアプリ GUID に使用します。コード・スニペットを変更して、Bluemix アプリの appRoute パラメーターと appGUID パラメーターを使用するようにします。


###Core SDK を初期化します。

```
// Initialize the SDK for Java (Android) with IBM Bluemix AppGUID and route
BMSClient.getInstance().initialize(getApplicationContext(), "applicationRoute","applicationGUID", bluemixRegion:"Location where your app Hosted");
```


**appRoute**

Bluemix で作成したサーバー・アプリケーションに割り当てられた経路を指定します。

**AppGUID**

Bluemix で作成したアプリケーションに割り当てられた固有キーを指定します。この値では、大/小文字が区別されます。

**bluemixRegionSuffix**

アプリがホストされている場所を指定します。次の 3 つの値のいずれかを使用できます。

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

###クライアント Push SDK を初期化します。

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext());
```

## Android デバイスの登録
{: #android_register}

```IMFPush.register()``` API を使用して、Push Notification Service にデバイスを登録します。Android デバイスを登録する場合、まず、Google Cloud Messaging (GCM) 情報を Bluemix プッシュ・サービス構成ダッシュボードに追加します。詳しくは、[Google Cloud Messaging の資格情報の構成](t_push_provider_android.html)を参照してください。

以下のコード・スニペットを Android モバイル・アプリケーションにコピーして貼り付けます。


```
	//Register Android devices
	push.register(new MFPPushResponseListener<String>() {
	    @Override
	    public void onSuccess(String deviceId) {
	           //handle success here
	    }
	    @Override
    public void onFailure(MFPPushException ex) {
         //handle failure here
	    }
	});
```

```
	//Handles the notification when it arrives
	MFPPushNotificationListener notificationListener = new MFPPushNotificationListener() {
	    @Override
	    public void onReceive (final MFPSimplePushNotification message){
	      // Handle Push Notification
	    }
	};
```


## Android デバイスでのプッシュ通知の受け取り
{: #android_receive}

notificationListener オブジェクトを Push に登録するには、**MFPPush.listen()** メソッドを呼び出します。このメソッドは通常、プッシュ通知を処理しているアクティビティーの **onResume()** メソッドから呼び出されます。

1. notificationListener オブジェクトを Push に登録するには、**listen()** メソッドを呼び出します。このメソッドは通常、プッシュ通知を処理しているアクティビティーの **onResume()** メソッドから呼び出されます。

	```
	@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
	       push.listen(notificationListener);
	   }
	}
```
2. プロジェクトをビルドし、デバイスまたはエミュレーター上で実行します。register() メソッド内で応答リスナーに onSuccess() メソッドを呼び出す際に、デバイスが Push Notification Service に正常に登録されていることを確認します。この時点で、『基本プッシュ通知の送信』に説明されている方法でメッセージを送信できます。
3. デバイスが通知を受信していることを確認します。アプリケーションがフォアグラウンドにある場合は、通知は **MFPPushNotificationListener** により処理されます。アプリケーションがバックグラウンドにある場合は、メッセージが通知バーに表示されます。



## 基本プッシュ通知の送信
{: #send}

アプリケーションを開発したら、(タグ、バッジ、追加のペイロード、音声ファイルを使用することなく) 基本プッシュ通知を送信できます。


基本プッシュ通知の送信を行います。

1. **「対象者の選択 (Choose the Audience)」**で、**「すべてのデバイス (All Devices)」**、またはプラットフォームに従って**「iOS デバイスのみ (Only iOS devices)」**または**「Android デバイスのみ (Only Anroid devices)」**のいずれかの対象者を選択します。 
	**注**: **「すべてのデバイス (All Devices)」**オプションを選択すると、プッシュ通知をサブスクライブしているすべてのデバイスが通知を受け取ることになります。


	![「通知」画面](images/tag_notification.jpg)

2. **「通知の作成 (Create your Notification)」**で、メッセージを入力して、**「送信」**をクリックします。
3. デバイスが通知を受信していることを確認します。

	次のスクリーン・ショットは、Android デバイスおよび iOS デバイス上のフォアグラウンドでプッシュ通知を処理しているアラート・ボックスを示しています。

	![Android 上のフォアグラウンドのプッシュ通知](images/Android_Screenshot.jpg)

	![iOS 上のフォアグラウンドのプッシュ通知](images/iOS_Screenshot.jpg)

	次のスクリーン・ショットは、Android のバックグラウンドでのプッシュ通知を示しています。
	![Android 上のバックグラウンドのプッシュ通知](images/background.jpg)



## 次のステップ
{: #next_steps_tags}

基本通知を正常にセットアップしたら、タグ・ベースの通知および詳細オプションの構成を行うことができます。


以下の Push Notifications Service の機能をご使用のアプリに追加します。タグ・ベースの通知を使用する場合は、[タグ・ベースの通知](c_tag_basednotifications.html)を参照してください。
拡張通知オプションを使用する場合は、[拡張プッシュ通知](t_advance_notifications.html)を参照してください。
