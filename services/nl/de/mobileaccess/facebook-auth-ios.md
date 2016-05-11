---

copyright:
  years: 2015, 2016

---

# Facebook-Authentifizierung in iOS-Apps aktivieren (Objective-C-SDK)
{: #facebook-auth-ios}

Wenn Sie Facebook als Identitätsprovider in Ihren iOS-Anwendungen verwenden möchten, müssen Sie die iOS-Plattform für Ihre Facebook-Anwendung hinzufügen und konfigurieren.

**Tipp:** Wenn Sie Ihre iOS-App mit Swift entwickeln, sollten Sie die Verwendung von {{site.data.keyword.amashort}}-Client-Swift-SDK in Erwägung ziehen. Die Anweisungen auf dieser Seite gelten für das {{site.data.keyword.amashort}}-Client-Objective-C-SDK. Anweisungen für die Verwendung des Swift-SDK finden Sie in [Facebook-Authentifizierung in iOS-Apps aktivieren (Swift-SDK)](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios-swift-sdk.html).

## Vorbereitungen
{: #facebook-auth-ios-before}
* Sie müssen über eine Ressource verfügen, die von {{site.data.keyword.amashort}} geschützt wird, und ein iOS-Projekt haben, das mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert ist.  Weitere Informationen finden Sie in [Einführung in {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) und [iOS-Objective-C-SDK einrichten](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html).  
* Schützen Sie Ihre Back-End-Anwendung manuell mit dem {{site.data.keyword.amashort}}-Server-SDK. Weitere Informationen finden Sie in [Ressourcen schützen](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).
* Erstellen Sie eine Facebook-Anwendungs-ID. Weitere Informationen finden Sie in [Facebook-Anwendungs-ID vom Facebook-Entwicklerportal anfordern](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).

## Facebook-Anwendung für die iOS-Plattform konfigurieren
{: #facebook-auth-ios-config}


1. Klicken Sie in Ihrer Facebook-Anwendung im Facebook-Entwicklerportal auf **Settings > Add Platform > iOS**.

1. Geben Sie die Bundle-ID (*bundleId*) Ihrer iOS-Anwendung an. Zum Ermitteln der Bundle-ID (*bundleId*) Ihrer iOS-Anwendung suchen Sie nach **Bundle Identifier** in der Datei `info.plist` oder auf der Registerkarte **General** des Projekts in Xcode.
**Tipp**: Ziehen Sie in Betracht, das URL-Schemasuffix oder Single Sign-on zu aktivieren, wenn Sie planen, diese Features zu verwenden.

1. Klicken Sie auf **Save Settings** (Einstellungen speichern).

## {{site.data.keyword.amashort}} für die Facebook-Authentifizierung konfigurieren
{: #facebook-auth-ios-configmca}

Nachdem Sie die Facebook-Anwendungs-ID und Ihre Facebook-Anwendung zur Bedienung von iOS-Clients konfiguriert haben, können Sie die Facebook-Authentifizierung in {{site.data.keyword.amashort}} aktivieren.

1. Öffnen Sie Ihre App im {{site.data.keyword.Bluemix}}-Dashboard.

1. Klicken Sie auf **Mobile Systemerweiterungen** und notieren Sie die Werte für **Route** (`applicationRoute`) und **App-GUID** (`applicationGUID`). Sie benötigen diese Werte, wenn Sie das SDK initialisieren.

1. Klicken Sie auf die Kachel für {{site.data.keyword.amashort}}. Das {{site.data.keyword.amashort}}-Dashboard wird geladen.

1. Klicken Sie auf die Kachel **Facebook**.

1. Geben Sie die Facebook-Anwendungs-ID an und klicken Sie auf **Speichern**.

## {{site.data.keyword.amashort}}-Client-SDK für iOS konfigurieren
{: #facebook-auth-ios-sdk}

### CocoaPods installieren
{: #facebook-auth-cocoapods}

Das {{site.data.keyword.amashort}}-Client-SDK wird mit CocoaPods, einem Abhängigkeitenmanager für iOS-Projekte, verteilt. CocoaPods lädt automatisch Artefakte aus Repositorys herunter und stellt sie für Ihre iOS-Anwendung zur Verfügung.

1. Öffnen Sie das Terminal und führen Sie den Befehl `pod --version` aus. Wenn CocoaPods bereits installiert ist, wird die Versionsnummer angezeigt. Sie können mit dem nächsten Abschnitt dieses Lernprogramms fortfahren.

1. Installieren Sie CocoaPods, indem Sie den Befehl `sudo gem install cocoapods` ausführen. Weitere Anweisungen finden Sie bei Bedarf auf der [CocoaPods-Website](https://cocoapods.org/).

### {{site.data.keyword.amashort}}-Client-SDK mit CocoaPods installieren
{: #facebook-auth-install-cocoapods}

1. Bearbeiten Sie in Ihrem iOS-Projekt die `Podfile` und die folgende Zeile:

	```
	pod 'IMFFacebookAuthentication'
	```

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
	<string>MyApp</string>
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
Aktualisieren Sie die Eigenschaften 'URL scheme' und 'FacebookappID' mit Ihrer Facebook-Anwendungs-ID.

 **Wichtig**: Stellen Sie sicher, dass Sie keine vorhandenen Eigenschaften in der Datei `info.plist` überschreiben. Wenn Sie sich überschneidende Eigenschaften haben, müssen Sie diese manuell zusammenfügen. Weitere Informationen finden Sie in den Abschnitten zum [Konfigurieren eines Xcode-Projekts](https://developers.facebook.com/docs/ios/getting-started/) und [Vorbereiten von Apps für iOS9](https://developers.facebook.com/docs/ios/ios9).

## {{site.data.keyword.amashort}}-Client-SDK initialisieren
{: #facebook-auth-ios-initalize}

Initialisieren Sie das Client-SDK, indem Sie die Route (`applicationRoute`) und die App-GUID (`applicationGUID`) Ihrer App übergeben.

Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode `application:didFinishLaunchingWithOptions` Ihres Anwendungsdelegats.

1. Öffnen Sie die Hauptseite im {{site.data.keyword.Bluemix_notm}}-Dashboard und klicken Sie auf Ihre App. Klicken Sie auf **Mobile Systemerweiterungen** und notieren Sie die Werte für **Route** (`applicationRoute`) und **App-GUID** (`applicationGUID`).

1. Importieren Sie das erforderliche Framework in die Klasse, die das {{site.data.keyword.amashort}}-Client-SDK verwenden soll, indem Sie die folgenden Header hinzufügen:

	**Objective-C**

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFFacebookAuthentication/IMFFacebookAuthenticationHandler.h>
	#import <FacebookSDK/FacebookSDK.h>
```

	**Swift**

	Das {{site.data.keyword.amashort}}-Client-SDK ist mit Objective-C implementiert. Daher müssen Sie möglicherweise Ihrem Swift-Projekt einen Überbrückungsheader hinzufügen.

	1. Klicken Sie mit der rechten Maustaste auf Ihr Projekt in Xcode und wählen Sie **New File...** aus.
	* Wählen Sie in der Kategorie **iOS Source** die Option `Header file` aus.
	* Geben Sie der Datei den Namen `BridgingHeader.h`.
	* Fügen Sie Ihrem Überbrückungsheader Import-Angaben hinzu:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFFacebookAuthentication/IMFFacebookAuthenticationHandler.h>
	#import <FacebookSDK/FacebookSDK.h>
```
	* Klicken Sie auf Ihr Projekt in Xcode und wählen Sie die Registerkarte **Build Settings** (Buildeinstellungen) aus.
	* Suchen Sie nach **Objective-C Bridging Header**.
	* Setzen Sie den Wert auf die Position Ihrer Datei `BridgingHeader.h`. Beispiel: `$(SRCROOT)/MyApp/BridgingHeader.h`.
	* Stellen Sie sicher, dass Ihr Überbrückungsheader von Xcode aufgenommen wird, indem Sie Ihr Projekt erstellen (Build). Dabei sollten keine Fehlernachrichten angezeigt werden.

3. Initialisieren Sie das Client-SDK.	Ersetzen Sie *applicationRoute* und *applicationGUID* durch die Werte für **Route** und **App-GUID**, die Sie im Abschnitt **Mobile Systemerweiterungen** im {{site.data.keyword.Bluemix_notm}}-Dashboard ermittelt haben.

	**Objective-C**

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	**Swift**

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```

1. Benachrichtigen Sie das Facebook-SDK über die App-Aktivierung und registrieren Sie den Facebook-Authentifizierungshandler, indem Sie den folgenden Code in der Methode `application:didFinishLaunchingWithOptions` in Ihrem App-Delegat hinzufügen. Fügen Sie diesen Code direkt nach dem Initialisieren der IMFClient-Instanz hinzu.

	**Objective-C**

	```Objective-C
		[FBAppEvents activateApp];
		[[IMFFacebookAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
```

	**Swift**

	```Swift
		FBAppEvents.activateApp()
		IMFFacebookAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
```

1. Fügen Sie Ihrem App-Delegat den folgenden Code hinzu.

	**Objective-C**

	```Objective-C
	- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url
			sourceApplication:(NSString *)sourceApplication annotation:(id)annotation {

		return [FBAppCall handleOpenURL:url sourceApplication:sourceApplication];

	}
```

	**Swift**

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		return FBAppCall.handleOpenURL(url, sourceApplication: sourceApplication)

	}
```

## Authentifizierung testen
{: #facebook-auth-ios-testing}
Nach der Initialisierung des Client-SDK und der Registrierung des Facebook-Authentifizierungsmanagers können Sie mit dem Senden von Anforderungen an Ihr mobiles Back-End beginnen.

### Vorbereitungen
{: #facebook-auth-ios-testing-before}
Sie müssen die {{site.data.keyword.mobilefirstbp}}-Boilerplate verwenden und bereits eine durch {{site.data.keyword.amashort}} geschützte Ressource am Endpunkt `/protected` haben. Wenn Sie einen Endpunkt `/protected` einrichten müssen, finden Sie weitere Informationen in [Ressourcen schützen](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Versuchen Sie, in Ihrem Browser eine Anforderung an den Endpunkt '/protected' Ihres neu erstellten mobilen Back-Ends zu senden. Öffnen Sie die folgende URL: `{applicationRoute}/protected`.
Beispiel: `http://my-mobile-backend.mybluemix.net/protected`
<br/>Der Endpunkt `/protected` eines mobilen Back-Ends, der mit der MobileFirst Services Starter-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Eine Nachricht `Unauthorized` (Nicht autorisiert) wird in Ihrem Browser zurückgegeben. Diese Nachricht wird deshalb zurückgegeben, weil auf diesen Endpunkt nur mobile Anwendungen zugreifen können, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind.

1. Verwenden Sie Ihre iOS-Anwendung, um eine Anforderung an denselben Endpunkt zu senden.

	**Objective-C**

	```Objective-C
	NSString *requestPath = [NSString stringWithFormat:@"%@/protected",
								[[IMFClient sharedInstance] backendRoute]];

	IMFResourceRequest *request =  [IMFResourceRequest requestWithPath:requestPath
																method:@"GET"];

	[request sendWithCompletionHandler:^(IMFResponse *response, NSError *error) {
		if (error){
			NSLog(@"Error :: %@", [error description]);
		} else {
			NSLog(@"Response :: %@", [response responseText]);
			NSLog(@"%@", [[IMFAuthorizationManager sharedInstance] userIdentity]);
		}
	}];
	```

	**Swift**

	```Swift
	let requestPath = IMFClient.sharedInstance().backendRoute + "/protected"

	let request = IMFResourceRequest(path: requestPath, method: "GET");
	request.sendWithCompletionHandler { (response, error) -> Void in
		if (nil != error){
			NSLog("Error :: %@", error.description)
		} else {
			NSLog("Response :: %@", response.responseText)
			NSLog("%@", IMFAuthorizationManager.sharedInstance().userIdentity)
		}
	};
 ```

1. Führen Sie Ihre Anwendung aus. Es wird eine Facebook-Anmeldefenster angezeigt.

	![Bild](images/ios-facebook-login.png)

	Diese Anzeige sieht möglicherweise geringfügig anders aus, wenn Sie die Facebook-App nicht auf Ihrem Gerät installiert haben oder wenn Sie zurzeit nicht bei Facebook angemeldet sind.

1. Klicken Sie auf **OK**, um {{site.data.keyword.amashort}} zu berechtigen, Ihre Facebook-Benutzeridentität zu Authentifizierungszwecken zu nutzen.

1. 	Wenn Ihre Anforderung erfolgreich ist, wird die folgende Ausgabe in der Xcode-Konsole angezeigt:
![image](images/ios-facebook-login-success.png)



	Durch Hinzufügen des folgenden Codes können Sie auch die Abmeldefunktion (logout) hinzufügen:


	**Objective-C**

	```Objective-C
	[[IMFFacebookAuthenticationHandler sharedInstance] logout : callBack]
	```

	**Swift**

	```Swift
	IMFFacebookAuthenticationHandler.sharedInstance().logout(callBack)
	```

	Wenn Sie diesen Code aufrufen, nachdem sich ein Benutzer bei Facebook angemeldet hat, und der Benutzer versucht, sich wieder anzumelden, muss er sich bei Mobile Client Access für die Verwendung von Facebook zu Authentifizierungszwecken berechtigen.

	Um Benutzer zu wechseln, müssen Sie diesen Code aufrufen, und der Benutzer muss sich in seinem Browser bei Facebook abmelden.
Die Übergabe von `callBack` an die Abmeldefunktion ist optional. Sie können auch `nil` übergeben.

