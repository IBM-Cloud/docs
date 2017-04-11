---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Protezione delle risorse Swift
{: #protecting-resources-swift}

Puoi utilizzare l'SDK server {{site.data.keyword.appid_short}} per proteggere risorse nella tua applicazione Swift.
{:shortdesc}


## Prima di cominciare
{: #before-you-begin}

* Devi avere dimestichezza con lo sviluppo di applicazioni Swift su {{site.data.keyword.Bluemix}}.
* Installare il software riportato di seguito:
    * Swift 3.0.2
    * Kitura 1.6


## Installazione dell'SDK

1. Apri il file `Package.swift` nella directory della tua applicazione Swift e aggiungi la dipendenza `appid-serversdk-swift`. Ad esempio:

  ```swift
  import PackageDescription

  let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
  ```
  {:pre}

## Protezione di risorse in Swift
{: #protecting}

L'SDK Swift fornisce i plugin Kitura Credential utilizzati per la protezione delle applicazioni web. Quando utilizzi questo plugin, un client non autenticato riceve un risposta HTTP 302. Il client viene reindirizzato alla pagina di accesso ospitata da {{site.data.keyword.appid_short_notm}} o alla pagina di accesso del provider di identità, a seconda della configurazione.



### Protezione delle applicazioni web
{: protect-webapps notoc}

WebAppKituraCredentialsPlugin si basa sul flusso di concessione del codice_autorizzazione OAuth2 e deve essere utilizzato per le applicazioni web che utilizzano i browser. Il plugin fornisce gli strumenti per implementare l'autenticazione e i flussi di autorizzazione. Il plugin inoltre fornisce il meccanismo di individuazione dei tentativi non autenticati di accesso alle risorse protette e automaticamente esegue il reindirizzamento a un browser dell'utente alla pagina di autenticazione. Dopo un'autenticazione corretta, a un utente viene fornito l'URL di callback dell'applicazione web, che utilizza il plugin per ottenere i token di identità e di accesso da {{site.data.keyword.appid_short_notm}}. Dopo aver ottenuto questi token, il plugin li archivia in una sessione HTTP in WebAppKituraCredentialsPlugin.AuthContext.

Il seguente codice illustra come utilizzare WebAppKituraCredentialsPlugin in un'applicazione Kitura per proteggere l'endpoint /protected.

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID

  // I seguenti URL saranno utilizzati per i flussi AppID OAuth
  var LOGIN_URL = "/ibm/bluemix/appid/login"
  var CALLBACK_URL = "/ibm/bluemix/appid/callback"
  var LOGOUT_URL = "/ibm/bluemix/appid/logout"
  var LANDING_PAGE_URL = "/index.html"

  // Configurare Kitura per utilizzare il middleware della sessione
  // Deve essere configurato con l'archivio della sessione corretto per gli ambienti
  // di produzione. Consulta https://github.com/IBM-Swift/Kitura-Session per
  // ulteriore documentazione
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

  // Endpoint di accesso esplicito
  router.get(LOGIN_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Callback per terminare il processo di autorizzazione. Richiamerà i token di identità e di accesso da AppID
  router.get(CALLBACK_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Disconnettere l'endpoint. Cancellare le informazioni di autenticazione dalla sessione
  router.get(LOGOUT_URL, handler:  { (request, response, next) in
  	kituraCredentials.logOut(request: request)
  	webappKituraCredentialsPlugin.logout(request: request)
  	_ = try? response.redirect(LANDING_PAGE_URL)
  })

  // Area protetta
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

  // Aggiungi un server HTTP e collegalo al router
  Kitura.addHTTPServer(onPort: port, with: router)

  // Avvia il runloop Kitura (questa chiamata non viene mai restituita)
  Kitura.run()
  ```
  {:pre}

Per ulteriori informazioni, visita il <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} Swift GitHub repository <img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a>.
