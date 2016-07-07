 ---

copyright:
  years: 2016

---
{:screen:  .screen}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}

# Google-Authentifizierung für iOS-Apps aktivieren (Swift-SDK)
{: #google-auth-ios}
Verwenden Sie die Google-Anmeldung, um Benutzer für Ihre {{site.data.keyword.amashort}}-iOS-Swift-App zu authentifizieren. Das neu freigegebene {{site.data.keyword.amashort}}-Swift-SDK ergänzt und verbessert die vom vorhandenen Objective-C-SDK Mobile Client Access bereitgestellte Funktionalität.

**Hinweis:** Das Objective-C-SDK wird zwar weiterhin vollständig unterstützt und gilt noch als primäres SDK für {{site.data.keyword.Bluemix_notm}} Mobile Services, seine Verwendung und Unterstützung sollen jedoch zugunsten des neuen Swift-SDK noch dieses Jahr eingestellt werden.



## Vorbereitungen
{: #google-auth-ios-before}
Voraussetzungen:

* iOS-Projekt in Xcode. Das Projekt muss nicht mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sein.  
* Instanz einer {{site.data.keyword.Bluemix_notm}}-Anwendung, die durch den {{site.data.keyword.amashort}}-Service geschützt ist. Weitere Informationen zur Erstellung eines {{site.data.keyword.Bluemix_notm}}-Back-Ends finden Sie in der [Einführung](index.html).


## App für Google-Anmeldung vorbereiten
{: #google-sign-in-ios}

Befolgen Sie die von Google unter [Google Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start-integrating) bereitgestellten Anweisungen, um Ihre App für die Google-Anmeldung vorzubereiten. 

Dieser Prozess beinhaltet Folgendes:
* Vorbereitung eines neuen Projekts auf der Google-Site für Entwickler (Google Developers), 
* Erstellung der Datei `GoogleService-Info.plist` und des Werts `REVERSE_CLIENT_ID` zum Hinzufügen zu Ihrem Xcode-Projekt und
* Erstellung der **Google-Client-ID** zum Hinzufügen zu Ihrer {{site.data.keyword.Bluemix_notm}}-Back-End-Anwendung.

Die folgenden Schritte stellen eine Kurzfassung der Aufgaben dar, die zum Vorbereiten Ihrer App notwendig sind. 

**Hinweis:** Der `Google/SignIn`-CocoaPod muss nicht hinzugefügt werden. Das notwendige SDK wird vom unten beschriebenen CocoaPod `BMSGoogleAuthentication` hinzugefügt.

1. Notieren Sie die Bundle-ID **Bundle Identifier** in Ihrem Xcode-Projekt aus dem Abschnitt **Identity** der Registerkarte **General** des Hauptziels. Sie benötigen Sie zum Erstellen Ihres Projekts zur Google-Anmeldung.

1. Erstellen Sie in Google Developer ein Projekt für die Google-Anmeldung für iOS unter https://developers.google.com/mobile/add?platform=ios. 

2. Fügen Sie den Service für die Google-Anmeldung (Google Sign-In) Ihrem Projekt hinzu.

3. Rufen Sie die Datei `GoogleService-Info.plist` ab.

  **Wichtig:** Sobald die Datei `GoogleService-Info.plist` vorliegt, öffnen Sie sie und notieren Sie den Wert für `CLIENT_ID`. Sie benötigen diesen Wert später zum Konfigurieren der {{site.data.keyword.amashort}}-Back-End-Anwendung.

1. Fügen Sie die Datei `GoogleService-Info.plist` zu Ihrem Xcode-Projekt hinzu. Weitere Informationen finden Sie im Abschnitt [Add the configuration file to your project](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config).

1. Aktualisieren Sie die URL-Schemas in Ihrem Xcode-Projekt mit Ihrer `REVERSE_CLIENT_ID` und mit der Bundle-ID. Weitere Informationen finden Sie in [Add URL schemes to your project](https://developers.google.com/identity/sign-in/ios/start-integrating#add_a_url_scheme_to_your_project).


1. Aktualisieren Sie die Datei 'project-Bridging-Header.h' für Ihre App mit dem folgenden Code:

 ```
 #import <Google/SignIn.h>
 ```

 Weitere Informationen zum Aktualisieren der Überbrückungsheaderdatei enthält der Schritt 1 in [Enable sign-in](https://developers.google.com/identity/sign-in/ios/sign-in#enable_sign-in).

## {{site.data.keyword.amashort}} für die Google-Authentifizierung konfigurieren
{: #google-auth-ios-config}

Jetzt, da Sie eine iOS-Client-ID haben, können Sie die Google-Authentifizierung im {{site.data.keyword.Bluemix}}-Dashboard aktivieren.

1. Öffnen Sie Ihre App im {{site.data.keyword.Bluemix_notm}}-Dashboard.

1. Klicken Sie auf **Mobile Systemerweiterungen** und notieren Sie die Werte für **Route** (*applicationRoute*) und **App GUID** (*applicationGUID*). Sie benötigen diese Werte, wenn Sie das SDK initialisieren.

1. Klicken Sie auf die Kachel für {{site.data.keyword.amashort}}. Das {{site.data.keyword.amashort}}-Dashboard wird geladen.

1. Klicken Sie auf die Kachel für **Google**.

1. Geben Sie in **Application ID for iOS** (Anwendungs-ID für iOS) den Wert für `CLIENT_ID` aus der Datei `GoogleService-Info.plist` an, den Sie zuvor notiert hatten, und klicken Sie auf **Speichern**.

## {{site.data.keyword.amashort}}-Client-SDK für iOS konfigurieren
{: #google-auth-ios-sdk}

### CocoaPods installieren
{: #install-cocoapods}

1. Öffnen Sie das Terminal und führen Sie den Befehl **pod --version** aus. Wenn CocoaPods bereits installiert ist, wird die Versionsnummer angezeigt. Sie können mit dem nächsten Abschnitt fortfahren, um das SDK zu installieren.

1. Wenn CocoaPods nicht installiert ist, führen Sie den folgenden Befehl aus:
```
sudo gem install cocoapods
```
Weitere Informationen finden Sie auf der [CocoaPods-Website](https://cocoapods.org/).

### {{site.data.keyword.amashort}}-Client-Swift-SDK mit CocoaPods installieren
{: #facebook-auth-install-swift-cocoapods}

1. Wenn Ihr iOS-Projekt keine `Podfile` enthält, führen Sie den Befehl `pod init` aus, um die Datei zu erstellen.

1. Bearbeiten Sie die `Podfile` und fügen Sie die folgenden Zeilen zum relevanten Ziel hinzu:

 ```
 use_frameworks!
 pod 'BMSGoogleAuthentication'
 ```
 
 **Hinweis:** Falls Sie das {{site.data.keyword.amashort}}-Kern-SDK bereits installiert haben, können Sie die folgende Zeile entfernen: `pod 'BMSSecurity'`. Der Pod `BMSGoogleAuthentication` installiert alle erforderlichen Frameworks.
	
 **Tipp:** Sie können `use_frameworks!` in Ihrem Xcode-Ziel hinzufügen anstatt in der Podfile-Datei.

1. Speichern Sie die `Podfile`-Datei und führen Sie den Befehl `pod install` über die Befehlszeile aus. CocoaPods installiert die Abhängigkeiten. Der Fortschritt und die hinzugefügten Komponenten werden angezeigt.

 **Wichtig**: Sie müssen Ihr Projekt von jetzt an über die von CocoaPods generierte Datei `xcworkspace` öffnen. In der Regel hat die Datei den Namen `{your-project-name}.xcworkspace`.  

1. Führen Sie den Befehl `open {your-project-name}.xcworkspace` über die Befehlszeile aus, um Ihren iOS-Projektarbeitsbereich zu öffnen.

1. Kopieren Sie die Datei `GoogleAuthenticationManager.swift` aus den `BMSGoogleAuthentication`-Pod-Quellendateien in Ihr Projektverzeichnis.

## {{site.data.keyword.amashort}}-Client-Swift-SDK initialisieren
{: #google-auth-ios-initialize}

Zur Verwendung des {{site.data.keyword.amashort}}-Client-SDK müssen Sie das SDK initialisieren, indem Sie die Parameter `applicationGUID` und `applicationRoute` übergeben.

Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode `application:didFinishLaunchingWithOptions` Ihres Anwendungsdelegats.

1. Ermitteln Sie Ihre Werte für die Anwendungsparameter. Öffnen Sie Ihre App im {{site.data.keyword.Bluemix_notm}}-Dashboard. Klicken Sie auf **Mobile Systemerweiterungen**. Die Werte für `applicationRoute` und `applicationGUID` werden in den Feldern **Route** und **App-GUID** angezeigt.

1. Importieren Sie die erforderlichen Frameworks in die Klasse, in der Sie das {{site.data.keyword.amashort}}-Client-SDK verwenden möchten. Fügen Sie die folgenden Header hinzu:

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```

1. Verwenden Sie den folgenden Code, um das Client-SDK zu initialisieren. Ersetzen Sie `<applicationRoute>` und `<applicationGUID>` durch die Werte für **Route** und **App-GUID**, die Sie im Abschnitt **Mobile Systemerweiterungen** des {{site.data.keyword.Bluemix_notm}}-Dashboards ermittelt haben. Ersetzen Sie `<applicationBluemixRegion>` durch die Region, in der Ihre {{site.data.keyword.Bluemix_notm}}-Anwendung per Hosting bereitgestellt wird. Klicken Sie zur Anzeige der {{site.data.keyword.Bluemix_notm}}-Region auf das Symbol mit dem Gesicht (![Gesicht](/face.png "Gesicht")) in der linken oberen Ecke des Dashboards.
 

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 // Client-SDK initialisieren.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUId, bluemixRegion: BMSClient.<applicationBluemixRegion>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 GoogleAuthenticationManager.sharedInstance.register()
      return true
 }

 // [START openurl]
      func application(application: UIApplication,
          openURL url: NSURL, sourceApplication: String?, annotation: AnyObject) -> Bool {
             return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, sourceApplication: sourceApplication, annotation: annotation)
      }

 @available(iOS 9.0, *)
 func application(app: UIApplication, openURL url: NSURL, options: [String : AnyObject]) -> Bool {
 return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, options: options)
  }
 ```

## Authentifizierung testen
{: #google-auth-ios-testing}

Nach der Initialisierung des Client-SDK und der Registrierung des Google-Authentifizierungsmanagers können Sie mit dem Senden von Anforderungen an Ihr mobiles Back-End beginnen.

### Vorbereitungen
{: #google-auth-ios-testing-before}

Sie müssen die {{site.data.keyword.mobilefirstbp}}-Boilerplate verwenden und bereits eine durch {{site.data.keyword.amashort}} geschützte Ressource am Endpunkt `/protected` haben. Wenn Sie einen Endpunkt `/protected` einrichten müssen, finden Sie weitere Informationen in [Ressourcen schützen](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Versuchen Sie, in Ihrem Desktop-Browser eine Anforderung an den geschützten Endpunkt Ihres mobilen Back-Ends zu senden, indem Sie `{applicationRoute}/protected` öffnen (z. B. `http://my-mobile-backend.mybluemix.net/protected`).

1. Der Endpunkt `/protected` eines mobilen Back-Ends, das mit der MobileFirst Services-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Deshalb kann auf ihn nur mit mobilen Anwendungen zugegriffen werden, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert wurden. Infolgedessen wird eine Nachricht `Unauthorized` (Nicht autorisiert) in Ihrem Desktop-Browser angezeigt.

1. Verwenden Sie Ihre iOS-Anwendung, um eine Anforderung an denselben Endpunkt zu senden.

 ```Swift
 let protectedResourceURL = "<Your protected resource URL>" // any protected resource
 let request = Request(url: protectedResourceURL , method: HttpMethod.GET)
 let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) in
 if error == nil {
    print ("response:\(response?.responseText), no error")
 } else {
    print ("error: \(error)")
 }
 }

 request.sendWithCompletionHandler(callBack)
	```

1. Führen Sie Ihre Anwendung aus. Ein Popup-Fenster für die Google-Anmeldung wird angezeigt.

 ![Bild](images/ios-google-login.png)

1. Wenn Sie sich anmelden und auf **OK** klicken, berechtigen Sie {{site.data.keyword.amashort}}, Ihre Google-Benutzeridentität zu Authentifizierungszwecken zu nutzen.

1. 	Ihre Anforderung sollte erfolgreich ausgeführt werden. Die folgende Ausgabe sollte im Protokoll angezeigt werden.

 ```
 onAuthenticationSuccess info = Optional({attributes = {};
     deviceId = 105747725068605084657;
     displayName = "donlonqwerty@gmail.com";
     isUserAuthenticated = 1;
     userId = 105747725068605084657;
 })
 response:Optional("Hello, this is a protected resource!"), no error
 ```
{: screen}

1. Durch Hinzufügen des folgenden Codes können Sie auch die Abmeldefunktion (logout) hinzufügen:

 ```
 GoogleAuthenticationManager.sharedInstance.logout(callBack)
 ```

  Wenn Sie diesen Code aufrufen, nachdem sich ein Benutzer bei Google angemeldet hat, und der Benutzer versucht, sich wieder anzumelden, muss er sich bei {{site.data.keyword.amashort}} für die Verwendung von Google zu Authentifizierungszwecken berechtigen. An dieser Stelle kann der Benutzer in der rechten oberen Ecke der Anzeige auf den Benutzernamen klicken, um einen anderen Benutzer auszuwählen und sich mit diesem anzumelden.

   Die Übergabe von `callBack` an die Abmeldefunktion ist optional. Sie können auch `nil` übergeben.
