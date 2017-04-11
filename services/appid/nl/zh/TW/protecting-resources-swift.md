---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# 保護 Swift 資源
{: #protecting-resources-swift}

您可以使用 {{site.data.keyword.appid_short}} 伺服器 SDK 來保護 Swift 應用程式中的資源。
{:shortdesc}


## 開始之前
{: #before-you-begin}

* 熟悉如何在 {{site.data.keyword.Bluemix}} 上開發 Swift 應用程式。
* 安裝下列軟體：
    * Swift 3.0.2
    * Kitura 1.6


## 安裝 SDK

1. 開啟 Swift 應用程式的目錄中的 `Package.swift` 檔案，並新增 `appid-serversdk-swift` 相依關係。例如：

  ```swift
  import PackageDescription

  let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
  ```
  {:pre}

## 保護 Swift 中的資源
{: #protecting}

Swift SDK 提供用於保護 Web 應用程式的「Kitura 認證外掛程式」。使用此外掛程式時，未經鑑別的用戶端會收到 HTTP 302 回應。用戶端會重新導向至 {{site.data.keyword.appid_short_notm}} 所管理的登入頁面或是身分提供者的登入頁面（視配置而定）。



### 保護 Web 應用程式
{: protect-webapps notoc}

WebAppKituraCredentialsPlugin 是根據 OAuth2 authorization_code 授與流程，而且必須用於使用瀏覽器的 Web 應用程式。此外掛程式提供工具來實作鑑別及授權流程。此外掛程式也提供機制來偵測未經鑑別的受保護資源存取嘗試，並且會自動將使用者的瀏覽器重新導向至鑑別頁面。成功鑑別之後，會將使用者帶至 Web 應用程式的回呼 URL，以使用此外掛程式自 {{site.data.keyword.appid_short_notm}} 中取得存取及身分記號。取得這些記號之後，外掛程式會將它們儲存在 HTTP 階段作業的 WebAppKituraCredentialsPlugin.AuthContext 下方。

下列程式碼示範如何在 Kitura 應用程式中使用 WebAppKituraCredentialsPlugin 來保護 /protected 端點。

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

如需相關資訊，請參閱 <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} Swift GitHub 儲存庫 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
