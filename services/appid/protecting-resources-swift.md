---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Protecting Swift resources
{: #protecting-resources-swift}

You can use the {{site.data.keyword.appid_short}} server SDK to protect resources in your Swift app.
{:shortdesc}


## Before you begin
{: #before-you-begin}

* Be familiar with developing Swift applications on {{site.data.keyword.Bluemix}}.
* Install the following software:
    * Swift 3.0.2
    * Kitura 1.6


## Installing the SDK

1. Open the `Package.swift` file in the directory of your Swift app and add the `appid-serversdk-swift` dependency. For example:

  ```swift
  import PackageDescription

  let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
  ```
  {:pre}

## Protecting resources in Swift
{: #protecting}

The Swift SDK provides Kitura Credential Plug-ins that is used for protecting web applications. When using this plug-in, an unauthenticated client receives an HTTP 302 response. The client is redirected to the login page that is hosted by {{site.data.keyword.appid_short_notm}} or to the identity provider's login page, depending on the configuration.



### Protecting web apps
{: protect-webapps notoc}

The WebAppKituraCredentialsPlugin is based on the OAuth2 authorization_code grant flow and must be used for web applications that use browsers. The plug-in provides tools to implement authentication and authorization flows. The plug-in also provides mechanisms to detect unauthenticated attempts to access protected resources and automatically redirects a user's browser to the authentication page. After successful authentication, a user is taken to the web application's callback URL, which uses the plug-in to obtain access and identity tokens from {{site.data.keyword.appid_short_notm}}. After obtaining these tokens, the plug-in stores them in an HTTP session under WebAppKituraCredentialsPlugin.AuthContext.

The following code demonstrates how to use WebAppKituraCredentialsPlugin in a Kitura application to protect the /protected endpoint.

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

For more information see the <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} Swift GitHub repository <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
