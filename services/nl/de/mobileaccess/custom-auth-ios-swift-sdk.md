---

copyright:
  years: 2016

---

# {{site.data.keyword.amashort}}-Client-SDK für iOS konfigurieren (Swift-SDK)
{: #custom-ios}

Konfigurieren Sie Ihre iOS-Anwendung, die mit der angepassten Authentifizierung arbeitet, zur Verwendung des {{site.data.keyword.amashort}}-Client-SDKs und verbinden Sie Ihre Anwendung mit {{site.data.keyword.Bluemix}}.

## Vorbereitungen
{: #before-you-begin}

Sie müssen über eine Ressource verfügen, die durch eine Instanz des {{site.data.keyword.amashort}}-Service geschützt wird, die zur Verwendung eines angepassten Identitätsproviders konfiguriert ist.  Ihre mobile App muss außerdem mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sein.  Weitere Informationen finden Sie über die folgenden Links:
 * [Einführung in {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [iOS-Swift-SDK einrichten](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html)
 * [Angepassten Identitätsprovider verwenden](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Angepassten Identitätsprovider erstellen](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [{{site.data.keyword.amashort}} für die angepasste Authentifizierung konfigurieren](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## {{site.data.keyword.amashort}} für eine angepasste Authentifizierung konfigurieren
 {: #custom-auth-ios-configmca}

 1. Öffnen Sie Ihre App im {{site.data.keyword.Bluemix_notm}}-Dashboard.

 1. Klicken Sie auf **Mobile Systemerweiterungen** und notieren Sie die Werte für **Route** (*applicationRoute*) und **App-GUID** (*applicationGUID*). Sie benötigen diese Werte, wenn Sie das SDK initialisieren.

 1. Klicken Sie auf die Kachel für {{site.data.keyword.amashort}}. Das {{site.data.keyword.amashort}}-Dashboard wird geladen.

 1. Klicken Sie auf die Kachel **Angepasst**.

 1. Geben Sie in **Realmname** Ihren angepassten Authentifizierungrealm an.

 1. Geben Sie in **URL** Ihre Anwendungsroute (applicationRoute) an.

 1. Klicken Sie auf **Speichern**.

## {{site.data.keyword.amashort}}-Client-SDK für iOS konfigurieren
 {: #custom-auth-ios-sdk}

### CocoaPods installieren
 {: #custom-auth-cocoapods}

 Das {{site.data.keyword.amashort}}-Client-SDK wird mit CocoaPods, einem Abhängigkeitenmanager für iOS-Projekte, verteilt. CocoaPods lädt automatisch Artefakte aus Repositorys herunter und stellt sie für Ihre iOS-Anwendung zur Verfügung.

 1. Öffnen Sie das Terminal und führen Sie den Befehl `pod --version` aus. Wenn CocoaPods bereits installiert ist, wird die Versionsnummer angezeigt. Sie können mit dem nächsten Abschnitt dieses Lernprogramms fortfahren.

 1. Installieren Sie CocoaPods, indem Sie den Befehl `sudo gem install cocoapods` ausführen. Weitere Anweisungen finden Sie bei Bedarf auf der [CocoaPods-Website](https://cocoapods.org/).

 1. Schließen Sie XCode.

 1. Öffnen Sie das Terminal und wechseln Sie mit dem Befehl `cd` in Ihr Projektverzeichnis.

 1.  Führen Sie den Befehl `pod init` aus.

### Client-SDK mit CocoaPods installieren
{: #custom-ios-sdk-cocoapods}

Verwenden Sie den CocoaPods-Abhängigkeitenmanager, um das {{site.data.keyword.amashort}}-Client-SDK zu installieren.

1. Öffnen Sie das Terminal und navigieren Sie zum Stammverzeichnis Ihres iOS-Projekts.

1. Bearbeiten Sie die `Podfile`-Datei und fügen Sie die folgenden Zeilen hinzu.

 ```
 use_frameworks!
 pod 'BMSSecurity'
 ```
 **Tipp:** Sie können `use_frameworks!` in Ihrem Xcode-Ziel hinzufügen anstatt in der Podfile-Datei.

1. Führen Sie über die Befehlszeile den Befehl `pod install` aus.
CocoaPods installiert die hinzugefügten Abhängigkeiten. Der Fortschritt und die hinzugefügten Komponenten werden angezeigt.

 **Wichtig**: Sie müssen Ihr Projekt jetzt über eine von CocoaPods generierte xcworkspace-Datei öffnen. In der Regel hat die Datei den Namen `{your-project-name}.xcworkspace`.  

1. Führen Sie den Befehl `open {your-project-name}.xcworkspace` über die Befehlszeile aus, um Ihren iOS-Projektarbeitsbereich zu öffnen.

### Client-SDK initialisieren
{: #custom-ios-sdk-initialize}

Initialisieren Sie das SDK, indem Sie die Parameter `applicationRoute` und `applicationGUID` übergeben. Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode `application:didFinishLaunchingWithOptions` Ihres Anwendungsdelegats.

1. Ermitteln Sie Ihre Werte für die Anwendungsparameter. Öffnen Sie Ihre App im {{site.data.keyword.Bluemix_notm}}-Dashboard. Klicken Sie auf **Mobile Systemerweiterungen**. Die Werte für `applicationRoute` und `applicationGUID` werden in den Feldern **Route** und **App-GUID** angezeigt.

1. Importieren Sie die erforderlichen Frameworks in die Klasse, in der Sie das {{site.data.keyword.amashort}}-Client-SDK verwenden möchten.

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
```

1. Initialisieren Sie das {{site.data.keyword.amashort}}-Client-SDK, geben Sie 'MCAAuthorizationManager' als Berechtigungsmanager an und definieren und registrierten Sie ein Authentifizierungsdelegat. Ersetzen Sie `<applicationRoute>` und `<applicationGUID>` durch die Werte für **Route** und **App-GUID**, die Sie im Abschnitt **Mobile Systemerweiterungen** des {{site.data.keyword.Bluemix_notm}}-Dashboards ermittelt haben.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"
 let customRealm = "<Realm Ihrer geschützten Ressource>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

  //Authentifizierungsdelegat zum Verarbeiten der angepassten Anforderung
 class MyAuthDelegate : AuthenticationDelegate {
      func onAuthenticationChallengeReceived(authContext: AuthenticationContext, challenge: AnyObject){
          print("onAuthenticationChallengeReceived")
              let answer = <Eine Antwort für die vom Back-End gesendete Anforderung (sollte den Typ [String:AnyObject] aufweisen)>
              authContext.submitAuthenticationChallengeAnswer(answer)
      }

      func onAuthenticationSuccess(info: AnyObject?) {
           print("onAuthenticationSuccess info = \(info)")
           print("onAuthenticationSuccess")
      }

      func onAuthenticationFailure(info: AnyObject?){
        print("onAuthenticationFailure info = \(info)")
        print("onAuthenticationFailure")
      }
  }

  let delegate = MyAuthDelegate()
  let mcaAuthManager = MCAAuthorizationManager.sharedInstance

 do {
      try mcaAuthManager.registerAuthenticationDelegate(delegate, realm: customRealm)
  } catch {
      print("error with register: \(error)")
  }
 return true
 }   
 ```

## Authentifizierung testen
{: #custom-ios-testing}

Nachdem Sie das Client-SDK initialisiert und ein angepasstes Authentifizierungsdelegat registriert haben, können Sie mit dem Senden von Anforderungen an Ihr mobiles Back-End beginnen.

### Vorbereitungen
{: #custom-ios-testing-before}

 Sie müssen eine Anwendung, die mit der {{site.data.keyword.mobilefirstbp}}-Boilerplate erstellt wurde, sowie eine Ressource, die durch {{site.data.keyword.amashort}} geschützt wird, am Endpunkt `/protected` haben.

1. Senden Sie eine Anforderung an den geschützten Endpunkt Ihres mobilen Back-Ends in Ihrem Browser, indem Sie die Adresse `{applicationRoute}/protected` öffnen (z. B. `http://my-mobile-backend.mybluemix.net/protected`).
  Der Endpunkt `/protected` eines mobilen Back-Ends, das mit der {{site.data.keyword.mobilefirstbp}}-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Auf den Endpunkt können nur mobile Anwendungen zugreifen, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind. Daher wird eine Nachricht `Unauthorized` (Nicht autorisiert) in Ihrem Browser angezeigt.

1. Verwenden Sie Ihre iOS-Anwendung, um eine Anforderung an denselben Endpunkt zu senden. Fügen Sie den folgenden Code hinzu, nachdem Sie `BMSClient` initialisiert und Ihr angepasstes Authentifizierungsdelegat registriert haben:

 ```Swift
 let customResourceURL = "<your protected resource's path>"
 let request = Request(url: customResourceURL, method: HttpMethod.GET)
 let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) in
  if error == nil {
      print ("response:\(response?.responseText), no error")
  } else {
      print ("error: \(error)")
  }
 }

 request.sendWithCompletionHandler(callBack)
 ```

1. 	Wenn Ihre Anforderung erfolgreich ist, wird die folgende Ausgabe in der Xcode-Konsole angezeigt:

 ```
 onAuthenticationSuccess info = Optional({
     attributes =     {
     };
     deviceId = don;
     displayName = "Don+Lon";
     isUserAuthenticated = 1;
     userId = don;
 })
 response:Optional("Hello Don Lon"), no error
 ```

1. Durch Hinzufügen des folgenden Codes können Sie auch die Abmeldefunktion (logout) hinzufügen:

 ```
 MCAAuthorizationManager.sharedInstance.logout(callBack)
 ```  

 Wenn Sie diesen Code aufrufen, nachdem sich ein Benutzer angemeldet hat, wird der Benutzer abgemeldet. Wenn der Benutzer versucht, sich wieder anzumelden, muss er auf die vom Server empfangene Anforderung erneut reagieren.

 Die Übergabe von `callBack` an die Abmeldefunktion ist optional. Sie können auch `nil` übergeben.
