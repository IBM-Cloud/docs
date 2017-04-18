---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# iOS アプリ用の Google 認証の使用可能化 (Swift SDK)
{: #google-auth-ios}

Google Sign-In を使用して、{{site.data.keyword.amafull}} iOS Swift アプリのユーザーを認証します。


## 開始する前に
{: #before-you-begin}

以下が必要です。

* {{site.data.keyword.amafull}} サービスのインスタンスおよび {{site.data.keyword.Bluemix_notm}} アプリケーション。{{site.data.keyword.Bluemix_notm}} バックエンド・アプリケーションの作成方法について詳しくは、[概説](index.html)を参照してください。




* バックエンド・アプリケーションの URL (**「アプリの経路 (App Route)」**)。バックエンド・アプリケーションの保護されたエンドポイントに要求を送信するためにこの値が必要になります。
* **TenantID** 値。{{site.data.keyword.amashort}} ダッシュボードでサービスを開きます。**「モバイル・オプション」**ボタンをクリックします。`tenantId` (`appGUID` とも呼ばれる) の値が、**「アプリ GUID」/「TenantId」**フィールドに表示されます。許可マネージャーを初期化するためにこの値が必要になります。
* {{site.data.keyword.Bluemix_notm}} **「地域」**。**「アバター」**アイコン![「アバター」アイコン](images/face.jpg "「アバター」アイコン") の横のヘッダー内に現在の {{site.data.keyword.Bluemix_notm}} 地域が表示されます。表示される地域の値は、**「米国南部」**、**「英国」**、または**「シドニー」**のいずれかでなければならず、またコードで必要な値 (`BMSClient.Region.usSouth`、`BMSClient.Region.unitedKingdom`、または `BMSClient.Region.sydney`) に対応している必要があります。
* Xcode の iOS プロジェクト。{{site.data.keyword.amashort}} Client SDK が装備されている必要はありません。  


## Google Sign-In 用のアプリの準備
{: #google-sign-in-ios}

Google の [Google Sign-In for iOS ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developers.google.com/identity/sign-in/ios/start-integrating "外部リンク・アイコン"){: new_window}に記載されている指示に従って、Google サインイン用にアプリを準備します。

このプロセスは以下を行います。

* Google Developers サイトで新規プロジェクトを準備します。
* `GoogleService-Info.plist` ファイルと `REVERSE_CLIENT_ID` 値を作成して、Xcode プロジェクトに追加します。
* **Google Client ID** を作成して {{site.data.keyword.Bluemix_notm}} バックエンド・アプリケーションに追加します。

以下のステップでは、アプリを準備するために必要な作業について、簡単な概要を示します。

**注:** Google Sign-In CocoaPod を追加する必要はありません。必要な SDK は `BMSGoogleAuthentication` CocoaPod によって追加されます。

1. メイン・ターゲットの**「General」**タブの**「Identity」**セクションから、Xcode プロジェクト内の**「Bundle Identifier」**をメモします。これは Google Sign-In プロジェクトの作成に必要です。

1. [Google Developer サイト![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developers.google.com/mobile/add?platform=ios "外部リンク・アイコン"){: new_window}上に Google Sign-In for iOS 用のプロジェクトを作成します。

1. プロジェクトに Google Sign-In API を追加します。

1. `GoogleService-Info.plist` を取得します。

   **重要:** `GoogleService-Info.plist` ファイルの取得時に、そのファイルを開いて、`CLIENT_ID` の値のメモを取ってください。後で、{{site.data.keyword.amashort}} バックエンド・アプリケーションを構成するためにこの値が必要になります。

1. Xcode プロジェクトに `GoogleService-Info.plist` ファイルを追加します。詳しくは、[Add the configuration file to your project ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config "外部リンク・アイコン"){: new_window}を参照してください。

1. Xcode プロジェクト内の URL スキームを、自分の `REVERSE_CLIENT_ID` およびバンドル ID によって更新します。詳しくは、[Add URL schemes to your project ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developers.google.com/identity/sign-in/ios/start-integrating#add_a_url_scheme_to_your_project "外部リンク・アイコン"){: new_window}を参照してください。

1. アプリの `project-Bridging-Header.h` ファイルを以下のコードで更新します。

	```
	#import <Google/SignIn.h>
	```
	{: codeblock}

	ブリッジング・ヘッダー・ファイルの更新について詳しくは、[Enable sign-in ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developers.google.com/identity/sign-in/ios/sign-in#enable_sign-in "外部リンク・アイコン"){: new_window}を参照してください。

## Google 認証用の {{site.data.keyword.amashort}} の構成
{: #google-auth-ios-config}

これで iOS のクライアント ID を取得したので、{{site.data.keyword.amashort}} サービスで Google 認証を使用可能にすることができます。

1. {{site.data.keyword.amashort}} ダッシュボードでサービスを開きます。
1. **「管理」**タブで、**「許可」**をオンに切り替えます。
1. **「Google」**セクションを展開します。
1. **「iOS のアプリケーション ID (Application ID for iOS)」**で、`GoogleService-Info.plist` ファイルから取得した `CLIENT_ID` 値を指定します。
1. **「保存」**をクリックします。

## iOS 用の {{site.data.keyword.amashort}} Client SDK の構成
{: #google-auth-ios-sdk}

### CocoaPods のインストール
{: #install-cocoapods}

1. 端末を開き、**pod --version** コマンドを実行します。既に CocoaPods がインストールされている場合は、バージョン番号が表示されます。次のセクションにスキップして SDK をインストールできます。

1. CocoaPods をインストールしていない場合は、以下を実行します。

	```
	sudo gem install cocoapods
```
	{: codeblock}

詳しくは、[CocoaPods Web サイト![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cocoapods.org/ "外部リンク・アイコン"){: new_window}を参照してください。

### CocoaPods を使用した {{site.data.keyword.amashort}} Client Swift SDK のインストール
{: #facebook-auth-install-swift-cocoapods}

1. iOS プロジェクト内に `Podfile` がない場合、`pod init` を実行してファイルを作成します。

1. `Podfile` を編集して、関連するターゲットに以下の行を追加します。

	```
	use_frameworks!
	pod 'BMSGoogleAuthentication'
	```
	{: codeblock}

	**注:** 既に {{site.data.keyword.amashort}} コア SDK をインストール済みの場合は、行 `pod 'BMSSecurity'` を削除できます。`BMSGoogleAuthentication` pod は、必要なすべてのフレームワークをインストールします。

	**ヒント:** `use_frameworks!` を、Podfile に含めるのではなく、Xcode ターゲットに追加できます。

1. `Podfile` を保存し、コマンド・ラインから `pod install` を実行します。CocoaPods は依存関係をインストールします。進行状況と、どのコンポーネントが追加されたかが表示されます。

	**重要**: この時点で、CocoaPods によって生成された `xcworkspace` ファイルを使用してプロジェクトを開く必要があります。通常、名前は `{your-project-name}.xcworkspace` です。  

1. コマンド・ラインから `open {your-project-name}.xcworkspace` を実行して、iOS プロジェクトのワークスペースを開きます。

1. `GoogleAuthenticationManager.swift` ファイルを、`BMSGoogleAuthentication` pod ソース・ファイルからプロジェクト・ディレクトリーにコピーします。

### iOS のキーチェーン共有 (Keychain Sharing) の使用可能化
{: #enable_keychain}

`「キーチェーン共有 (Keychain Sharing)」`を使用可能にします。Xcode プロジェクトで、`「Capabilities」`タブに移動し、`「Keychain Sharing」`を`「On」`に切り替えます。


## {{site.data.keyword.amashort}} Client Swift SDK の初期化
{: #google-auth-ios-initialize}

{{site.data.keyword.amashort}} Client SDK を使用するには、`tenantID` パラメーターを渡して、それを初期化します。

初期化コードを入れる場所は一般的に (必須ではありませんが)、アプリケーション代行の `application:didFinishLaunchingWithOptions` メソッドの中です。

1. {{site.data.keyword.amashort}} Client SDK を使用したいクラス内で必要なフレームワークをインポートします。以下のヘッダーを追加します。

	```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {

 let mcaAuthManager = MCAAuthorizationManager.sharedInstance
		mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
		//the regionName should be one of the following: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney   
		BMSClient.sharedInstance.authorizationManager = mcaAuthManager
		GoogleAuthenticationManager.sharedInstance.register()
		return true
	}

	// [START openurl]
	    func application(_ application: UIApplication,
			     open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
		return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, sourceApplication: sourceApplication, annotation: annotation)
      }

 @available(iOS 9.0, *)
 func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any]) -> Bool {
		return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, options: options)
  }
 ```
	{: codeblock}

	コードの中で次のようにします。

      * `<serviceTenantID>` を、**「モバイル・オプション」**で取得した値に置き換えます。
      * `<applicationBluemixRegion>` をご使用の {{site.data.keyword.Bluemix_notm}} **「地域」**に置き換えます。

	これらの値の取得について詳しくは、[開始する前に](#before-you-begin)を参照してください。


## 認証のテスト
{: #google-auth-ios-testing}

Client SDK が初期化され、Google 認証マネージャーの登録が完了すると、モバイル・バックエンド・アプリケーションに要求を出すことができるようになります。

### 開始する前に
{: #google-auth-ios-testing-before}

{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用していて、{{site.data.keyword.amashort}}により`/protected` エンドポイントで保護されているリソースを既に持っている必要があります。`/protected` エンドポイントをセットアップする必要がある場合、[リソースの保護 ](protecting-resources.html)を参照してください。

1. デスクトップ・ブラウザーで、`{applicationRoute}/protected` を開いて、モバイル・バックエンド・アプリケーションの保護エンドポイントへの要求の送信を試行します。例: `http://my-mobile-backend.mybluemix.net/protected`。

1. MobileFirst Services ボイラープレートを使用して作成されたモバイル・バックエンド・アプリケーションの `/protected` エンドポイントは、{{site.data.keyword.amashort}} によって保護されています。したがって、このエンドポイントにアクセスできるのは、{{site.data.keyword.amashort}} Client SDK が装備されたモバイル・アプリケーションのみです。結果的に、デスクトップ・ブラウザーに `Unauthorized` が表示されます。

1. iOS アプリケーションを使用して、同じエンドポイントへ要求を出します。

	```Swift
	let protectedResourceURL = "<your protected resource absolute path>"
	let request = Request(url: protectedResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
     if error == nil {
             print ("response:\(response?.responseText), no error")
 } else {
    print ("error: \(error)")
  }
  }

	request.send(completionHandler: callBack)

	```
	{: codeblock}

1. アプリケーションを実行します。Google のログイン画面のポップアップが表示されます。

 ![image](images/ios-google-login.png)

1. ログインして**「OK」**をクリックすると、{{site.data.keyword.amashort}} が Google ユーザー ID を認証目的に使用することを許可したことになります。

1. ユーザーの要求は正常に処理されます。以下の内容がログに出力されます。

	```
	 response:Optional("Hello, this is a protected resource of the mobile backend application!"), no error
 ```
	{: screen}

1. 次のコードを追加してログアウト機能を追加することもできます。

	```
	GoogleAuthenticationManager.sharedInstance.logout(callBack)
 ```
	{: codeblock}

	ユーザーが Google にログインした後でこのコードを呼び出し、そのユーザーが再度ログインしようとする場合、{{site.data.keyword.amashort}} が認証を目的として Google を使用することについての許可を求めるプロンプトが出されます。その時点で、ユーザー名をクリックすると、別のユーザーを選択してログインすることができます。<!--in the upper-right corner of the screen-->

	ログアウト機能へ `callBack` を渡すことは、オプションです。`nil` を渡すこともできます。
