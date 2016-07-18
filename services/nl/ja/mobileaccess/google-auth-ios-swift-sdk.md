 ---

copyright:
  years: 2016

---
{:screen:  .screen}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}

# iOS アプリ用の Google 認証の使用可能化 (Swift SDK)
{: #google-auth-ios}
Google Sign-In を使用して、{{site.data.keyword.amashort}} iOS Swift アプリのユーザーを認証します。新しくリリースされた {{site.data.keyword.amashort}} Swift SDK は、既存の Mobile Client Access Objective-C SDK によって提供される機能を増強します。

**注:** Objective-C SDK は現在も完全にサポートされており、{{site.data.keyword.Bluemix_notm}} モバイル・サービス用の主要 SDK とされていますが、今年後半には廃止され、この新しい Swift SDK が後継になる予定です。



## 開始する前に
{: #google-auth-ios-before}
以下が必要です。

* Xcode の iOS プロジェクト。{{site.data.keyword.amashort}} Client SDK が装備されている必要はありません。  
* {{site.data.keyword.amashort}} サービスによって保護された {{site.data.keyword.Bluemix_notm}} アプリケーションのインスタンス。{{site.data.keyword.Bluemix_notm}} バックエンドの作成方法について詳しくは、[入門](index.html)を参照してください。


## Google Sign-In 用のアプリの準備
{: #google-sign-in-ios}

Google の [Google Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start-integrating) に記載されている指示に従って、Google Sign-In 用にアプリを準備します。 

このプロセスは以下を行います。
* Google Developers サイトで新規プロジェクトを準備します。 
* `GoogleService-Info.plist` ファイルを作成し、`REVERSE_CLIENT_ID` 値を Xcode プロジェクトに追加します。
* **Google Client ID** を作成して {{site.data.keyword.Bluemix_notm}} バックエンド・アプリケーションに追加します。

以下のステップでは、アプリを準備するために必要な作業について、簡単な概要を示します。 

**注:** `Google/SignIn` CocoaPod を追加する必要はありません。必要な SDK は下記の `BMSGoogleAuthentication` CocoaPod によって追加されます。

1. メイン・ターゲットの**「General」**タブの**「Identity」**セクションから、Xcode プロジェクト内の**「Bundle Identifier」**をメモします。これは Google Sign-In プロジェクトの作成に必要です。

1. Google Developer for Google Sign-In for iOS (https://developers.google.com/mobile/add?platform=ios) で、プロジェクトを作成します。 

2. プロジェクトに Google Sign-In サービスを追加します。

3. `GoogleService-Info.plist` を取得します。

  **重要:** `GoogleService-Info.plist` ファイルの取得時に、そのファイルを開いて、`CLIENT_ID` の値のメモを取ってください。後で、{{site.data.keyword.amashort}} バックエンド・アプリケーションを構成するためにこの値が必要になります。

1. Xcode プロジェクトに `GoogleService-Info.plist` ファイルを追加します。詳しくは、[Add the configuration file to your project](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config) を参照してください。

1. Xcode プロジェクト内の URL スキームを、自分の `REVERSE_CLIENT_ID` およびバンドル ID によって更新します。詳しくは、[Add URL schemes to your project](https://developers.google.com/identity/sign-in/ios/start-integrating#add_a_url_scheme_to_your_project) を参照してください。


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
{: #install-cocoapods}

1. 端末を開き、**pod --version** コマンドを実行します。既に CocoaPods がインストールされている場合は、バージョン番号が表示されます。次のセクションにスキップして SDK をインストールできます。

1. CocoaPods をインストールしていない場合は、以下を実行します。

```
sudo gem install cocoapods```
詳細については、[CocoaPods の Web サイト](https://cocoapods.org/)を参照してください。### CocoaPods を使用した {{site.data.keyword.amashort}} Client Swift SDK のインストール
{: #facebook-auth-install-swift-cocoapods}

1. iOS プロジェクト内に `Podfile` がない場合、`pod init` を実行してファイルを作成します。

1. `Podfile` を編集して、関連するターゲットに以下の行を追加します。

 ```
 use_frameworks!
 pod 'BMSGoogleAuthentication'
 ```
 
 **注:** 既に {{site.data.keyword.amashort}} コア SDK をインストール済みの場合は、行 `pod 'BMSSecurity'` を削除できます。`BMSGoogleAuthentication` pod は、必要なすべてのフレームワークをインストールします。
	
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

1. 以下のコードを使用して、Client SDK を初期化します。`<applicationRoute>` および `<applicationGUID>` を、{{site.data.keyword.Bluemix_notm}} ダッシュボードの**「モバイル・オプション」**から取得した**「経路」**および**「アプリ GUID」**の値に置き換えます。`<applicationBluemixRegion>` を、{{site.data.keyword.Bluemix_notm}} アプリケーションがホストされている地域に置き換えます。{{site.data.keyword.Bluemix_notm}} 地域を表示するには、ダッシュボードの左上隅にある顔アイコン (![Face](/face.png "Face")) をクリックします。 

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 // Initialize the client SDK.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUId, bluemixRegion: BMSClient.<applicationBluemixRegion>)

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


1. デスクトップ・ブラウザーで、`{applicationRoute}/protected` (例えば、`http://my-mobile-backend.mybluemix.net/protected`) を開くことによって、モバイル・バックエンドの保護エンドポイントへの要求の送信を試行します。

1. MobileFirst Services ボイラープレートを使用して作成されたモバイル・バックエンドの `/protected` エンドポイントは、{{site.data.keyword.amashort}} によって保護されています。したがって、このエンドポイントにアクセスできるのは、{{site.data.keyword.amashort}} Client SDK が装備されたモバイル・アプリケーションのみです。結果的に、デスクトップ・ブラウザーに `Unauthorized` が表示されます。

1. iOS アプリケーションを使用して、同じエンドポイントへ要求を出します。

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
{: screen}

1. 次のコードを追加してログアウト機能を追加することもできます。

 ```
 GoogleAuthenticationManager.sharedInstance.logout(callBack)
 ```

  ユーザーが Google にログインした後でこのコードを呼び出し、そのユーザーが再度ログインしようとする場合、{{site.data.keyword.amashort}} が認証を目的として Google を使用することについての許可を求めるプロンプトが出されます。その時点で、画面の右上隅にあるユーザー名をクリックすると、別のユーザーを選択してログインすることができます。

   ログアウト機能へ `callBack` を渡すことは、オプションです。`nil` を渡すこともできます。
