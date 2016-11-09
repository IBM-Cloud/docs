---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"
---
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Cordova アプリ用の Facebook 認証の使用可能化
{: #facebook-auth-cordova}


{{site.data.keyword.amafull}} Cordova アプリケーションを Facebook 認証統合用に構成するには、Cordova アプリケーションのネイティブ・コード (Java、Objective-C、または Swift) を変更します。各プラットフォームは別々に構成します。この Cordova アプリケーションには既に {{site.data.keyword.amashort}} SDK が装備されている必要があります。 


ネイティブ・コードの変更は、Android Studio や Xcode などのネイティブ開発環境で行ってください。

{:shortdesc}

## 開始する前に
{: #facebook-auth-before}
以下が必要です。
* {{site.data.keyword.amashort}} Client SDK が装備された Cordova プロジェクト。[Cordova プラグインのセットアップ](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)を参照してください。
* {{site.data.keyword.amashort}} サービスによって保護された {{site.data.keyword.Bluemix_notm}} アプリケーションのインスタンス。{{site.data.keyword.Bluemix_notm}} バックエンド・アプリケーションの作成方法について詳しくは、[概説](index.html)を参照してください。
* Facebook App ID。詳しくは、『[Facebook for Developers Web サイトからの Facebook App ID の取得](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)』を参照してください。



## Android プラットフォームの構成
{: #facebook-auth-cordova-android}

Cordova アプリケーションの Android プラットフォームを Facebook 認証統合用に構成するために必要なステップは、ネイティブ Android アプリケーションの場合とよく似ています。詳しくは、[Android アプリで Facebook 認証を使用可能にする](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html)を参照してください。以下のステップを完了してください:

* Android プラットフォーム用の Facebook アプリケーションの構成
* Facebook 認証用の {{site.data.keyword.amashort}} の構成

### Android 用の {{site.data.keyword.amashort}} Client SDK の構成

Cordova アプリケーション内の Android 用の {{site.data.keyword.amashort}} Client SDK を構成します。

1. Android プロジェクト・フォルダーで、アプリケーション・モジュールの `build.gradle` ファイルを開きます (プロジェクト `build.gradle` ファイル**ではありません**)。依存関係セクションを見つけ、Client SDK の新しいコンパイル依存関係を追加します。

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
     		name:'facebookauthentication',
     		version: '1.+',
     		ext: 'aar',
     		transitive: true
     		// other dependencies  
		 }
	```
	
2. **「ツール」>「Android」>「プロジェクトを Gradle ファイルと同期 (Sync Project with Gradle Files)」**をクリックして Gradle とプロジェクトを同期します。

3. `android/res/values/strings.xml` ファイルを開いて、Facebook App ID が入った `facebook_app_id` ストリングを追加します。

	```XML
	<resources>
		<string name="app_name">HelloCordova</string>
		<string name="launcher_name">@string/app_name</string>
		<string name="activity_name">@string/launcher_name</string>
		<string name="facebook_app_id">522733366802111</string>
	</resources>
	```
	
4. Android プロジェクトの `AndroidManifest.xml` ファイル (`android/manifests/AndroidManifest.xml`) で、以下を実行します。

	* Facebook SDK に必要なメタデータを <application> エレメントに追加します。

	```XML
	<application .......>

		<meta-data
			android:name="com.facebook.sdk.ApplicationId"
			android:value="@string/facebook_app_id"/>

		<activity ...../>
		<activity ...../>
	</application>
	```

	* 既存のアクティビティーの下に Facebook Activity エレメントを追加します。

	```XML
	<application .....>
		<activity ...../>
		<activity ...../>
	<activity   android:name="com.facebook.FacebookActivity"
	              android:configChanges="keyboard|keyboardHidden|screenLayout|screenSize|orientation"
	              android:theme="@android:style/Theme.Translucent.NoTitleBar"
	              android:label="@string/app_name" 
			    />
	</application>
	```

2. Cordova アプリケーションの場合、Java コードではなく JavaScript コードで {{site.data.keyword.amashort}} Client SDK を初期化する必要があります。`FacebookAuthenticationManager` API は引き続きネイティブ・コードで登録する必要があります。次のコードをメイン・アクティビティー `onCreate` メソッドに追加します。  

	```Java
	FacebookAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
	```

6. 以下のコードをアクティビティーに追加します。

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
```

## iOS プラットフォームの構成
{: #facebook-auth-cordova-ios}

Cordova アプリケーションの iOS プラットフォームを Facebook 認証統合用に構成するために必要なステップは、ネイティブ iOS アプリケーションの場合と似ています。主な違いは、現在 Cordova CLI が CocoaPods の依存関係マネージャーをサポートしていない点です。Facebook 認証との統合に必要なファイルを手動で追加する必要があります。詳しくは、[iOS アプリで Facebook 認証を使用可能にする](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html)を参照してください。以下のステップを完了してください:

* iOS プラットフォーム用の Facebook アプリケーションの構成
* Facebook 認証用の {{site.data.keyword.amashort}} の構成

### Facebook 認証のための {{site.data.keyword.amashort}} SDK および Facebook SDK の手動インストール
{: #facebook-auth-cordova-ios-sdk}
1. [{{site.data.keyword.Bluemix_notm}} Mobile Services SDK for iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master) が含まれたアーカイブをダウンロードします。

1. `Sources/Authenticators/IMFFacebookAuthentication` ディレクトリーに移動し、全てのファイルを Xcode 内の iOS プロジェクトにコピー (ドラッグ・アンド・ドロップ) します。以下のファイルをコピーしてください。

	* IMFDefaultFacebookAuthenticationDelegate.h

	* IMFDefaultFacebookAuthenticationDelegate.m

	* IMFFacebookAuthenticationDelegate.h

	* IMFFacebookAuthenticationHandler.h

	* IMFFacebookAuthenticationHandler.m

	Xcode からプロンプトが出されたら、**「ファイルをコピー... (Copy files...)」**を選択します。

1. [Facebook SDK v3.19](https://developers.facebook.com/resources/facebook-ios-sdk-3.19.pkg) をダウンロードしてインストールします。

1. Facebook SDK は `~/Documents/FacebookSDK` ディレクトリーにインストールされます。そのディレクトリーにナビゲートし、`FacebookSDK.framework` ファイルを Xcode 内の iOS プロジェクトにコピー (ドラッグ・アンド・ドロップ) します。

1. Xcode でプロジェクト・ルートをクリックし、**「ビルド・フェーズ」**を選択します。

1. `FacebookSDK.framework` ファイルを**「バイナリーをライブラリーとリンク (Link binary with libraries)」**のリンク・ライブラリーのリストに追加します。

 [Facebook 認証用の iOS プラットフォームの構成](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html)を参照してください。**「{{site.data.keyword.amashort}} Client SDK の初期化」**セクションの説明に従って、`IMFFacebookAuthenticationHandler` API をネイティブ・コードで登録します。`IMFClient` はネイティブ・コードで初期化しないでください。

アプリケーション代行の `application:openURL:sourceApplication:annotation` メソッドに以下の行を追加します。このコードにより、すべての Cordova プラグインに対し各イベントが確実に通知されます。

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```
{: codeblock}

## {{site.data.keyword.amashort}} Client SDK の初期化
{: #facebook-auth-cordova-init}

Cordova アプリケーションで以下の JavaScript コードを使用して、{{site.data.keyword.amashort}} Client SDK を初期化します。

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```
{: codeblock}

`applicationRoute` および `applicationGUID` を、**「モバイル・オプション」**から取得した**「経路」**および**「アプリ GUID」**の値に置き換えます。
	



##{{site.data.keyword.amashort}} AuthorizationManager の初期化
Cordova アプリケーションで以下の JavaScript コードを使用して、{{site.data.keyword.amashort}} AuthorizationManager を初期化します。
```JavaScript
  MFPAuthorizationManager.initialize("tenantId");
  ```
{: codeblock}

`tenantId` 値を、{{site.data.keyword.amashort}} サービスの `tenantId` に置き換えます。この値は、{{site.data.keyword.amashort}} サービス・タイルの**「資格情報の表示」**ボタンをクリックすると、表示されます。



## 認証のテスト
{: #facebook-auth-cordova-test}
Client SDK が初期化され、Facebook 認証マネージャーの登録が完了すると、モバイル・バックエンド・アプリケーションに要求を出すことができるようになります。

### 開始する前に
{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用していて、{{site.data.keyword.amashort}}により`/protected` エンドポイントで保護されているリソースを既に持っている必要があります。詳しくは、[リソースの保護](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)を参照してください。

1. ブラウザーから、新しく作成されたモバイル・バックエンド・アプリケーションの保護エンドポイントへの要求の送信を試行します。次の URL を開きます。`{applicationRoute}/protected` (たとえば、 `http://my-mobile-backend.mybluemix.net/protected`)
<br/>MobileFirst Services Starter ボイラープレートを使用して作成されたモバイル・バックエンド・アプリケーションの `/protected` エンドポイントは、{{site.data.keyword.amashort}} で保護されています。 `認証されていない`というメッセージがブラウザーに戻されます。このエンドポイントは {{site.data.keyword.amashort}} Client SDK により装備されたモバイル・アプリケーションからのみアクセス可能であるため、このメッセージが戻されます。

1. Cordova アプリケーションを使用して、同じエンドポイントへ要求を出します。`BMSClient` を初期化した後に、以下のコードを追加してください。

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new MFPRequest("/protected", MFPRequest.GET);
	request.send(success, failure);
	```
{: codeblock}

1. アプリケーションを実行します。Facebook のログイン画面が表示されます。

	![image](images/android-facebook-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![image](images/ios-facebook-login.png)

	この画面は、デバイスに Facebook アプリをインストールしていない場合、または現在 Facebook に ログインしていない場合は少し違って見えるかもしれません。 

1. 「**OK**」をクリックし、{{site.data.keyword.amashort}} が認証を目的として Facebook のユーザー ID を使用することを承認します。

1. 	要求が成功すると、LogCat ユーティリティーまたは Xcode コンソールに以下のように出力されます。

	![Android 用の Facebook 認証完了メッセージ](images/android-facebook-login-success.png)

	![iOS 用の Facebook 認証完了メッセージ](images/ios-facebook-login-success.png)
