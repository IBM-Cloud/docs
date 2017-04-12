---

copyright:
  years: 2017 lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Protegendo recursos do Swift
{: #protecting-resources-swift}

É possível usar o SDK do servidor {{site.data.keyword.appid_short}} para proteger recursos em seu app Swift.
{:shortdesc}


## Antes de Começar
{: #before-you-begin}

* Familiarize-se com o desenvolvimento de aplicativos Swift no {{site.data.keyword.Bluemix}}.
* Instale o seguinte software:
    * Swift 3.0.2
    * Kitura 1.6


## Instalando o SDK

1. Abra o arquivo `Package.swift` no diretório de seu app Swift e inclua a dependência `appid-serversdk-swift`. Por exemplo:

  ```swift
  import PackageDescription

  let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
  ```
  {:pre}

## Protegendo recursos no Swift
{: #protecting}

O SDK do Swift fornece o Kitura Credential Plug-ins que é usado para proteger aplicativos da web. Ao usar esse plug-in, um cliente não autenticado recebe uma
resposta HTTP 302. O cliente é redirecionado para a página de login que é hospedada pelo {{site.data.keyword.appid_short_notm}} ou para a página de login do
provedor de identidade, dependendo da configuração.



### Protegendo aplicativos da web
{: protect-webapps notoc}

O WebAppKituraCredentialsPlugin é baseado no fluxo de concessão authorization_code do OAuth2 e deve ser usado para aplicativos da web que usam navegadores. O
plug-in fornece ferramentas para implementar fluxos de autenticação e de autorização. O plug-in também fornece mecanismos para detectar tentativas não autenticadas
para acessar recursos protegidos e automaticamente redireciona um navegador do usuário para a página de autenticação. Após a autenticação bem-sucedida, um usuário é
levado para a URL de retorno de chamada do aplicativo da web, que usa o plug-in para obter tokens de acesso e a identidade do
{{site.data.keyword.appid_short_notm}}. Após obter esses tokens, o plug-in os armazena em uma sessão de HTTP sob WebAppKituraCredentialsPlugin.AuthContext.

O código a seguir demonstra como usar WebAppKituraCredentialsPlugin em um aplicativo Kitura para proteger o terminal /protected.

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

Para obter mais informações, veja o <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">repositório do GitHub
<img src="../../icons/launch-glyph.svg" alt="ícone de Link externo"></a>.
