---

copyright:
  years: 2016

---

# iOS 用の {{site.data.keyword.amashort}} Client SDK の構成 (Swift SDK)
{: #custom-ios}

{{site.data.keyword.amashort}} Client SDK の使用および {{site.data.keyword.Bluemix}} へのアプリケーションの接続のためにカスタム認証を使用する iOS アプリケーションを構成します。

## 開始する前に
{: #before-you-begin}

カスタム ID プロバイダーを使用するように構成済みの{{site.data.keyword.amashort}} サービスのインスタンスにより保護されているリソースを持っている必要があります。また、モバイル・アプリに {{site.data.keyword.amashort}} Client SDK が装備されている必要があります。詳しくは、以下の情報を参照してください。

 * [{{site.data.keyword.amashort}} 入門](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [iOS Swift SDK のセットアップ](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html)
 * [カスタム ID プロバイダーの使用](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [カスタム ID プロバイダーの作成](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [カスタム認証用の {{site.data.keyword.amashort}} の構成 ](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## カスタム認証用の {{site.data.keyword.amashort}} の構成
 {: #custom-auth-ios-configmca}

 1. {{site.data.keyword.Bluemix_notm}}ダッシュボードでアプリを開きます。

 1. **「モバイル・オプション」**をクリックし、**「経路」** (*applicationRoute*) と **「アプリ GUID」** (*applicationGUID*) のメモを取ります。SDK を初期化する際に、これらの値が必要になります。

 1. {{site.data.keyword.amashort}} タイルをクリックします。{{site.data.keyword.amashort}} ダッシュボードがロードされます。

 1. **「カスタム」**タイルをクリックします。

 1. **「レルム名」**で、カスタム認証レルムを指定します。

 1. **「URL」**で、applicationRoute を指定します。

 1. **「保存」**をクリックします。

## iOS 用の {{site.data.keyword.amashort}} Client SDK の構成
 {: #custom-auth-ios-sdk}

### CocoaPods のインストール
 {: #custom-auth-cocoapods}

 {{site.data.keyword.amashort}} Client SDK は、iOS プロジェクト用の依存関係マネージャーである CocoaPods を使用して配布されます。CocoaPods は、自動的にリポジトリーから成果物をダウンロードし、iOS アプリケーションで使用できるようにします。

 1. 端末エミュレーターを開いて `pod --version` コマンドを実行します。既に CocoaPods をインストール済みの場合は、バージョン番号が表示されます。この場合、このチュートリアルの次のセクションはスキップすることができます。

 1. `sudo gem install cocoapods` を実行して CocoaPods をインストールします。更にガイダンスが必要な場合は、[CocoaPods の Web サイト](https://cocoapods.org/)を参照してください。

 1. XCode を閉じます。

 1. 端末を開き、`cd` コマンドによってプロジェクト・ディレクトリーに移動します。

 1.  `pod init` を実行します。

### CocoaPods を使用した Client SDK のインストール
{: #custom-ios-sdk-cocoapods}

CocoaPods 依存関係マネージャーを使用して {{site.data.keyword.amashort}} Client SDK をインストールします。

1. 端末を開いて、iOS プロジェクトのルート・ディレクトリーに移動します。

1. `Podfile` を編集して以下の行を追加します。

 ```
 use_frameworks!
 pod 'BMSSecurity'
 ```
 **ヒント:** `use_frameworks!` を、Podfile に含めるのではなく、Xcode ターゲットに追加できます。

1. コマンド・ラインで `pod install` を実行します。
追加された依存関係が CocoaPods によってインストールされます。進行状況および追加されたコンポーネントが表示されます。

 **重要**: この時点で、CocoaPods によって生成された xcworkspace ファイルを使用してプロジェクトを開く必要があります。通常、名前は `{your-project-name}.xcworkspace` です。  

1. コマンド・ラインから `open {your-project-name}.xcworkspace` を実行して、iOS プロジェクトのワークスペースを開きます。

### Client SDK の初期化 
{: #custom-ios-sdk-initialize}

`applicationRoute` パラメーターと `applicationGUID` パラメーターを渡すことによって、SDK を初期化します。初期化コードを入れる場所は一般的に (必須ではありませんが)、アプリケーション代行の `application:didFinishLaunchingWithOptions` メソッドの中です。

1. アプリケーション・パラメーター値を取得します。{{site.data.keyword.Bluemix_notm}}ダッシュボードでアプリを開きます。「**Mobile オプション**」をクリックします。`applicationRoute` と `applicationGUID` の値は、**「経路」**フィールドと**「アプリ GUID」**フィールドに表示されます。

1. {{site.data.keyword.amashort}} Client SDK を使用したいクラス内で必要なフレームワークをインポートします。

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
```

1. {{site.data.keyword.amashort}} Client SDK を初期化し、許可マネージャーを MCAAuthorizationManager に変更し、認証代行を定義して登録します。`<applicationRoute>` および `<applicationGUID>` を、{{site.data.keyword.Bluemix_notm}} ダッシュボードの**「モバイル・オプション」**から取得した**「経路」**および**「アプリ GUID」**の値に置き換えます。

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"
 let customRealm = "<your protected resource's realm>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {


 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

  //Auth delegate for handling custom challenge
 class MyAuthDelegate : AuthenticationDelegate {
      func onAuthenticationChallengeReceived(authContext: AuthenticationContext, challenge: AnyObject){
          print("onAuthenticationChallengeReceived")
              let answer = <An answer to the challenge sent by the backend (Should be of type [String:AnyObject])>
              authContext.submitAuthenticationChallengeAnswer(answer)
      }

      func onAuthenticationSuccess(info: AnyObject?) {
           print("onAuthenticationSuccess info = \(info)")
           print("onAuthenticationSuccess")
      }

      func onAuthenticationFailure(info: AnyObject?){
        print("onAuthenticationFailure info = \(info)")
        print("onAuthenticationFailure")
      }
  }

  let delegate = MyAuthDelegate()
  let mcaAuthManager = MCAAuthorizationManager.sharedInstance

 do {
      try mcaAuthManager.registerAuthenticationDelegate(delegate, realm: customRealm)
  } catch {
      print("error with register: \(error)")
  }
 return true
 }   
 ```

## 認証のテスト
{: #custom-ios-testing}

Client SDK を初期化し、カスタム認証代行を登録した後、モバイル・バックエンドに要求を出すことを開始できます。

### 開始する前に
{: #custom-ios-testing-before}

 {{site.data.keyword.mobilefirstbp}} ボイラープレートを使用して作成されたアプリケーションと、 `/protected` エンドポイントで{{site.data.keyword.amashort}} により保護されているリソースを持っている必要があります。

1. ブラウザーで `{applicationRoute}/protected` (例えば `http://my-mobile-backend.mybluemix.net/protected`) を開いて、モバイル・バックエンドの保護エンドポイントに要求を送信します。{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用して作成されたモバイル・バックエンドの`/protected` エンドポイントは、{{site.data.keyword.amashort}} で保護されています。このエンドポイントは {{site.data.keyword.amashort}} Client SDK により装備されたモバイル・アプリケーションからのみアクセス可能です。
その結果、`承認されていない`というメッセージがブラウザーに表示されます。

1. iOS アプリケーションを使用して、同じエンドポイントへの要求を実行します。`BMSClient` を初期化し、カスタム認証代行を登録した後に、以下のコードを追加します。

 ```Swift
 let customResourceURL = "<your protected resource's path>"
 let request = Request(url: customResourceURL, method: HttpMethod.GET)
 let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) in
  if error == nil {
      print ("response:\(response?.responseText), no error")
  } else {
      print ("error: \(error)")
  }
 }

 request.sendWithCompletionHandler(callBack)
 ```

1. 	要求が成功したら、Xcode コンソールに次のような出力が表示されます。

 ```
 onAuthenticationSuccess info = Optional({
     attributes =     {
     };
     deviceId = don;
     displayName = "Don+Lon";
     isUserAuthenticated = 1;
     userId = don;
 })
 response:Optional("Hello Don Lon"), no error
 ```

1. 次のコードを追加してログアウト機能を追加することもできます。

 ```
 MCAAuthorizationManager.sharedInstance.logout(callBack)
 ```  

 ユーザーのログイン後に、このコードを呼び出すと、そのユーザーはログアウトされます。そのユーザーが再度ログインしようとする場合は、サーバーから受信した要求に再度応じる必要があります。

 ログアウト機能へ `callBack` を渡すことは、オプションです。`nil` を渡すこともできます。
