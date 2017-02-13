---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Cordova プラグインのセットアップ
{: #getting-started-cordova}

Cordova クライアント・アプリケーションに {{site.data.keyword.amafull}} Client SDK を装備します。Android (Java) コードまたは iOS コード (Swift SDK および関連ヘッダー・ファイルを使用した Objective C) で、許可マネージャーを初期化します。クライアントを初期化し、WebView からの保護されたリソースまたは無保護のリソースへの要求を実行します。

{:shortdesc}

## 開始する前に
{: #before-you-begin}
以下が必要です。

* {{site.data.keyword.Bluemix_notm}} アプリケーションのインスタンス。{{site.data.keyword.Bluemix_notm}} バックエンド・アプリケーションの作成方法について詳しくは、[概説](index.html)を参照してください。




* {{site.data.keyword.amafull}} サービスのインスタンス。
* バックエンド・アプリケーションの URL (**「アプリの経路 (App Route)」**)。バックエンド・アプリケーションの保護されたエンドポイントに要求を送信するためにこの値が必要になります。
* **TenantID** 値。{{site.data.keyword.amashort}} ダッシュボードでサービスを開きます。**「モバイル・オプション」**ボタンをクリックします。`tenantId` (`appGUID` とも呼ばれる) の値が、**「アプリ GUID」/「TenantId」**フィールドに表示されます。許可マネージャーを初期化するためにこの値が必要になります。
* {{site.data.keyword.Bluemix_notm}} **「地域」**。**「アバター」**アイコン![「アバター」アイコン](images/face.jpg "「アバター」アイコン") の横のヘッダー内に現在の {{site.data.keyword.Bluemix_notm}} 地域が表示されます。表示される地域の値は、`「米国南部」`、`「英国」`、または`「シドニー」`のいずれかでなければならず、また WebView Javascript コードで必要な SDK 値 (`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_SYDNEY`、または `BMSClient.REGION_UK`) に対応している必要があります。{{site.data.keyword.amashort}} クライアントを初期化するためにこの値が必要になります。
* Cordova アプリケーションまたは既存のプロジェクト。Cordova アプリケーションのセットアップ方法について詳しくは、[Cordova Web サイト![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cordova.apache.org/ "外部リンク・アイコン"){: new_window}を参照してください。

## {{site.data.keyword.amashort}} Cordova プラグインのインストール
{: #getting-started-cordova-plugin}

{{site.data.keyword.amashort}} Client SDK for Cordova は、ネイティブ {{site.data.keyword.amashort}} Client SDK をラップする Cordova プラグインです。これは、Cordova コマンド・ライン・インターフェース (CLI) と、Cordova プロジェクト用のプラグイン・リポジトリーである `npmjs` を使用して配布されます。Cordova CLI は自動的にリポジトリーからプラグインをダウンロードし、Cordova アプリケーションで使用できるようにします。

1. Android プラットフォームまたは iOS プラットフォーム (あるいはその両方) を Cordova アプリケーションに追加します。以下のコマンドのいずれかまたは両方をコマンド・ラインから実行します。

	###Android
	{: #install-cordova-android}

	```
	cordova platform add android
	```
	{: codeblock}

	###iOS
	{: #install-cordova-ios}

	```Bash
	cordova platform add ios
	```
	{: codeblock}

2. Android プラットフォームを追加した場合は、Cordova アプリケーションの `config.xml` ファイルに、サポートされる最小 API レベルを追加する必要があります。`config.xml` ファイルを開き、以下の行を `<platform name="android">` エレメントに追加します。

	```XML
	<platform name="android">
		<preference name="android-minSdkVersion" value="15"/>
		<preference name="android-targetSdkVersion" value="23"/>
		<!-- add minimum and target Android API level declaration -->
	</platform>
	```
	{: codeblock}

	*minSdkVersion* の値は、`15` 以上でなければなりません。Android SDK 用にサポートされる *targetSdkVersion* を最新の状態に保つ方法については、[Android Platform Guide![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cordova.apache.org/docs/en/latest/guide/platforms/android/ "外部リンク・アイコン"){: new_window} を参照してください。

3. iOS オペレーティング・システムを追加した場合は、以下のように、ターゲット宣言で `<platform name="ios">` エレメントを更新してください。

	```XML
 	  <platform name="ios">
		<preference name="deployment-target" value="8.0"/>
		<!-- add deployment target declaration -->
	 </platform>
	```
	{: codeblock}

4. 以下のようにして、{{site.data.keyword.amashort}} Cordova プラグインをインストールします。

 	```Bash
	cordova plugin add bms-core
	```
	{: codeblock}

5. Android、iOS、またはその両方に対応するようにプラットフォームを構成します。

	####Android
	{: #cordova-android}

	Android Studio でプロジェクトを開く前に、コマンド・ライン・インターフェース (CLI) を通じて Cordova アプリケーションをビルドして、ビルド・エラーを回避します。

	```Bash
	cordova build android
	```
	{: codeblock}

	####iOS
	{: #cordova-ios}

	Xcode プロジェクトを以下のように構成します。

	1. 最新バージョンの Xcode を使用して、`<app_name>/platforms/ios` ディレクトリー内の `xcode.proj` ファイルを開きます。

		**重要:** 最新の Swift 構文に変換するメッセージが表示されたら、**「キャンセル」**をクリックします。

	2. Xcode で、アプリケーションをビルドして実行します。

	**注**: `cordova build ios` の実行時に以下のエラーを受け取ることがあります。この問題は、依存関係プラグイン内のバグが原因であり、現在、[Issue 12 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/blakgeek/cordova-plugin-cocoapods-support/issues/12 "外部リンク・アイコン"){: new_window} で追跡中です。シミュレーターまたはデバイスを使用して、XCode の iOS プロジェクトを引き続き実行できます。

	```
	xcodebuild: error: Unable to find a destination matching the provided destination specifier:
			{ platform:iOS Simulator }

		Missing required device specifier option.
		The device type “iOS Simulator” requires that either “name” or “id” be specified.
		Please supply either “name” or “id”.
	```

6. 次のコマンドを実行して、プラグインが正常にインストールされたことを確認します。

	```Bash
	cordova plugin list
	```
	{: codeblock}

7. **「Capabilities」**タブで**「Keychain Sharing」**を`「On」`に切り替えて、iOS のキーチェーン共有 (Keychain Sharing) を使用可能にします。

8. **「ビルド設定 (Build Settings)」** > **「パッケージ化 (Packaging)」**タブで、**「モジュールの定義 (Defines Module)」** を`「YES」`に切り替えて、iOS 用の**「モジュールの定義 (Defines Module)」**を使用可能にします。


## Cordova WebView (Javascript) での {{site.data.keyword.amashort}} クライアントの初期化
{: #getting-started-cordova-initialize}

{{site.data.keyword.amashort}} Client SDK を使用するには、`applicationBluemixRegion` を渡して SDK を初期化する必要があります。

以下の呼び出しを `index.js` ファイルに追加して、{{site.data.keyword.amashort}} Client SDK を初期化します。

```JavaScript
BMSClient.initialize(<applicationBluemixRegion>);
```
{: codeblock}

**注:** `<applicationBluemixRegion>` を、{{site.data.keyword.Bluemix_notm}} サービスがホストされている地域 ([開始する前に](#before-you-begin)を参照) に置き換えます。

##ネイティブ・コードからの {{site.data.keyword.amashort}} AuthorizationManager の初期化
{: #initializing-auth-manager}

`BMSAuthorizationManager` を使用するためには、以下のコード・スニペットを追加する必要があります。以下のネイティブ・コードは、{{site.data.keyword.amashort}} サービス `tenantId` ([開始する前に](#before-you-begin)を参照) を使用して、`BMSAuthorizationManager` を初期化します。

### Android (Java)

`MainActivity.java` ファイル内の `OnCreate` メソッドで、`loadUrl` の前にコードを追加します。
```Java
MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),"<tenantId>");
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
```
{: codeblock}
### iOS (Objective C)
Xcode のバージョンに応じて、`AppDelegate.m` に許可マネージャーの初期化を追加します。

```Objective-C
  #import "<your_module_name>-Swift.h"
  [CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];
```
{: codeblock}

**注:** インポートされたヘッダー・ファイル名は、モジュール名をストリング `-Swift.h` に連結して構成されます。例えば、モジュール名が `Cordova` の場合、インポート行は `#import "Cordova-Swift.h"` となります。モジュール名を見つけるには、`「ビルド設定 (Build Settings)」` > `「パッケージ化 (Packaging)」` > `「製品モジュール名 (Product Module Name)」`に移動してください。`<tenantId>` をテナント ID ([開始する前に](#before-you-begin)を参照) に置き換えます。


## モバイル・バックエンド・サービスへの要求の実行
{: #getting-started-request}

{{site.data.keyword.amashort}} Client SDK が初期化された後、モバイル・バックエンド・サービスに要求を出すことができるようになります。

1. モバイル・バックエンド・アプリケーションの、保護されたエンドポイントに要求を送信してみてください。ブラウザーで次の URL を開きます。`{applicationRoute}/protected` (例えば、`http://my-mobile-backend.mybluemix.net/protected`)

	MobileFirst Services Starter ボイラープレートを使用して作成されたモバイル・バックエンド・アプリケーションの `/protected` エンドポイントは、{{site.data.keyword.amashort}} で保護されています。 `認証されていない`というメッセージがブラウザーに戻されます。このエンドポイントにアクセスできるのは、{{site.data.keyword.amashort}} Client SDK が装備されたモバイル・アプリケーションのみであるため、このメッセージが返されます。

2. Cordova アプリケーションを使用して、同じエンドポイントに要求を実行します。`BMSClient` を初期化した後に、以下のコードを追加してください。

	```Javascript
	var success = function(data){
	 console.log("success", data);
	 }

	 var failure = function(error){
	 console.log("failure", error);
	 }

	 var request = new BMSRequest("<your route>/protected", BMSRequest.GET);

	 request.send(success, failure);
	```
	{: codeblock}

3. 要求が正常に実行されると、LogCat コンソールまたは Xcode コンソール (使用しているプラットフォームによって決まる) に以下の出力が表示されます。

	![成功メッセージ](images/getting-started-android-success.png)

	## 次のステップ
	{: #next-steps}

	保護されているエンドポイントに繋がった場合、資格情報は必要とされません。アプリケーションにユーザーのログインを要求する場合、Facebook、Google またはカスタム認証を構成する必要があります。
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [カスタム](custom-auth-cordova.html)
