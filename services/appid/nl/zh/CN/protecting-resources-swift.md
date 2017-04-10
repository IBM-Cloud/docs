---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# 保护 Swift 资源
{: #protecting-resources-swift}

您可以使用 {{site.data.keyword.appid_short}} 服务器 SDK 来保护 Swift 应用程序中的资源。
{:shortdesc}


## 开始之前
{: #before-you-begin}

* 熟悉如何在 {{site.data.keyword.Bluemix}} 上开发 Swift 应用程序。
* 安装以下软件：
    * Swift 3.0.2
    * Kitura 1.6


## 安装 SDK

1. 打开 Swift 应用程序目录中的 `Package.swift` 文件，并添加 `appid-serversdk-swift` 依赖项。例如：


  ```swift
  import PackageDescription

  let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
  ```
  {:pre}

## 保护 Swift 中的资源
{: #protecting}

Swift SDK 提供了 Kitura 凭证插件，用于保护 Web 应用程序。使用此插件时，未经认证的客户端将收到 HTTP 302 响应。根据配置，客户端会重定向到 {{site.data.keyword.appid_short_notm}} 托管的登录页面，或者重定向到身份提供者的登录页面。



### 保护 Web 应用程序
{: protect-webapps notoc}

WebAppKituraCredentialsPlugin 基于 OAuth2 authorization_code 授权流程，并且必须用于使用浏览器的 Web 应用程序。此插件提供了用于实施认证和授权流程的工具。此插件还提供了相应机制来检测对受保护资源的未经认证的访问尝试，并自动将用户的浏览器重定向到认证页面。成功认证后，用户会转至 Web 应用程序的回调 URL，该 URL 使用此插件从 {{site.data.keyword.appid_short_notm}} 获取访问令牌和身份令牌。获取这些令牌后，此插件会将其存储在 HTTP 会话中的 WebAppKituraCredentialsPlugin.AuthContext 下。

以下代码演示了如何在 Kitura 应用程序中使用 WebAppKituraCredentialsPlugin 来保护 /protected 端点。

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

有关更多信息，请参阅 <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} Swift GitHub 存储库 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。
