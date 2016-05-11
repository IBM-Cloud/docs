---

copyright:
  years: 2015, 2016

---

# Google-Authentifizierung in iOS-Apps aktivieren
{: #google-auth-ios}

**Tipp:** Wenn Sie Ihre iOS-App mit Swift entwickeln, sollten Sie die Verwendung von {{site.data.keyword.amashort}}-Client-Swift-SDK in Erwägung ziehen. Die Anweisungen auf dieser Seite gelten für das {{site.data.keyword.amashort}}-Client-Objective-C-SDK. Anweisungen für die Verwendung des Swift-SDK finden Sie in [Google-Authentifizierung in iOS-Apps aktivieren (Swift-SDK)](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html)

## Vorbereitungen
{: #google-auth-ios-before}
* Sie müssen über eine durch {{site.data.keyword.amashort}} geschützte Ressource verfügen und ein iOS-Projekt haben, das mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert ist.  Weitere Informationen finden Sie in [Einführung in {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) und [iOS-Objective-C-SDK einrichten](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html).  
* Schützen Sie Ihre Back-End-Anwendung manuell mit dem {{site.data.keyword.amashort}}-Server-SDK. Weitere Informationen finden Sie in [Ressourcen schützen](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


## Google-Projekt für die iOS-Plattform konfigurieren
{: #google-auth-ios-project}
Zur Verwendung von Google als Identitätsprovider erstellen Sie ein Projekt in Google Developer Console, um eine Google-Client-ID zu erhalten.  Diese Client-ID ist eine eindeutige Kennung, an der Google erkennen kann, welche Anwendung versucht, eine Verbindung herzustellen.   Wenn Sie bereits ein Google-Projekt haben, können Sie die Schritte, in denen die Projekterstellung beschrieben wird, überspringen und mit dem Hinzufügen von Berechtigungsnachweisen beginnen.



1. Erstellen Sie ein Projekt in [Google Developer Console](https://console.developers.google.com).
Wenn Sie bereits ein Projekt haben, können Sie die Schritte, in denen die Projekterstellung beschrieben wird, überspringen und mit dem Hinzufügen von Berechtigungsnachweisen beginnen.
   1.    Öffnen Sie ein neues Projektmenü. 
         
         ![Bild](images/FindProject.jpg)

   2.    Klicken Sie auf **Create a project**.
   
         ![Bild](images/CreateAProject.jpg)


1. Wählen Sie in der Liste **Social APIs** den Eintrag **Google+ API** aus.

     ![Bild](images/chooseGooglePlus.jpg)

1. Klicken Sie in der nächsten Anzeige auf **Enable**.

1. Wählen Sie die Registerkarte **Consent Screen** aus und geben Sie den Produktnamen an, der den Benutzern angezeigt wird. Weitere Werte sind optional. Klicken Sie auf **Save**.

    ![Bild](images/consentScreen.png)
    
1. Wählen Sie in der Liste **Credentials** die OAuth-Client-ID aus.

     ![Bild](images/chooseCredentials.png)
     


1. An diesem Punkt wird eine Auswahl für den Anwendungstyp angezeigt. Wählen Sie **iOS** aus.

1. Geben Sie einen aussagekräftigen Namen für Ihren iOS-Client an. Geben Sie die Bundle-ID Ihrer iOS-Anwendung an. Zum Ermitteln der Bundle-ID Ihrer iOS-Anwendung suchen Sie nach **Bundle Identifier** in der Datei `info.plist` oder auf der Registerkarte **General** des Projekts in Xcode.

1. Notieren Sie sich Ihre neue iOS-Client-ID. Sie benötigen den Wert, wenn Sie die Anwendung in {{site.data.keyword.Bluemix}} einrichten.


## {{site.data.keyword.amashort}} für die Google-Authentifizierung konfigurieren
{: #google-auth-ios-config}

Jetzt, da Sie eine iOS-Client-ID haben, können Sie die Google-Authentifizierung im {{site.data.keyword.Bluemix_notm}}-Dashboard aktivieren.

1. Öffnen Sie Ihre App im {{site.data.keyword.Bluemix_notm}}-Dashboard.

1. Klicken Sie auf **Mobile Systemerweiterungen** und notieren Sie die Werte für **Route** (`applicationRoute`) und **App-GUID** (`applicationGUID`). Sie benötigen diese Werte, wenn Sie das SDK initialisieren.

1. Klicken Sie auf die Kachel für {{site.data.keyword.amashort}}. Das {{site.data.keyword.amashort}}-Dashboard wird geladen.

1. Klicken Sie auf die Kachel für **Google**.

1. Geben Sie in **Application ID for iOS** (Anwendungs-ID für iOS) Ihre iOS-Client-ID für Android an und klicken Sie auf **Save** (Speichern).

	Anmerkung: Zusätzlich zur Google-Client-ID ist auch der Umkehrwert für Ihre Clientkonfiguration erforderlich (siehe unten). Um auf beide Werte zuzugreifen, müssen Sie mithilfe des Stiftsymbols die Beispiel-PList herunterladen:
		![Download der Datei info.plist](images/download_plist.png)

## {{site.data.keyword.amashort}}-Client-SDK für iOS konfigurieren
{: #google-auth-ios-sdk}

### {{site.data.keyword.amashort}}-Client-SDK mit CocoaPods installieren
{: #google-auth-ios-sdk-cocoapods}

1. Navigieren Sie zu Ihrem iOS-Projekt.

1. Bearbeiten Sie die `Podfile`-Datei und fügen Sie die folgende Zeile hinzu:

	```
	pod 'IMFGoogleAuthentication'
	```

1. Speichern Sie die `Podfile`-Datei und führen Sie den Befehl `pod install` über die Befehlszeile aus. CocoaPods installiert die Abhängigkeiten. Der Fortschritt und die hinzugefügten Komponenten werden angezeigt.

  **Wichtig**: Sie müssen Ihr Projekt von jetzt an über die von CocoaPods generierte Datei `xcworkspace` öffnen. In der Regel hat die Datei den Namen `{your-project-name}.xcworkspace`.  

1. Führen Sie den Befehl `open {your-project-name}.xcworkspace` über die Befehlszeile aus, um Ihren iOS-Projektarbeitsbereich zu öffnen.

### iOS-Projekt für die Google-Authentifizierung konfigurieren
{: #google-auth-ios-googleauth}
Konfigurieren Sie die Google-Integration, indem Sie die Datei `info.plist` aktualisieren. Die Datei `info.plist` befindet sich normalerweise im Ordner `Supporting files` in Ihrem Xcode-Projekt. Sie können die Datei entweder im Listeneditor für Eigenschaften oder mit einem Texteditor bearbeiten.

* Konfigurieren Sie die Google-Integration, indem Sie die folgenden URL-Schemas in Ihrer Datei `info.plist` hinzufügen.
	![Datei 'info.plist'](images/ios-google-infoplist-settings.png)

	Das erste URL-Schema ist eine umgekehrte Version der Client-ID aus Google Developer Console.  Beispiel: Wenn Ihre Client-ID `123123-abcabc.apps.googleusercontent.com` ist, sollte Ihr URL-Schema `com.googleusercontent.apps.123123-abcabc` sein. 

	Das zweite URL-Schema ist die Bundle-ID Ihrer Anwendung.

* Verwenden Sie einen Texteditor. Klicken Sie mit der rechten Maustaste auf `info.plist` und wählen Sie die Optionen **Open as > Source code** aus. Fügen Sie den folgenden XML-Code zu der Datei hinzu:

	```XML
	<key>CFBundleURLTypes</key>
	<array>
		<dict>
			<key>CFBundleTypeRole</key>
			<string>Editor</string>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>com.googleusercontent.apps.123123-abcabc</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeRole</key>
			<string>Editor</string>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>com.ibm.HelloWorld</string>
			</array>
		</dict>
	</array>

	```
	Aktualisieren Sie beide URL-Schemas.

	**Wichtig**: Stellen Sie sicher, dass Sie keine vorhandenen Eigenschaften in der Datei `info.plist` überschreiben. Wenn sich überschneidende Eigenschaften vorliegen, müssen Sie die betreffenden Eigenschaften manuell zusammenfügen. Weitere Informationen finden Sie in [Try Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start).

## {{site.data.keyword.amashort}}-Client-SDK initialisieren
{: #google-auth-ios-initialize}

Zur Verwendung des {{site.data.keyword.amashort}}-Client-SDK müssen Sie das SDK initialisieren, indem Sie die Parameter 'applicationGUID' und 'applicationRoute' übergeben.

Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode `application:didFinishLaunchingWithOptions` Ihres Anwendungsdelegats.

1. Ermitteln Sie die Werte für 'applicationGUID' und 'applicationRoute'. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf Ihre App. Klicken Sie auf **Mobile Systemerweiterungen**. Die Werte für die Anwendungsroute und die GUID der Anwendung werden angezeigt.

1. Importieren Sie die erforderlichen Frameworks in die Klasse, in der Sie das {{site.data.keyword.amashort}}-Client-SDK verwenden möchten. Fügen Sie die folgenden Header hinzu:

	Objective-C:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```

	Swift:

	Das {{site.data.keyword.amashort}}-Client-SDK ist mit Objective-C implementiert. Sie müssen Ihrem Swift-Projekt möglicherweise einen Überbrückungsheader hinzufügen, um das SDK verwenden zu können.

	1. Klicken Sie mit der rechten Maustaste auf Ihr Projekt in Xcode und wählen Sie **New File...** aus.
	2. Wählen Sie in der Kategorie **iOS Source** die Option **Header file** aus.
	3. Geben Sie der Datei den Namen `BridgingHeader.h`.
	4. Fügen Sie die folgenden Importe zu Ihrem Überbrückungsheader hinzu:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```
	5. Klicken Sie auf Ihr Projekt in Xcode und wählen Sie die Registerkarte **Build Settings** (Buildeinstellungen) aus.
	6. Suchen Sie nach `Objective-C Bridging Header`.
	7. Setzen Sie den Wert auf die Position Ihrer Datei `BridgingHeader.h` (z. B. `$(SRCROOT)/MyApp/BridgingHeader.h`).
	8. Stellen Sie sicher, dass Ihr Überbrückungsheader von Xcode aufgenommen wird, indem Sie Ihr Projekt erstellen (Build).

3. Verwenden Sie den folgenden Code, um das SDK zu initialisieren.  Ersetzen Sie *applicationRoute* und *applicationGUID* durch die Werte für **Route** und **App-GUID**, die Sie im Abschnitt **Mobile Systemerweiterungen** ermittelt haben.

	Objective-C:

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	Swift:

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```



1. Registrieren Sie den Google-Authentifizierungshandler, indem Sie den folgenden Code in der Methode `application:didFinishLaunchingWithOptions` in Ihrem App-Delegat hinzufügen. Fügen Sie diesen Code direkt nach dem Initialisieren des IMFClients hinzu:

	Objective-C:

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```

	Swift:

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```

1. Fügen Sie Ihrem App-Delegat den folgenden Code hinzu.

	Objective-C:

	```Objective-C
	- (void)applicationDidBecomeActive:(UIApplication *)application {
		[[IMFGoogleAuthenticationHandler sharedInstance] handleDidBecomeActive];
	}

	- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url
					sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {

		BOOL shouldHandleGoogleURL = [GPPURLHandler handleURL:url
					sourceApplication:sourceApplication annotation:annotation];

		[[IMFGoogleAuthenticationHandler sharedInstance] handleOpenURL:shouldHandleGoogleURL];
		return  shouldHandleGoogleURL;
	}
	```

	Swift:

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		let shouldHandleGoogleURL = GPPURLHandler.handleURL(url,
				sourceApplication: sourceApplication, annotation: annotation)

		IMFGoogleAuthenticationHandler.sharedInstance()
							.handleOpenURL(shouldHandleGoogleURL)

		return shouldHandleGoogleURL;
	}
```

## Authentifizierung testen
{: #google-auth-ios-testing}
Nach der Initialisierung des Client-SDK können Sie mit dem Senden von Anforderungen an Ihr mobiles Back-End beginnen.

### Vorbereitungen
{: #google-auth-ios-testing-before}
Sie müssen die {{site.data.keyword.mobilefirstbp}}-Boilerplate verwenden und bereits eine durch {{site.data.keyword.amashort}} geschützte Ressource am Endpunkt `/protected` haben. Wenn Sie einen Endpunkt `/protected` einrichten müssen, finden Sie weitere Informationen in [Ressourcen schützen](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Versuchen Sie, in Ihrem Desktop-Browser eine Anforderung an den geschützten Endpunkt Ihres mobilen Back-Ends zu senden, indem Sie `{applicationRoute}/protected` öffnen (z. B. `http://my-mobile-backend.mybluemix.net/protected`).

1. Der Endpunkt `/protected` eines mobilen Back-Ends, das mit der MobileFirst Services-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Deshalb auf ihn nur mit mobilen Anwendungen zugegriffen werden, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert wurden. Infolgedessen wird eine Nachricht `Unauthorized` (Nicht autorisiert) in Ihrem Desktop-Browser angezeigt.

1. Verwenden Sie Ihre iOS-Anwendung, um eine Anforderung an denselben Endpunkt zu senden.

	Objective-C:

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

	Swift:

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

1. Führen Sie Ihre Anwendung aus. Ein Popup-Fenster für die Gooble-Anmeldung wird angezeigt.

	![Bild](images/ios-google-login.png)

	Diese Anzeige sieht möglicherweise geringfügig anders aus, wenn Sie die Facebook-App nicht auf Ihrem Gerät installiert haben oder wenn Sie zurzeit nicht bei Facebook angemeldet sind.

1. Indem Sie auf **OK** klicken, berechtigen Sie {{site.data.keyword.amashort}}, Ihre Google-Benutzeridentität zu Authentifizierungszwecken zu nutzen.

1. 	Ihre Anforderung sollte erfolgreich ausgeführt werden. Die folgende Ausgabe sollte in LogCat angezeigt werden.

	![Bild](images/ios-google-login-success.png)
	
	
	Durch Hinzufügen des folgenden Codes können Sie auch die Abmeldefunktion (logout) hinzufügen:
	
	Objective-C:
	
	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] logout : callBack]
	```

	Swift:

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().logout(callBack)
	```


	Wenn Sie diesen Code aufrufen, nachdem sich ein Benutzer bei Google angemeldet hat, und der Benutzer versucht, sich wieder anzumelden, muss er sich bei Mobile Client Access für die Verwendung von Google zu Authentifizierungszwecken berechtigen. An dieser Stelle kann der Benutzer in der rechten oberen Ecke der Anzeige auf den Benutzernamen klicken, um einen anderen Benutzer auszuwählen und sich mit diesem anzumelden.

	Die Übergabe von `callBack` an die Abmeldefunktion ist optional. Sie können auch `nil` übergeben.
