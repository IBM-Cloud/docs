---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:pre: .pre}


# iOS Swift SDK のセットアップ
{: #getting-started-ios}

{{site.data.keyword.appid_short}} Client SDK を使用して Swift アプリケーションを構築し、SDK を初期化し、ユーザーを認証し、保護リソースや無保護リソースへの要求を実行します。
{:shortdesc}


## 開始する前に
{: #before-you-begin}

以下の情報が必要です。
  * {{site.data.keyword.appid_short_notm}} のインスタンス。
  * テナント ID。
    * サービスのダッシュボードの**「サービス資格情報」**タブの**「資格情報の表示」**をクリックします。**「TenantID」**フィールドに、テナント ID が表示されます。その値をアプリの初期化に使用します。
  * {{site.data.keyword.Bluemix_notm}} 地域。地域は UI に表示されています。その値をアプリの初期化に使用します。<table> <caption> 表 1. {{site.data.keyword.Bluemix_notm}} 地域と対応する SDK 値</caption>
    <tr>
      <th> Bluemix 地域</th>
      <th> SDK 値</th>
    </tr>
    <tr>
      <td> 米国南部</td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> シドニー</td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> 英国</td>
      <td> AppID.REGION_UK </td>
    </tr>
  </table>

  * Xcode プロジェクト (バージョン 8.1 以上)。
  * CocoaPods (バージョン 1.1.0 以上)。


## Client SDK のインストール
{: #install-appid-sdk}

{{site.data.keyword.appid_short_notm}} Client SDK には、Swift プロジェクトと Objective-C Cocoa プロジェクト用の従属関係マネージャーである CocoaPods が付属しています。CocoaPods は成果物をダウンロードし、プロジェクトで使用できるようにします。

1. Xcode プロジェクトを作成するか、既存のプロジェクトを開きます。
2. プロジェクトのディレクトリー内の Podfile を開くか、このディレクトリー内に Podfile を作成します。
3. プロジェクトのターゲットの下に、「BluemixAppID」Pod の従属関係を追加します。ターゲットの下に `use_frameworks!` コマンドもあることを確認します。
  

  以下に例を示します。

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'BluemixAppID'
  end
  ```
  {:pre}

4. `BluemixAppID` の従属関係をダウンロードするには、以下のコマンドを実行します。

  ```swift
  pod install --repo-update
  ```
  {:pre}

6. Xcode プロジェクトを開き、キーチェーン共有を使用可能にします。**「Project Settings」**の下で、**「Capabilities」** > **「Keychain Sharing」**をクリックします。
7. **「Project Settings」** > **「Info」** > **「URL Types」**の下で、URL タイプを追加します。**「Identifier」**テキスト・ボックスと**「URL Scheme」**テキスト・ボックスに値 $(PRODUCT_BUNDLE_IDENTIFIER) を入力します。


## Client SDK の初期化
{: #initialize-client-sdk}

1. `AppDelegate.swift` ファイルに以下のインポートを追加します。

  ```swift
  import BluemixAppID
  ```
  {:pre}

2. tenant ID パラメーターと region パラメーターを initialize メソッドに渡して、Client SDK を初期化します。初期化コードの配置場所として一般的な (必須ではありません) 場所は、Swift アプリケーションの AppDelegate の application:didFinishLaunchingWithOptions: メソッド内です。

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.Region_UK)
  ```
  {:pre}

  * 「tenantId」を App ID サービスのテナント ID に置き換えます。
  * AppID.REGION_UK を、該当する {{site.data.keyword.appid_short_notm}} 地域に置き換えます。

3. 以下のコードを AppDelegate ファイルに追加します。

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {:pre}

## ログイン・ウィジェットを使用したユーザーの認証
{: #authenticate-login}

{{site.data.keyword.appid_short_notm}} Client SDK が初期化されたら、ログイン・ウィジェットを実行してユーザーを認証できるようになります。ログイン・ウィジェットのデフォルト構成では、認証オプションとして Facebook、Google、またはその両方が使用されます。一方だけを構成した場合、ログイン・ウィジェットは起動せずに、ユーザーは構成済みの IDP 認証画面にリダイレクトされます。



1. SDK を使用するファイルに以下のインポートを追加します。

  ```swift
  import BluemixAppID
  ```
  {:pre}

2. 以下のコマンドを実行してウィジェットを起動します。

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //ユーザーの認証
      }

      public func onAuthorizationCanceled() {
          //ユーザーによる認証の取り消し
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //例外の発生
      }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {:pre}

## ユーザー属性へのアクセス
{: #accessing}

アクセス・トークンを取得すれば、ユーザーの保護された属性のエンドポイントにアクセスできます。以下の API メソッドを使用すると、アクセスできるようになります。

  ```swift
  func setAttribute(key: String, value: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func setAttribute(key: String, value: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttributes(completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttributes(accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func deleteAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func deleteAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  ```
  {:pre}

アクセス・トークンを明示的に渡さないと、{{site.data.keyword.appid_short_notm}} は最後に受け取ったトークンを使用します。

例えば、以下のコードを呼び出して、新しい属性を設定したり既存の属性をオーバーライドしたりできます。

  ```swift
  AppID.sharedInstance.userAttributeManager?.setAttribute("key", "value", completionHandler: { (error, result) in
      if error = nil {
          //Attributes recieved as a Dictionary
      } else {
          // An error has occurred
      }
  })
  ```
  {:pre}


### 匿名ログイン
{: #anonymous notoc}

{{site.data.keyword.appid_short_notm}} では、[匿名](/docs/services/appid/user-profile.html#anonymous)ログインが可能です。

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //ユーザーの認証
      }

      public func onAuthorizationCanceled() {
          //ユーザーによる認証の取り消し
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //エラーの発生
      }
   }

  AppID.sharedInstance.loginAnonymously( authorizationDelegate: delegate())
  ```
  {:pre}

### 段階的な認証
{: #progressive notoc}

匿名のアクセス・トークンを保持している場合、このトークンを loginWidget.launch メソッドに渡すと、ユーザーを識別済みのユーザーにすることができます。

  ```swift
  func launch(accessTokenString: String? , delegate: AuthorizationDelegate)
  ```
  {:pre}

匿名ログインの後には、アクセス・トークンを渡さずにログイン・ウィジェットを呼び出した場合であっても段階的な認証が行われます。最後に受け取ったトークンがサービスで使用されるからです。保管されているトークンをクリアする場合は、以下のコマンドを実行します。

  ```swift
  var appIDAuthorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)
  appIDAuthorizationManager.clearAuthorizationData()
  ```
  {:pre}



## 次のステップ
{: #next-steps}

初めて ID プロバイダーをセットアップするときに、{{site.data.keyword.appid_short_notm}} からデフォルト構成が示されます。このデフォルト構成は開発モードのみで使用できます。アプリケーションを公開する前に、デフォルトの [Facebook](/docs/services/appid/identity-providers.html#facebook) と [Google](/docs/services/appid/identity-providers.html#google) の構成を自分の資格情報に更新してください。
