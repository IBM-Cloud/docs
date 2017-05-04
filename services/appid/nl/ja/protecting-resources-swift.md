---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Swift リソースの保護
{: #protecting-resources-swift}

{{site.data.keyword.appid_short}} Server SDK を使用して、Swift アプリ内のリソースを保護することができます。
{:shortdesc}


## 開始する前に
{: #before-you-begin}

* {{site.data.keyword.Bluemix}} での Swift アプリケーションの開発に精通している必要があります。
* 以下のソフトウェアをインストールします。
    * Swift 3.0.2
    * Kitura 1.6


## SDK のインストール

1. Swift アプリのディレクトリーにある `Package.swift` ファイルを開き、`appid-serversdk-swift` 従属関係を追加します。以下に例を示します。

  ```swift
  import PackageDescription

  let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
  ```
  {:pre}

## Swift のリソースの保護
{: #protecting}

Swift SDK には、Web アプリケーションを保護するために使用する Kitura Credential プラグインが用意されています。このプラグインを使用する場合、非認証のクライアントは HTTP 302 応答を受け取ります。
構成に応じて、クライアントは {{site.data.keyword.appid_short_notm}} によってホストされるログイン・ページか、ID プロバイダーのログイン・ページにリダイレクトされます。



### Web アプリの保護
{: protect-webapps notoc}

WebAppKituraCredentialsPlugin は、OAuth2 の authorization_code 認可フローに基づくものであり、ブラウザーを使用する Web アプリケーションで使用する必要があります。このプラグインには、認証フローと許可フローを実装するためのツールが用意されています。プラグインはまた、保護リソースに対する非認証のアクセス試行を検出し、ユーザーのブラウザーを認証ページに自動的にリダイレクトするメカニズムも備えています。認証に成功すると、ユーザーは Web アプリケーションのコールバック URL に送られ、この URL がプラグインを使用して {{site.data.keyword.appid_short_notm}} からアクセス・トークンと識別トークンを取得します。それらのトークンを取得すると、プラグインはそれらを WebAppKituraCredentialsPlugin.AuthContext の下の HTTP セッションに保管します。

以下のコードは、WebAppKituraCredentialsPlugin を Kitura アプリケーションで使用して /protected エンドポイントを保護する方法を示しています。

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID

  // The following URLs will be used for AppID OAuth flows
  var LOGIN_URL = "/ibm/bluemix/appid/login"
  var CALLBACK_URL = "/ibm/bluemix/appid/callback"
  var LOGOUT_URL = "/ibm/bluemix/appid/logout"
  var LANDING_PAGE_URL = "/index.html"

  // Setup Kitura to use session middleware
  // Must be configured with proper session storage for production
  // environments. See https://github.com/IBM-Swift/Kitura-Session for
  // additional documentation
  let router = Router()
  let session = Session(secret: "Some secret")
  router.all(middleware: session)

  let options = [
  	"clientId": "{client-id}",
  	"secret": "{secret}",
  	"tenantId": "{tenant-id}",
  	"oauthServerUrl": "{oauth-server-url}",
  	"redirectUri": "{app-url}" + CALLBACK_URL
  ]
  let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin(options: options)
  let kituraCredentials = Credentials()
  kituraCredentials.register(plugin: webappKituraCredentialsPlugin)

  // Explicit login endpoint
  router.get(LOGIN_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Callback to finish the authorization process. Will retrieve access and identity tokens from AppID
  router.get(CALLBACK_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Logout endpoint. Clears authentication information from session
  router.get(LOGOUT_URL, handler:  { (request, response, next) in
  	kituraCredentials.logOut(request: request)
  	webappKituraCredentialsPlugin.logout(request: request)
  	_ = try? response.redirect(LANDING_PAGE_URL)
  })

  // Protected area
  router.get("/protected", handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name), { (request, response, next) in
      let appIdAuthContext:JSON? = request.session?[WebAppKituraCredentialsPlugin.AuthContext]
      let identityTokenPayload:JSON? = appIdAuthContext?["identityTokenPayload"]

      guard appIdAuthContext?.dictionary != nil, identityTokenPayload?.dictionary != nil else {
          response.status(.unauthorized)
          return next()
      }

      response.send(json: identityTokenPayload!)
      next()
			})
  var port = 3000
  if let portString = ProcessInfo.processInfo.environment["PORT"]{
      port = Int(portString)!
  }
  print("Starting on \(port)")

  // Add an HTTP server and connect it to the router
  Kitura.addHTTPServer(onPort: port, with: router)

  // Start the Kitura runloop (this call never returns)
  Kitura.run()
  ```
  {:pre}

詳しくは、<a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}}Swift GitHub リポジトリー <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。
