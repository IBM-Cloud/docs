---

copyright:
  years: 2015, 2016

---

# Cordova アプリで Facebook 認証を使用可能にする
{: #facebook-auth-cordova}
Cordova アプリケーションを Facebook 認証統合用に構成するには、Java、Objective-C、または Swift でその Cordova アプリケーションのネイティブ・コードに変更を加える必要があります。各プラットフォームは別々に構成します。ネイティブ・コードの変更は、Android Studio や Xcode などのネイティブ開発環境で行ってください。

## 開始する前に
{: #facebook-auth-before}
* {{site.data.keyword.amashort}} により保護されたリソース、および {{site.data.keyword.amashort}} Client SDK が装備された Cordova プロジェクトが必要です。詳しくは、[{{site.data.keyword.amashort}} 入門](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)および [Cordova プラグインのセットアップ](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)を参照してください。
* {{site.data.keyword.amashort}}  Server SDK を使用して手作業でバックエンド・アプリケーションを保護します。詳しくは、[リソースの保護](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)を参照してください。
* Facebook Application ID を作成します。詳しくは、[Facebook Developer Portal から Facebook アプリケーション ID を取得する](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)を参照してください。
* (オプション) 次のセクションの内容をよく理解してください。
   * [Android アプリで Facebook 認証を使用可能にする](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html)
   * [iOS アプリで Facebook 認証を使用可能にする](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html)


## Android プラットフォームの構成
{: #facebook-auth-cordova-android}

Cordova アプリケーションの Android プラットフォームを Facebook 認証統合用に構成するために必要なステップは、ネイティブ Android アプリケーションの場合とよく似ています。詳しくは、[Android アプリで Facebook 認証を使用可能にする](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html)を参照してください。以下のステップを完了してください:

* Android プラットフォーム用の Facebook アプリケーションの構成
* Facebook 認証用の {{site.data.keyword.amashort}} の構成
* Android 用の {{site.data.keyword.amashort}}  Client SDK の構成

Cordova アプリケーションを構成する際の唯一の違いは、 Java コードではなく JavaScript コードで {{site.data.keyword.amashort}} Client SDK を初期化する必要がある点です。`FacebookAuthenticationManager` API は引き続きネイティブ・コードで登録する必要があります。

## iOS プラットフォームの構成
{: #facebook-auth-cordova-ios}

Cordova アプリケーションの iOS プラットフォームを Facebook 認証統合用に構成するために必要なステップは、ネイティブ iOS アプリケーションの場合と似ています。主な違いは、現在 Cordova CLI が CocoaPods の依存関係マネージャーをサポートしていない点です。Facebook 認証との統合に必要なファイルを手動で追加する必要があります。詳しくは、[iOS アプリで Facebook 認証を使用可能にする](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html)を参照してください。以下のステップを完了してください:

* iOS プラットフォーム用の Facebook アプリケーションの構成
* Facebook 認証用の {{site.data.keyword.amashort}} の構成

### Facebook 認証のための {{site.data.keyword.amashort}} SDK および Facebook SDK の手動インストール
{: #facebook-auth-cordova-ios-sdk}
1. [{{site.data.keyword.Bluemix_notm}} Mobile Services SDK for iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master) が含まれたアーカイブをダウンロードします。

1. `Sources/Authenticators/IMFFacebookAuthentication` ディレクトリーに移動し、全てのファイルを Xcode 内の iOS プロジェクトにコピー (ドラッグ・アンド・ドロップ) します。以下のファイルをコピーしてください。
	* IMFDefaultFacebookAuthenticationDelegate.h

  * IMFDefaultFacebookAuthenticationDelegate.m

	* IMFFacebookAuthenticationDelegate.h

	* IMFFacebookAuthenticationHandler.h

	* IMFFacebookAuthenticationHandler.m

	Xcode からプロンプトが出されたら、**「ファイルをコピー... (Copy files...)」**を選択します。

1. [Facebook SDK v3.19](https://developers.facebook.com/resources/facebook-ios-sdk-3.19.pkg) をダウンロードしてインストールします。

1. Facebook SDK は `~/Documents/FacebookSDK` ディレクトリーにインストールされます。そのディレクトリーにナビゲートし、`FacebookSDK.framework` ファイルを Xcode 内の iOS プロジェクトにコピー (ドラッグ・アンド・ドロップ) します。

1. 	Xcode の左ペインにあるプロジェクト・ルートをクリックし、**「ビルド・フェーズ (Build Phases)」**を選択します。

1. `FacebookSDK.framework` ファイルを**「バイナリーをライブラリーとリンク (Link binary with libraries)」**のリンク・ライブラリーのリストに追加します。

 [Facebook 認証用の iOS プラットフォームの構成](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html)を参照してください。**「{{site.data.keyword.amashort}} Client SDK の初期化」**セクションの説明に従って、`IMFFacebookAuthenticationHandler` API をネイティブ・コードで登録します。`IMFClient` はネイティブ・コードで初期化しないでください。

アプリケーション代行の `application:openURL:sourceApplication:annotation` メソッドに以下の行を追加します。このコードにより、すべての Cordova プラグインに対し各イベントが確実に通知されます。

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```

## {{site.data.keyword.amashort}} Client SDK の初期化
{: #facebook-auth-cordova-init}

Cordova アプリケーションで以下の JavaScript コードを使用して、{{site.data.keyword.amashort}} Client SDK を初期化します。

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```

*applicationRoute* および *applicationGUID* を、**「モバイル・オプション」**から取得した**「経路」**および**「アプリ GUID」**の値に置き換えます。

## 認証のテスト
{: #facebook-auth-cordova-test}
Client SDK が初期化され、Facebook 認証マネージャーの登録が完了すると、モバイル・バックエンドに要求を出すことができるようになります。

### 開始する前に
{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用していて、{{site.data.keyword.amashort}}により`/protected` エンドポイントで保護されているリソースを既に持っている必要があります。詳しくは、[リソースの保護](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)を参照してください。

1. ブラウザーで、新しく作成されたモバイル・バックエンドの保護エンドポイントに要求を送信してみてください。次の URL を開きます。`{applicationRoute}/protected` (たとえば、 `http://my-mobile-backend.mybluemix.net/protected`)
<br/>MobileFirst Services Starter ボイラープレートを使用して作成されたモバイル・バックエンドの`/protected` エンドポイントは、{{site.data.keyword.amashort}}で保護されています。 `認証されていない`というメッセージがブラウザーに戻されます。このエンドポイントは {{site.data.keyword.amashort}} Client SDK により装備されたモバイル・アプリケーションからのみアクセス可能であるため、このメッセージが戻されます。
1. Cordova アプリケーションを使用して同じエンドポイントに対する要求を作成します。`BMSClient` を初期化した後で次のコードを追加します。

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

1. アプリケーションを実行します。Facebook のログイン画面が表示されます。

	![image](images/android-facebook-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![image](images/ios-facebook-login.png)

	> この画面は、デバイスに Facebook アプリをインストールしていない場合、または現在 Facebook に ログインしていない場合は少し違って見えるかも知れません。

1. 「**OK**」をクリックし、{{site.data.keyword.amashort}} が認証を目的として Facebook のユーザー ID を使用することを承認します。

1. 	要求が成功すると、LogCat ユーティリティーまたは Xcode コンソールに以下のように出力されます。

	![Android 用の Facebook 認証完了メッセージ](images/android-facebook-login-success.png)

	![iOS 用の Facebook 認証完了メッセージ](images/ios-facebook-login-success.png)
