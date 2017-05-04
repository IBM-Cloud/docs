---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

**重要: {{site.data.keyword.amafull}} サービスは {{site.data.keyword.appid_full}} サービス**に置き換えられます。

# Cordova アプリ用の Facebook 認証の使用可能化
{: #facebook-auth-cordova}

{{site.data.keyword.amafull}} Cordova アプリケーションを Facebook 認証統合用に構成するには、各プラットフォームを個別に構成します。Cordova アプリケーションには既に {{site.data.keyword.amashort}} SDK が装備されている必要があります。

Facebook 認証を使用可能にするために、ネイティブ・プラットフォームと Cordova WebView Javascript の両方のコードを変更する必要があります。

ネイティブ・コードの変更は、Android Studio や Xcode などのネイティブ開発環境で行ってください。

{:shortdesc}

## 開始する前に
{: #facebook-auth-before}

以下が必要です。
* {{site.data.keyword.amashort}} Client SDK が装備された Cordova プロジェクト (Android または iOS)。[Cordova プラグインのセットアップ](getting-started-cordova.html#getting-started-cordova-plugin)を参照してください。
* {{site.data.keyword.amashort}} サービスによって保護された {{site.data.keyword.Bluemix_notm}} アプリケーションのインスタンス。{{site.data.keyword.Bluemix_notm}} バックエンド・サービスの作成方法について詳しくは、[概説](index.html)を参照してください。
* アプリケーションの経路。これは、バックエンド・アプリケーションの URL です。
* `tenantId` 値。{{site.data.keyword.amashort}} サービス・ダッシュボードを開きます。**「モバイル・オプション」**をクリックします。`tenantId` (`appGUID` とも呼ばれる) の値が、**「アプリ GUID」/「TenantId」**フィールドに表示されます。これらの値は、SDK を初期化するため、および要求をバックエンド・サービスに送信するために必要になります。
*  {{site.data.keyword.Bluemix_notm}} サービスがホストされている地域を見つけます。メニュー・バーの **「アバター」**アイコン![「アバター」アイコン](images/face.jpg "「アバター」アイコン") の横のヘッダー内に現在の {{site.data.keyword.Bluemix_notm}} 地域が表示されます。地域値は、**「米国南部」**、**「シドニー」**、または**「英国」**のいずれかでなければなりません。これらの名前に対応する正確な SDK の定数値は、コードの例に示しています。
* Facebook アプリケーションと App ID。詳しくは、[Facebook for Developers Web サイトでのアプリケーションの作成](facebook-auth-overview.html#facebook-appID)を参照してください。



## Android プラットフォームの構成
{: #facebook-auth-cordova-android}

Cordova アプリケーションの Android プラットフォームを Facebook 認証統合用に構成するために必要なステップは、ネイティブ Android アプリケーションの場合とよく似ています。詳しくは、[Android アプリで Facebook 認証を使用可能にする](facebook-auth-android.html)を参照してください。以下のステップを完了してください:

* [Android プラットフォーム用の Facebook アプリケーションの構成](facebook-auth-android.html#facebook-auth-android-config)。これは、Facebook Developers サイト上で Android アプリケーション用に Facebook 認証をセットアップします。
* [Facebook 認証用の MCA の構成](facebook-auth-android.html#facebook-auth-android-mca)。これは、{{site.data.keyword.Bluemix}} サーバー上で Android Facebook 認証用に {{site.data.keyword.amashort}} サービスを構成します。


### Android プラットフォーム用の {{site.data.keyword.amashort}} Facebook Client SDK の構成
{: #configure_android}

{{site.data.keyword.amashort}} Facebook Client SDK は、ネイティブ Android アプリケーション・プロジェクト内で Gradle によって追加する必要があります。

1. Android プロジェクト・フォルダーで、アプリケーション・モジュールの `build.gradle` ファイルを開きます (プロジェクト `build.gradle` ファイル**ではありません**)。依存関係セクションを見つけ、Client SDK の新しいコンパイル依存関係を追加します。

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
	{: codeblock}

2. **「ツール」>「Android」>「プロジェクトを Gradle ファイルと同期 (Sync Project with Gradle Files)」**をクリックして、プロジェクトと Gradle を同期します。

3. `android/res/values/strings.xml` ファイルを開いて、Facebook App ID が入った `<facebook_app_id>` ストリングを追加します。

	```XML
	<resources>
		<string name="app_name">HelloCordova</string>
		<string name="launcher_name">@string/app_name</string>
		<string name="activity_name">@string/launcher_name</string>
		<string name="facebook_app_id">"<facebook_app_id>"</string>
	</resources>
	```
	{: codeblock}

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
    {: codeblock}

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
    {: codeblock}

5. アクティビティー Java コードに以下を追加します。

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}

### ネイティブ Android コードでの許可マネージャーの初期化
{: #initialize_android}

`FacebookAuthenticationManager` API は引き続きネイティブ・コードで登録する必要があります。`<tenantId>` ([開始する前に](#before-you-begin)を参照) を使用して、このコードをメイン・アクティビティーの `onCreate` メソッドに追加します。

```
String tenantId = "<tenantId>";
MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
FacebookAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
```
{: codeblock}


## iOS プラットフォームの構成
{: #facebook-auth-cordova-ios}

Cordova アプリケーションの iOS プラットフォームを Facebook 認証統合用に構成するために必要なステップは、ネイティブ iOS Swift アプリケーションの場合と似ています (Swift SDK で Objective-C コードを使用するためにヘッダー・ファイルが必要です)。主な違いは、現在 Cordova CLI が CocoaPods の依存関係マネージャーをサポートしていない点です。{{site.data.keyword.amashort}} クライアントと Facebook 認証を統合するために必要なファイルを手動で追加する必要があります。詳しくは、[iOS アプリ用の Facebook 認証の使用可能化 (Swift SDK)](facebook-auth-ios-swift-sdk.html)を参照してください。以下のステップを完了してください:

* [iOS プラットフォーム用の Facebook アプリケーションの構成](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-config)。これは、Facebook Developers サイトで Facebook 認証サービスをセットアップします。
* [Facebook 認証用の MCA の構成](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-configmca)。これは、{{site.data.keyword.Bluemix}} サーバー上で {{site.data.keyword.amashort}} サービスを構成します。
* [iOS 用の MCA Facebook Client SDK の構成](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-sdk)。これは、CocoaPods を使用して Facebook 許可用の {{site.data.keyword.amashort}} iOS Swift SDK をインストールします。


### iOS のキーチェーン共有 (Keychain Sharing) の使用可能化
{: #enable_keychain}

`「キーチェーン共有 (Keychain Sharing)」`を使用可能にします。Xcode プロジェクトで、`「Capabilities」`タブに移動し、`「Keychain Sharing」`を`「On」`に切り替えます。

### Objective-C での {{site.data.keyword.amashort}} 許可マネージャーの初期化
{: #initialize_objc}

Xcode のバージョンに応じて、`app-delegate.m` ファイル内のネイティブ Objective-C コードで、許可マネージャーを初期化する必要があります。

```
	#import "<your_module_name>-Swift.h"

	- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

	{

	    [CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];

	    [[FacebookAuthenticationManager sharedInstance] register];

	    self.viewController = [[MainViewController alloc] init];

	    [[FacebookAuthenticationManager sharedInstance] onFinishLaunchingWithApplication:application withOptions:launchOptions];


	    return [super application:application didFinishLaunchingWithOptions:launchOptions];
	}
	

	- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(NSString *)sourceApplication annotation:(id)annotation

{

   return [[FacebookAuthenticationManager sharedInstance] onOpenURLWithApplication:application 
	   		url:url sourceApplication:sourceApplication annotation:annotation];
	}

```
{: codeblock}

**注:** インポートされたヘッダー・ファイル名は、モジュール名をストリング `-Swift.h` に連結して構成されます。例えば、モジュール名が `Cordova` の場合、インポート行は `#import "Cordova-Swift.h"` となります。モジュール名を見つけるには、`「ビルド設定 (Build Settings)」` > `「パッケージ化 (Packaging)」` > `「製品モジュール名 (Product Module Name)」`に移動してください。

`<tenantId>` をテナント ID ([開始する前に](#facebook-auth-before)を参照) に置き換えます。


##Cordova WebView での {{site.data.keyword.amashort}} Client SDK の初期化
{: #initialize_webview}

すべてのプラットフォームについて、Cordova Javascript WebView で以下の JavaScript コードを使用して、{{site.data.keyword.amashort}} Client SDK を初期化します。

```javascript
BMSClient.initialize(<applicationBluemixRegion>);
```
{: codeblock}

`<applicationBluemixRegion>` をご使用の地域 ([開始する前に](#facebook-auth-before)を参照) に置き換えます。

## 認証のテスト
{: #facebook-auth-cordova-test}

Client SDK が初期化され、Facebook 認証マネージャーの登録が完了すると、モバイル・バックエンド・サービスに要求を出すことができるようになります。

### 開始する前に
{: #testing_auth_before}

{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用していて、{{site.data.keyword.amashort}}により`/protected` エンドポイントで保護されているリソースを既に持っている必要があります。詳しくは、[リソースの保護](protecting-resources.html)を参照してください。

1. ブラウザーから、モバイル・バックエンド・アプリケーションの保護エンドポイントへの要求の送信を試行します。次の URL を開きます。`{applicationRoute}/protected` 例: `http://my-mobile-backend.mybluemix.net/protected`。

	`/protected` エンドポイント値は、MobileFirst Services Starter ボイラープレートを使用して作成されて {{site.data.keyword.amashort}} で保護されている、モバイル・バックエンド・アプリケーションの保護されたエンドポイントでなければなりません。 `認証されていない`というメッセージがブラウザーに戻されます。このエンドポイントは {{site.data.keyword.amashort}} Client SDK により装備されたモバイル・アプリケーションからのみアクセス可能であるため、このメッセージが戻されます。 

1. Cordova アプリケーションを使用して、同じエンドポイントへ要求を出します。`BMSClient` を初期化した後に、以下のコードを追加してください。

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error){
    	console.log("failure", error);
    }
	var request = new BMSRequest("<applicationRoute}/protected>", BMSRequest.GET);
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
