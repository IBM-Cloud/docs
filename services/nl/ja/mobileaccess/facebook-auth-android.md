---

copyright:
  years: 2015, 2016

---
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Android アプリ用の Facebook 認証の使用可能化
{: #facebook-auth-android}

*最終更新日: 2016 年 7 月 5 日*
{: .last-updated}


Android アプリケーションで Facebook を ID プロバイダーとして使用するには、Facebook for Developers サイトで Facebook アプリケーション用に Android プラットフォームを追加して構成する必要があります。
{:shortdesc}

## 開始する前に
{: #facebook-auth-android-before}
以下が必要です。
* Gradle と連動して機能するように構成された Android プロジェクト。このプロジェクトに {{site.data.keyword.amashort}} Client SDK が装備される必要はありません。  
* {{site.data.keyword.amashort}} サービスによって保護された {{site.data.keyword.Bluemix_notm}} アプリケーションのインスタンス。{{site.data.keyword.Bluemix_notm}} バックエンド・アプリケーションの作成方法について詳しくは、[入門](index.html)を参照してください。




* Facebook for Developers サイト (https://developers.facebook.com) 上の Android プラットフォームを伴う Facebook アプリ。

**重要:** Facebook SDK (`com.facebook.FacebookSdk`) を別個にインストールする必要はありません。Facebook SDK は、{{site.data.keyword.amashort}} Facebook Client SDK を追加する際に Gradle によって自動的にインストールされます。Facebook for Developers サイトで Android プラットフォームを追加する場合はこのステップをスキップできます。

## Android プラットフォーム用の Facebook アプリケーションの構成
{: #facebook-auth-android-config}
Facebook for Developers サイト (https://developers.facebook.com) から以下を行います。

1. Facebook for Developers サイトで自分のアカウントにログインします。
2. Android プラットフォームを追加または構成します。詳しい情報が次のステップのためにそこで提供されます。
1. Google Play パッケージ名のプロンプトで、Android アプリケーションのパッケージ名を指定します。Android アプリケーションのパッケージ名を見つけるには、Android Studio プロジェクト内の `AndroidManifest.xml` ファイルで `<manifest ..... package="{your-package-name}">` を探してください。

1. **クラス名**のプロンプトでメイン・アクティビティーのクラス名を指定します。クラス名は、activity で囲まれた中にある `android:name` プロパティーの値です。`AndroidManifest.xml` ファイル内に複数の activity がある場合、`<intent-filter>` を含んでいる activity を探してください。

	```XML
	<activity
		android:name=".MainActivity"
		android:label="@string/app_name">
		<intent-filter>
			<action android:name="android.intent.action.MAIN"/>
			<category android:name="android.intent.category.LAUNCHER"/>
		</intent-filter>
	</activity>
	```

1. Facebook でアプリケーションの認証性を確保するためには、ご使用のデベロッパー証明書 SHA1 のハッシュを指定する必要があります。

	**Android セキュリティーの詳細:** Android OS では、Android デバイスにインストールされたすべてのアプリケーションがデベロッパー証明書によって署名されている必要があります。Android アプリケーションのビルドは、デバッグ・モードとリリース・モードの 2 つのモードで行えます。<br/>
  デバッグ・モードとリリース・モードには、異なる証明書を使用してください。デバッグ・モードで Android アプリケーションの署名に使用する証明書は Android SDK にバンドルされています。Android SDK は通常、Android Studio によって自動的にインストールされます。作成したアプリを Google Play ストアでリリースする場合、通常自身で生成する別の証明書を使ってアプリに署名する必要があります。<br/>Facebook のキー・ハッシュは 2 セット入力することができます。1 つはデバッグ証明書を使用してデバッグ・モードでビルドされたアプリケーションのキー・ハッシュで、もう 1 つはリリース証明書を使用してリリース・モードでビルドされたアプリケーションのキー・ハッシュです。詳しくは、[signing your Android applications](http://developer.android.com/tools/publishing/app-signing.html) を参照してください。1. 開発環境用に使用する証明書が含まれた鍵ストアは、`~/.android/debug.keystore` ファイルに保管されています。デフォルトの鍵ストア・パスワードは `android` です。デバッグ・モードでアプリケーションをビルドする際はこの証明書を使用してください。

1. 以下の要領でデバッグ・モード証明書のキー・ハッシュを取得します。

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore | openssl sha1 -binary | openssl base64
	```

	**ヒント**: リリース・モード証明書のキー・ハッシュを取得する際にも同じ構文が使用できます。コマンド内の別名と鍵ストアのパスを置換してください。

1. **keytool** コマンドで取得したキー・ハッシュをコピーして、Facebook for Developers サイト内の開発／リリース用キー・ハッシュのプロンプトにペーストします。

	**ヒント**: この機能を使用する予定がある場合は、シングル・サインオンを使用可能にすることを検討してください。

1. **「設定の保存」**をクリックします。

## Facebook 認証用の {{site.data.keyword.amashort}} の構成
{: #facebook-auth-android-mca}
Facebook Application ID を取得し、Android クライアントに対して機能するよう Facebook アプリケーションを構成したら、{{site.data.keyword.amashort}} ダッシュボードで Facebook 認証を使用可能にすることができます。

1. {{site.data.keyword.Bluemix_notm}}ダッシュボードでアプリを開きます。

1. **「モバイル・オプション」**をクリックし、**「経路」** (`applicationRoute`) と **「アプリ GUID」** (`applicationGUID`) のメモを取ります。SDK を初期化する際に、これらの値が必要になります。

1. {{site.data.keyword.amashort}} タイルをクリックします。{{site.data.keyword.amashort}} ダッシュボードがロードされます。

1. **「Facebook」**パネルで**「構成」**ボタンをクリックします。

1. Facebook Application ID を指定して**「保存」**をクリックします。

## Android 用の {{site.data.keyword.amashort}} Client SDK の構成
{: #facebook-auth-android-sdk}
Client SDK を Android 用に構成するには、Android Studio 内の Gradle 依存関係マネージャーを使用します。

1.  アプリケーション・モジュールの `build.gradle` ファイルを開きます。
ご使用の Android プロジェクトには、プロジェクト用とアプリケーション・モジュール用の 2 つの `build.gradle` ファイルが含まれている可能性があります。アプリケーション・モジュールのファイルを使用してください。

1. `build.gradle` ファイルの依存関係セクションを探し、Client SDK 用の新しいコンパイル依存関係を追加します。

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

	**注:** `com.ibm.mobilefirstplatform.clientsdk.android` グループの `core` モジュールへの依存関係がファイル内にある場合は削除することができます。`facebookauthentication` モジュールは、`core` モジュールと、Facebook 自体の SDK を自動的にダウンロードします。

  

  更新を保存すると、`facebookauthentication` モジュールはすべての必要な SDK をダウンロードして Android プロジェクトにインストールします。


1. プロジェクトを Gradle と同期化します。**「ツール」>「Android」>「プロジェクトを Gradle ファイルと同期 (Sync project with Gradle Files)」**とクリックします。

1. `res/values/strings.xml` ファイルを開いて、Facebook Application ID が入った `facebook_app_id` ストリングを追加します。

	```XML
	<resources>
		<string name="app_name">HelloWorld</string>
		<string name="action_settings">Settings</string>
		<string name="facebook_app_id">522733366802111</string>
	</resources>
```

1. Android プロジェクトの `AndroidManifest.xml` ファイルで、以下を実行します。
   1. 以下のように、`<manifest>` エレメントの下にインターネット・アクセス許可を追加します。

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```
  2. Facebook SDK に必要なメタデータを `<application>` エレメントに追加します。

	```XML
	<application .......>

		<meta-data
			android:name="com.facebook.sdk.ApplicationId"
			android:value="@string/facebook_app_id"/>

		<activity ...../>
		<activity ...../>
	</application>
                        ```

   1. 既存のアクティビティーの下に Facebook Activity エレメントを追加します。

	```XML
	<application .....>
		<activity ...../>
		<activity ...../>
	<activity 	android:name="com.facebook.FacebookActivity"
					android:configChanges=
						"keyboard|keyboardHidden|screenLayout|screenSize|orientation"
					android:theme="@android:style/Theme.Translucent.NoTitleBar"
					android:label="@string/app_name" />

	</application>
                        ```

1. Client SDK を初期化し、Facebook 認証マネージャーを登録します。コンテキスト、アプリ GUID (`applicationGUID`)、および経路 (`applicationRoute`) の各パラメーターを渡すことによって、{{site.data.keyword.amashort}} Client SDK を初期化します。<br/>
初期化コードを入れる一般的な場所 (ただし、必須ではない) は、Android アプリケーション内のメイン・アクティビティーの `onCreate` メソッド内です。<br/>
*applicationRoute* および *applicationGUID* を、Bluemix ダッシュボード内のご使用のアプリのメインページにある**「モバイル・オプション」**メニューの**「経路」**および**「アプリ GUID」**の値と置き換えてください。

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID",
					BMSClient.REGION_UK);
FacebookAuthenticationManager.getInstance().register(this);
```
,
					
`BMSClient.REGION_UK` は適切な地域に置き換えてください。

1. 以下のコードをアクティビティーに追加します。

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
```

## 認証のテスト
Client SDK が初期化され、Facebook 認証マネージャーの登録が完了すると、モバイル・バックエンドに要求を出すことができるようになります。

### 開始する前に
{: #facebook-auth-android-testing-before}
{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用していて、{{site.data.keyword.amashort}}により`/protected` エンドポイントで保護されているリソースを既に持っている必要があります。`/protected` エンドポイントをセットアップする必要がある場合、[リソースの保護 ](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)を参照してください。

1. ブラウザーで、新しく作成されたモバイル・バックエンド・アプリケーションの保護エンドポイントへの要求の送信を試行します。次の URL を開きます。`{applicationRoute}/protected` (たとえば、 `http://my-mobile-backend.mybluemix.net/protected`)
<br/>MobileFirst Services Starter ボイラープレートを使用して作成されたモバイル・バックエンド・アプリケーションの `/protected` エンドポイントは、{{site.data.keyword.amashort}} で保護されています。 `認証されていない`というメッセージがブラウザーに戻されます。このエンドポイントは {{site.data.keyword.amashort}} Client SDK により装備されたモバイル・アプリケーションからのみアクセス可能であるため、このメッセージが戻されます。

1. Android アプリケーションを使用して、同じエンドポイントへ要求を出します。`BMSClient` を初期化し、`FacebookAuthenticationManager` を登録した後、次のコードを追加します。

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

1. アプリケーションを実行します。Facebook のログイン画面が表示されます。

	![image](images/android-facebook-login.png)

	この画面は、デバイスに Facebook アプリをインストールしていない場合、または現在 Facebook に ログインしていない場合は少し違って見えるかもしれません。 

1. 「**OK**」をクリックし、{{site.data.keyword.amashort}} が認証を目的として Facebook のユーザー ID を使用することを承認します。

1. 	要求が成功すると、以下の出力が LogCat ユーティリティーに表示されます。

	![image](images/android-facebook-login-success.png)

 次のコードを追加してログアウト機能を追加することもできます。

 ```
FacebookAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
 ```

 ユーザーが Facebook にログインした後で、このコードを呼び出すと、そのユーザーは Facebook からログアウトされます。そのユーザーが再度ログインしようとする場合は、Facebook 資格情報を求めるプロンプトが出されます。

 ログアウト機能に渡される `listener` の値は、`ヌル`にすることができます。
