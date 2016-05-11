---

copyright:
  years: 2015, 2016

---

# Android アプリでの Google 認証の使用可能化
{: #google-auth-android}

## 開始する前に
{: #before-you-begin}

* {{site.data.keyword.amashort}} によって保護されているリソース、および {{site.data.keyword.amashort}} Client SDK が装備された Android プロジェクトが必要です。詳しくは、[{{site.data.keyword.amashort}} 入門](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)および [Android SDK のセットアップ](https://console.{DomainName}/docs/services/mobileaccess/getting-started-android.html)を参照してください。  
* {{site.data.keyword.amashort}}  Server SDK を使用して手作業でバックエンド・アプリケーションを保護します。詳しくは、[リソースの保護](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)を参照してください。

## Android プラットフォーム用の Google プロジェクトの構成
{: #google-auth-android-project}
Google を ID プロバイダーとして使用することを開始するには、Google Developer Console 内にプロジェクトを作成します。プロジェクト作成の一部は、Google のクライアント ID を取得することです。Google クライアント ID は、Google の認証で使用される、アプリケーションの固有 ID です。

1. [Google Developer Console](https://console.developers.google.com)にプロジェクトを作成します。既にプロジェクトがある場合は、プロジェクト作成について説明している手順をスキップし、資格情報の追加を開始してください。
   1.    新規プロジェクトのメニューを開きます。 
         
         ![image](images/FindProject.jpg)

   2.    **「プロジェクトの作成 (Create a project)」**をクリックします。
   
         ![image](images/CreateAProject.jpg)


   1. **「Social API」**リストから、**「Google+ API」**を選択します。

     ![image](images/chooseGooglePlus.jpg)

   1. 次の画面から、**「使用可能 (Enable)」**をクリックします。

1. **「同意取得」**タブを選択し、ユーザーに表示する製品名を指定します。その他の値はオプションです。**「保存」**をクリックします。

    ![image](images/consentScreen.png)
    
1. **「資格情報」**リストから、「OAuth クライアント ID」を選択します。

     ![image](images/chooseCredentials.png)
     


1. アプリケーション・タイプを選択します。**「Android」**をクリックします。Android クライアントに、意味のある名前を指定します。

1. Google がユーザーのアプリケーションの認証性を検証するためには、署名証明書の指紋を指定する必要があります。

	 **Android セキュリティーの追加情報:** Android OS では、Android デバイス上にインストールされているすべてのアプリケーションがデベロッパー証明書によって署名されていることが要求されます。Android アプリケーションは、デバッグおよびリリースという 2 つのモードで構築できます。通常は、デバッグ・モード用とリリース・モード用に別々の証明書を用意することが推奨されます。デバッグ・モードでの Android アプリケーションの署名に使用される証明書は、Android SDK にバンドルされています。Android SDK は、通常、Android Studio によって自動的にインストールされます。アプリケーションを Google Play にリリースする場合は、通常ユーザー自身で生成する、別の証明書を使用してアプリに署名する必要があります。詳しくは、[signing your Android applications](http://developer.android.com/tools/publishing/app-signing.html) を参照してください。

1. 開発環境用の証明書が含まれた鍵ストアは、`~/.android/debug.keystore` ファイル内に保管されています。鍵ストアのデフォルト・パスワードは、`android` です。この証明書は、デバッグ・モードでのアプリケーションの構築に使用されます。

     1. 署名証明書の指紋を取得するには、以下のように指定します。

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore -list -v
	```
	リリース・モードの証明書の鍵ハッシュも同じ構文を使用して取得できます。コマンド内の別名と鍵ストアのパスを置換してください。

1. **「Certificate Fingerprints」**の下で `SHA1` で始まる行を見つけます。**keytool** コマンドを実行して取得した指紋を Google Developer Console にコピーします。

1. Android アプリケーションのパッケージ名を指定します。Android アプリケーションのパッケージ名を見つけるには、Android Studio で `AndroidManifest.xml` ファイルを開き、`<manifest package="{your-package-name}">` を探してください。完了したら、**「Create (作成)」**をクリックします。

Google クライアント ID を示すダイアログが表示されます。この値のメモを取ります。この値を {{site.data.keyword.Bluemix}} に登録する必要があります。


## Google 認証用の {{site.data.keyword.amashort}} の構成
{: #google-auth-android-config}

Android の Google クライアント ID を取得したので、{{site.data.keyword.amashort}} ダッシュボードで Google 認証を有効にすることができます。

1. {{site.data.keyword.Bluemix_notm}}ダッシュボードでアプリを開きます。

1. **「モバイル・オプション」**をクリックし、**「経路」** (`applicationRoute`) と **「アプリ GUID」** (`applicationGUID`) のメモを取ります。SDK を初期化する際に、これらの値が必要になります。

1. {{site.data.keyword.amashort}} タイルをクリックします。{{site.data.keyword.amashort}} ダッシュボードがロードされます。

1. **「Google」**タイルをクリックします。

1. **「Android のアプリケーション ID (Application ID for Android)」**で、Android の Google クライアント ID を指定し、**「保存」**をクリックします。

## Android 用の {{site.data.keyword.amashort}}  Client SDK の構成
{: #google-auth-android-sdk}

1. Android Studio に戻ります。

1. アプリケーション・モジュールの `build.gradle` ファイルを開きます。


	Android プロジェクトは、2 つの `build.gradle` ファイル (1 つはプロジェクト用で、もう 1 つはアプリケーション・モジュール用) を持っている場合があります。アプリケーション・モジュール用を使用します。

  以下のように、依存関係セクションを見つけ、Client SDK の新しいコンパイル依存関係を追加します。

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

	`com.ibm.mobilefirstplatform.clientsdk.android` グループの `core` モジュールへの依存関係がある場合は削除することができます。`googleauthentication` モジュールは、ユーザーの代わりに自動的にそれをダウンロードします。`googleauthentication` モジュールは、Google SDK をダウンロードし、Android プロジェクトにインストールします。

1. **「ツール」>「Android」>「プロジェクトを Gradle ファイルと同期 (Sync Project with Gradle Files)」**をクリックして Gradle とプロジェクトを同期します。

1. Android プロジェクトの `AndroidManifest.xml` ファイルを開きます。


1. 以下のようにして、`<manifest>` エレメントにインターネット・アクセス許可を追加します。

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.GET_ACCOUNTS" />
<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	```

1. {{site.data.keyword.amashort}} Client SDK を使用するには、context、applicationGUID、および applicationRoute の各パラメーターを渡して初期化する必要があります。

	初期化コードを入れる一般的な場所 (ただし、必須ではない) は、Android アプリケーション内のメイン・アクティビティーの onCreate メソッド内です。

1. Client SDK を初期化し、Google 認証マネージャーを登録します。*applicationRoute* および *applicationGUID* を、ダッシュボード内の**「モバイル・オプション」**セクションから取得した**「経路」**および**「アプリ GUID」**の値に置き換えます。

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");

	GoogleAuthenticationManager.getInstance().register(this);```

1. 以下のコードをアクティビティーに追加します。

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		GoogleAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```

## 認証のテスト
{: #google-auth-android-test}
Client SDK が初期化され、Google 認証マネージャーが登録されたら、モバイル・バックエンドへの要求の実行を開始できます。

### 開始する前に
{: #google-auth-android-testing-before}
MobileFirst Services Starter ボイラープレートを使用して作成されたモバイル・バックエンドがあり、`/protected` エンドポイントに {{site.data.keyword.amashort}} によって保護されたリソースが既に存在している必要があります。詳しくは、[リソースの保護](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)を参照してください。

1. `{applicationRoute}/protected` (例えば、`http://my-mobile-backend.mybluemix.net/protected`) を開いて、デスクトップ・ブラウザーで、モバイル・バックエンドの保護エンドポイントに要求を送信してみてください。MobileFirst Services ボイラープレートを使用して作成されたモバイル・バックエンドの `/protected` エンドポイントは、{{site.data.keyword.amashort}} によって保護されています。したがって、このエンドポイントにアクセスできるのは、{{site.data.keyword.amashort}} Client SDK が装備されたモバイル・アプリケーションのみになります。結果的に、デスクトップ・ブラウザーに `Unauthorized` が表示されます。

1. Android アプリケーションを使用して同じエンドポイントに対する要求を作成します。`BMSClient` インスタンスを初期化し、`GoogleAuthenticationManager` を登録した後、以下のコードを追加します。

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

1. アプリケーションを実行します。Google のログイン画面が表示されます。ログイン後、アプリは、リソースへのアクセス許可を要求します。

	![image](images/android-google-login.png)

	ご使用の Android デバイスと、現在 Google にログインしているかどうかによって、UI が異なる可能性があります。

  **「OK」**をクリックして、{{site.data.keyword.amashort}} が Google ユーザー ID を認証目的に使用することを許可します。

1. 	要求が正常に実行されると、LogCat ツールに以下の出力が表示されます。

	![image](images/android-google-login-success.png)

1. 次のコードを追加してログアウト機能を追加することもできます。

 ```Java
 GoogleAuthenticationManager.getInstance().logout(getApplicationContext(),, listener);
 ```

 ユーザーが Google にログインした後で、このコードを呼び出すと、そのユーザーは Google からログアウトされます。そのユーザーが再度ログインしようとする場合は、再度のログイン先での、Google アカウントを選択する必要があります。以前にログインした Google ID を使用してログインしようとする場合は、資格情報を求めるプロンプトが再度ユーザーに出されることはありません。ログインの資格情報を求めるプロンプトが再度出されるようにするには、ユーザーは、Android デバイスから Google アカウントを削除する必要があります。

 ログアウト機能に渡される `listener` の値は、ヌルにすることができます。
