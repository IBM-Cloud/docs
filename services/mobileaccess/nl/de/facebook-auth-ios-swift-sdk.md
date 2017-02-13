---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Facebook-Authentifizierung für iOS-Apps aktivieren (Swift-SDK)
{: #facebook-auth-ios}

Wenn Sie Facebook als Identitätsprovider in Ihren {{site.data.keyword.amafull}}-iOS-Anwendungen verwenden möchten, müssen Sie die iOS-Plattform für Ihre Facebook-Anwendung hinzufügen und konfigurieren.
{: shortdesc}

## Vorbereitungen
{: #before-you-begin}

Voraussetzungen:

* Eine Instanz einer {{site.data.keyword.amafull}} service and {{site.data.keyword.Bluemix_notm}}-Anwendung. Weitere Informationen zur Erstellung einer {{site.data.keyword.Bluemix_notm}}-Back-End-Anwendung finden Sie in der [Einführung](index.html).
* Die URL der Back-End-Anwendung (**App-Route**). Sie benötigen diese Werte zum Senden von Anforderungen an die geschützten Endpunkte der Back-End-Anwendung.
* Der Wert für die **Tenant-ID**. Öffnen Sie den Service im {{site.data.keyword.amashort}}-Dashboard. Klicken Sie auf die Schaltfläche **Mobile Systemerweiterungen**. Im Feld **App-GUID/TenantId** wird der Wert `tenantId` (auch als `appGUID` bezeichnet) angezeigt. Sie benötigen diesen Wert für die Initialisierung von Authorization Manager.
* Die {{site.data.keyword.Bluemix_notm}}-**Region**. Ihre aktuelle {{site.data.keyword.Bluemix_notm}}-Region finden Sie im Header neben dem Symbol **Avatar** ![Avatarsymbol](images/face.jpg "Avatarsymbol"). Der Regionswert, der angezeigt wird, sollte einer der folgenden sein: `USA (Süden)`, `Vereinigtes Königreich` oder `Sydney`. Zudem sollte er den für das Swift-SDK erforderlichen SDK-Werten entsprechen: `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` oder `BMSClient.Region.sydney`. Sie benötigen diesen Wert für die Initialisierung des {{site.data.keyword.amashort}}-Clients.
* iOS-Projekt, das für das Arbeiten mit CocoaPods eingerichtet ist.  Weitere Informationen finden Sie unter **Install CocoaPods** in [Setting up the iOS Swift SDK](getting-started-ios-swift-sdk.html).  
   **Hinweis:** Sie müssen nicht den Kern des {{site.data.keyword.amashort}}-Client-SDK installieren, bevor Sie fortfahren.
* Eine Facebook-Anwendung auf der [Facebook for Developers-Website ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developers.facebook.com "Symbol für externen Link"){: new_window}.

**Wichtig:** Sie müssen das Facebook-SDK (`com.facebook.FacebookSdk`) nicht separat installieren. Das Facebook-SDK wird automatisch mit dem Pod `BMSFacebookAuthentication` von {{site.data.keyword.amashort}} installiert. Sie können den Schritt zum Hinzufügen des Facebook-SDK zum Xcode-Projekt überspringen, wenn Sie Ihre App auf der Facebook for Developers-Website hinzufügen oder konfigurieren.

## Facebook-Anwendung für die iOS-Plattform konfigurieren
{: #facebook-auth-ios-config}

Führen Sie die folgenden Schritte auf der Site 'Facebook for Developers' aus:

1. Melden Sie sich bei Ihrem Konto in [Facebook for Developers ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developers.facebook.com "Symbol für externen Link"){: new_window} an.

1. Stellen Sie sicher, dass die iOS-Plattform zu Ihrer App hinzugefügt wurde. Wenn Sie die iOS-Plattform hinzufügen oder konfigurieren, müssen Sie die **Bundle-ID** der iOS-Anwendung angeben. Zum Ermitteln der Bundle-ID (**bundleId**) Ihrer iOS-Anwendung suchen Sie nach **Bundle Identifier** in der Datei `info.plist` oder auf der Registerkarte **General** des Projekts in Xcode.

  **Tipp**: Ziehen Sie in Betracht, das URL-Schemasuffix oder Single Sign-on zu aktivieren, wenn Sie planen, diese Features zu verwenden.

1. Klicken Sie auf **Save Settings** (Einstellungen speichern).

## {{site.data.keyword.amashort}} für die Facebook-Authentifizierung konfigurieren
{: #facebook-auth-ios-configmca}

Nachdem Sie die Facebook-App-ID und Ihre Facebook-Anwendung zur Bedienung von iOS-Clients konfiguriert haben, können Sie die Facebook-Authentifizierung im {{site.data.keyword.amashort}}-Service aktivieren.

1. Öffnen Sie den Service im {{site.data.keyword.amashort}}-Dashboard.
1. Aktivieren Sie auf der Registerkarte **Verwalten** die Option **Berechtigung**.
1. Erweitern Sie den Abschnitt **Facebook**.
1. Fügen Sie die **Facebook-Anwendungs-ID** hinzu und klicken Sie auf **Speichern**.

## {{site.data.keyword.amashort}}-Client-SDK für iOS konfigurieren
{: #facebook-auth-ios-sdk}

### CocoaPods installieren
{: #install-cocoapods}

1. Öffnen Sie das Terminal und führen Sie den Befehl **pod --version** aus. Wenn CocoaPods installiert ist, wird die Versionsnummer angezeigt. Sie können mit dem nächsten Abschnitt fortfahren, um das SDK zu installieren.

1. Wenn CocoaPods nicht installiert ist, führen Sie den folgenden Befehl aus:

   ```
   sudo gem install cocoapods
   ```
   {: codeblock}

Weitere Informationen finden Sie auf der [CocoaPods-Website ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cocoapods.org/ "Symbol für externen Link"){: new_window}.

### {{site.data.keyword.amashort}}-Client-Swift-SDK mit CocoaPods installieren
{: #facebook-auth-install-swift-cocoapods}

1. Wenn Ihr iOS-Projekt keine `Podfile` enthält, führen Sie den Befehl `pod init` aus, um die Datei zu erstellen.

1. Bearbeiten Sie die `Podfile` und fügen Sie die folgenden Zeilen hinzu:

   ```
   use_frameworks!
   pod 'BMSFacebookAuthentication'
   ```
   {: codeblock}

   **Hinweis:** Falls Ihre Pod-Datei die Zeile `pod 'BMSSecurity'` enthält, müssen Sie sie entfernen. Der Pod `BMSFacebookAuthentication` installiert alle notwendigen Frameworks.

   **Tipp:** Sie können `use_frameworks!` in Ihrem Xcode-Ziel hinzufügen anstatt in der Podfile-Datei.

1. Speichern Sie die `Podfile` und führen Sie den Befehl `pod install` über die Befehlszeile aus. CocoaPods installiert die Abhängigkeiten. Der Fortschritt und die hinzugefügten Komponenten werden angezeigt.

   **Wichtig**: Sie müssen Ihr Projekt von jetzt an über die von CocoaPods generierte Datei `xcworkspace` öffnen. In der Regel hat die Datei den Namen `{your-project-name}.xcworkspace`.  

1. Führen Sie den Befehl `open {your-project-name}.xcworkspace` über die Befehlszeile aus, um Ihren iOS-Projektarbeitsbereich zu öffnen.

### Gemeinsame Nutzung der Schlüsselkette (Keychain) für iOS aktivieren
{: #enable_keychain}

Aktivieren Sie `Keychain Sharing`. Rufen Sie dazu die Registerkarte `Capabilities` auf und setzen Sie `Keychain Sharing` in Ihrem Xcode-Projekt auf `On`.

### iOS-Projekt für die Facebook-Authentifizierung konfigurieren
{: #facebook-auth-ios-configproject}

1. Suchen Sie die Datei `info.plist`, die sich gewöhnlich unter dem Ordner `Supporting files` in Ihrem Xcode-Projekt befindet.

1. Konfigurieren Sie die Facebook-Integration, indem Sie Ihrer Datei `info.plist` die folgenden Eigenschaften hinzufügen:

   ![Bild](images/ios-facebook-infoplist-settings.png)

   Aktualisieren Sie die Eigenschaften 'URL scheme' und 'FacebookAppID' mit Ihrer Facebook-Anwendungs-ID.

   Sie können die Datei `info.plist` auch aktualisieren, indem Sie mit der rechten Maustaste auf die Datei klicken, die Optionen **Open as > Source Code** auswählen und das folgende XML hinzufügen:

   ```XML
   <key>CFBundleURLTypes</key>
   <array>
      <dict>
         <key>CFBundleURLSchemes</key>
         <array>
            <string>fb{your-facebook-application-id}</string>
         </array>
      </dict>
   </array>
   <key>FacebookAppID</key>
   <string>{your-facebook-application-id}</string>
   <key>FacebookDisplayName</key>
   <string>{your-faceebook-application-name}</string>
   <key>LSApplicationQueriesSchemes</key>
   <array>
      <string>fbauth</string>
      <string>fbauth2</string>
   </array>
   <key>NSAppTransportSecurity</key>
   <dict>
      <key>NSExceptionDomains</key>
      <dict>
         <key>facebook.com</key>
         <dict>
            <key>NSIncludesSubdomains</key>
            <true/>                
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
         </dict>
         <key>fbcdn.net</key>
         <dict>
            <key>NSIncludesSubdomains</key>
            <true/>
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
         </dict>
         <key>akamaihd.net</key>
         <dict>
            <key>NSIncludesSubdomains</key>
            <true/>
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
         </dict>
      </dict>
   </dict>
   ```
   {: codeblock}

   Aktualisieren Sie die Eigenschaften `CFBundleURLSchemes` und `FacebookappID` mit Ihrer Facebook-Anwendungs-ID. Aktualisieren Sie die Eigenschaft `FacebookDisplayName` mit dem Namen Ihrer Facebook-Anwendung.

   **Wichtig**: Stellen Sie sicher, dass Sie keine vorhandenen Eigenschaften in der Datei `info.plist` überschreiben. Wenn Sie sich überschneidende Eigenschaften haben, müssen Sie diese manuell zusammenfügen. Weitere Informationen finden Sie in [Xcode-Projekt konfigurieren ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developers.facebook.com/docs/ios/getting-started/ "Symbol für externen Link"){: new_window} und [Apps für iOS9 vorbereiten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developers.facebook.com/docs/ios/ios9 "Symbol für externen Link"){: new_window}.

## {{site.data.keyword.amashort}}-Client-Swift-SDK initialisieren
{: #facebook-auth-ios-initalize-swift}

Initialisieren Sie das Client-SDK, indem Sie den Parameter `tenantId` übergeben.

Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode `application:didFinishLaunchingWithOptions` Ihres Anwendungsdelegats.

1. Importieren Sie das erforderliche Framework in die Klasse, die das {{site.data.keyword.amashort}}-Client-SDK verwenden soll, indem Sie die folgenden Header hinzufügen:

   ```swift
 import UIKit
 import BMSCore
 import BMSSecurity
   ```
   {: codeblock}

1. Initialisieren Sie das Client-SDK.

   ```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

   func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
      let mcaAuthManager = MCAAuthorizationManager.sharedInstance
      mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
      //the regionName should be one of the following: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney
      BMSClient.sharedInstance.authorizationManager = mcaAuthManager
      FacebookAuthenticationManager.sharedInstance.register()
   }
   ```
   {: codeblock}

   Gehen Sie im Code wie folgt vor:

   * Ersetzen Sie `<applicationBluemixRegion>` durch die Region, in der Ihre {{site.data.keyword.Bluemix_notm}}-Anwendung per Hosting bereitgestellt wird.
   * Ersetzen Sie `tenantId` durch den Wert für **TenantId/App-GUID**.

   Weitere Informationen zu diesen Werten finden Sie in [Vorbereitungen](#before-you-begin).

1. Benachrichtigen Sie das Facebook-SDK über die App-Aktivierung und registrieren Sie den Facebook-Authentifizierungshandler, indem Sie den folgenden Code der Methode `application:didFinishLaunchingWithOptions` in Ihrem App-Delegat hinzufügen. Fügen Sie diesen Code nach dem Initialisieren der BMSClient-Instanz hinzu und registrieren Sie Facebook als den Authentifizierungsmanager.

   ```Swift
  return FacebookAuthenticationManager.sharedInstance.onFinishLaunching(application, withOptions: launchOptions)
   ```
   {: codeblock}

1. Kopieren Sie die Datei `FacebookAuthenticationManager.swift` aus den Quellendateien des Pods `BMSFacebookAuthentication` in Ihr Projektverzeichnis.

1. Fügen Sie Ihrem App-Delegat den folgenden Code hinzu.

   ```Swift
   func application(_ app: UIApplication,
      open url: URL,
      options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool{
         return FacebookAuthenticationManager.sharedInstance.onOpenURL(app, open: url, options: options)
      }
   ```
   {: codeblock}

## Authentifizierung testen
{: #facebook-auth-ios-testing}

Nach der Initialisierung des Client-SDK und der Registrierung des Facebook-Authentifizierungsmanagers können Sie mit dem Senden von Anforderungen an Ihre mobile Back-End-Anwendung beginnen.

### Vorbereitungen
{: #facebook-auth-ios-testing-before}

Sie müssen die {{site.data.keyword.mobilefirstbp}}-Boilerplate verwenden und bereits eine durch {{site.data.keyword.amashort}} geschützte Ressource am Endpunkt `/protected` haben. Wenn Sie einen Endpunkt `/protected` einrichten müssen, finden Sie weitere Informationen in [Ressourcen schützen](protecting-resources.html).

1. Versuchen Sie, in Ihrem Browser eine Anforderung an den geschützten Endpunkt Ihrer neu erstellten mobilen Back-End-Anwendung zu senden. Öffnen Sie die URL `{applicationRoute}/protected`, wobei Sie `{applicationRoute}` durch den Wert ersetzen, den Sie aus **Mobile Systemerweiterungen** abgerufen haben (siehe [Mobile Client Access für Facebook-Authentifizierung konfigurieren](#facebook-auth-ios-configmca)).
Beispiel: `http://my-mobile-backend.mybluemix.net/protected`
<br/>Der Endpunkt `/protected` einer mobilen Back-End-Anwendung, die mit der MobileFirst Services Starter-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Eine Nachricht `Unauthorized` (Nicht autorisiert) wird in Ihrem Browser zurückgegeben. Diese Nachricht wird deshalb zurückgegeben, weil auf diesen Endpunkt nur mobile Anwendungen zugreifen können, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind.

1. Verwenden Sie Ihre iOS-Anwendung, um eine Anforderung an denselben Endpunkt zu senden.

   ```Swift
	let protectedResourceURL = "<your protected resource absolute path>"
	let request = Request(url: protectedResourceURL, method: HttpMethod.GET)

   let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
  if error == nil {
         print ("response:\(response?.responseText), no error")
  } else {
         print ("error: \(error)")
  }
   }
	request.send(completionHandler: callBack)
   ```
   {: codeblock}

1. Führen Sie Ihre Anwendung aus. Es wird ein Facebook-Anmeldefenster angezeigt.

   ![Bild](images/ios-facebook-login.png)

   Diese Anzeige sieht möglicherweise geringfügig anders aus, wenn Sie zurzeit nicht bei Facebook angemeldet sind.

1. Klicken Sie auf **OK**, um {{site.data.keyword.amashort}} zu berechtigen, Ihre Facebook-Benutzeridentität zu Authentifizierungszwecken zu nutzen.

1. 	Wenn Ihre Anforderung erfolgreich ist, wird die folgende Ausgabe in der Xcode-Konsole angezeigt:

   ```
   response:Optional("Hello, this is a protected resouce of the mobile backend application!"), no error
   ```
   {: screen}

1. Durch Hinzufügen des folgenden Codes können Sie auch die Abmeldefunktion (logout) hinzufügen:

   ```
   FacebookAuthenticationManager.sharedInstance.logout(callBack)
   ```
   {: codeblock}

   Wenn Sie diesen Code aufrufen, nachdem sich ein Benutzer bei Facebook angemeldet hat, und der Benutzer versucht, sich wieder anzumelden, wird er dazu aufgefordert, {{site.data.keyword.amashort}} für die Verwendung von Facebook zu Authentifizierungszwecken zu berechtigen.

   Um Benutzer zu wechseln, müssen Sie diesen Code aufrufen, und der Benutzer muss sich in seinem Browser bei Facebook abmelden.

   Die Übergabe von `callBack` an die Abmeldefunktion ist optional. Sie können auch `nil` übergeben.
