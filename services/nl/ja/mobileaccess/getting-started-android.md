---

copyright:
  years: 2015, 2016
  
---

# Android SDK のセットアップ
{: #getting-started-android}

Android アプリケーションに {{site.data.keyword.amashort}} Client SDK を装備し、SDK を初期化し、保護されたリソースまたは無保護のリソースへの要求を実行します。

## 開始する前に
{: #before-you-begin}
* {{site.data.keyword.amashort}} サービスによって保護されたモバイル・バックエンドのインスタンスが存在している必要があります。モバイル・バックエンドの作成方法について詳しくは、[入門](getting-started.html)を参照してください。
* Android Studio および Android Studio SDK をセットアップします。Android 開発環境のセットアップ方法について詳しくは、[Google Developer Tools](http://developer.android.com/sdk/index.html) を参照してください。


## {{site.data.keyword.amashort}} Client SDK のインストール
{: #install-mca-sdk}

{{site.data.keyword.amashort}} Client SDK は、Android プロジェクト用の依存関係マネージャーである Gradle とともに配布されます。Gradle は、自動的にリポジトリーから成果物をダウンロードし、Android アプリケーションで使用できるようにします。

1. Android Studio プロジェクトを作成するか、既存のプロジェクトを開きます。

1. `build.gradle` ファイルを開きます。
**ヒント**: Android プロジェクトには、プロジェクト用とアプリケーション・モジュール用の 2 つの `build.gradle` ファイルがある場合があります。アプリケーション・モジュールのファイルを使用してください。



1. `build.gradle` ファイルの **Dependencies** セクションを見つけます。以下のようにして、{{site.data.keyword.amashort}} Client SDK のコンパイル依存関係を追加します。

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

1. プロジェクトを Gradle と同期化します。**「ツール」&gt;「Android」&gt;「プロジェクトを Gradle ファイルと同期 (Sync Project with Gradle Files)」**とクリックします。

1. Android プロジェクトの `AndroidManifest.xml` ファイルを開きます。以下のようにして、`<manifest>` エレメントにインターネット・アクセス許可を追加します。

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
```

## {{site.data.keyword.amashort}} Client SDK の初期化
{: #initalize-mca-sdk}

context、applicationGUID、および applicationRoute の各パラメーターを `initialize` メソッドに渡して SDK を初期化します。


1. {{site.data.keyword.Bluemix_notm}} ダッシュボードのメインページからアプリをクリックします。「**Mobile オプション**」をクリックします。SDK を初期化するには、**「アプリケーション経路 (Application route)」**と**アプリケーション GUID (Application GUID)」**の値が必要です。

2. Android アプリケーションで {{site.data.keyword.amashort}} Client SDK を初期化します。初期化コードを入れる一般的な場所 (ただし、必須ではない) は、Android アプリケーション内のメイン・アクティビティーの `onCreate` メソッド内です。
<br/>*applicationRoute* および *applicationGUID* は、{{site.data.keyword.Bluemix_notm}} ダッシュボード内の**「モバイル・オプション」**の値に置換します。
	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");```


## モバイル・バックエンドへの要求の実行
{: #request}

{{site.data.keyword.amashort}} Client SDK が初期化された後、モバイル・バックエンドに要求を出すことができるようになります。

1. 新しいモバイル・バックエンドの保護されているエンドポイントに要求を送信してみてください。ブラウザーで次の URL を開きます。`{applicationRoute}/protected` (たとえば、 `http://my-mobile-backend.mybluemix.net/protected`)
<br/>MobileFirst Services Starter ボイラープレートを使用して作成されたモバイル・バックエンドの`/protected` エンドポイントは、{{site.data.keyword.amashort}}で保護されています。このエンドポイントにアクセスできるのは、{{site.data.keyword.amashort}} Client SDK が装備されたモバイル・アプリケーションのみであるため、ブラウザーに `Unauthorized` メッセージが返されます。
1. Android アプリケーションを使用して、同じエンドポイントへの要求を実行します。`BMSClient` を初期化した後に、以下のコードを追加してください。

	```Java
	Request request = new Request("/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
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

1. 要求が正常に実行されると、LogCat ユーティリティーに以下の出力が表示されます。

	![image](images/getting-started-android-success.png)

## 次のステップ
{: #next-steps}

保護されているエンドポイントに繋がった場合、資格情報は必要とされません。アプリケーションにユーザーのログインを要求する場合、Facebook、Google またはカスタム認証を構成する必要があります。
* [Facebook](facebook-auth-android.html)
* [Google](google-auth-android.html)
* [カスタム](custom-auth-android.html)
