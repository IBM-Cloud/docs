---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Protección de recursos Swift
{: #protecting-resources-swift}

Puede utilizar el SDK del servidor de {{site.data.keyword.appid_short}} para proteger recursos en la app Swift.
{:shortdesc}


## Antes de empezar
{: #before-you-begin}

* Familiarícese con el desarrollo de aplicaciones Swift en {{site.data.keyword.Bluemix}}.
* Instale el siguiente software:
    * Swift 3.0.2
    * Kitura 1.6


## Instalación del SDK

1. Abra el archivo `Package.swift` en el directorio de su app Swift y añada la dependencia `appid-serversdk-swift`. Por ejemplo:

  ```swift
  import PackageDescription

  let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
  ```
  {:pre}

## Protección de recursos en Swift
{: #protecting}

El SDK de Swift proporciona plugins de credenciales de Kitura que se utilizan para proteger aplicaciones web. Al utilizar este plugin, un cliente no autenticado recibe una respuesta HTTP 302. El cliente es redirigido a la página de inicio de sesión que aloja {{site.data.keyword.appid_short_notm}} o a la página de inicio de sesión del proveedor de identidad, en función de la configuración.



### Protección de apps web
{: protect-webapps notoc}

WebAppKituraCredentialsPlugin se basa en el flujo de concesión authorization_code de OAuth2 y debe utilizarse para aplicaciones web que usan navegadores. El plugin proporciona herramientas para implementar flujos de autorización y autenticación. El plugin también proporciona mecanismos para detectar intentos no autenticados de acceder a los recursos protegidos y redirige automáticamente el navegador de un usuario a una página de autenticación. Tras la correcta autenticación, se conduce al usuario al URL de devolución de llamada de la aplicación web, que utiliza el plugin para obtener señales de acceso e identidad de {{site.data.keyword.appid_short_notm}}. Después de obtener estas señales, el plugin las almacena en una sesión HTTP bajo WebAppKituraCredentialsPlugin.AuthContext.

El código siguiente muestra cómo utilizar WebAppKituraCredentialsPlugin en una aplicación Kitura para proteger el /punto final protegido.

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID

  // Los siguientes URL se utilizarán para flujos AppID OAuth
  var LOGIN_URL = "/ibm/bluemix/appid/login"
  var CALLBACK_URL = "/ibm/bluemix/appid/callback"
  var LOGOUT_URL = "/ibm/bluemix/appid/logout"
  var LANDING_PAGE_URL = "/index.html"

  // Configure Kitura para utilizar el middleware de sesión
  // Debe configurarse con el almacenamiento de sesión adecuado para entornos
  // de producción. Consulte https://github.com/IBM-Swift/Kitura-Session para
  // obtener documentación adicional
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

  // Punto final de inicio de sesión explícito
  router.get(LOGIN_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Devolución de llamada para finalizar el proceso de autorización. Se recuperarán las señales de acceso e identidad de AppID
  router.get(CALLBACK_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Punto final de cierre de sesión. Borra la información de la sesión
  router.get(LOGOUT_URL, handler:  { (request, response, next) in
  	kituraCredentials.logOut(request: request)
  	webappKituraCredentialsPlugin.logout(request: request)
  	_ = try? response.redirect(LANDING_PAGE_URL)
  })

  // Área protegida
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

  // Añada un servidor HTTP y conéctelo al direccionador
  Kitura.addHTTPServer(onPort: port, with: router)

  // Inicie Kitura runloop (esta llamada nunca vuelve)
  Kitura.run()
  ```
  {:pre}

Para obtener más información, consulte el <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">Repositorio de GitHub de Swift de {{site.data.keyword.appid_short_notm}}<img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
