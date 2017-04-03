---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---

{{site.data.keyword.amafull}} サービスは {{site.data.keyword.appid_full}} サービスに置き換えられます。

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# {{site.data.keyword.amashort}} Android アプリ用のカスタム認証の構成
{: #custom-android}


{{site.data.keyword.amashort}} Client SDK の使用のためにカスタム認証を使用するよう Android アプリケーションを構成し、アプリケーションを {{site.data.keyword.Bluemix}} に接続します。

## 開始する前に
{: #before-you-begin}
開始する前に以下が必要です。

* カスタム ID プロバイダーを使用するように構成済みの {{site.data.keyword.amashort}} サービスのインスタンスによって保護されているリソース ([カスタム認証の構成](custom-auth-config-mca.html)を参照してください)。  
* **TenantID** 値。{{site.data.keyword.amashort}} ダッシュボードでサービスを開きます。**「モバイル・オプション」**ボタンをクリックします。`tenantId` (`appGUID` とも呼ばれる) の値が、**「アプリ GUID」/「TenantId」**フィールドに表示されます。許可マネージャーを初期化するためにこの値が必要になります。
* **「レルム」**名。これは、{{site.data.keyword.amashort}} ダッシュボードの**「管理」**タブで、**「カスタム」**セクションの**「レルム名」**フィールドに指定した値です。
* バックエンド・アプリケーションの URL (**「アプリの経路 (App Route)」**)。バックエンド・アプリケーションの保護されたエンドポイントに要求を送信するためにこの値が必要になります。
* {{site.data.keyword.Bluemix_notm}} **「地域」**。**「アバター」**アイコン![「アバター」アイコン](images/face.jpg "「アバター」アイコン") の横のヘッダー内に現在の {{site.data.keyword.Bluemix_notm}} 地域が表示されます。表示される地域の値は、`「米国南部」`、`「英国」`、または`「シドニー」`のいずれかでなければならず、また WebView Javascript コードで必要な SDK 値 (`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_SYDNEY`、または `BMSClient.REGION_UK`) に対応している必要があります。{{site.data.keyword.amashort}} クライアントを初期化するためにこの値が必要になります。

詳しくは、以下の情報を参照してください。

 * [{{site.data.keyword.amashort}} 概説](getting-started.html)
 * [Android SDK のセットアップ](getting-started-android.html)
 * [カスタム ID プロバイダーの使用](custom-auth.html)
 * [カスタム ID プロバイダーの作成](custom-auth-identity-provider.html)
 * [カスタム認証用の {{site.data.keyword.amashort}} の構成 ](custom-auth-config-mca.html)



## {{site.data.keyword.amashort}} Client SDK の初期化
{: #custom-android-initialize}
{{site.data.keyword.amashort}} Android SDK が装備された Android アプリケーションがある場合は、このセクションをスキップできます。
1. Android Studio にある Android プロジェクトで、アプリケーション・モジュールの `build.gradle` ファイルを開きます (プロジェクト `build.gradle` ではありません)。

1. `build.gradle` ファイル内で `dependencies` セクションを見つけて、以下の依存関係があるか確認します。

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'core',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```
	{: codeblock}

1. プロジェクトを Gradle と同期化します。**「ツール」>「Android」>「プロジェクトを Gradle ファイルと同期 (Sync Project with Gradle Files)」**とクリックします。

1. Android プロジェクトの `AndroidManifest.xml` ファイルを開きます。
以下のように、`<manifest>` エレメントの下にインターネット・アクセス許可を追加します。

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```
	{: codeblock}

1. SDK を初期化します。  
	初期化コードを入れる一般的な場所 (ただし、必須ではない) は、Android アプリケーション内のメイン・アクティビティーの `onCreate` メソッド内です。

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

	```
	{: codeblock}

`BMSClient.REGION_UK` を {{site.data.keyword.amashort}} 地域に置き換えます。これらの値の取得について詳しくは、[開始する前に](#before-you-begin)を参照してください。


## AuthenticationListener インターフェース
{: #custom-android-authlistener}

{{site.data.keyword.amashort}} Client SDK は、カスタム認証フローを実装できるように `AuthenticationListener` インターフェースを提供しています。`AuthenticationListener` インターフェースは 3 つのメソッドを公開し、それらは認証プロセス中に異なるフェーズで呼び出されます。

### onAuthenticationChallengeReceived メソッド
{: #custom-onAuth}
{{site.data.keyword.amashort}} サービスからカスタム認証チャレンジを受け取ったときに、このメソッドを呼び出します。

```Java
void onAuthenticationChallengeReceived(AuthenticationContext authContext, JSONObject challenge, Context context);
```
{: codeblock}


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
{: codeblock}

### onAuthenticationFailure メソッド
{: #custom-android-authlistener-onfail}
認証が失敗した後、このメソッドを呼び出します。引数には、Android Context と、認証の失敗に関する詳しい情報を含む `JSONObject` (オプション) があります。
```Java
void onAuthenticationFailure(Context context, JSONObject info);
```
{: codeblock}

## AuthenticationContext インターフェース
{: #custom-android-authcontext}

`AuthenticationContext` は、カスタム `AuthenticationListener` の `onAuthenticationChallengeReceived` メソッドへの引数として提供されます。資格情報を収集し、`AuthenticationContext` のメソッドを使用して、資格情報を {{site.data.keyword.amashort}} Client SDK に返すか、失敗を報告する必要があります。以下のいずれかのメソッドを使用します。

```Java
void submitAuthenticationChallengeAnswer(JSONObject answer);
```
{: codeblock}

```Java
void submitAuthenticationFailure (JSONObject info);
```
{: codeblock}

## カスタム AuthenticationListener の実装例
{: #custom-android-samplecustom}

この AuthenticationListener サンプルは、カスタム ID プロバイダーと連携するよう設計されています。このサンプルは、[GitHub リポジトリー![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}からダウンロードできます。

```Java
package com.ibm.helloworld;
import android.content.Context;
import android.util.Log;
import com.ibm.mobilefirstplatform.clientsdk.android.security.mca.api.AuthenticationContext;
import com.ibm.mobilefirstplatform.clientsdk.android.security.mca.api.AuthenticationListener;
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
			// Access client SDK will remain in a waiting-for-credentials state
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
{: codeblock}

## カスタム AuthenticationListener の登録
{: #custom-android-register}

カスタム AuthenticationListener を作成したら、そのリスナーの使用を開始する前に `BMSClient` に登録します。以下のコードをアプリケーションに追加します。このコードは保護リソースに要求を送信する前に呼び出される必要があります。

```Java
MCAAuthorizationManager mcaAuthorizationManager = 
      MCAAuthorizationManager.createInstance(this.getApplicationContext(),"<MCAServiceTenantId>");
mcaAuthorizationManager.registerAuthenticationListener(realmName, new CustomAuthenticationListener());
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);

```
{: codeblock}


コードの中で次のようにします。
* `MCAServiceTenantId` を **TenantId** 値 (『[開始する前に](##before-you-begin)』を参照) に置き換えます。
* `realmName` には {{site.data.keyword.amashort}} ダッシュボードで指定したものを使用します ([カスタム認証の構成](custom-auth-config-mca.html)を参照してください)。


## 認証のテスト
{: #custom-android-testing}
Client SDK が初期化され、カスタム AuthenticationListener の登録が完了すると、モバイル・バックエンド・アプリケーションに要求を出すことができるようになります。

### テストする前に
{: #custom-android-testing-before}
`/protected` エンドポイントで {{site.data.keyword.amashort}} によって保護されているリソースを持つアプリケーションを用意する必要があります。


1. モバイル・バックエンド・アプリケーションの保護エンドポイント (`{applicationRoute}/protected`) にブラウザーから要求を送信します。例えば、`http://my-mobile-backend.mybluemix.net/protected` です。`{applicationRoute}` 値の取得については、『[開始する前に](#before-you-begin)』を参照してください。

1. {{site.data.keyword.mobilefirstbp}} ボイラープレートを使用して作成されたモバイル・バックエンド・アプリケーションの `/protected` エンドポイントは、{{site.data.keyword.amashort}} で保護されています。このエンドポイントは {{site.data.keyword.amashort}} Client SDK により装備されたモバイル・アプリケーションからのみアクセス可能です。その結果、`承認されていない`というメッセージがブラウザーに表示されます。

1. Android アプリケーションを使用して、`{applicationRoute}` が含まれている同じ保護エンドポイントへ要求を出します。`BMSClient` を初期化した後で次のコードを追加して、カスタムの AuthenticationListener を登録します。

	```Java
	Request request = new Request("{applicationRoute}/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp",  MCAAuthorizationManager.getInstance().getUserIdentity().toString());
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
	{: codeblock}

1. 	要求が成功したら、LogCat ツールで以下のように出力されます。

	![image](images/android-custom-login-success.png)

 次のコードを追加してログアウト機能を追加することもできます。

 ```Java
 MCAAuthorizationManager.getInstance().logout(getApplicationContext(), listener);
 ```
 {: codeblock}


 ユーザーのログイン後に、このコードを呼び出すと、そのユーザーはログアウトされます。そのユーザーが再度ログインしようとする場合は、サーバーから受信した要求に再度応じる必要があります。

 ログアウト機能に渡される `listener` の値は、`ヌル`にすることができます。
