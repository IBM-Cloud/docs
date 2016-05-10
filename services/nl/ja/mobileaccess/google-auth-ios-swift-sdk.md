---

copyright:
  years: 2016

---

# iOS アプリで Google 認証を使用可能にする (Swift SDK)
{: #google-auth-ios}

## 開始する前に
{: #google-auth-ios-before}

* {{site.data.keyword.amashort}} によって保護されたリソースと、{{site.data.keyword.amashort}} Client SDK が装備された iOS プロジェクトが必要です。詳しくは、[{{site.data.keyword.amashort}} 入門](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)および [iOS Swift SDK のセットアップ](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html)を参照してください。  
* {{site.data.keyword.amashort}}  Server SDK を使用して手作業でバックエンド・アプリケーションを保護します。詳しくは、[リソースの保護](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)を参照してください。

## Google サインイン用のアプリの準備
{: #google-sign-in-ios}

Google の [Goolge Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start-integrating) に記載されている指示に従って、Google サインイン用にアプリを準備します。以下のステップでは、アプリを準備するために実行する必要のある作業について、簡単な概要を示します。

1. アプリで iOS 用の Google サインインを有効にします。詳細については、[Try Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start?ver=swift) を参照してください。

1. 自分のプロジェクト用の構成ファイル (`GoogleService-Info.plist`) を取得します。このファイルを取得するには、[Enable Google services for your app](https://developers.google.com/mobile/add?platform=ios) を参照してください。

 **重要:** `GoogleService-Info.plist` ファイルの取得時に、そのファイルを開いて、`CLIENT_ID` の値のメモを取ってください。後で、{{site.data.keyword.amashort}} を構成するためにこの値が必要になります。

1. Xcode プロジェクトに `GoogleService-Info.plist` ファイルを追加します。詳しくは、[Add the configuration file to your project](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config) を参照してください。

1. Xcode プロジェクト内の URL スキームを、自分の `REVERSE_CLIENT_ID` およびバンドル ID によって更新します。詳しくは、[Add URL schemes to your project](https://developers.google.com/identity/sign-in/ios/start-integrating#add_url_schemes_to_your_project) を参照してください。

1. アプリの project-Bridging-Header.h ファイルを以下のコードで更新します。

 ```
 #import <Google/SignIn.h>
 ```

 ブリッジング・ヘッダー・ファイルの更新について詳しくは、[Enable sign-in](https://developers.google.com/identity/sign-in/ios/sign-in#enable_sign-in) のステップ 1 を参照してください。

## Google 認証用の {{site.data.keyword.amashort}} の構成
{: #google-auth-ios-config}

これで iOS のクライアント ID を取得したので、{{site.data.keyword.Bluemix}} ダッシュボードで Google 認証を使用可能にすることができます。

1. {{site.data.keyword.Bluemix_notm}}ダッシュボードでアプリを開きます。

1. **「モバイル・オプション」**をクリックし、**「経路」** (*applicationRoute*) と **「アプリ GUID」** (*applicationGUID*) のメモを取ります。SDK を初期化する際に、これらの値が必要になります。

1. {{site.data.keyword.amashort}} タイルをクリックします。{{site.data.keyword.amashort}} ダッシュボードがロードされます。

1. **「Google」**タイルをクリックします。

1. **「iOS のアプリケーション ID (Application ID for iOS)」**で、前に取得した `GoogleService-Info.plist` ファイルからの `CLIENT_ID` の値を指定し、**「保存」**をクリックします。

## iOS 用の {{site.data.keyword.amashort}} Client SDK の構成
{: #google-auth-ios-sdk}

### CocoaPods のインストール
{: #google-auth-cocoapods}

{{site.data.keyword.amashort}} Client SDK は、iOS プロジェクト用の依存関係マネージャーである CocoaPods を使用して配布されます。CocoaPods は、自動的にリポジトリーから成果物をダウンロードし、iOS アプリケーションで使用できるようにします。

1. 端末エミュレーターを開いて `pod --version` コマンドを実行します。既に CocoaPods をインストール済みの場合は、バージョン番号が表示されます。この場合、このチュートリアルの次のセクションはスキップすることができます。

1. `sudo gem install cocoapods` を実行して CocoaPods をインストールします。更にガイダンスが必要な場合は、[CocoaPods の Web サイト](https://cocoapods.org/)を参照してください。

1. XCode を閉じます。

1. 端末を開き、`cd` コマンドによってプロジェクト・ディレクトリーに移動します。

1.  `pod init` を実行します。

### CocoaPods を使用した {{site.data.keyword.amashort}} Client Swift SDK のインストール
{: #google-auth-ios-sdk-cocoapods}

1. iOS プロジェクトにナビゲートします。

1. `Podfile` を編集して以下の行を追加します。

 ```
 use_frameworks!
 pod 'BMSGoogleAuthentication'
 ```
 **ヒント:** `use_frameworks!` を、Podfile に含めるのではなく、Xcode ターゲットに追加できます。

1. `Podfile` を保存し、コマンド・ラインから `pod install` を実行します。CocoaPods は依存関係をインストールします。進行状況と、どのコンポーネントが追加されたかが表示されます。

 **重要**: この時点で、CocoaPods によって生成された `xcworkspace` ファイルを使用してプロジェクトを開く必要があります。通常、名前は `{your-project-name}.xcworkspace` です。  

1. コマンド・ラインから `open {your-project-name}.xcworkspace` を実行して、iOS プロジェクトのワークスペースを開きます。

1. `GoogleAuthenticationManager.swift` ファイルを、`BMSGoogleAuthentication` pod ソース・ファイルからプロジェクト・ディレクトリーにコピーします。

## {{site.data.keyword.amashort}} Client Swift SDK の初期化
{: #google-auth-ios-initialize}

{{site.data.keyword.amashort}} Client SDK を使用するには、`applicationGUID` パラメーターと `applicationRoute` パラメーターを渡して SDK を初期化する必要があります。

初期化コードを入れる場所は一般的に (必須ではありませんが)、アプリケーション代行の `application:didFinishLaunchingWithOptions` メソッドの中です。

1. アプリケーション・パラメーター値を取得します。{{site.data.keyword.Bluemix_notm}}ダッシュボードでアプリを開きます。「**Mobile オプション**」をクリックします。`applicationRoute` と `applicationGUID` の値は、**「経路」**フィールドと**「アプリ GUID」**フィールドに表示されます。

1. {{site.data.keyword.amashort}} Client SDK を使用したいクラス内で必要なフレームワークをインポートします。以下のヘッダーを追加します。

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```

1. 以下のコードを使用して、Client SDK を初期化します。`<applicationRoute>` および `<applicationGUID>` を、{{site.data.keyword.Bluemix_notm}} ダッシュボードの**「モバイル・オプション」**から取得した**「経路」**および**「アプリ GUID」**の値に置き換えます。

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {


 // Initialize the Client SDK.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUId, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 GoogleAuthenticationManager.sharedInstance.register()
      return true
      }

 // [START openurl]
      func application(application: UIApplication,
          openURL url: NSURL, sourceApplication: String?, annotation: AnyObject) -> Bool {
             return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, sourceApplication: sourceApplication, annotation: annotation)
      }

 @available(iOS 9.0, *)
 func application(app: UIApplication, openURL url: NSURL, options: [String : AnyObject]) -> Bool {
 return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, options: options)
  }
 ```

## 認証のテスト
{: #google-auth-ios-testing}

Client SDK が初期化され、Google 認証マネージャーが登録されると、モバイル・バックエンドに要求を出すことができるようになります。

### 開始する前に
{: #google-auth-ios-testing-before}

{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用していて、{{site.data.keyword.amashort}}により`/protected` エンドポイントで保護されているリソースを既に持っている必要があります。`/protected` エンドポイントをセットアップする必要がある場合、[リソースの保護 ](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)を参照してください。


1. `{applicationRoute}/protected` (例えば、`http://my-mobile-backend.mybluemix.net/protected`) を開いて、デスクトップ・ブラウザーで、モバイル・バックエンドの保護エンドポイントに要求を送信してみてください。

1. MobileFirst Services ボイラープレートを使用して作成されたモバイル・バックエンドの `/protected` エンドポイントは、{{site.data.keyword.amashort}} によって保護されています。したがって、このエンドポイントにアクセスできるのは、{{site.data.keyword.amashort}} Client SDK の装備されたモバイル・アプリケーションのみとなります。結果的に、デスクトップ・ブラウザーに `Unauthorized` が表示されます。

1. iOS アプリケーションを使用して、同じエンドポイントへの要求を実行します。

 ```Swift
 let protectedResourceURL = "<Your protected resource URL>" // any protected resource
 let request = Request(url: protectedResourceURL , method: HttpMethod.GET)
 let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) in
 if error == nil {
    print ("response:\(response?.responseText), no error")
 } else {
    print ("error: \(error)")
 }
 }

 request.sendWithCompletionHandler(callBack)
	```

1. アプリケーションを実行します。Google のログイン画面のポップアップが表示されます。

 ![image](images/ios-google-login.png)

1. ログインして**「OK」**をクリックすると、{{site.data.keyword.amashort}} が Google ユーザー ID を認証目的に使用することを許可したことになります。

1. 	ユーザーの要求は正常に処理されます。ログに以下の出力が表示されます。

 ```
 onAuthenticationSuccess info = Optional({attributes = {};
     deviceId = 105747725068605084657;
     displayName = "donlonqwerty@gmail.com";
     isUserAuthenticated = 1;
     userId = 105747725068605084657;
 })
 response:Optional("Hello, this is a protected resource!"), no error
 ```

1. 次のコードを追加してログアウト機能を追加することもできます。

 ```
 GoogleAuthenticationManager.sharedInstance.logout(callBack)
 ```

  ユーザーが Google にログインした後でこのコードを呼び出し、そのユーザーが再度ログインしようとする場合、{{site.data.keyword.amashort}} が認証を目的として Google を使用することについての許可を求めるプロンプトが出されます。その時点で、画面の右上隅にあるユーザー名をクリックすると、別のユーザーを選択してログインすることができます。

   ログアウト機能へ `callBack` を渡すことは、オプションです。`nil` を渡すこともできます。
