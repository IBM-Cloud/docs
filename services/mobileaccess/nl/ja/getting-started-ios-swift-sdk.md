---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

{{site.data.keyword.amafull}} サービスは {{site.data.keyword.appid_full}} サービスに置き換えられます。

# iOS Swift SDK のセットアップ
{: #getting-started-ios}

iOS Swift アプリケーションに {{site.data.keyword.amashort}} SDK を装備し、SDK を初期化し、保護されたリソースまたは無保護のリソースへの要求を実行します。


{:shortdesc}


## 開始する前に
{: #before-you-begin}
以下が必要です。

* {{site.data.keyword.Bluemix_notm}} アプリケーションのインスタンス。
* {{site.data.keyword.amafull}} サービスのインスタンス。
* **「TenantID」**。{{site.data.keyword.amashort}} ダッシュボードでサービスを開きます。**「モバイル・オプション」**をクリックします。`tenantId` (`appGUID` とも呼ばれる) の値が、**「アプリ GUID」/「TenantId」**フィールドに表示されます。{{site.data.keyword.amashort}} 許可マネージャーを初期化するためにこの値が必要になります。
* **「アプリケーションの経路 (Application Route)」**。これは、バックエンド・アプリケーションの URL です。保護されているエンドポイントに要求を送信するためにこの値が必要になります。
* {{site.data.keyword.Bluemix_notm}} **「地域」**。**「アバター」**アイコン![「アバター」アイコン](images/face.jpg "「アバター」アイコン") の横のヘッダー内に現在の {{site.data.keyword.Bluemix_notm}} 地域が表示されます。表示される地域の値は、`「米国南部」`、`「シドニー」`、または`「英国」`のいずれかでなければならず、またコードで必要な SDK 値 (`BMSClient.Region.usSouth`、`BMSClient.Region.unitedKingdom`、または `BMSClient.Region.sydney`) に対応している必要があります。{{site.data.keyword.amashort}} SDK を初期化するためにこの値が必要になります。
* Xcode プロジェクト。iOS 開発環境のセットアップ方法について詳しくは、[Apple Developer Web サイト![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.apple.com/support/xcode/){: new_window}を参照してください。


## {{site.data.keyword.amashort}} Client SDK のインストール
{: #install-mca-sdk-ios}
{{site.data.keyword.amashort}} SDK は、iOS プロジェクト用の依存関係マネージャーである CocoaPods とともに配布されています。CocoaPods は、自動的にリポジトリーから成果物をダウンロードし、iOS アプリケーションで使用できるようにします。


### CocoaPods のインストール
{: #install-cocoapods}

1. 端末ウィンドウで **pod --version** コマンドを実行します。既に CocoaPods がインストールされている場合はバージョン番号が表示され、次のセクションにスキップして SDK をインストールできます。

1. CocoaPods をインストールしていない場合は、以下を実行します。

```
sudo gem install cocoapods
```
{: codeblock}

詳しくは、[CocoaPods Web サイト![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cocoapods.org/){: new_window}を参照してください。

### CocoaPods を使用した {{site.data.keyword.amashort}} Client SDK のインストール
{: #install-sdk-cocoapods}

1. 端末ウィンドウで、iOS プロジェクトのルート・ディレクトリーにナビゲートします。

1. まだ CocoaPods 用にワークスペースを初期化していない場合は、`pod init` コマンドを実行します。<br/>
CocoaPods によって、iOS プロジェクトの依存関係を定義する `Podfile` ファイルが作成されます。

1. `Podfile` ファイルを編集し、必要なターゲットに以下の行を追加します。

	```
use_frameworks!
 pod 'BMSSecurity'
	```
	{: codeblock}

  **ヒント:** `use_frameworks!` を、Podfile に含めるのではなく、Xcode ターゲットに追加できます。

1. `Podfile` ファイルを保存し、コマンド・ラインから `pod install` を実行します。CocoaPods は、関連する依存関係をインストールし、追加された依存関係および pod を表示します。<br/>

   **重要**: CocoaPods は `xcworkspace` ファイルを生成します。プロジェクトの開発を進めるためには、このファイルを開く必要があります。

1. iOS プロジェクト・ワークスペースを開きます。CocoaPods によって生成された `xcworkspace` ファイルを開きます。例えば、`{your-project-name}.xcworkspace` の場合、以下を実行します。

	`open {your-project-name}.xcworkspace`

### iOS のキーチェーン共有 (Keychain Sharing) の使用可能化
{: #enable_keychain}

`「キーチェーン共有 (Keychain Sharing)」`を使用可能にします。Xcode プロジェクトで、`「Capabilities」`タブに移動し、`「Keychain Sharing」`を`「On」`に切り替えます。

## {{site.data.keyword.amashort}} Client SDK の初期化
{: #init-mca-sdk-ios}

 `tenantId` パラメーターを渡して、SDK を初期化します。初期化コードを入れる場所は一般的に (必須ではありませんが)、アプリケーション代行の `application:didFinishLaunchingWithOptions` メソッドの中です。

1. {{site.data.keyword.amashort}} Client SDK を使用したいクラス内で必要なフレームワークをインポートします。

 ```Swift
 import BMSCore
 import BMSSecurity
 ```

1. {{site.data.keyword.amashort}} Client SDK を初期化します。

 ```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

	func application(_ application: UIApplication, 
	    didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {

	let mcaAuthManager = MCAAuthorizationManager.sharedInstance
    mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
      // regionName に指定可能な値: BMSClient.Region.usSouth、BMSClient.Region.unitedKingdom、BMSClient.Region.sydney
	BMSClient.sharedInstance.authorizationManager = mcaAuthManager	
	return true
	}
 ```
  {: codeblock}

* `tenantId` を、**「モバイル・オプション」**から取得した値に置き換えます。
* `<applicationBluemixRegion>` を、{{site.data.keyword.Bluemix_notm}} アプリケーションがホストされている地域に置き換えます。

これらの値については、[開始する前に](#before-you-begin)を参照してください。


## モバイル・バックエンド・アプリケーションへの要求の実行
{: #request}

{{site.data.keyword.amashort}} Client SDK が初期化された後、モバイル・バックエンド・アプリケーションに要求を出すことができるようになります。

1. ブラウザーで、モバイル・バックエンド・アプリケーション上の保護されたエンドポイントへの要求の送信を試行します。URL: `{applicationRoute}/protected` を開きます。`{applicationRoute}` は、**「モバイル・オプション」**から取得した **applicationRoute** 値 ([Mobile Client Access Client SDK の初期化](#init-mca-sdk-ios)』を参照) に置き換えます。以下に例を示します。

	`http://my-mobile-backend.mybluemix.net/protected`

	このエンドポイントにアクセスできるのは、{{site.data.keyword.amashort}} Client SDK が装備されたモバイル・アプリケーションのみであるため、ブラウザーに `Unauthorized` メッセージが返されます。 

1. iOS アプリケーションを使用して、同じエンドポイントへ要求を出します。`BMSClient` を初期化した後に、以下のコードを追加してください。

 ```Swift
	let customResourceURL = "<your protected resource absolute path>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

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

1.  要求が成功すると、以下の出力が Xcode コンソールに表示されます。

 ```
 response:Optional("Hello, this is a protected resource of the mobile backend application!"), no error
 ```
{: screen}

## 次のステップ
{: #next-steps}
保護されているエンドポイントに繋がった場合、資格情報は必要とされません。アプリケーションにユーザーのログインを要求する場合、Facebook、Google またはカスタム認証を構成する必要があります。

  * [Facebook](facebook-auth-ios-swift-sdk.html)
  * [Google](google-auth-ios-swift-sdk.html)
  * [カスタム](custom-auth-ios-swift-sdk.html)
