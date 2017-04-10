---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:pre: .pre}


# iOS-Swift-SDK einrichten
{: #getting-started-ios}

Erstellen Sie Ihre Swift-Anwendungen mit dem {{site.data.keyword.appid_short}}-Client-SDK, initialisieren Sie das SDK, authentifizieren Sie Benutzer und senden Sie Anforderungen an geschützte und nicht geschützte Ressourcen.
{:shortdesc}


## Vorbereitungen
{: #before-you-begin}

Sie benötigen die folgenden Informationen:
  * Eine Instanz von {{site.data.keyword.appid_short_notm}}.
  * Ihre Tenant-ID.
    * Klicken Sie in der Registerkarte **Serviceberechtigungsnachweise** Ihres Service-Dashboards auf **Berechtigungsnachweise anzeigen**. Ihre Tenant-ID wird im Feld **Tenant-ID** angezeigt. Dieser Wert wird für die Initialisierung Ihrer App verwendet.
  * Ihre {{site.data.keyword.Bluemix_notm}}-Region.
  Sie finden Ihre Region in Ihrer Benutzerschnittstelle. Der Wert wird für die Initialisierung Ihrer App verwendet.
    <table> <caption> Tabelle 1: {{site.data.keyword.Bluemix_notm}}-Regionen und entsprechende SDK-Werte </caption>
    <tr>
      <th> Bluemix-Region </th>
      <th> SDK-Wert </th>
    </tr>
    <tr>
      <td> Vereinigte Staaten (Süden) </td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> Sydney </td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> Vereinigtes Königreich </td>
      <td> AppID.REGION_UK </td>
    </tr>
  </table>

  * Ein Xcode-Projekt (Version 8.1 oder höher).
  * CocoaPods (Version 1.1.0 oder höher).


## {{site.data.keyword.appid_short_notm}}-Client-SDK installieren
{: #install-appid-sdk}

Das {{site.data.keyword.appid_short_notm}}-Client-SDK wird mit CocoaPods verteilt, einem Abhängigkeitenmanager für Swift- und Objective-C Cocoa-Projekte. CocoaPods lädt Artefakte herunter und stellt sie für Ihr Projekt zur Verfügung.

1. Erstellen Sie ein Xcode-Projekt oder öffnen Sie ein vorhandenes Projekt.
2. Öffnen oder erstellen Sie die Podfile im Projektverzeichnis.
3. Fügen Sie unter dem Ziel Ihres Projekts eine Abhängigkeit für 'BluemixAppID' Pod hinzu. Stellen Sie sicher, dass sich der Befehl `use_frameworks!` auch unter dem Ziel befindet.

  Beispiel:

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'BluemixAppID'
  end
  ```
  {:pre}

4. Um die `BluemixAppID`-Abhängigkeit herunterzuladen, führen Sie den folgenden Befehl aus:

  ```swift
  pod install --repo-update
  ```
  {:pre}

6. Öffnen Sie Ihr Xcode-Projekt und aktivieren Sie das Keychain-Sharing. Klicken Sie in **Projekteinstellungen** auf **Funktionen** > **Keychain-Sharing**.
7. Fügen Sie unter **Projekteinstellungen** > **Info** > **URL-Typen** einen URL-Typ hinzu. Tragen Sie sowohl in das Textfeld **ID** als auch **URL-Schema** diesen Wert ein: $(PRODUCT_BUNDLE_IDENTIFIER)


## {{site.data.keyword.appid_short_notm}}-Client-SDK initialisieren
{: #initialize-client-sdk}

1. Fügen Sie den folgenden Import zu Ihrer Datei `AppDelegate.swift` hinzu:

  ```swift
  import BluemixAppID
  ```
  {:pre}

2. Initialisieren Sie das SDK, indem Sie die Parameter 'tenantID' und 'region' an die Methode 'initialize' übergeben. Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode 'application:didFinishLaunchingWithOptions:' von AppDelegate in Ihrer Swift-Anwendung.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.Region_UK)
  ```
  {:pre}

  * Ersetzen Sie 'tenantId' durch die Tenant-ID für Ihren App-ID-Service.
  * Ersetzen Sie AppID.REGION_UK durch Ihre {{site.data.keyword.appid_short_notm}}-Region.

3. Fügen Sie Ihrer Anwendung die folgende AppDelegate-Datei hinzu.

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {:pre}

## Benutzer über das Anmelde-Widget authentifizieren
{: #authenticate-login}

Nach der Initialisierung des {{site.data.keyword.appid_short_notm}}-Client-SDK können Sie Benutzer authentifizieren, indem Sie das Anmelde-Widget ausführen. Die Standardkonfiguration des Anmelde-Widgets verwendet Facebook, Google oder beides als Authentifizierungsoption. Wenn Sie nur Facebook oder Google konfigurieren, wird das Anmelde-Widget nicht gestartet und der Benutzer wird zur konfigurierten IDP-Authentifizierungsanzeige umgeleitet.



1. Fügen Sie den folgenden Import zu der Datei hinzu, in der das SDK verwendet werden soll.

  ```swift
  import BluemixAppID
  ```
  {:pre}

2. Führen Sie den folgenden Befehl aus, um das Widget zu starten:

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //Benutzer authentifiziert
      }

      public func onAuthorizationCanceled() {
          //Authentifizierung von Benutzer abgebrochen
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Ausnahmebedingung aufgetreten
      }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {:pre}

## Auf Benutzerattribute zugreifen
{: #accessing}

Wenn Sie ein Zugriffstoken anfordern, können Sie Zugriff auf den Endpunkt der geschützten Benutzerattribute zugreifen. Sie können Zugriff durch die folgenden API-Methoden erhalten:

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

Wenn ein Zugriffstoken nicht explizit übergeben wird, verwendet {{site.data.keyword.appid_short_notm}} das zuletzt empfangene Token.

Sie können beispielsweise diesen Code aufrufen, um ein neues Attribut festzulegen oder ein vorhandenes Attribut zu überschreiben:

  ```swift
  AppID.sharedInstance.userAttributeManager?.setAttribute("key", "value", completionHandler: { (error, result) in
      if error = nil {
          //Attribute als Wörterbuch erhalten
      } else {
          // Ein Fehler ist aufgetreten
      }
  })
  ```
  {:pre}


### Anonyme Anmeldung
{: #anonymous notoc}

Sie können sich mit {{site.data.keyword.appid_short_notm}} anonym anmelden; siehe [anonyme Identität](/docs/services/appid/user-profile.html#anonymous).

  ```swift
  class delegate : AuthorizationDelegate {

      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //Benutzer authentifiziert
      }

      public func onAuthorizationCanceled() {
          //Authentifizierung von Benutzer abgebrochen
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Fehler aufgetreten
      }
   }

  AppID.sharedInstance.loginAnonymously( authorizationDelegate: delegate())
  ```
  {:pre}

### Progressive Authentifizierung
{: #progressive notoc}

Benutzer mit einem anonymen Zugriffstoken können identifiziert werden, indem es der Methode 'loginWidget.launch' übergeben wird:

  ```swift
  func launch(accessTokenString: String? , delegate: AuthorizationDelegate)
  ```
  {:pre}

Nach einer anonymen Anmeldung tritt eine progressive Authentifizierung auf, sogar wenn das Anmelde-Widget aufgerufen wird, ohne dass dabei ein Zugriffstoken übergeben wird. Grund hierfür ist, dass der Service das zuletzt empfangene Token verwendet. Führen Sie den folgenden Befehl aus, um gespeicherte Token zu löschen:

  ```swift
  var appIDAuthorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)
  appIDAuthorizationManager.clearAuthorizationData()
  ```
  {:pre}



## Nächste Schritte
{: #next-steps}

{{site.data.keyword.appid_short_notm}} stellt eine Standardkonfiguration bereit, wenn Sie Ihre Identitätsprovider erstmalig einrichten. Die Standardkonfiguration können Sie nur im Entwicklungsmodus verwenden. Bevor Sie Ihre Anwendung veröffentlichen, aktualisieren Sie die Standardkonfiguration für [Facebook](/docs/services/appid/identity-providers.html#facebook) und [Google](/docs/services/appid/identity-providers.html#google) mit Ihren eigenen Berechtigungsnachweisen.
