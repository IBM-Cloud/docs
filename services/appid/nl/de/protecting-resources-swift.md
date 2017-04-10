---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Swift-Ressourcen schützen
{: #protecting-resources-swift}

Sie können das {{site.data.keyword.appid_short}}-Server-SDK verwenden, um Ressourcen in Ihrer Swift-App zu schützen.
{:shortdesc}


## Vorbereitungen
{: #before-you-begin}

* Sie sollten mit der Entwicklung von Swift-Anwendungen in {{site.data.keyword.Bluemix}} vertraut sein.
* Installieren Sie die folgende Software:
    * Swift 3.0.2
    * Kitura 1.6


## SDK installieren

1. Öffnen Sie die Datei `Package.swift`, die sich im Verzeichnis Ihrer Swift-App befindet, und fügen Sie die Abhängigkeit `appid-serversdk-swift` hinzu. Beispiel:

  ```swift
  import PackageDescription

  let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
  ```
  {:pre}

## Ressourcen in Swift schützen
{: #protecting}

Das Swift-SDK stellt Kitura Credential Plug-ins bereit, das zum Schützen von Webanwendungen verwendet wird. Wenn Sie dieses Plug-in verwenden, empfängt ein nicht authentifizierter Client eine HTTP 302-Antwort. Der Client wird je nach Konfiguration zur Anmeldeseite, die von {{site.data.keyword.appid_short_notm}} gehostet wird, oder zur Anmeldeseite des Identitätsproviders umgeleitet.



### Web-Apps schützen
{: protect-webapps notoc}

Das WebAppKituraCredentialsPlugin basiert auf dem Grant-Ablauf des OAuth2-Berechtigungscodes und muss für Webanwendungen verwendet werden, die Browser nutzen. Das Plug-in enthält Tools, um Authentifizierungs- und Berechtigungsabläufe zu implementieren. Das Plug-in stellt außerdem Mechanismen zur Verfügung, um nicht authentifizierte Versuche aufzudecken, auf geschützte Ressourcen zuzugreifen, und leitet einen Benutzerbrowser zur Authentifizierungsseite weiter. Nach einer erfolgreichen Authentifizierung wird der Benutzer zur Callback-URL der Webanwendung weitergeleitet, die das Plug-in verwendet, um Zugriff und Identitätstoken von {{site.data.keyword.appid_short_notm}} zu erhalten. Nach Erhalt dieser Token werden diese vom Plug-in in einer HTTP-Sitzung unter WebAppKituraCredentialsPlugin.AuthContext gespeichert.

Der folgende Code demonstriert, wie WebAppKituraCredentialsPlugin in einer Kitura-Anwendung verwendet wird, um den Endpunkt '/protected' zu schützen.

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID

  // Folgende URLs werden für AppID OAuth-Abläufe genutzt
  var LOGIN_URL = "/ibm/bluemix/appid/login"
  var CALLBACK_URL = "/ibm/bluemix/appid/callback"
  var LOGOUT_URL = "/ibm/bluemix/appid/logout"
  var LANDING_PAGE_URL = "/index.html"

  // Setup von Kitura zur Nutzung von Sitzungs-Middleware
  // Muss mit korrektem Sitzungsspeicher für Produktionsumgebungen
  // konfiguriert werden. Siehe https://github.com/IBM-Swift/Kitura-Session für
  // weitere Dokumentationen
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

  // Expliziter Anmelde-Endpunkt
  router.get(LOGIN_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Callback zum Beenden des Berechtigungsprozesses. Ruft Zugriffs- und Identitätstokens von AppID ab
  router.get(CALLBACK_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Abmelde-Endpunkt. Löscht Authentifizierungsinformationen aus Sitzung
  router.get(LOGOUT_URL, handler:  { (request, response, next) in
  	kituraCredentials.logOut(request: request)
  	webappKituraCredentialsPlugin.logout(request: request)
  	_ = try? response.redirect(LANDING_PAGE_URL)
  })

  // Geschützter Bereich
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

  //HTTP-Server hinzufügen und mit Router verbinden
  Kitura.addHTTPServer(onPort: port, with: router)

  // Start des Kitura-Runloops (Aufruf wird nie zurückgegeben)
  Kitura.run()
  ```
  {:pre}

Weitere Informationen finden Sie im Abschnitt zum <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}}-Swift GitHub-Repository <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.
