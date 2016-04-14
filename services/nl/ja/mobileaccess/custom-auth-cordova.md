---

copyright:
  years: 2015, 2016

---

# Cordova 用の {{site.data.keyword.amashort}} Client SDK の構成
{: #custom-cordova}
{{site.data.keyword.amashort}} Client SDK の使用および {{site.data.keyword.Bluemix}} へのアプリケーションの接続のためにカスタム認証を使用する Cordova アプリケーションを構成します。


## 開始する前に
{: #before-you-begin}
カスタム ID プロバイダーを使用するように構成済みの{{site.data.keyword.amashort}} サービスのインスタンスにより保護されているリソースを持っている必要があります。また、モバイル・アプリに {{site.data.keyword.amashort}} Client SDK が装備されている必要があります。詳しくは、以下の情報を参照してください。

 * [{{site.data.keyword.amashort}} 入門](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Cordova SDK のセットアップ](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)
 * [カスタム ID プロバイダーの使用](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [カスタム ID プロバイダーの作成](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [カスタム認証用の {{site.data.keyword.amashort}} の構成 ](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)

## {{site.data.keyword.amashort}} Client SDK の初期化
{: #custom-cordova-sdk}
applicationGUID および applicationRoute パラメーターを渡すことによって、SDK を初期化します。

1. アプリケーション・パラメーター値を取得します。{{site.data.keyword.Bluemix_notm}}ダッシュボードでアプリを開きます。「**Mobile オプション**」をクリックします。**「経路」** (`applicationRoute`) と**「アプリ GUID」** (`applicationGUID`) の値が表示されます。
1. Client SDK を初期化します。

	```JavaScript
	BMSClient.initialize(applicationRoute, applicationGUID);

	```
 *applicationRoute* および *applicationGUID* を、{{site.data.keyword.Bluemix_notm}} ダッシュボード上のアプリケーションの**「モバイル・オプション」**パネルから取得した**「経路」**および**「アプリ GUID」**の値に置き換えます。

## 認証リスナー・インターフェース
{: #custom-cordva-auth}

{{site.data.keyword.amashort}} Client SDK は、カスタム認証フローを実装するための認証リスナー・インターフェースを提供します。以下のメソッドを追加する必要があります。これらのメソッドは、認証プロセスの異なるフェーズで呼び出されます。

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...},
	onAuthenticationSuccess: function(info){...},
	onAuthenticationFailure: function(info){...}
}
```

各メソッドは、認証プロセスの異なるフェーズを処理します。

### onAuthenticationChallengeReceived メソッド
{: #onAuthenticationChallengeReceived}
このメソッドは、{{site.data.keyword.amashort}} サービスからカスタム認証チャレンジを受け取ったときに呼び出されます。
```JavaScript
onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...}
```

#### 引数
{: #onAuthenticationChallengeReceived-args}
* `authenticationContext`: 開発者が認証チャレンジ応答、または資格情報収集中の失敗 (例: ユーザーによる認証要求の取り消し）を返すことができるように、{{site.data.keyword.amashort}} Client SDK によって提供されます。
* `challenge`: カスタム ID プロバイダーによって返されるカスタム認証チャレンジを含む JSON オブジェクト。

`onAuthenticationChallengeReceived` メソッドを呼び出すことによって、{{site.data.keyword.amashort}} Client SDK は開発者に制御を委任します。{{site.data.keyword.amashort}} は資格情報を待機します。開発者は、以下の `authContext` インターフェース・メソッドのいずれかを使用して、資格情報を収集して {{site.data.keyword.amashort}} Client SDK に返す必要があります。

```JavaScript
onAuthenticationSuccess: function(info){...}
```

このメソッドは認証が成功した後で呼び出されます。オプション引数として、認証の成功に関する詳しい情報を含む JSONObject があります。


```JavaScript
onAuthenticationFailure: function(info){...}
```

このメソッドは認証が失敗した後で呼び出されます。オプション引数として、認証の失敗に関する詳しい情報を含む JSONObject があります。

## authenticationContext
{: #custom-cordova-authcontext}

カスタム認証リスナーの `onAuthenticationChallengeReceived` メソッドに引数として `authenticationContext` 値が提供されます。開発者は、資格情報を収集し、`authenticationContext` メソッドを使用して、資格情報を {{site.data.keyword.amashort}} Client SDK に返すか、または失敗を報告する必要があります。以下のいずれかのメソッドを使用します。

```JavaScript
authenticationContext.submitAuthenticationChallengeAnswer(challengeAnswer);

authenticationContext.submitAuthenticationFailure(info);
```

## カスタム認証リスナーの実装例
{: #custom-cordova-authlisten-sample}

認証リスナーのこのサンプルは、カスタム ID プロバイダーと連携するよう設計されています。7このカスタム ID プロバイダーは [Github リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)からダウンロードできます。

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
		// Access Client SDK will remain in a waiting-for-credentials state
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

## カスタム認証リスナーの登録
{: #custom-cordova-authreg}

カスタム認証リスナーを作成したら、使用を開始する前に `BMSClient` に登録します。以下のコードをアプリケーションに追加します。このコードは保護リソースに要求を送信する前に呼び出してください。

```Java
BMSClient.registerAuthenticationListener(realmName, customAuthenticationListener);
```
 *realmName* には {{site.data.keyword.amashort}} ダッシュボードで指定したものを使用してください。


## 認証のテスト
{: #custom-cordova-test}
Client SDK が初期化され、カスタム AuthenticationListener が登録されたら、モバイル・バックエンドに要求を出すことを開始できます。

### 開始する前に
{: #custom-cordova-testing-before}
{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用して作成されたアプリケーションと、 `/protected` エンドポイントで{{site.data.keyword.amashort}} により保護されているリソースを持っている必要があります。


1. ブラウザーで `{applicationRoute}/protected` (例えば `http://my-mobile-backend.mybluemix.net/protected`) を開いて、モバイル・バックエンドの保護エンドポイントに要求を送信します。{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用して作成されたモバイル・バックエンドの`/protected` エンドポイントは、{{site.data.keyword.amashort}} で保護されています。このエンドポイントは {{site.data.keyword.amashort}} Client SDK により装備されたモバイル・アプリケーションからのみアクセス可能です。
その結果、`承認されていない`というメッセージがブラウザーに表示されます。

1. Cordova アプリケーションを使用して同じエンドポイントに対する要求を作成します。`BMSClient` を初期化した後で次のコードを追加して、カスタムの AuthenticationListener を登録します。

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

1. 	要求が成功したら、LogCat または Xcode コンソールに以下のように出力されます。

	![image](images/android-custom-login-success.png)

	![image](images/ios-custom-login-success.png)
