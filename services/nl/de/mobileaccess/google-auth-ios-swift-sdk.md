---

copyright:
  years: 2016

---

# Google-Authentifizierung in iOS-Apps aktivieren (Swift-SDK)
{: #google-auth-ios}

## Vorbereitungen
{: #google-auth-ios-before}

* Sie müssen über eine durch {{site.data.keyword.amashort}} geschützte Ressource verfügen und ein iOS-Projekt haben, das mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert ist.  Weitere Informationen finden Sie in [Einführung in {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) und [iOS-Swift-SDK einrichten](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html).  
* Schützen Sie Ihre Back-End-Anwendung manuell mit dem {{site.data.keyword.amashort}}-Server-SDK. Weitere Informationen finden Sie in [Ressourcen schützen](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

## Apps für Google-Anmeldung vorbereiten
{: #google-sign-in-ios}

Befolgen Sie die von Google in [Goolge Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start-integrating) bereitgestellten Anweisungen, um Ihre App für die Google-Anmeldung vorzubereiten. Die folgenden Schritte enthalten eine Kurzfassung der erforderlichen Tasks zum Vorbereiten Ihrer App.

1. Aktivieren Sie Google Sign-In for iOS für Ihre App. Weitere Informationen finden Sie in [Try Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start?ver=swift).

1. Rufen Sie eine Konfigurationsdatei (`GoogleService-Info.plist`) für Ihr Projekt ab. Informationen zum Abrufen der Datei finden Sie in [Enable Google services for your app](https://developers.google.com/mobile/add?platform=ios).

 **Wichtig:** Sobald die Datei `GoogleService-Info.plist` vorliegt, öffnen Sie sie und notieren Sie den Wert für `CLIENT_ID`. Sie benötigen diesen Wert später zum Konfigurieren von {{site.data.keyword.amashort}}.

1. Fügen Sie die Datei `GoogleService-Info.plist` zu Ihrem Xcode-Projekt hinzu. Weitere Informationen finden Sie in [Add the configuration file to your project](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config).

1. Aktualisieren Sie die URL-Schemas in Ihrem Xcode-Projekt mit Ihrer `REVERSE_CLIENT_ID` und mit der Bundle-ID. Weitere Informationen finden Sie in [Add URL schemes to your project](https://developers.google.com/identity/sign-in/ios/start-integrating#add_url_schemes_to_your_project).

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
{: #google-auth-cocoapods}

Das {{site.data.keyword.amashort}}-Client-SDK wird mit CocoaPods, einem Abhängigkeitenmanager für iOS-Projekte, verteilt. CocoaPods lädt automatisch Artefakte aus Repositorys herunter und stellt sie für Ihre iOS-Anwendung zur Verfügung.

1. Öffnen Sie das Terminal und führen Sie den Befehl `pod --version` aus. Wenn CocoaPods bereits installiert ist, wird die Versionsnummer angezeigt. Sie können mit dem nächsten Abschnitt dieses Lernprogramms fortfahren.

1. Installieren Sie CocoaPods, indem Sie den Befehl `sudo gem install cocoapods` ausführen. Weitere Anweisungen finden Sie bei Bedarf auf der [CocoaPods-Website](https://cocoapods.org/).

1. Schließen Sie XCode.

1. Öffnen Sie das Terminal und wechseln Sie mit dem Befehl `cd` in Ihr Projektverzeichnis.

1.  Führen Sie den Befehl `pod init` aus.

### {{site.data.keyword.amashort}}-Client-Swift-SDK mit CocoaPods installieren
{: #google-auth-ios-sdk-cocoapods}

1. Navigieren Sie zu Ihrem iOS-Projekt.

1. Bearbeiten Sie die `Podfile`-Datei und fügen Sie die folgenden Zeilen hinzu:

 ```
 use_frameworks!
 pod 'BMSGoogleAuthentication'
 ```
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

1. Verwenden Sie den folgenden Code, um das SDK zu initialisieren. Ersetzen Sie `<applicationRoute>` und `<applicationGUID>` durch die Werte für **Route** und **App-GUID**, die Sie im Abschnitt **Mobile Systemerweiterungen** des {{site.data.keyword.Bluemix_notm}}-Dashboards ermittelt haben.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 // Initialize the Client SDK.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUId, bluemixRegion: BMSClient.<application Bluemix region>)

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

1. Der Endpunkt `/protected` eines mobilen Back-Ends, das mit der MobileFirst Services-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Deshalb auf ihn nur mit mobilen Anwendungen zugegriffen werden, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert wurden. Infolgedessen wird eine Nachricht `Unauthorized` (Nicht autorisiert) in Ihrem Desktop-Browser angezeigt.

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

1. Durch Hinzufügen des folgenden Codes können Sie auch die Abmeldefunktion (logout) hinzufügen:

 ```
 GoogleAuthenticationManager.sharedInstance.logout(callBack)
 ```

  Wenn Sie diesen Code aufrufen, nachdem sich ein Benutzer bei Google angemeldet hat, und der Benutzer versucht, sich wieder anzumelden, muss er sich bei {{site.data.keyword.amashort}} für die Verwendung von Google zu Authentifizierungszwecken berechtigen. An dieser Stelle kann der Benutzer in der rechten oberen Ecke der Anzeige auf den Benutzernamen klicken, um einen anderen Benutzer auszuwählen und sich mit diesem anzumelden.

   Die Übergabe von `callBack` an die Abmeldefunktion ist optional. Sie können auch `nil` übergeben.
