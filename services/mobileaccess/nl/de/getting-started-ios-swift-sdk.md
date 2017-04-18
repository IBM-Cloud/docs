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


# iOS-Swift-SDK einrichten
{: #getting-started-ios}

Instrumentieren Sie Ihre iOS-Swift-Anwendung mit dem {{site.data.keyword.amashort}}-SDK, initialisieren Sie das SDK und senden Sie Anforderungen an geschützte und ungeschützte Ressourcen.

{:shortdesc}


## Vorbereitungen
{: #before-you-begin}
Voraussetzungen:

* Eine Instanz einer {{site.data.keyword.Bluemix_notm}}-Anwendung.
* Eine Instanz eines {{site.data.keyword.amafull}}-Service.
* Die **Tenant-ID**. Öffnen Sie den Service im {{site.data.keyword.amashort}}-Dashboard. Klicken Sie auf **Mobile Systemerweiterungen**. Im Feld **App-GUID/TenantId** wird der Wert `tenantId` (auch als `appGUID` bezeichnet) angezeigt. Sie benötigen diesen Wert für die Initialisierung von {{site.data.keyword.amashort}} Authorization Manager.
* Die **Anwendungsroute**. Dies ist die URL Ihrer Back-End-Anwendung. Sie benötigen diesen Wert zum Senden von Anforderungen an die geschützten Endpunkte der Anwendung.
* Die {{site.data.keyword.Bluemix_notm}}-**Region**.  Ihre aktuelle {{site.data.keyword.Bluemix_notm}}-Region finden Sie im Header neben dem Symbol **Avatar** ![Avatarsymbol](images/face.jpg "Avatarsymbol"). Der Regionswert, der angezeigt wird, sollte einer der folgenden sein: `USA (Süden)`, `Vereinigtes Königreich` oder `Sydney`. Außerdem sollte er den im Code erforderlichen SDK-Werten entsprechen: `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` oder `BMSClient.Region.sydney`.  Sie benötigen diesen Wert für die Initialisierung des {{site.data.keyword.amashort}}-SDK.
* Xcode-Projekt. Weitere Informationen zum Einrichten Ihrer iOS-Entwicklungsumgebung finden Sie auf der [Apple Developer-Website ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.apple.com/support/xcode/ "Symbol für externen Link"){: new_window}.


## {{site.data.keyword.amashort}}-Client-SDK installieren
{: #install-mca-sdk-ios}
Das {{site.data.keyword.amashort}}-SDK wird mit CocoaPods, einem Abhängigkeitenmanager für iOS-Projekte, verteilt. CocoaPods lädt automatisch Artefakte aus Repositorys herunter und stellt sie für Ihre iOS-Anwendung zur Verfügung.


### CocoaPods installieren
{: #install-cocoapods}

1. Führen Sie den Befehl **pod --version** in einem Terminalfenster aus. Wenn CocoaPods bereits installiert ist, wird die Versionsnummer angezeigt und Sie können mit dem nächsten Abschnitt fortfahren, um das SDK zu installieren.

1. Wenn CocoaPods nicht installiert ist, führen Sie den folgenden Befehl aus:

```
sudo gem install cocoapods
```
{: codeblock}

Weitere Informationen finden Sie auf der [CocoaPods-Website ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cocoapods.org/ "Symbol für externen Link"){: new_window}.

### {{site.data.keyword.amashort}}-Client-SDK mit CocoaPods installieren
{: #install-sdk-cocoapods}

1. Navigieren Sie in einem Terminalfenster zum Stammverzeichnis Ihres iOS-Projekts.

1. Wenn Sie Ihren Arbeitsbereich für CocoaPods noch nicht initialisiert haben, führen Sie den Befehl `pod init` aus.<br/>
 CocoaPods erstellt eine `Podfile`-Datei für Sie, in der Sie die Abhängigkeiten für Ihr iOS-Projekt definieren.

1. Bearbeiten Sie die `Podfile`-Datei und fügen Sie den erforderlichen Zielen die folgende Zeile hinzu:

	```
  use_frameworks!
  pod 'BMSSecurity'
	```
	{: codeblock}

  **Tipp:** Sie können `use_frameworks!` in Ihrem Xcode-Ziel hinzufügen anstatt in der Podfile-Datei.

1. Speichern Sie die `Podfile`-Datei und führen Sie den Befehl `pod install` über die Befehlszeile aus. Cocoapods installiert die relevanten Abhängigkeiten und zeigt die hinzugefügten Abhängigkeiten und Pods an.<br/>

   **Wichtig**: CocoaPods generiert eine Datei `xcworkspace`.  Sie müssen diese Datei öffnen, um mit Ihrem Projekt in Zukunft arbeiten zu können.

1. Öffnen Sie Ihren iOS-Projektarbeitsbereich. Öffnen Sie die `xcworkspace`-Datei, die von CocoaPods generiert wurde. Führen Sie zum Beispiel für `{your-project-name}.xcworkspace` Folgendes aus:

	`open {your-project-name}.xcworkspace`

### Gemeinsame Nutzung der Schlüsselkette (Keychain) für iOS aktivieren
{: #enable_keychain}

Aktivieren Sie `Keychain Sharing`. Rufen Sie dazu die Registerkarte `Capabilities` auf und setzen Sie `Keychain Sharing` in Ihrem Xcode-Projekt auf `On`.

## {{site.data.keyword.amashort}}-Client-SDK initialisieren
{: #init-mca-sdk-ios}

 Initialisieren Sie das SDK, indem Sie den Parameter `tenantId` übergeben. Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode `application:didFinishLaunchingWithOptions` Ihres Anwendungsdelegats.

1. Importieren Sie die erforderlichen Frameworks in die Klasse, in der Sie das {{site.data.keyword.amashort}}-Client-SDK verwenden möchten.

 ```Swift
 import BMSCore
 import BMSSecurity
 ```

1. Initialisieren Sie das {{site.data.keyword.amashort}}-Client-SDK.

 ```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

	func application(_ application: UIApplication, 
	    didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {

	let mcaAuthManager = MCAAuthorizationManager.sharedInstance
    mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
      // Mögliche Werte für Regionsnamen: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, BMSClient.Region.sydney
	BMSClient.sharedInstance.authorizationManager = mcaAuthManager	
	return true
	}
  ```
  {: codeblock}

* Ersetzen Sie `tenantId` durch den Wert, den Sie aus **Mobile Systemerweiterungen** abgerufen haben.
* Ersetzen Sie `<applicationBluemixRegion>` durch die Region, in der Ihre {{site.data.keyword.Bluemix_notm}}-Anwendung per Hosting bereitgestellt wird.

Weitere Informationen zu diesen Werten finden Sie unter [Vorbereitungen](#before-you-begin).


## Anforderung an mobile Back-End-Anwendung senden
{: #request}

Nach der Initialisierung des {{site.data.keyword.amashort}}-Client-SDK können Sie mit dem Senden von Anforderungen an Ihre mobile Back-End-Anwendung beginnen.

1. Versuchen Sie, in Ihrem Browser eine Anforderung an einen geschützten Endpunkt in Ihrer mobilen Back-End-Anwendung zu senden. Öffnen Sie die URL `{applicationRoute}/protected`, wobei Sie `{applicationRoute}` durch den Wert **applicationRoute** ersetzen, den Sie aus **Mobile Systemerweiterungen** abgerufen haben (siehe [Client-SDK für Mobile Client Access initialisieren](#init-mca-sdk-ios)). Beispiel:

	`http://my-mobile-backend.mybluemix.net/protected
	`

	Eine Nachricht des Typs `Unauthorized` (Nicht autorisiert) wird in Ihrem Browser zurückgegeben, weil auf diesen Endpunkt nur mobile Anwendungen zugreifen können, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind.

1. Verwenden Sie Ihre iOS-Anwendung, um eine Anforderung an denselben Endpunkt zu senden. Fügen Sie den folgenden Code hinzu, nachdem Sie `BMSClient` initialisiert haben:

 ```Swift
	let customResourceURL = "<your protected resource absolute path>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

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

1.  Wenn Ihre Anforderung erfolgreich ist, wird die folgende Ausgabe in der Xcode-Konsole angezeigt:

 ```
 response:Optional("Hello, this is a protected resource of the mobile backend application!"), no error
 ```
{: screen}

## Nächste Schritte
{: #next-steps}
Wenn Sie eine Verbindung zu dem geschützten Endpunkt hergestellt haben, waren keine Berechtigungsnachweise erforderlich. Wenn Sie die Benutzer zur Anmeldung bei Ihrer Anwendung veranlassen wollen, müssen Sie eine Authentifizierung über Facebook oder Google oder eine angepasste Authentifizierung konfigurieren.

  * [Facebook](facebook-auth-ios-swift-sdk.html)
  * [Google](google-auth-ios-swift-sdk.html)
  * [Angepasst](custom-auth-ios-swift-sdk.html)
