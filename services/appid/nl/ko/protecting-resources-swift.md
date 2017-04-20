---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Swift 리소스 보호
{: #protecting-resources-swift}

{{site.data.keyword.appid_short}} 서버 SDK를 사용하여 Swift 앱의 리소스를 보호할 수 있습니다.
{:shortdesc}


## 시작하기 전에
{: #before-you-begin}

* {{site.data.keyword.Bluemix}}에서 Swift 애플리케이션 개발에 익숙해지십시오.
* 다음 소프트웨어를 설치하십시오.
    * Swift 3.0.2
    * Kitura 1.6


## SDK 설치

1. Swift 앱의 디렉토리에서 `Package.swift` 파일을 열고 `appid-serversdk-swift` 종속성을 추가하십시오. 예를 들면 다음과 같습니다. 

  ```swift
  import PackageDescription

  let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
  ```
  {:pre}

## Swift의 리소스 보호
{: #protecting}

Swift SDK는 웹 애플리케이션 보호에 사용되는 Kitura 신임 정보 플러그인을 제공합니다. 이 플러그인을 사용하는 경우 인증되지 않은 클라이언트가 HTTP 302 응답을 수신합니다. 클라이언트는 구성에 따라서 {{site.data.keyword.appid_short_notm}}에서 호스팅하는 로그인 페이지로 경로 재지정되거나 ID 제공자의 로그인 페이지로 경로 재지정됩니다. 



### 웹 앱 보호
{: protect-webapps notoc}

WebAppKituraCredentialsPlugin은 OAuth2 authorization_code 권한 부여 플로우를 기반으로 하며 브라우저를 사용하는 웹 애플리케이션에 사용해야 합니다. 플러그인은 권한 및 인증 플로우를 구현하기 위한 도구를 제공합니다. 또한, 플러그인은 보호된 리소스에 액세스하려는 인증되지 않은 시도를 발견하기 위한 메커니즘을 제공하며 사용자의 브라우저를 인증 페이지로 자동으로 경로 재지정합니다. 인증에 성공하면 사용자는 웹 애플리케이션의 콜백 URL로 이동하며 {{site.data.keyword.appid_short_notm}}에서 액세스 및 ID 토큰을 확보하기 위해 플러그인을 사용합니다. 해당 토큰을 확보한 후에 플러그인은 WebAppKituraCredentialsPlugin.AuthContext 아래의 HTTP 세션에 토큰을 저장합니다.

다음 코드는 /protected 엔드포인트를 보호하기 위해 Kitura 애플리케이션에서 WebAppKituraCredentialsPlugin을 사용하는 방법을 보여줍니다. 

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

자세한 정보는 <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} Swift GitHub 저장소 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>을 참조하십시오. 
