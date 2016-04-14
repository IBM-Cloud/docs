---

copyright:
  years: 2016

---

# iOS Swift SDK のセットアップ
{: #getting-started-ios}

iOS アプリケーションに {{site.data.keyword.amashort}} SDK を装備し、SDK を初期化し、保護されたリソースまたは無保護のリソースへの要求を実行します。

## 開始する前に
{: #before-you-begin}
* {{site.data.keyword.amashort}} サービスによって保護されたモバイル・バックエンドのインスタンスが存在している必要があります。モバイル・バックエンドの作成方法について詳しくは、[入門](getting-started.html)を参照してください。
* Xcode が正しくセットアップされていることを確認してください。iOS 開発環境のセットアップ方法について詳しくは、[Apple 開発者の Web サイト](https://developer.apple.com/support/xcode/)を参照してください。


## {{site.data.keyword.amashort}} Client SDK のインストール
{: #install-mca-sdk-ios}
{{site.data.keyword.amashort}} SDK は、iOS プロジェクト用の依存関係マネージャーである CocoaPods とともに配布されています。CocoaPods は、自動的にリポジトリーから成果物をダウンロードし、iOS アプリケーションで使用できるようにします。


### CocoaPods のインストール
{: #install-cocoapods}
1. 端末を開き、**pod --version** コマンドを実行します。既に CocoaPods がインストールされている場合は、バージョン番号が表示されます。次のセクションにスキップして SDK をインストールできます。

1. CocoaPods をインストールしていない場合は、以下を実行します。
```
sudo gem install cocoapods```
詳細については、[CocoaPods の Web サイト](https://cocoapods.org/)を参照してください。

### CocoaPods を使用した {{site.data.keyword.amashort}} Client SDK のインストール
{: #install-sdk-cocoapods}

1. 端末で、iOS プロジェクトのルート・ディレクトリーにナビゲートします。

1. まだ CocoaPods 用にワークスペースを初期化していない場合は、`pod init` コマンドを実行します。<br/> CocoaPods が、iOS プロジェクトの依存関係を定義する `Podfile` ファイルを作成します。

1. `Podfile` ファイルを編集し、必要なターゲットに以下の行を追加します。

	```
  use_frameworks!
	pod 'BMSSecurity'
	```
  **ヒント:** `use_frameworks!` を、Podfile に含めるのではなく、Xcode ターゲットに追加できます。

1. `Podfile` ファイルを保存し、コマンド・ラインから `pod install` を実行します。<br/>Cocoapods が、追加の依存関係をインストールします。進行状況と、どのコンポーネントが追加されたかを確認できます。<br/>
**重要**: CocoaPods は、`xcworkspace` ファイルを生成します。プロジェクトの開発を進めるためには、このファイルを開く必要があります。

1. iOS プロジェクト・ワークスペースを開きます。CocoaPods によって生成された `xcworkspace` ファイルを開きます。例えば、`{your-project-name}.xcworkspace` などです。`open {your-project-name}.xcworkspace` を実行します。

## {{site.data.keyword.amashort}} Client SDK の初期化
{: #init-mca-sdk-ios}

 `applicationRoute` パラメーターと `applicationGUID` パラメーターを渡すことによって、SDK を初期化します。初期化コードを入れる場所は一般的に (必須ではありませんが)、アプリケーション代行の `application:didFinishLaunchingWithOptions` メソッドの中です。

1. アプリケーション・パラメーター値を取得します。{{site.data.keyword.Bluemix_notm}}ダッシュボードでアプリを開きます。「**Mobile オプション**」をクリックします。`applicationRoute` と `applicationGUID` の値は、**「経路」**フィールドと**「アプリ GUID」**フィールドに表示されます。

1. {{site.data.keyword.amashort}} Client SDK を使用したいクラス内で必要なフレームワークをインポートします。

 ```Swift
 import BMSCore
 import BMSSecurity
 ```  

1. {{site.data.keyword.amashort}} Client SDK を初期化します。`<applicationRoute>` および `<applicationGUID>` を、{{site.data.keyword.Bluemix_notm}} ダッシュボードの**「モバイル・オプション」**から取得した**「経路」**および**「アプリ GUID」**の値に置き換えます。

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {


 // Initialize the Client SDK.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 return true
 }
 ```

## モバイル・バックエンドへの要求の実行
{: #request}

{{site.data.keyword.amashort}} Client SDK が初期化された後、モバイル・バックエンドに要求を出すことができるようになります。

1. ブラウザーで、モバイル・バックエンド上の保護されたエンドポイントへの要求の送信を試行します。次の URL を開きます。`{applicationRoute}/protected` (たとえば、 `http://my-mobile-backend.mybluemix.net/protected`)
<br/>MobileFirst Services Starter ボイラープレートを使用して作成されたモバイル・バックエンドの`/protected` エンドポイントは、{{site.data.keyword.amashort}}で保護されています。このエンドポイントにアクセスできるのは、{{site.data.keyword.amashort}} Client SDK が装備されたモバイル・アプリケーションのみであるため、ブラウザーに `Unauthorized` メッセージが返されます。
1. iOS アプリケーションを使用して同じエンドポイントに対する要求を作成します。`BMSClient` を初期化した後に、以下のコードを追加してください。

 ```Swift
 let customResourceURL = "<your protected resource's path>"
 let request = Request(url: customResourceURL, method: HttpMethod.GET)
 let callBack:MfpCompletionHandler = {(response: Response?, error: NSError?) in
     if error == nil {
         print ("response:\(response?.responseText), no error")
     } else {
         print ("error: \(error)")
     }
 }

 request.sendWithCompletionHandler(callBack)
 ```

1.  要求が正常に実行されると、Xcode コンソールに以下の出力が表示されます。

 ```
 response:Optional("Hello, this is a protected resouce of the mobile backend application!"), no error
 ```

## 次のステップ
{: #next-steps}
保護されているエンドポイントに繋がった場合、資格情報は必要とされません。アプリケーションにユーザーのログインを要求する場合、Facebook、Google またはカスタム認証を構成する必要があります。
  * [Facebook](facebook-auth-ios-swift-sdk.html)
  * [Google](google-auth-ios-swift-sdk.html)
  * [カスタム](custom-auth-ios-swift-sdk.html)
