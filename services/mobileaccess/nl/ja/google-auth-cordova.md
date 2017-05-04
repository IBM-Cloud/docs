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

# Cordova アプリ用の Google 認証の使用可能化
{: #google-auth-cordova}

{{site.data.keyword.amafull}} Cordova アプリケーションを Google 認証に統合するには、Cordova アプリケーションのネイティブ・プラットフォーム・コード (Java または Objective-C) および Cordova WebView (Javascript) で変更を行う必要があります。各プラットフォームは別々に構成する必要があります。ネイティブ・コードの変更は、Android Studio や Xcode などのネイティブ開発環境で行ってください。

## 開始する前に
{: #before-you-begin}

以下が必要です。

* {{site.data.keyword.amashort}} Client SDK が装備された Cordova プロジェクト。詳しくは、[Cordova プラグインのセットアップ](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)を参照してください。  
* {{site.data.keyword.amashort}} サービスによって保護された {{site.data.keyword.Bluemix_notm}} アプリケーションのインスタンス。{{site.data.keyword.Bluemix_notm}} バックエンド・サービスの作成方法について詳しくは、[概説](index.html)を参照してください。
* アプリケーションの経路。これは、バックエンド・アプリケーションの URL です。
* **「TenantID」**。{{site.data.keyword.Bluemix_notm}} ダッシュボードでサービスを開きます。**「モバイル・オプション」**をクリックします。`tenantId` (`appGUID` とも呼ばれる) の値が、**「アプリ GUID」/「TenantId」**フィールドに表示されます。許可マネージャーを初期化するためにこの値が必要になります。
*  {{site.data.keyword.Bluemix_notm}} アプリケーションがホストされている地域を見つけます。**「アバター」**アイコン![「アバター」アイコン](images/face.jpg "「アバター」アイコン") の横のヘッダー内に現在の Bluemix 地域が表示されます。地域値は、**「米国南部」**、**「シドニー」**、または**「英国」**のいずれかでなければなりません。これらの名前に対応する正確な SDK の定数値は、コードの例に示しています。
* (オプション) 次のセクションの内容をよく理解してください。
   * [Android アプリ用の Google 認証の使用可能化](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)
   * [iOS アプリ用の Google 認証の使用可能化](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html)


## Android プラットフォームの構成
{: #google-auth-cordova-android}

Cordova アプリケーションの Android プラットフォームを Google 認証用に構成するために必要なステップは、ネイティブ・アプリケーションに必要なステップに非常に似ています。[Android アプリでの Google 認証の使用可能化](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)を参照して、以下をセットアップします。

   * [Google Developer Console でのプロジェクトの作成](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html#create-google-project)。これは、Google Developers Web サイトで認証サービスをセットアップする方法を示します。
   * [Google 認証用の MCA の構成](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html#google-auth-android-config)。これは、Google 許可を使用するように {{site.data.keyword.amashort}} をセットアップする方法を示します。

### Android Cordova 用の Client SDK の構成

1. Android プロジェクト・フォルダーで、アプリケーション・モジュールの `build.gradle` ファイルを開きます (プロジェクト `build.gradle` ファイル**ではありません**)。以下のように、依存関係セクションを見つけ、Client SDK の新しいコンパイル依存関係を追加します。

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'googleauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```
	{: codeblock}

1. **「ツール」>「Android」>「プロジェクトを Gradle ファイルと同期 (Sync Project with Gradle Files)」**をクリックして Gradle とプロジェクトを同期します。

1. ネイティブ・コードでの `GoogleAuthenticationManager` API の登録はまだ必要になります。次のコードをメイン・アクティビティー `onCreate` メソッドに追加します。

	```Java
	String tenantId = "<tenantId>";
	MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
	BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
	GoogleAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
	```
	{: codeblock}

1. 以下のコードをアクティビティーに追加します。

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		GoogleAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}

## iOS プラットフォームの構成
{: #google-auth-cordova-ios}

Cordova アプリケーションの iOS プラットフォームを Google 認証統合用に構成するために必要なステップは、ネイティブ・アプリケーション用のステップに似ています。主な違いは、現在 Cordova CLI が CocoaPods の依存関係マネージャーをサポートしていない点です。Google 認証との統合に必要なファイルは、手動で追加する必要があります。詳しくは、[iOS アプリ用の Google 認証の使用可能化 (Swift SDK)](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html)を参照してください。以下のステップを完了してください。

   * [Google Sign-In 用のアプリケーションの準備](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-sign-in-ios): {{site.data.keyword.amashort}} iOS アプリを認証するために Google Sign-In を準備します。

   * [Google 認証用の MCA の構成](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-auth-ios-config): Google Sign-In を処理するように {{site.data.keyword.amashort}} サービスを構成します。

   * [iOS 用の MCA Client SDK の構成](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-auth-ios-sdk): Google Sign-In を処理するように {{site.data.keyword.amashort}} クライアントを構成します。


### iOS のキーチェーン共有 (Keychain Sharing) の使用可能化
{: #enable_keychain}

`「キーチェーン共有 (Keychain Sharing)」`を使用可能にします。Xcode プロジェクトで、`「Capabilities」`タブに移動し、`「Keychain Sharing」`を`「On」`に切り替えます。


### iOS コードでの許可マネージャーの初期化

`AppDelgate.m` ファイル内の Objective-C で、{{site.data.keyword.amashort}} 許可マネージャーを初期化します。

```
 #import "<your_module_name>-Swift.h" 
 
- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

	{

	    [CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];

	    [[GoogleAuthenticationManager sharedInstance] register];

    self.viewController = [[MainViewController alloc] init];

	    [[GoogleAuthenticationManager sharedInstance] onFinishLaunchingWithApplication:application withOptions:launchOptions];

	return [super application:application didFinishLaunchingWithOptions:launchOptions];
}

- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(NSString *)sourceApplication annotation:(id)annotation

{

   return [[GoogleAuthenticationManager sharedInstance] onOpenURLWithApplication:application url:url
	sourceApplication:sourceApplication annotation:annotation];
}
```
{: codeblock}


####注:
{: #note notoc}

* `<your_module_name>` をプロジェクトのモジュール名に置き換えます。例えば、モジュール名が `Cordova` の場合、インポート行は `#import "Cordova-Swift.h"` になります。モジュール名を見つけるには、`「ビルド設定 (Build Settings)」`タブ、`「パッケージ化 (Packaging)」` > `「製品モジュール名 (Product Module Name)」`に移動します。
* `<tenantId>` をご使用のテナント ID ([開始する前に](#before-you-begin)を参照) に置き換えます。


## Cordova WebView での {{site.data.keyword.amashort}} Client SDK の初期化
{: #google-auth-cordova-initialize}

すべてのプラットフォームについて、Cordova アプリケーションで以下の JavaScript コードを使用して、{{site.data.keyword.amashort}} Client SDK を初期化します。

```JavaScript
BMSClient.initialize("<applicationBluemixRegion>");
```
{: codeblock}

`<applicationBluemixRegion>` をご使用の地域 ([開始する前に](#before-you-begin)を参照) に置き換えます。

## 認証のテスト
{: #google-auth-cordova-test}

Client SDK が初期化されたら、モバイル・バックエンド・アプリケーションに要求を出すことができるようになります。

### 開始する前に
{: #google-auth-cordova-testing-before}

`/protected` エンドポイントに {{site.data.keyword.amashort}} によって保護されたバックエンド・アプリケーションがなければなりません。`/protected` エンドポイントをセットアップする必要がある場合、[リソースの保護 ](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)を参照してください。

1. デスクトップ・ブラウザーで、`{applicationRoute}/protected` (例えば、`http://my-mobile-backend.mybluemix.net/protected`) を開くことによって、モバイル・バックエンド・アプリケーションの保護エンドポイントへの要求の送信を試行します。

1. MobileFirst Services ボイラープレートを使用して作成されたモバイル・バックエンド・アプリケーションの `/protected` エンドポイントは、{{site.data.keyword.amashort}} によって保護されています。したがって、このエンドポイントにアクセスできるのは、{{site.data.keyword.amashort}} Client SDK が装備されたモバイル・アプリケーションのみです。結果的に、デスクトップ・ブラウザーに `Unauthorized` が表示されます。

1. Cordova アプリケーションを使用し、完全な URL (例えば、`http://my-mobile-backend.mybluemix.net/protected`) を使用して、同じエンドポイントに要求を行います。`BMSClient` を初期化した後に、以下のコードを追加してください。

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new BMSRequest("<your-application-route>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}

1. アプリケーションを実行します。Google のログイン画面が表示されます。

	![Google ログイン画面](images/android-google-login.png)

	![Google ログイン画面](images/ios-google-login.png)

	この画面は、デバイスに Facebook アプリをインストールしていない場合、または現在 Facebook に ログインしていない場合は少し違って見えるかもしれません。 

1. **「OK」**をクリックして、{{site.data.keyword.amashort}} が Google ユーザー ID を認証目的に使用することを許可します。

1. ユーザーの要求は正常に処理されます。使用しているプラットフォームに応じて、LogCat/Xcode コンソールに以下の出力が表示されます。

	![Android のコード・スニペット](images/android-google-login-success.png)

	![iOS のコード・スニペット](images/ios-google-login-success.png)
