---

copyright:
  years: 2016

---

# iOS-Swift-SDK einrichten
{: #getting-started-ios}

Instrumentieren Sie Ihre iOS-Anwendung mit dem {{site.data.keyword.amashort}}-SDK, initialisieren Sie das SDK und senden Sie Anforderungen an geschützte und nicht geschützte Ressourcen.

## Vorbereitungen
{: #before-you-begin}
* Sie müssen über eine Instanz eines mobilen Back-Ends verfügen, die durch den {{site.data.keyword.amashort}}-Service geschützt wird. Weitere Informationen zur Erstellung eines mobilen Back-Ends finden Sie in der [Einführung](getting-started.html).
* Stellen Sie sicher, dass Sie Xcode ordnungsgemäß eingerichtet haben. Weitere Informationen zur Einrichtung Ihrer iOS-Entwicklungsumgebung finden Sie auf der [Apple Developer-Website](https://developer.apple.com/support/xcode/).


## {{site.data.keyword.amashort}}-Client-SDK installieren
{: #install-mca-sdk-ios}
Das {{site.data.keyword.amashort}}-SDK wird mit CocoaPods, einem Abhängigkeitenmanager für iOS-Projekte, verteilt. CocoaPods lädt automatisch Artefakte aus Repositorys herunter und stellt sie für Ihre iOS-Anwendung zur Verfügung.


### CocoaPods installieren
{: #install-cocoapods}
1. Öffnen Sie das Terminal und führen Sie den Befehl **pod --version** aus. Wenn CocoaPods bereits installiert ist, wird die Versionsnummer angezeigt. Sie können mit dem nächsten Abschnitt fortfahren, um das SDK zu installieren.

1. Wenn CocoaPods nicht installiert ist, führen Sie den folgenden Befehl aus:
```
sudo gem install cocoapods
```
Weitere Informationen finden Sie auf der [CocoaPods-Website](https://cocoapods.org/).

### {{site.data.keyword.amashort}}-Client-SDK mit CocoaPods installieren
{: #install-sdk-cocoapods}

1. Navigieren Sie im Terminal zum Stammverzeichnis Ihres iOS-Projekts.

1. Wenn Sie Ihren Arbeitsbereich für CocoaPods noch nicht initialisiert haben, führen Sie den Befehl `pod init` aus.<br/>
 CocoaPods erstellt eine `Podfile`-Datei für Sie, in der Sie die Abhängigkeiten für Ihr iOS-Projekt definieren.

1. Bearbeiten Sie die `Podfile`-Datei und fügen Sie den erforderlichen Zielen die folgende Zeile hinzu:

	```
  use_frameworks!
	pod 'BMSSecurity'
	```
  **Tipp:** Sie können `use_frameworks!` in Ihrem Xcode-Ziel hinzufügen anstatt in der Podfile-Datei.

1. Speichern Sie die `Podfile`-Datei und führen Sie den Befehl `pod install` über die Befehlszeile aus. <br/>Cocoapods installiert die hinzugefügten Abhängigkeiten. Der Fortschritt und die hinzugefügten Komponenten werden angezeigt.<br/>
**Wichtig**: CocoaPods generiert eine `xcworkspace`-Datei.  Sie müssen diese Datei öffnen, um mit Ihrem Projekt in Zukunft arbeiten zu können.

1. Öffnen Sie Ihren iOS-Projektarbeitsbereich. Öffnen Sie die `xcworkspace`-Datei, die von CocoaPods generiert wurde. Beispiel: `{your-project-name}.xcworkspace`. Führen Sie den Befehl `open {your-project-name}.xcworkspace` aus.

## {{site.data.keyword.amashort}}-Client-SDK initialisieren
{: #init-mca-sdk-ios}

 Initialisieren Sie das SDK, indem Sie die Parameter `applicationRoute` und `applicationGUID` übergeben. Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode `application:didFinishLaunchingWithOptions` Ihres Anwendungsdelegats.

1. Ermitteln Sie Ihre Werte für die Anwendungsparameter. Öffnen Sie Ihre App im {{site.data.keyword.Bluemix_notm}}-Dashboard. Klicken Sie auf **Mobile Systemerweiterungen**. Die Werte für `applicationRoute` und `applicationGUID` werden in den Feldern **Route** und **App-GUID** angezeigt.

1. Importieren Sie die erforderlichen Frameworks in die Klasse, in der Sie das {{site.data.keyword.amashort}} Client-SDK verwenden möchten.

 ```Swift
 import BMSCore
 import BMSSecurity
 ```  

1. Initialisieren Sie das {{site.data.keyword.amashort}}-Client-SDK. Ersetzen Sie `<applicationRoute>` und `<applicationGUID>` durch die Werte für **Route** und **App-GUID**, die Sie im Abschnitt **Mobile Systemerweiterungen** des {{site.data.keyword.Bluemix_notm}}-Dashboards ermittelt haben.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 // Initialize the Client SDK.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 return true
 }
 ```

## Anforderung an das mobile Back-End senden
{: #request}

Nach der Initialisierung des {{site.data.keyword.amashort}}-Client-SDK können Sie mit dem Senden von Anforderungen an Ihr mobiles Back-End beginnen.

1. Versuchen Sie, in Ihrem Browser eine Anforderung an den Endpunkt '/protected' in Ihrem mobilen Back-End zu senden. Öffnen Sie die folgende URL: `{applicationRoute}/protected`. Beispiel: `http://my-mobile-backend.mybluemix.net/protected`
<br/>Der Endpunkt `/protected` eines mobilen Back-Ends, der mit der MobileFirst Services Starter-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Eine Nachricht `Unauthorized` (Nicht autorisiert) wird in Ihrem Browser zurückgegeben, weil auf diesen Endpunkt nur mobile Anwendungen zugreifen können, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind.

1. Verwenden Sie Ihre iOS-Anwendung, um eine Anforderung an denselben Endpunkt zu senden. Fügen Sie den folgenden Code hinzu, nachdem Sie `BMSClient` initialisiert haben:

 ```Swift
 let customResourceURL = "<your protected resource's path>"
 let request = Request(url: customResourceURL, method: HttpMethod.GET)
 let callBack:MfpCompletionHandler = {(response: Response?, error: NSError?) in
     if error == nil {
         print ("response:\(response?.responseText), no error")
     } else {
         print ("error: \(error)")
     }
 }

 request.sendWithCompletionHandler(callBack)
 ```

1.  Wenn Ihre Anforderung erfolgreich ist, wird die folgende Ausgabe in der Xcode-Konsole angezeigt:

 ```
 response:Optional("Hello, this is a protected resouce of the mobile backend application!"), no error
 ```

## Nächste Schritte
{: #next-steps}
Wenn Sie eine Verbindung zu dem geschützten Endpunkt hergestellt haben, waren keine Berechtigungsnachweise erforderlich. Wenn Sie die Benutzer zur Anmeldung bei Ihrer Anwendung veranlassen wollen, müssen Sie eine Authentifizierung über Facebook oder Google oder eine angepasste Authentifizierung konfigurieren.
  * [Facebook](facebook-auth-ios-swift-sdk.html)
  * [Google](google-auth-ios-swift-sdk.html)
  * [Angepasst](custom-auth-ios-swift-sdk.html)
