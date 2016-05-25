---

copyright:
  years: 2015, 2016

---

# Android 用の {{site.data.keyword.amashort}} Client SDK の構成
{: #custom-android}
{{site.data.keyword.amashort}} Client SDK の使用および {{site.data.keyword.Bluemix}} へのアプリケーションの接続のためにカスタム認証を使用する Android アプリケーションを構成します。

## 開始する前に
{: #before-you-begin}
カスタム ID プロバイダーを使用するように構成済みの{{site.data.keyword.amashort}} サービスのインスタンスにより保護されているリソースを持っている必要があります。また、モバイル・アプリに {{site.data.keyword.amashort}} Client SDK が装備されている必要があります。詳しくは、以下の情報を参照してください。

 * [{{site.data.keyword.amashort}} 入門](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Android SDK のセットアップ](https://console.{DomainName}/docs/services/mobileaccess/getting-started-android.html)
 * [カスタム ID プロバイダーの使用](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [カスタム ID プロバイダーの作成](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [カスタム認証用の {{site.data.keyword.amashort}} の構成 ](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## {{site.data.keyword.amashort}} Client SDK の初期化
{: #custom-android-initialize}
1. Android Studio にある Android プロジェクトで、アプリケーション・モジュールの `build.gradle` ファイルを開きます。
<br/>**ヒント:** Android プロジェクトには、プロジェクト用とアプリケーション・モジュール用に 2 つの `build.gradle` ファイルがある場合があります。アプリケーション・モジュールのファイルを使用してください。

1. `build.gradle` ファイル内で `dependencies` セクションを見つけて、以下のコンパイル依存関係があるか確認します。以下の依存関係がまだない場合は追加します。

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'core',
        version: '1.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```

1. プロジェクトを Gradle と同期化します。**「ツール」>「Android」>「プロジェクトを Gradle ファイルと同期 (Sync Project with Gradle Files)」**とクリックします。

1. Android プロジェクトの `AndroidManifest.xml` ファイルを開きます。
以下のように、`<manifest>` エレメントの下にインターネット・アクセス許可を追加します。

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```

1. SDK を初期化します。初期化コードを入れる一般的な場所 (ただし、必須ではない) は、Android アプリケーション内のメイン・アクティビティーの `onCreate` メソッド内です。*applicationRoute* および *applicationGUID* を、{{site.data.keyword.Bluemix_notm}} ダッシュボード上のアプリ内で**「モバイル・オプション」**をクリックしたときに取得した**「経路」**および**「アプリ GUID」**の値に置き換えます。

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");```

## AuthenticationListener インターフェース
{: #custom-android-authlistener}

{{site.data.keyword.amashort}} Client SDK は、カスタム認証フローを実装できるように `AuthenticationListener` インターフェースを提供しています。`AuthenticationListener` インターフェースは、認証プロセスの異なるフェーズで呼び出される 3 つのメソッドを公開します。

### onAuthenticationChallengeReceived メソッド
{: #custom-onAuth}
{{site.data.keyword.amashort}} サービスからカスタム認証チャレンジを受け取ったときに、このメソッドを呼び出します。

```Java
void onAuthenticationChallengeReceived(AuthenticationContext authContext, JSONObject challenge, Context context);
```
#### 引数
{: #custom-android-onAuth-arg}

* `AuthenticationContext`: {{site.data.keyword.amashort}} Client SDK によって提供されます。これによって、認証チャレンジ応答を返すか、または資格情報収集中の失敗を報告することができます。例えば、ユーザーが認証を取り消す場合などです。
* `JSONObject`: カスタム ID プロバイダーによって返されるカスタム認証チャレンジを含みます。
* `Context`: 要求が送信されたときに使用された Android Context への参照。通常、この引数は Android Activity を表します。

`onAuthenticationChallengeReceived` メソッドを呼び出すことによって、{{site.data.keyword.amashort}} Client SDK は制御を開発者に委任します。サービスは資格情報を待機します。開発者は、`AuthenticationContext` インターフェース・メソッドのいずれかを使用して、資格情報を収集して {{site.data.keyword.amashort}} Client SDK に返す必要があります。

### onAuthenticationSuccess メソッド
{: #custom-android-authlistener-onsuccess}
認証が成功した後、このメソッドを呼び出します。引数には、Android Context と、認証の成功に関する詳しい情報を含む JSONObject (これはオプションです) があります。
```Java
void onAuthenticationSuccess(Context context, JSONObject info);
```

### onAuthenticationFailure メソッド
{: #custom-android-authlistener-onfail}
認証が失敗した後、このメソッドを呼び出します。引数には、Android Context と、認証の失敗に関する詳しい情報を含む JSONObject (これはオプションです) があります。
```Java
void onAuthenticationFailure(Context context, JSONObject info);
```

## AuthenticationContext インターフェース
{: #custom-android-authcontext}

`AuthenticationContext` は、カスタム `AuthenticationListener` の `onAuthenticationChallengeReceived` メソッドへの引数として提供されます。資格情報を収集し、`AuthenticationContext` のメソッドを使用して、資格情報を {{site.data.keyword.amashort}} Client SDK に返すか、失敗を報告する必要があります。以下のいずれかのメソッドを使用します。

```Java
void submitAuthenticationChallengeAnswer(JSONObject answer);
```
```Java
void submitAuthenticationFailure (JSONObject info);
```

## カスタム AuthenticationListener の実装例
{: #custom-android-samplecustom}

この AuthenticationListener サンプルは、カスタム ID プロバイダーと連携するよう設計されています。このサンプルは [Github リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)からダウンロードできます。

```Java
package com.ibm.helloworld;
import android.content.Context;
import android.util.Log;
import com.ibm.mobilefirstplatform.clientsdk.android.security.api.AuthenticationContext;
import com.ibm.mobilefirstplatform.clientsdk.android.security.api.AuthenticationListener;
import org.json.JSONException;
import org.json.JSONObject;

public class CustomAuthenticationListener implements AuthenticationListener {

	@Override
	public void onAuthenticationChallengeReceived (AuthenticationContext authContext,
											JSONObject challenge, Context context) {

		log("onAuthenticationChallengeResceived :: " + challenge.toString());

		// In this sample the AuthenticationListener immediatelly returns a hardcoded
		// set of credentials. In a real life scenario this is where developer would
		// show a login screen, collect credentials and invoke
		// authContext.submitAuthenticationChallengeAnswer() API

		JSONObject challengeResponse = new JSONObject();
		try {
			challengeResponse.put("username", "john.lennon");
			challengeResponse.put("password", "12345");
			authContext.submitAuthenticationChallengeAnswer(challengeResponse);
		} catch (JSONException e){

			// In case there was a failure collecting credentials you need to report
			// it back to the AuthenticationContext. Otherwise Mobile Client
			// Access Client SDK will remain in a waiting-for-credentials state
			// forever

			log("This should never happen...");
			authContext.submitAuthenticationFailure(null);
		}
	}

	@Override
	public void onAuthenticationSuccess (Context context, JSONObject info) {
		log("onAuthenticationSuccess :: " + info.toString());
	}

	@Override
	public void onAuthenticationFailure (Context context, JSONObject info) {
		log("onAuthenticationFailure :: " + info.toString());
	}

	private void log(String text){
		Log.d("CustomAuthListener", text);
	}
}
```

## カスタム AuthenticationListener の登録
{: #custom-android-register}

カスタム AuthenticationListener を作成したら、そのリスナーの使用を開始する前に `BMSClient` に登録します。以下のコードをアプリケーションに追加します。このコードは保護リソースに要求を送信する前に呼び出される必要があります。

```Java
BMSClient.getInstance().registerAuthenticationListener(realmName,
									new CustomAuthenticationListener());
```

*realmName* には {{site.data.keyword.amashort}} ダッシュボードで指定したものを使用してください。


## 認証のテスト
{: #custom-android-testing}
Client SDK が初期化され、カスタム AuthenticationListener が登録されたら、モバイル・バックエンドに要求を出すことを開始できます。

### 開始する前に
{: #custom-android-testing-before}
{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用して作成されたアプリケーションと、 `/protected` エンドポイントで{{site.data.keyword.amashort}} により保護されているリソースを持っている必要があります。


1. ブラウザーで `{applicationRoute}/protected` (例えば `http://my-mobile-backend.mybluemix.net/protected`) を開いて、モバイル・バックエンドの保護エンドポイントに要求を送信します。

1. {{site.data.keyword.mobilefirstbp}} ボイラープレートを使用して作成されたモバイル・バックエンドの`/protected` エンドポイントは、{{site.data.keyword.amashort}} で保護されています。このエンドポイントは {{site.data.keyword.amashort}} Client SDK により装備されたモバイル・アプリケーションからのみアクセス可能です。
その結果、`承認されていない`というメッセージがブラウザーに表示されます。

1. Android アプリケーションを使用して同じエンドポイントに対する要求を作成します。`BMSClient` を初期化した後で次のコードを追加して、カスタムの AuthenticationListener を登録します。

	```Java
	Request request = new Request("/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp", AuthorizationManager.getInstance().getUserIdentity().toString());
		}
		@Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
			if (null != t) {
				Log.d("Myapp", "onFailure :: " + t.getMessage());
			} else if (null != extendedInfo) {
				Log.d("Myapp", "onFailure :: " + extendedInfo.toString());
			} else {
				Log.d("Myapp", "onFailure :: " + response.getResponseText());
			}
		}
	});
```

1. 	要求が成功したら、LogCat ツールで以下のように出力されます。

	![image](images/android-custom-login-success.png)

1. 次のコードを追加してログアウト機能を追加することもできます。

 ```Java
 AuthorizationManager.getInstance().logout(getApplicationContext(), listener);
 ```

 ユーザーのログイン後に、このコードを呼び出すと、そのユーザーはログアウトされます。そのユーザーが再度ログインしようとする場合は、サーバーから受信した要求に再度応じる必要があります。

 ログアウト機能に渡される `listener` の値は、ヌルにすることができます。
