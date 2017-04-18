---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.amashort}} Cordova アプリ用のカスタム認証の構成
{: #custom-cordova}

保護されたアプリケーションにアクセスするためにカスタム認証および {{site.data.keyword.amafull}}Client SDK を使用するように、Cordova アプリケーションを装備します。

## 開始する前に
{: #before-you-begin}
* カスタム ID プロバイダーを使用するように構成済みの {{site.data.keyword.amashort}} サービスのインスタンスによって保護されているリソース ([カスタム認証の構成](custom-auth-config-mca.html)を参照してください)。  
* **TenantID** 値。{{site.data.keyword.amashort}} ダッシュボードでサービスを開きます。**「モバイル・オプション」**ボタンをクリックします。`tenantId` (`appGUID` とも呼ばれる) の値が、**「アプリ GUID」/「TenantId」**フィールドに表示されます。許可マネージャーを初期化するためにこの値が必要になります。
* **「レルム」**名。これは、{{site.data.keyword.amashort}} ダッシュボードの**「管理」**タブで、**「カスタム」**セクションの**「レルム名」**フィールドに指定した値です。
* {{site.data.keyword.Bluemix_notm}} **「地域」**。**「アバター」**アイコン![「アバター」アイコン](images/face.jpg "「アバター」アイコン") の横のヘッダー内に現在の {{site.data.keyword.Bluemix_notm}} 地域が表示されます。表示される地域値は、`「米国南部」`、`「英国」`、または`「シドニー」`のいずれかでなければなりません。対応する SDK 定数の正確な構文は、コードの例に示しています。

詳しくは、以下の情報を参照してください。


 * [カスタム認証用の {{site.data.keyword.amashort}} の構成 ](custom-auth-config-mca.html)。これは、カスタム認証用に {{site.data.keyword.amashort}} サービスをセットアップする方法を示します。ここで、**「レルム」**値を定義します。
 * [Cordova SDK のセットアップ](getting-started-cordova.html)。Cordova クライアント・アプリケーションのセットアップに関する情報。
 * [カスタム ID プロバイダーの使用](custom-auth.html)。カスタム ID プロバイダーを使用してユーザーを認証する方法。
 * [カスタム ID プロバイダーの作成](custom-auth-identity-provider.html)。カスタム ID プロバイダーがどのように機能するかを示すいくつかの例。

## Cordova WebView コードの構成
### Cordova WebView での {{site.data.keyword.amashort}} Client SDK の初期化
{: #custom-cordova-sdk}
`index.js` ファイルで `<applicationBluemixRegion>` パラメーターを渡して、SDK を初期化します。

```JavaScript
BMSClient.initialize("<applicationBluemixRegion>");
```
{: codeblock}

`<applicationBluemixRegion>` をご使用の地域 ([開始する前に](#before-you-begin)を参照) に置き換えます。


### 認証リスナー・インターフェース
{: #custom-cordva-auth}

{{site.data.keyword.amashort}} Client SDK は、カスタム認証フローを実装するための認証リスナー・インターフェースを提供します。以下のメソッドを追加する必要があります。これらのメソッドは、認証プロセスの異なるフェーズで呼び出されます。

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...},
	onAuthenticationSuccess: function(info){...},
	onAuthenticationFailure: function(info){...}
}
```
{: codeblock}

各メソッドは、認証プロセスの異なるフェーズを処理します。

### onAuthenticationChallengeReceived メソッド
{: #onAuthenticationChallengeReceived}
このメソッドは、{{site.data.keyword.amashort}} サービスからカスタム認証チャレンジを受け取ったときに呼び出されます。

```JavaScript
onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...}
```
{: codeblock}

* `authenticationContext`: 開発者が認証チャレンジ応答、または資格情報収集中の失敗 (例: ユーザーによる認証要求の取り消し）を返すことができるように、{{site.data.keyword.amashort}} Client SDK によって提供されます。
* `challenge`: カスタム ID プロバイダーによって返されるカスタム認証チャレンジを含む JSON オブジェクト。

`onAuthenticationChallengeReceived` メソッドを呼び出すことによって、{{site.data.keyword.amashort}} Client SDK は開発者に制御を委任します。{{site.data.keyword.amashort}} は資格情報を待機します。開発者は、以下の `authContext` インターフェース・メソッドのいずれかを使用して、資格情報を収集して {{site.data.keyword.amashort}} Client SDK に返す必要があります。

```JavaScript
onAuthenticationSuccess: function(info){...}
```
{: codeblock}

このメソッドは認証が成功した後で呼び出されます。引数には、認証の成功に関する詳しい情報が含まれた、オプションの JSON オブジェクトが含まれます。

```JavaScript
onAuthenticationFailure: function(info){...}
```
{: codeblock}

このメソッドは認証が失敗した後で呼び出されます。引数には、認証の失敗に関する詳しい情報が含まれた、オプションの JSON オブジェクトが含まれます。

### authenticationContext
{: #custom-cordova-authcontext}

カスタム認証リスナーの `onAuthenticationChallengeReceived` メソッドに引数として `authenticationContext` 値が提供されます。開発者は、資格情報を収集し、`authenticationContext` メソッドを使用して、資格情報を {{site.data.keyword.amashort}} Client SDK に返すか、または失敗を報告する必要があります。以下のいずれかのメソッドを使用します。

```JavaScript
authenticationContext.submitAuthenticationChallengeAnswer(challengeAnswer);

```
{: codeblock}

```JavaScript
authenticationContext.submitAuthenticationFailure(info);
```
{: codeblock}

以下のコードは、カスタム認証リスナーがどのように資格情報を収集し、チャレンジを処理し、認証応答を提供できるかを示しています。

## カスタム認証リスナーのワークフローの実装例
{: #custom-cordova-authlisten-sample}

認証リスナーのこのサンプルは、カスタム ID プロバイダーと連携するよう設計されています。カスタム ID プロバイダーは、[この GitHub リポジトリー![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "外部リンク・アイコン"){: new_window}からダウンロードできます。

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {
		console.log("onAuthenticationChallengeReceived :: ", challenge);

		// In this sample the authentication listener immediatelly returns a hardcoded
		// set of credentials. In a real life scenario this is where developer would
		// show a login screen, collect credentials and invoke
		// authenticationContext.submitAuthenticationChallengeAnswer() API

		var challengeResponse = {
			username: "john.lennon",
			password: "12345"
		}

		authenticationContext.submitAuthenticationChallengeAnswer(challengeResponse);

		// In case there was a failure collecting credentials you need to report
		// it back to the authenticationContext. Otherwise Mobile Client
		// Access client SDK will remain in a waiting-for-credentials state
		// forever

	},

	onAuthenticationSuccess: function(info){
		console.log("onAuthenticationSuccess :: ", info);
	},

	onAuthenticationFailure: function(info){
		console.log("onAuthenticationFailure :: ", info);
	}
}
```
{: codeblock}

## Cordova WebView でのカスタム認証リスナーの登録
{: #custom-cordova-authreg}

カスタム認証リスナーを作成した後、使用を開始する前に `BMSClient` に登録する必要があります。以下のコードをアプリケーションに追加します。このコードは保護リソースに要求を送信する前に呼び出してください。

```Java
BMSClient.registerAuthenticationListener(<realmName>, customAuthenticationListener);
```
{: codeblock}
`realmName` には {{site.data.keyword.amashort}} ダッシュボードで指定したものを使用してください。


## ネイティブ・コードでの許可マネージャーの設定

ネイティブ・プラットフォーム・コードで、{{site.data.keyword.amashort}} 許可マネージャーを登録する必要があります。

**Android** (メイン・アクティビティーの `onCreate` に追加します)

```
String tenantId = "<tenantId>";
MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
```
{: codeblock}

**iOS Objective-C** (`AppDelegate.m` に追加します)

Xcode のバージョンに応じて、許可マネージャーを登録します。

```
# import "<your_module_name>-Swift.h"

- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

{  
	
    //[CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];
 }
```
{: codeblock}

注: 正しい Swift ヘッダー・ファイル名については、`your_module_name` をプロジェクトのモジュール名に置き換えます。例えば、モジュール名が `Cordova` の場合は、`#import "Cordova-Swift.h"` のようになります。モジュール名を見つけるには、**「ビルド設定 (Build Settings)」>「パッケージ化 (Packaging)」>「製品モジュール名 (Product Module Name)」**に移動します。

**注:** `tenantId` を、{{site.data.keyword.amashort}} サービス・ダッシュボードの**「モバイル・オプション」** ボタンで見つかったテナント ID に置き換えます。


## iOS のキーチェーン共有 (Keychain Sharing) の使用可能化

Xcode プロジェクトで、`「Capabilities」`タブに移動して`「Keychain Sharing」`を使用可能にし、`「Keychain Sharing」`を`「On」`に切り替えます。


## 認証のテスト
{: #custom-cordova-test}
Client SDK が初期化され、カスタム `AuthenticationListener` の登録が完了すると、モバイル・バックエンド・アプリケーションに要求を出すことができるようになります。

### 開始する前に
{: #custom-cordova-testing-before}
{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用して作成されたアプリケーションと、 `/protected` エンドポイントで{{site.data.keyword.amashort}} により保護されているリソースを持っている必要があります。


1. ブラウザーで `{applicationRoute}/protected` (例えば `http://my-mobile-backend.mybluemix.net/protected`) を開くことによって、モバイル・バックエンド・アプリケーションの保護エンドポイントに要求を送信します。{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用して作成されたモバイル・バックエンド・アプリケーションの `/protected` エンドポイントは、{{site.data.keyword.amashort}} で保護されています。このエンドポイントには、{{site.data.keyword.amashort}} Client SDK を装備したモバイル・アプリケーションのみがアクセスできます。その結果、`承認されていない`というメッセージがブラウザーに表示されます。

1. Cordova アプリケーションを使用して、同じエンドポイントへ要求を出します。`BMSClient` を初期化した後で次のコードを追加して、カスタムの AuthenticationListener を登録します。

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

	`<your-application-route>` をご使用のバックエンド・アプリケーション URL ([開始する前に](#before-you-begin)を参照) に置き換えます。

1. 	要求が成功したら、`LogCat` または Xcode コンソールに以下のように出力されます。

	![image](images/android-custom-login-success.png)

	![image](images/ios-custom-login-success.png)
