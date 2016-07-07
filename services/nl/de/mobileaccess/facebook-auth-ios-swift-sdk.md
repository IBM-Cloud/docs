---

copyright:
  years: 2016

---
{:screen: .screen}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}

# Facebook-Authentifizierung für iOS-Apps aktivieren (Swift-SDK)
{: #facebook-auth-ios}

*Letzte Aktualisierung: 15. Juni 2016*
{: .last-updated}

Wenn Sie Facebook als Identitätsprovider in Ihren iOS-Anwendungen verwenden möchten, müssen Sie die iOS-Plattform für Ihre Facebook-Anwendung hinzufügen und konfigurieren.
{:shortdesc}

## Vorbereitungen
{: #facebook-auth-ios-before}
Voraussetzungen:
* iOS-Projekt, das für das Arbeiten mit CocoaPods eingerichtet ist. Weitere Informationen finden Sie unter **Install CocoaPods** in [Setting up the iOS Swift SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html).
   **Hinweis:** Sie müssen nicht den Kern des {{site.data.keyword.amashort}}-Client-SDK installieren, bevor Sie fortfahren.
* Instanz einer {{site.data.keyword.Bluemix_notm}}-Anwendung, die durch den {{site.data.keyword.amashort}}-Service geschützt ist. Weitere Informationen zur Erstellung eines {{site.data.keyword.Bluemix_notm}}-Back-Ends finden Sie in der [Einführung](index.html).
* Facebook-Anwendungs-ID. Weitere Informationen finden Sie in [Facebook-Anwendungs-ID vom Facebook-Entwicklerportal anfordern](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).


**Wichtig:** Sie müssen das Facebook-SDK nicht separat installieren. Das Facebook-SDK wird automatisch durch den nachfolgend beschriebenen Pod `BMSFacebookAuthentication` installiert. Sie können den Schritt zum Hinzufügen des Facebook-SDK zum Xcode-Projekt (**Add the Facebook SDK to your Xcode Project**) im Facebook-Entwicklerportal (**Facebook Developer Portal**) überspringen.

**Hinweis:** Das Objective-C-SDK wird zwar weiterhin vollständig unterstützt und gilt noch als primäres SDK für {{site.data.keyword.Bluemix_notm}} Mobile Services, seine Verwendung und Unterstützung sollen jedoch zugunsten des neuen Swift-SDK noch dieses Jahr eingestellt werden.
## Facebook-Anwendung für die iOS-Plattform konfigurieren
{: #facebook-auth-ios-config}

1. Melden Sie sich beim [Dashboard Ihrer Facebook-App](https://developers.facebook.com/apps/) an.

1. Notieren Sie die App-ID (**App ID**) für Ihre App. Sie benötigen diesen Wert beim Konfigurieren Ihres iOS-Projekts für die Facebook-Authentifizierung.

1. Klicken Sie auf **Settings > Add Platform > iOS**.

1. Geben Sie die Bundle-ID (*bundleId*) Ihrer iOS-Anwendung an. Zum Ermitteln der Bundle-ID (*bundleId*) Ihrer iOS-Anwendung suchen Sie nach **Bundle Identifier** in der Datei `info.plist` oder auf der Registerkarte **General** des Projekts in Xcode.
**Tipp**: Ziehen Sie in Betracht, das URL-Schemasuffix oder Single Sign-on zu aktivieren, wenn Sie planen, diese Features zu verwenden.

1. Klicken Sie auf **Save Settings** (Einstellungen speichern).

## {{site.data.keyword.amashort}} für die Facebook-Authentifizierung konfigurieren
{: #facebook-auth-ios-configmca}

Nachdem Sie die Facebook-Anwendungs-ID und Ihre Facebook-Anwendung zur Bedienung von iOS-Clients konfiguriert haben, können Sie die Facebook-Authentifizierung in {{site.data.keyword.amashort}} aktivieren.

1. Öffnen Sie Ihre App im {{site.data.keyword.Bluemix}}-Dashboard.

1. Klicken Sie auf **Mobile Systemerweiterungen** und notieren Sie die Werte für **Route** (*applicationRoute*) und **App-GUID** (*applicationGUID*). Sie benötigen diese Werte, wenn Sie das SDK initialisieren.

1. Klicken Sie auf die Kachel für {{site.data.keyword.amashort}}. Das {{site.data.keyword.amashort}}-Dashboard wird geladen.

1. Klicken Sie auf die Kachel **Facebook**.

1. Geben Sie die Facebook-Anwendungs-ID an und klicken Sie auf **Speichern**.

## {{site.data.keyword.amashort}}-Client-SDK für iOS konfigurieren
{: #facebook-auth-ios-sdk}

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

1. Bearbeiten Sie die `Podfile` und fügen Sie die folgenden Zeilen hinzu:

 ```
use_frameworks!
pod 'BMSFacebookAuthentication'

	```

   **Hinweis:** Falls Ihre Pod-Datei die Zeile `pod 'BMSSecurity'` enthält, müssen Sie sie entfernen. Der Pod `BMSFacebookAuthentication` installiert alle notwendigen Frameworks.

   **Tipp:** Sie können `use_frameworks!` in Ihrem Xcode-Ziel hinzufügen anstatt in der Podfile-Datei.

1. Speichern Sie die `Podfile` und führen Sie den Befehl `pod install` über die Befehlszeile aus. CocoaPods installiert die Abhängigkeiten. Der Fortschritt und die hinzugefügten Komponenten werden angezeigt.

 **Wichtig**: Sie müssen Ihr Projekt von jetzt an über die von CocoaPods generierte Datei `xcworkspace` öffnen. In der Regel hat die Datei den Namen `{your-project-name}.xcworkspace`.  

1. Führen Sie den Befehl `open {your-project-name}.xcworkspace` über die Befehlszeile aus, um Ihren iOS-Projektarbeitsbereich zu öffnen.

### iOS-Projekt für die Facebook-Authentifizierung konfigurieren
{: #facebook-auth-ios-configproject}

1. Suchen Sie die Datei `info.plist`, die sich gewöhnlich unter dem Ordner `Supporting files` in Ihrem Xcode-Projekt befindet.

1. Konfigurieren Sie die Facebook-Integration, indem Sie Ihrer Datei `info.plist` die folgenden Eigenschaften hinzufügen:

   ![Bild](images/ios-facebook-infoplist-settings.png)


   Aktualisieren Sie die Eigenschaften 'URL scheme' und 'FacebookappID' mit Ihrer Facebook-Anwendungs-ID.

   Sie können die Datei `info.plist` auch aktualisieren, indem Sie mit der rechten Maustaste auf die Datei klicken, die Optionen **Open as > Source Code** auswählen auswählen und das folgende XML hinzufügen:

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
   Aktualisieren Sie die Eigenschaften 'URL scheme' und 'FacebookappID' mit Ihrer Facebook-Anwendungs-ID. Aktualisieren Sie die Eigenschaft 'FacebookDisplayName' mit dem Namen Ihrer Facebook-Anwendung.

    **Wichtig**: Stellen Sie sicher, dass Sie keine vorhandenen Eigenschaften in der Datei `info.plist` überschreiben. Wenn Sie sich überschneidende Eigenschaften haben, müssen Sie diese manuell zusammenfügen. Weitere Informationen finden Sie in den Abschnitten zum [Konfigurieren eines Xcode-Projekts](https://developers.facebook.com/docs/ios/getting-started/) und [Vorbereiten von Apps für iOS9](https://developers.facebook.com/docs/ios/ios9).

## {{site.data.keyword.amashort}}-Client-Swift-SDK initialisieren
{: #facebook-auth-ios-initalize-swift}

Initialisieren Sie das Client-SDK, indem Sie die Parameter `applicationGUID` und `applicationRoute` übergeben.

Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode `application:didFinishLaunchingWithOptions` Ihres Anwendungsdelegats.

1. Rufen Sie Ihre Werte für die Anwendungsparameter ab. Öffnen Sie Ihre App im {{site.data.keyword.Bluemix_notm}}-Dashboard. Klicken Sie auf **Mobile Systemerweiterungen**. Die Werte für `applicationRoute` und `applicationGUID` werden in den Feldern **Route** und **App-GUID** angezeigt.

1. Importieren Sie das erforderliche Framework in die Klasse, die das {{site.data.keyword.amashort}}-Client-SDK verwenden soll, indem Sie die folgenden Header hinzufügen:

	```swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```
2. Initialisieren Sie das Client-SDK.	Ersetzen Sie `<applicationRoute>` und `<applicationGUID>` durch die Werte für **Route** und **App-GUID**, die Sie im Abschnitt **Mobile Systemerweiterungen** des {{site.data.keyword.Bluemix_notm}}-Dashboards ermittelt haben.
Ersetzen Sie `<applicationBluemixRegion>` durch die Region, in der Ihre {{site.data.keyword.Bluemix_notm}}-Anwendung per Hosting bereitgestellt wird. Klicken Sie zur Anzeige der {{site.data.keyword.Bluemix_notm}}-Region auf das Symbol mit dem Gesicht (![Gesicht](images/face.jpg "Symbol 'Gesicht'")) in der linken oberen Ecke des Dashboards.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<applicationBluemixRegion>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 FacebookAuthenticationManager.sharedInstance.register()
 ```

1. Benachrichtigen Sie das Facebook-SDK über die App-Aktivierung und registrieren Sie den Facebook-Authentifizierungshandler, indem Sie den folgenden Code der Methode `application:didFinishLaunchingWithOptions` in Ihrem App-Delegat hinzufügen. Fügen Sie diesen Code direkt nach dem Initialisieren der BMSClient-Instanz hinzu und registrieren Sie Facebook als den Authentifizierungsmanager.

 ```Swift
  return FacebookAuthenticationManager.sharedInstance.onFinishLaunching(application, withOptions: launchOptions)
 ```

1. Kopieren Sie die Datei `FacebookAuthenticationManager.swift` aus den Quellendateien des Pods `BMSFacebookAuthentication` in Ihr Projektverzeichnis.

1. Fügen Sie Ihrem App-Delegat den folgenden Code hinzu.

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		return FacebookAuthenticationManager.sharedInstance.onOpenURL(application, url: url, sourceApplication: sourceApplication, annotation: annotation)

	}
 ```

## Authentifizierung testen
{: #facebook-auth-ios-testing}

Nach der Initialisierung des Client-SDK und der Registrierung des Facebook-Authentifizierungsmanagers können Sie mit dem Senden von Anforderungen an Ihr mobiles Back-End beginnen.

### Vorbereitungen
{: #facebook-auth-ios-testing-before}

Sie müssen die {{site.data.keyword.mobilefirstbp}}-Boilerplate verwenden und bereits eine durch {{site.data.keyword.amashort}} geschützte Ressource am Endpunkt `/protected` haben. Wenn Sie einen Endpunkt `/protected` einrichten müssen, finden Sie weitere Informationen in [Ressourcen schützen](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Versuchen Sie, in Ihrem Browser eine Anforderung an den geschützten Endpunkt Ihres neu erstellten mobilen Back-Ends zu senden. Öffnen Sie die folgende URL: `{applicationRoute}/protected`.
Beispiel: `http://my-mobile-backend.mybluemix.net/protected`
<br/>Der Endpunkt `/protected` eines mobilen Back-Ends, der mit der MobileFirst Services Starter-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Eine Nachricht `Unauthorized` (Nicht autorisiert) wird in Ihrem Browser zurückgegeben. Diese Nachricht wird deshalb zurückgegeben, weil auf diesen Endpunkt nur mobile Anwendungen zugreifen können, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind.

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

1. Führen Sie Ihre Anwendung aus. Es wird eine Facebook-Anmeldefenster angezeigt.
 
   ![Bild](images/ios-facebook-login.png)

	Diese Anzeige sieht möglicherweise geringfügig anders aus, wenn Sie zurzeit nicht bei Facebook angemeldet sind.

1. Klicken Sie auf **OK**, um {{site.data.keyword.amashort}} zu berechtigen, Ihre Facebook-Benutzeridentität zu Authentifizierungszwecken zu nutzen.

1. 	Wenn Ihre Anforderung erfolgreich ist, wird die folgende Ausgabe in der Xcode-Konsole angezeigt:

 ```
 "onAuthenticationSuccess info = Optional({
     attributes =     {
     };
     deviceId = 218227041863639;
     displayName = "Don+Lon";
     isUserAuthenticated = 1;
     userId = 218227041863639;
 })
 response:Optional("Hello, this is a protected resouce of the mobile backend application!"), no error
 ```
  {: screen}

1. Durch Hinzufügen des folgenden Codes können Sie auch die Abmeldefunktion (logout) hinzufügen:

 ```
FacebookAuthenticationManager.sharedInstance.logout(callBack)
```

 Wenn Sie diesen Code aufrufen, nachdem sich ein Benutzer bei Facebook angemeldet hat, und der Benutzer versucht, sich wieder anzumelden, muss er sich bei {{site.data.keyword.amashort}} für die Verwendung von Facebook zu Authentifizierungszwecken berechtigen.

 Um Benutzer zu wechseln, müssen Sie diesen Code aufrufen, und der Benutzer muss sich in seinem Browser bei Facebook abmelden.

 Die Übergabe von `callBack` an die Abmeldefunktion ist optional. Sie können auch `nil` übergeben.
