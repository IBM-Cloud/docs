---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

**重要: {{site.data.keyword.amafull}} サービスは {{site.data.keyword.appid_full}} サービス**に置き換えられます。

# iOS アプリ用の Facebook 認証の使用可能化 (Swift SDK)
{: #facebook-auth-ios}

{{site.data.keyword.amafull}} iOS アプリケーションで Facebook を ID プロバイダーとして使用するには、iOS プラットフォームを追加して Facebook アプリケーション用に構成します。
{: shortdesc}

## 開始する前に
{: #before-you-begin}

以下が必要です。

* {{site.data.keyword.amafull}} サービスのインスタンスおよび {{site.data.keyword.Bluemix_notm}} アプリケーション。{{site.data.keyword.Bluemix_notm}} バックエンド・アプリケーションの作成方法について詳しくは、[概説](index.html)を参照してください。




* バックエンド・アプリケーションの URL (**「アプリの経路 (App Route)」**)。バックエンド・アプリケーションの保護されたエンドポイントに要求を送信するためにこの値が必要になります。
* **TenantID** 値。{{site.data.keyword.amashort}} ダッシュボードでサービスを開きます。**「モバイル・オプション」**ボタンをクリックします。`tenantId` (`appGUID` とも呼ばれる) の値が、**「アプリ GUID」/「TenantId」**フィールドに表示されます。許可マネージャーを初期化するためにこの値が必要になります。
* {{site.data.keyword.Bluemix_notm}} **「地域」**。**「アバター」**アイコン![「アバター」アイコン](images/face.jpg "「アバター」アイコン") の横のヘッダー内に現在の {{site.data.keyword.Bluemix_notm}} 地域が表示されます。表示される地域の値は、`「米国南部」`、`「英国」`、または`「シドニー」`のいずれかでなければならず、また Swift SDK に必要な SDK 値 (`BMSClient.Region.usSouth`、`BMSClient.Region.unitedKingdom`、または `BMSClient.Region.sydney`) に対応している必要があります。{{site.data.keyword.amashort}} クライアントを初期化するためにこの値が必要になります。
* CocoaPods と連動して機能するようにセットアップされた iOS プロジェクト。詳しくは、[iOS Swift SDK のセットアップ](getting-started-ios-swift-sdk.html)の **CocoaPods のインストール**を参照してください。
     
   **注:** 先に進む前にコア {{site.data.keyword.amashort}} Client SDK をインストールする必要はありません。
* [Facebook for Developers![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developers.facebook.com){: new_window} Web サイト上の Facebook アプリケーション。

**重要:** Facebook SDK (`com.facebook.FacebookSdk`) を別個にインストールする必要はありません。Facebook SDK は {{site.data.keyword.amashort}} `BMSFacebookAuthentication` ポッドで自動的にインストールされます。Facebook for Developers の Web サイトでアプリを追加または構成する場合は、**Xcode プロジェクトへの Facebook SDK の追加**のステップをスキップできます。

## iOS プラットフォーム用の Facebook アプリケーションの構成
{: #facebook-auth-ios-config}

Facebook for Developers サイトで以下を行います。

1. [Facebook for Developers ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developers.facebook.com){: new_window}で自分のアカウントにログインします。

1. iOS プラットフォームがアプリに追加済みであることを確認します。iOS プラットフォームを追加または構成する場合、iOS アプリケーションの **bundleId** を提供する必要があります。ご使用の iOS アプリケーションの **bundleId** を調べるには、`info.plist` ファイル内または Xcode プロジェクトの**「一般 (General)」**タブ内で**「バンドル ID (Bundle Identifier)」**を探します。

  **ヒント**: これらの機能を使用する予定がある場合は、URL スキーム・サフィックスまたはシングル・サインオンを使用可能にすることを検討してください。

1. **「設定の保存」**をクリックします。

## Facebook 認証用の {{site.data.keyword.amashort}} の構成
{: #facebook-auth-ios-configmca}

Facebook App ID および Facebook アプリケーションを iOS クライアントに対して機能するよう構成したら、{{site.data.keyword.amashort}} サービスで Facebook 認証を使用可能にすることができます。

1. {{site.data.keyword.amashort}} ダッシュボードでサービスを開きます。
1. **「管理」**タブで、**「許可」**をオンに切り替えます。
1. **「Facebook」**セクションを展開します。
1. **Facebook Application ID** を追加して**「保存」**をクリックします。

## iOS 用の {{site.data.keyword.amashort}} Client SDK の構成
{: #facebook-auth-ios-sdk}

### CocoaPods のインストール
{: #install-cocoapods}

1. 端末を開き、**pod --version** コマンドを実行します。CocoaPods がインストールされている場合は、バージョン番号が表示されます。次のセクションにスキップして SDK をインストールできます。

1. CocoaPods をインストールしていない場合は、以下を実行します。

   ```
sudo gem install cocoapods
```
   {: codeblock}

詳しくは、[CocoaPods Web サイト![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cocoapods.org/){: new_window}を参照してください。

### CocoaPods を使用した {{site.data.keyword.amashort}} Client Swift SDK のインストール
{: #facebook-auth-install-swift-cocoapods}

1. iOS プロジェクト内に `Podfile` がない場合、`pod init` を実行してファイルを作成します。

1. `Podfile` を編集して以下の行を追加します。

   ```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```
   {: codeblock}

   **注:** Podfile 内に行 `pod 'BMSSecurity'` がある場合、その行を削除する必要があります。`BMSFacebookAuthentication` pod は、必要なすべてのフレームワークをインストールします。

   **ヒント:** `use_frameworks!` を、Podfile に含めるのではなく、Xcode ターゲットに追加できます。

1. `Podfile` を保存して、コマンド・ラインから `pod install` コマンドを実行します。CocoaPods は依存関係をインストールします。進行状況および追加されたコンポーネントが表示されます。

   **重要**: この時点で、CocoaPods によって生成された `xcworkspace` ファイルを使用してプロジェクトを開く必要があります。通常、名前は `{your-project-name}.xcworkspace` です。  

1. コマンド・ラインから `open {your-project-name}.xcworkspace` を実行して、iOS プロジェクトのワークスペースを開きます。

### iOS のキーチェーン共有 (Keychain Sharing) の使用可能化
{: #enable_keychain}

`「キーチェーン共有 (Keychain Sharing)」`を使用可能にします。Xcode プロジェクトで、`「Capabilities」`タブに移動し、`「Keychain Sharing」`を`「On」`に切り替えます。

### Facebook 認証用の iOS プロジェクトの構成
{: #facebook-auth-ios-configproject}

1. `info.plist` ファイルを見つけます。このファイルは、通常、Xcode プロジェクトの `Supporting files` フォルダーにあります。

1. `info.plist` ファイルに以下のプロパティーを追加して、Facebook 統合を構成します。

   ![image](images/ios-facebook-infoplist-settings.png)

   Facebook Application ID を使用して URL スキームおよび FacebookAppID プロパティーを更新します。

   `info.plist` ファイルの更新は、このファイルを右クリックし、**「指定して開く」>「ソース・コード」**を選択して以下の XML を追加することでも行えます。

   ```XML
   <key>CFBundleURLTypes</key>
   <array>
      <dict>
         <key>CFBundleURLSchemes</key>
         <array>
            <string>fb{your-facebook-application-id}</string>
         </array>
      </dict>
   </array>
   <key>FacebookAppID</key>
   <string>{your-facebook-application-id}</string>
   <key>FacebookDisplayName</key>
   <string>{your-faceebook-application-name}</string>
   <key>LSApplicationQueriesSchemes</key>
   <array>
      <string>fbauth</string>
      <string>fbauth2</string>
   </array>
   <key>NSAppTransportSecurity</key>
   <dict>
      <key>NSExceptionDomains</key>
      <dict>
         <key>facebook.com</key>
         <dict>
            <key>NSIncludesSubdomains</key>
            <true/>
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
         </dict>
         <key>fbcdn.net</key>
         <dict>
            <key>NSIncludesSubdomains</key>
            <true/>
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
         </dict>
         <key>akamaihd.net</key>
         <dict>
            <key>NSIncludesSubdomains</key>
            <true/>
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
         </dict>
      </dict>
   </dict>
   ```
   {: codeblock}

   Facebook Application ID を使用して `CFBundleURLSchemes` および `FacebookappID` プロパティーを更新します。Facebook アプリケーションの名前で `FacebookDisplayName` を更新します。

   **重要**: `info.plist` ファイル内の既存のプロパティーをオーバーライドすることのないようにしてください。重複するプロパティーがある場合は、手動でマージする必要があります。詳しくは、[Xcode プロジェクトを構成する![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developers.facebook.com/docs/ios/getting-started/){: new_window}および[アプリを iOS9 用に準備する![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developers.facebook.com/docs/ios/ios9){: new_window}を参照してください。

## {{site.data.keyword.amashort}} Client Swift SDK の初期化
{: #facebook-auth-ios-initalize-swift}

`tenantId` を渡して、Client SDK を初期化します。

初期化コードを入れる場所は一般的に (必須ではありませんが)、アプリケーション代行の `application:didFinishLaunchingWithOptions` メソッドの中です。

1. 1. 以下のヘッダーを追加することによって、{{site.data.keyword.amashort}} Client SDK を使用したいクラスに、必要なフレームワークをインポートします。

   ```swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```
   {: codeblock}

1. Client SDK を初期化します。

   ```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
let mcaAuthManager = MCAAuthorizationManager.sharedInstance
      mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
      //the regionName should be one of the following: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney
      BMSClient.sharedInstance.authorizationManager = mcaAuthManager
      FacebookAuthenticationManager.sharedInstance.register()
   }
   ```
   {: codeblock}

   コードの中で次のようにします。

   * `<applicationBluemixRegion>` を、{{site.data.keyword.Bluemix_notm}} アプリケーションがホストされている地域に置き換えます。
   * `tenantId` を**「TenantId」/「アプリ GUID」**値に置き換えます。

   これらの値について詳しくは、[開始する前に](#before-you-begin)を参照してください。

1. アプリ代行の `application:didFinishLaunchingWithOptions` メソッドに以下のコードを追加することによって、Facebook SDK にアプリのアクティベーションについて通知し、Facebook Authentication Handler を登録します。BMSClient インスタンスの初期化の後にこのコードを追加し、Facebook を認証マネージャーとして登録します。

   ```Swift
  return FacebookAuthenticationManager.sharedInstance.onFinishLaunching(application, withOptions: launchOptions)
 ```
   {: codeblock}

1. `FacebookAuthenticationManager.swift` ファイルを `BMSFacebookAuthentication` pod ソース・ファイルからプロジェクト・ディレクトリーにコピーします。

1. アプリ代行に以下のコードを追加します。

   ```Swift
   func application(_ app: UIApplication,
      open url: URL,
      options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool{
         return FacebookAuthenticationManager.sharedInstance.onOpenURL(app, open: url, options: options)
      }
   ```
   {: codeblock}

## 認証のテスト
{: #facebook-auth-ios-testing}

Client SDK が初期化され、Facebook 認証マネージャーの登録が完了すると、モバイル・バックエンド・アプリケーションに要求を出すことができるようになります。

### 開始する前に
{: #facebook-auth-ios-testing-before}

{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用していて、{{site.data.keyword.amashort}}により`/protected` エンドポイントで保護されているリソースを既に持っている必要があります。`/protected` エンドポイントをセットアップする必要がある場合、[リソースの保護 ](protecting-resources.html)を参照してください。

1. ブラウザーで、新しく作成されたモバイル・バックエンド・アプリケーションの保護エンドポイントへの要求の送信を試行します。URL `{applicationRoute}/protected` を開きます。`{applicationRoute}` は、**「モバイル・オプション」**から取得した値 (『[Facebook 認証用の Mobile Client Access の構成](#facebook-auth-ios-configmca)』を参照) に置き換えます。
(たとえば、 `http://my-mobile-backend.mybluemix.net/protected`)
<br/>MobileFirst Services Starter ボイラープレートを使用して作成されたモバイル・バックエンド・アプリケーションの `/protected` エンドポイントは、{{site.data.keyword.amashort}} で保護されています。 `認証されていない`というメッセージがブラウザーに戻されます。このエンドポイントにアクセスできるのは、{{site.data.keyword.amashort}} Client SDK が装備されたモバイル・アプリケーションのみであるため、このメッセージが返されます。

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

1. アプリケーションを実行します。Facebook のログイン画面が表示されます。

   ![image](images/ios-facebook-login.png)

   この画面は、現在 Facebook にログインしていない場合、若干異なって見える可能性があります。

1. 「**OK**」をクリックし、{{site.data.keyword.amashort}} が認証を目的として Facebook のユーザー ID を使用することを承認します。

1. 	要求が成功すると、以下の出力が Xcode コンソールに表示されます。

   ```
response:Optional("Hello, this is a protected resouce of the mobile backend application!"), no error
 ```
   {: screen}

1. 次のコードを追加してログアウト機能を追加することもできます。

   ```
FacebookAuthenticationManager.sharedInstance.logout(callBack)
```
   {: codeblock}

   ユーザーが Facebook にログインした後でこのコードを呼び出し、そのユーザーが再度ログインしようとする場合、{{site.data.keyword.amashort}} が認証を目的として Facebook を使用することについての許可を求めるプロンプトが出されます。

   ユーザーを切り替えるには、このコードを呼び出す必要があり、ユーザーはブラウザーで Facebook からログアウトしなければなりません。

   ログアウト機能へ `callBack` を渡すことは、オプションです。`nil` を渡すこともできます。
