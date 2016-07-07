---

copyright:
  years: 2016

---

# {{site.data.keyword.amashort}}-Client-SDK für iOS konfigurieren (Swift-SDK)
{: #custom-ios}

Konfigurieren Sie Ihre iOS-Anwendung, die mit der angepassten Authentifizierung arbeitet, zur Verwendung des {{site.data.keyword.amashort}}-Client-SDK und verbinden Sie Ihre Anwendung mit {{site.data.keyword.Bluemix}}. Das neu freigegebene {{site.data.keyword.amashort}}-Swift-SDK ergänzt und verbessert die vom vorhandenen Mobile Client Access-Objective-C-SDK bereitgestellte Funktionalität.

**Hinweis:** Das Objective-C-SDK wird zwar weiterhin vollständig unterstützt und gilt noch als primäres SDK für {{site.data.keyword.Bluemix_notm}} Mobile Services, seine Verwendung und Unterstützung sollen jedoch zugunsten des neuen Swift-SDK noch dieses Jahr eingestellt werden.

## Vorbereitungen
{: #before-you-begin}

Sie müssen über eine Ressource verfügen, die durch eine Instanz des {{site.data.keyword.amashort}}-Service geschützt wird, die zur Verwendung eines angepassten Identitätsproviders konfiguriert ist.  Ihre mobile App muss außerdem mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sein.  Weitere Informationen finden Sie über die folgenden Links:
 * [Einführung in {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/index.html)
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

1. Initialisieren Sie das {{site.data.keyword.amashort}}-Client-SDK, geben Sie 'MCAAuthorizationManager' als Berechtigungsmanager an und definieren und registrieren Sie ein Authentifizierungsdelegat. Ersetzen Sie `<applicationRoute>` und `<applicationGUID>` durch die Werte für **Route** und **App-GUID**, die Sie im Abschnitt **Mobile Systemerweiterungen** des {{site.data.keyword.Bluemix_notm}}-Dashboards ermittelt haben. 

  Ersetzen Sie `<applicationBluemixRegion>` durch die Region, in der Ihre {{site.data.keyword.Bluemix_notm}}-Anwendung per Hosting bereitgestellt wird. Klicken Sie zur Anzeige der {{site.data.keyword.Bluemix_notm}}-Region auf das Symbol mit dem Gesicht (![Gesicht](/face.png "Gesicht")) in der linken oberen Ecke des Dashboards.

  Verwenden Sie als `<yourProtectedRealm>` den **Realmnamen**, den Sie in der Kachel **Angepasst** des {{site.data.keyword.amashort}}-Dashboards definiert haben.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"
 let customRealm = "<yourProtectedRealm>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<applicationBluemixRegion>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

  //Authentifizierungsdelegat zum Verarbeiten der angepassten Anforderung
 class MyAuthDelegate : AuthenticationDelegate {
      func onAuthenticationChallengeReceived(authContext: AuthenticationContext, challenge: AnyObject){
          print("onAuthenticationChallengeReceived")
              let answer = <Eine Antwort auf die vom Backend gesendete Anforderung (sollte den Typ [String:AnyObject] aufweisen)>
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
