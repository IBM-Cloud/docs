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

# Google-Authentifizierung für iOS-Apps aktivieren (Swift-SDK)
{: #google-auth-ios}

Verwenden Sie die Google-Anmeldung, um Benutzer für Ihre {{site.data.keyword.amafull}}-iOS-Swift-App zu authentifizieren.


## Vorbereitungen
{: #before-you-begin}

Voraussetzungen:

* Eine Instanz einer {{site.data.keyword.amafull}} service and {{site.data.keyword.Bluemix_notm}}-Anwendung. Weitere Informationen zur Erstellung einer {{site.data.keyword.Bluemix_notm}}-Back-End-Anwendung finden Sie in der [Einführung](index.html).
* Die URL der Back-End-Anwendung (**App-Route**). Sie benötigen diese Werte zum Senden von Anforderungen an die geschützten Endpunkte der Back-End-Anwendung.
* Der Wert für die **Tenant-ID**. Öffnen Sie den Service im {{site.data.keyword.amashort}}-Dashboard. Klicken Sie auf die Schaltfläche **Mobile Systemerweiterungen**. Im Feld **App-GUID/TenantId** wird der Wert `tenantId` (auch als `appGUID` bezeichnet) angezeigt. Sie benötigen diesen Wert für die Initialisierung von Authorization Manager.
* Die {{site.data.keyword.Bluemix_notm}}-**Region**. Ihre aktuelle {{site.data.keyword.Bluemix_notm}}-Region finden Sie im Header neben dem Symbol **Avatar** ![Avatarsymbol](images/face.jpg "Avatarsymbol"). Der Regionswert, der angezeigt wird, sollte einer der folgenden sein: **USA (Süden)**, **Vereinigtes Königreich** oder **Sydney**. Außerdem sollte er den im Code erforderlichen Werten entsprechen: `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` oder `BMSClient.Region.sydney`.
* iOS-Projekt in Xcode. Das Projekt muss nicht mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sein.  


## App für Google-Anmeldung vorbereiten
{: #google-sign-in-ios}

Befolgen Sie die von Google unter [Google Sign-In for iOS ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developers.google.com/identity/sign-in/ios/start-integrating "Symbol für externen Link"){: new_window} bereitgestellten Anweisungen, um Ihre App für die Google-Anmeldung vorzubereiten.

Dieser Prozess beinhaltet Folgendes:

* Vorbereitung eines neuen Projekts auf der Google-Site für Entwickler (Google Developers),
* Erstellung der Datei `GoogleService-Info.plist` und des Werts `REVERSE_CLIENT_ID` zum Hinzufügen zu Ihrem Xcode-Projekt und
* Erstellung der **Google-Client-ID** zum Hinzufügen zu Ihrer {{site.data.keyword.Bluemix_notm}}-Back-End-Anwendung.

Die folgenden Schritte stellen eine Kurzfassung der Aufgaben dar, die zum Vorbereiten Ihrer App notwendig sind.

**Hinweis:** Der Sign-In-CocoaPod von Google muss nicht hinzugefügt werden. Das notwendige SDK wird vom CocoaPod `BMSGoogleAuthentication` hinzugefügt.

1. Notieren Sie die Bundle-ID **Bundle Identifier** in Ihrem Xcode-Projekt aus dem Abschnitt **Identity** der Registerkarte **General** des Hauptziels. Sie benötigen Sie zum Erstellen Ihres Projekts zur Google-Anmeldung.

1. Erstellen Sie ein Projekt für Google Sign-In for iOS auf der [Google Developer-Website ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developers.google.com/mobile/add?platform=ios "Symbol für externen Link"){: new_window}.

1. Fügen Sie die API für die Google-Anmeldung (Google Sign-In) Ihrem Projekt hinzu.

1. Rufen Sie die Datei `GoogleService-Info.plist` ab.

   **Wichtig:** Sobald die Datei `GoogleService-Info.plist` vorliegt, öffnen Sie sie und notieren Sie den Wert für `CLIENT_ID`. Sie benötigen diesen Wert später zum Konfigurieren der {{site.data.keyword.amashort}}-Back-End-Anwendung.

1. Fügen Sie die Datei `GoogleService-Info.plist` zu Ihrem Xcode-Projekt hinzu. Weitere Informationen finden Sie in [Add the configuration file to your project ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config "Symbol für externen Link"){: new_window}.

1. Aktualisieren Sie die URL-Schemas in Ihrem Xcode-Projekt mit Ihrer `REVERSE_CLIENT_ID` und mit der Bundle-ID. Weitere Informationen finden Sie in [Add URL schemes to your project ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developers.google.com/identity/sign-in/ios/start-integrating#add_a_url_scheme_to_your_project "Symbol für externen Link"){: new_window}.

1. Aktualisieren Sie die Datei `project-Bridging-Header.h` für Ihre App mit dem folgenden Code:

	```
	#import <Google/SignIn.h>
	```
	{: codeblock}

	Weitere Informationen zum Aktualisieren der Überbrückungsheaderdatei finden Sie in [Enable sign-in ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developers.google.com/identity/sign-in/ios/sign-in#enable_sign-in "Symbol für externen Link"){: new_window}.

## {{site.data.keyword.amashort}} für die Google-Authentifizierung konfigurieren
{: #google-auth-ios-config}

Jetzt, da Sie eine iOS-Client-ID haben, können Sie die Google-Authentifizierung im {{site.data.keyword.amashort}}-Service aktivieren.

1. Öffnen Sie den Service im {{site.data.keyword.amashort}}-Dashboard.
1. Aktivieren Sie auf der Registerkarte **Verwalten** die Option **Berechtigung**.
1. Erweitern Sie den Abschnitt **Google**.
1. Geben Sie in **Application ID for iOS** den Wert für `CLIENT_ID` an, den Sie aus der Datei `GoogleService-Info.plist` abgerufen haben.
1. Klicken Sie auf **Speichern**.

## {{site.data.keyword.amashort}}-Client-SDK für iOS konfigurieren
{: #google-auth-ios-sdk}

### CocoaPods installieren
{: #install-cocoapods}

1. Öffnen Sie das Terminal und führen Sie den Befehl **pod --version** aus. Wenn CocoaPods bereits installiert ist, wird die Versionsnummer angezeigt. Sie können mit dem nächsten Abschnitt fortfahren, um das SDK zu installieren.

1. Wenn CocoaPods nicht installiert ist, führen Sie den folgenden Befehl aus:

	```
	sudo gem install cocoapods
	```
	{: codeblock}

Weitere Informationen finden Sie auf der [CocoaPods-Website ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cocoapods.org/ "Symbol für externen Link"){: new_window}.

### {{site.data.keyword.amashort}}-Client-Swift-SDK mit CocoaPods installieren
{: #facebook-auth-install-swift-cocoapods}

1. Wenn Ihr iOS-Projekt keine `Podfile` enthält, führen Sie den Befehl `pod init` aus, um die Datei zu erstellen.

1. Bearbeiten Sie die `Podfile` und fügen Sie die folgenden Zeilen zum relevanten Ziel hinzu:

	```
	use_frameworks!
	pod 'BMSGoogleAuthentication'
	```
	{: codeblock}

	**Hinweis:** Falls Sie das {{site.data.keyword.amashort}}-Kern-SDK bereits installiert haben, können Sie die folgende Zeile entfernen: `pod 'BMSSecurity'`. Der Pod `BMSGoogleAuthentication` installiert alle erforderlichen Frameworks.

	**Tipp:** Sie können `use_frameworks!` in Ihrem Xcode-Ziel hinzufügen anstatt in der Podfile-Datei.

1. Speichern Sie die `Podfile`-Datei und führen Sie den Befehl `pod install` über die Befehlszeile aus. CocoaPods installiert die Abhängigkeiten. Der Fortschritt und die hinzugefügten Komponenten werden angezeigt.

	**Wichtig**: Sie müssen Ihr Projekt von jetzt an über die von CocoaPods generierte Datei `xcworkspace` öffnen. In der Regel hat die Datei den Namen `{your-project-name}.xcworkspace`.  

1. Führen Sie den Befehl `open {your-project-name}.xcworkspace` über die Befehlszeile aus, um Ihren iOS-Projektarbeitsbereich zu öffnen.

1. Kopieren Sie die Datei `GoogleAuthenticationManager.swift` aus den `BMSGoogleAuthentication`-Pod-Quellendateien in Ihr Projektverzeichnis.

### Gemeinsame Nutzung der Schlüsselkette (Keychain) für iOS aktivieren
{: #enable_keychain}

Aktivieren Sie `Keychain Sharing`. Rufen Sie dazu die Registerkarte `Capabilities` auf und setzen Sie `Keychain Sharing` in Ihrem Xcode-Projekt auf `On`.


## {{site.data.keyword.amashort}}-Client-Swift-SDK initialisieren
{: #google-auth-ios-initialize}

Zur Verwendung des {{site.data.keyword.amashort}}-Client-SDK initialisieren Sie dieses, indem Sie den Parameter `tenantID` übergeben.

Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode `application:didFinishLaunchingWithOptions` Ihres Anwendungsdelegats.

1. Importieren Sie die erforderlichen Frameworks in die Klasse, in der Sie das {{site.data.keyword.amashort}}-Client-SDK verwenden möchten. Fügen Sie die folgenden Header hinzu:

	```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {

		let mcaAuthManager = MCAAuthorizationManager.sharedInstance
		mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
		//the regionName should be one of the following: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney   
		BMSClient.sharedInstance.authorizationManager = mcaAuthManager
		GoogleAuthenticationManager.sharedInstance.register()
		return true
	}

	// [START openurl]
	    func application(_ application: UIApplication,
			     open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
			return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, sourceApplication: sourceApplication, annotation: annotation)
      }

	@available(iOS 9.0, *)
	func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any]) -> Bool {
		return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, options: options)
  }

	```
	{: codeblock}

	Gehen Sie im Code wie folgt vor:

      * Ersetzen Sie `<serviceTenantID>` durch den Wert, den Sie aus **Mobile Systemerweiterungen** abgerufen haben.
      * Ersetzen Sie `<applicationBluemixRegion>` durch Ihre {{site.data.keyword.Bluemix_notm}}-**Region**.

	Weitere Informationen zum Abrufen dieser Werte finden Sie unter [Vorbereitungen](#before-you-begin).


## Authentifizierung testen
{: #google-auth-ios-testing}

Nach der Initialisierung des Client-SDK und der Registrierung des Google-Authentifizierungsmanagers können Sie mit dem Senden von Anforderungen an Ihre mobile Back-End-Anwendung beginnen.

### Vorbereitungen
{: #google-auth-ios-testing-before}

Sie müssen die {{site.data.keyword.mobilefirstbp}}-Boilerplate verwenden und bereits eine durch {{site.data.keyword.amashort}} geschützte Ressource am Endpunkt `/protected` haben. Wenn Sie einen Endpunkt `/protected` einrichten müssen, finden Sie weitere Informationen in [Ressourcen schützen](protecting-resources.html).

1. Versuchen Sie, in Ihrem Desktop-Browser eine Anforderung an den geschützten Endpunkt Ihrer mobilen Back-End-Anforderung zu senden, indem Sie `{applicationRoute}/protected` öffnen.  Beispiel: `http://my-mobile-backend.mybluemix.net/protected`.

1. Der Endpunkt `/protected` einer mobilen Back-End-Anwendung, die mit der MobileFirst Services-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Deshalb kann auf ihn nur mit mobilen Anwendungen zugegriffen werden, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert wurden. Infolgedessen wird eine Nachricht `Unauthorized` (Nicht autorisiert) in Ihrem Desktop-Browser angezeigt.

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

1. Führen Sie Ihre Anwendung aus. Ein Popup-Fenster für die Google-Anmeldung wird angezeigt.

 ![Bild](images/ios-google-login.png)

1. Wenn Sie sich anmelden und auf **OK** klicken, berechtigen Sie {{site.data.keyword.amashort}}, Ihre Google-Benutzeridentität zu Authentifizierungszwecken zu nutzen.

1. Ihre Anforderung sollte erfolgreich ausgeführt werden. Die folgende Ausgabe wird im Protokoll angezeigt.

	```
	response:Optional("Hello, this is a protected resource of the mobile backend application!"), no error
	```
	{: screen}

1. Durch Hinzufügen des folgenden Codes können Sie auch die Abmeldefunktion (logout) hinzufügen:

	```
	GoogleAuthenticationManager.sharedInstance.logout(callBack)
	```
	{: codeblock}

	Wenn Sie diesen Code aufrufen, nachdem sich ein Benutzer bei Google angemeldet hat, und der Benutzer versucht, sich wieder anzumelden, muss er sich bei {{site.data.keyword.amashort}} für die Verwendung von Google zu Authentifizierungszwecken berechtigen. An dieser Stelle kann der Benutzer auf den Benutzernamen klicken,<!--in the upper-right corner of the screen--> um einen anderen Benutzer auszuwählen und sich mit diesem anzumelden.

	Die Übergabe von `callBack` an die Abmeldefunktion ist optional. Sie können auch `nil` übergeben.
