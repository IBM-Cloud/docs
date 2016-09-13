---

copyright:
  years: 2015, 2016
  
---
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Android SDK のセットアップ
{: #getting-started-android}

最終更新日: 2016 年 8 月 2 日
{: .last-updated}

Android アプリケーションに {{site.data.keyword.amashort}} Client SDK を装備し、SDK を初期化し、保護されたリソースまたは無保護のリソースへの要求を実行します。
{:shortdesc}

## 開始する前に
{: #before-you-begin}
以下が必要です。
* {{site.data.keyword.amashort}} サービスによって保護された {{site.data.keyword.Bluemix_notm}} アプリケーションのインスタンス。{{site.data.keyword.Bluemix_notm}} バックエンド・アプリケーションの作成方法について詳しくは、[入門](index.html)を参照してください。
* Gradle と連動して機能するようにセットアップされた Android Studio プロジェクト。Android 開発環境のセットアップ方法について詳しくは、[Google Developer Tools](http://developer.android.com/sdk/index.html) を参照してください。


## {{site.data.keyword.amashort}} Client SDK のインストール
{: #install-mca-sdk}

{{site.data.keyword.amashort}} Client SDK は、Android プロジェクト用の依存関係マネージャーである Gradle とともに配布されます。Gradle は、自動的にリポジトリーから成果物をダウンロードし、Android アプリケーションで使用できるようにします。

1. Android Studio プロジェクトを作成するか、既存のプロジェクトを開きます。

1. アプリケーションの `build.gradle` ファイルを開きます (プロジェクト `build.gradle` ファイル**ではありません**)。

1. `build.gradle` ファイルの **dependencies** セクションを見つけます。以下のようにして、{{site.data.keyword.amashort}} Client SDK のコンパイル依存関係を追加します。

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

1. プロジェクトを Gradle と同期化します。**「ツール」&gt;「Android」&gt;「プロジェクトを Gradle ファイルと同期 (Sync Project with Gradle Files)」**とクリックします。

1. Android プロジェクトの `AndroidManifest.xml` ファイルを開きます。以下のようにして、`<manifest>` エレメントにインターネット・アクセス許可を追加します。

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
```

## {{site.data.keyword.amashort}} Client SDK の初期化
{: #initalize-mca-sdk}

`context` パラメーター、`applicationGUID` パラメーター、`applicationRoute` パラメーター、および `BMSClient.REGION_UK` パラメーターを `initialize` メソッドに渡すことによって、SDK を初期化します。


1. {{site.data.keyword.Bluemix_notm}} ダッシュボードのメインページからアプリをクリックします。「**Mobile オプション**」をクリックします。SDK を初期化するには、**「アプリケーション経路 (Application route)」**と**アプリケーション GUID (Application GUID)」**の値が必要です。

2. Android アプリケーションで {{site.data.keyword.amashort}} Client SDK を初期化します。初期化コードを入れる一般的な場所 (ただし、必須ではない) は、Android アプリケーション内のメイン・アクティビティーの `onCreate` メソッド内です。
<br/>*applicationRoute* および *applicationGUID* は、{{site.data.keyword.Bluemix_notm}} ダッシュボード内の**「モバイル・オプション」**の値に置換します。

```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID",
					BMSClient.REGION_UK);
```
`
BMSClient.REGION_UK` は適切な地域に置き換えてください。 	

{{site.data.keyword.Bluemix_notm}} 地域を表示するには、メニュー・バーにある**「アバター」**アイコン ![「アバター」アイコン](images/face.jpg "「アバター」アイコン") をクリックして、**「アカウントとサポート」**ウィジェットを開きます。

## モバイル・バックエンド・アプリケーションへの要求の実行
{: #request}

{{site.data.keyword.amashort}} Client SDK が初期化された後、モバイル・バックエンド・アプリケーションに要求を出すことができるようになります。

1. 新しいモバイル・バックエンド・アプリケーションの、保護されたエンドポイントに要求を送信してみてください。ブラウザーで次の URL を開きます。`{applicationRoute}/protected` (たとえば、 `http://my-mobile-backend.mybluemix.net/protected`)
<br/>MobileFirst Services Starter ボイラープレートを使用して作成されたモバイル・バックエンド・アプリケーションの `/protected` エンドポイントは、{{site.data.keyword.amashort}} で保護されています。このエンドポイントにアクセスできるのは、{{site.data.keyword.amashort}} Client SDK が装備されたモバイル・アプリケーションのみであるため、ブラウザーに `Unauthorized` メッセージが返されます。

1. Android アプリケーションを使用して、同じエンドポイントへ要求を出します。`BMSClient` を初期化した後に、以下のコードを追加してください。

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

1. 要求が正常に実行されると、LogCat ユーティリティーで以下の出力が表示されます。

	![image](images/getting-started-android-success.png)

## 次のステップ
{: #next-steps}

保護されているエンドポイントに繋がった場合、資格情報は必要とされません。アプリケーションにユーザーのログインを要求する場合、Facebook、Google またはカスタム認証を構成する必要があります。
* [Facebook](facebook-auth-android.html)
* [Google](google-auth-android.html)
* [カスタム](custom-auth-android.html)
