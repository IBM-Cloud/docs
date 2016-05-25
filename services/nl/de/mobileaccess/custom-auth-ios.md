---

copyright:
  years: 2015, 2016

---

# {{site.data.keyword.amashort}}-Client-SDK für iOS konfigurieren
{: #custom-ios}

Konfigurieren Sie Ihre iOS-Anwendung, die mit der angepassten Authentifizierung arbeitet, zur Verwendung des {{site.data.keyword.amashort}}-Client-SDKs und verbinden Sie Ihre Anwendung mit {{site.data.keyword.Bluemix}}.

**Tipp:** Wenn Sie Ihre iOS-App mit Swift entwickeln, sollten Sie die Verwendung von {{site.data.keyword.amashort}}-Client-Swift-SDK in Erwägung ziehen. Die Anweisungen auf dieser Seite gelten für das {{site.data.keyword.amashort}}-Client-Objective-C-SDK. Anweisungen für die Verwendung des Swift-SDK finden Sie in [{{site.data.keyword.amashort}}-Client-SDK für iOS konfigurieren (Swift-SDK)](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-ios-swift-sdk.html).

## Vorbereitungen
{: #before-you-begin}
Sie müssen über eine Ressource verfügen, die durch eine Instanz des {{site.data.keyword.amashort}}-Service geschützt wird, die zur Verwendung eines angepassten Identitätsproviders konfiguriert ist.  Ihre mobile App muss außerdem mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sein.  Weitere Informationen finden Sie über die folgenden Links:
 * [Einführung in {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [iOS-Objective-C-SDK einrichten](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html)
 * [Angepassten Identitätsprovider verwenden](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Angepassten Identitätsprovider erstellen](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [{{site.data.keyword.amashort}} für die angepasste Authentifizierung konfigurieren](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)



## Client-SDK mit CocoaPods installieren
{: #custom-ios-sdk-cocoapods}
Verwenden Sie den CocoaPods-Abhängigkeitenmanager, um das {{site.data.keyword.amashort}}-Client-SDK zu installieren.

1. Öffnen Sie das Terminal und navigieren Sie zum Stammverzeichnis Ihres iOS-Projekts.

1. Bearbeiten Sie die `Podfile` und fügen Sie die folgende Zeile hinzu.

	```
	pod 'IMFCore'
	```

1. Führen Sie über die Befehlszeile den Befehl `pod install` aus.
CocoaPods installiert die hinzugefügten Abhängigkeiten. Der Fortschritt und die hinzugefügten Komponenten werden angezeigt.

**Wichtig**: Sie müssen Ihr Projekt jetzt über eine von CocoaPods generierte xcworkspace-Datei öffnen. In der Regel hat die Datei den Namen `{your-project-name}.xcworkspace`.

1. Führen Sie den Befehl `open {your-project-name}.xcworkspace` über die Befehlszeile aus, um Ihren iOS-Projektarbeitsbereich zu öffnen.



### Client-SDK initialisieren
{: #custom-ios-sdk-initialize}

Initialisieren Sie das SDK, indem Sie die Parameter für Route (`applicationRoute`) und GUID (`applicationGUID`) der Anwendung übergeben. Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode `application:didFinishLaunchingWithOptions` Ihres Anwendungsdelegats.

1. Ermitteln Sie Ihre Werte für die Anwendungsparameter. Öffnen Sie Ihre App im {{site.data.keyword.Bluemix_notm}}-Dashboard. Klicken Sie auf **Mobile Systemerweiterungen**, um die Werte für **Route** (`applicationRoute`) und **App-GUID** (`applicationGUID`) anzuzeigen.

1. Importieren Sie das Framework `IMFCore` in die Klasse, die das Client-SDK verwenden soll.

	Objective-C:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	```

	Swift:

	Das {{site.data.keyword.amashort}}-Client-SDK ist mit Objective-C implementiert. Sie müssen Ihrem Swift-Projekt möglicherweise einen Überbrückungsheader hinzufügen, um das SDK verwenden zu können.

	* Klicken Sie mit der rechten Maustaste auf Ihr Projekt in Xcode und wählen Sie **New File...** aus.
	* Wählen Sie in der Kategorie **iOS Source** die Option **Header file** aus. Geben Sie der Datei den Namen `BridgingHeader.h`.
	* Fügen Sie Ihrem Überbrückungsheader die Angabe `#import <IMFCore/IMFCore.h>` hinzu.
	* Klicken Sie auf Ihr Projekt in Xcode und wählen Sie die Registerkarte **Build Settings** (Buildeinstellungen) aus.
	* Suchen Sie nach `Objective-C Bridging Header`.
	* Setzen Sie den Wert auf die Position Ihrer Datei `BridgingHeader.h`. Beispiel: `$(SRCROOT)/MyApp/BridgingHeader.h`
	* Überprüfen Sie, ob Ihr Überbrückungsheader von Xcode beim Erstellen (Build) Ihres Projekts aufgenommen wird.

1. Initialisieren Sie das Client-SDK. Ersetzen Sie 'applicationRoute' und 'applicationGUID' durch die Werte für **Route** (`applicationRoute`) und **App-GUID** (`applicationGUID`), die Sie im Abschnitt **Mobile Systemerweiterungen** ermittelt haben.

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


## IMFAuthenticationHandler-Delegat
{: #custom-ios-sdk-authhandler}


Das {{site.data.keyword.amashort}}-Client-SDK stellt eine Schnittstelle `IMFAuthenticationHandler` zur Implementierung eines angepassten Authentifizierungsablaufs bereit. Die Schnittstelle `IMFAuthenticationHandler` macht drei Methoden verfügbar, die in verschiedenen Phasen des Authentifizierungsprozesses aufgerufen werden.

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
 						didReceiveAuthenticationChallenge:(NSDictionary*)challenge;
```

Diese Methode wird aufgerufen, wenn eine angepasste Authentifizierungsanforderung (Challenge) aus dem {{site.data.keyword.amashort}}-Service empfangen wird. Argumente:

* Das `IMFAuthenticationContext`-Protokoll wird vom {{site.data.keyword.amashort}}-Client-SDK bereitgestellt, sodass Entwickler Antworten auf Authentifizierungsanforderungen oder Fehler bei der Erfassung von Berechtigungsnachweisen (z. B. Abbruch durch den Benutzer) zurückmelden können.
* Das `NSDictionary`-Objekt, das eine angepasste Authentifizierungsanforderung enthält, wie sie durch einen angepassten Identitätsprovider zurückgegeben wird.

Durch Aufrufen der Methode `authenticationContext:didReceiveAuthenticationChallenge` delegiert das {{site.data.keyword.amashort}}-Client-SDK die Steuerung an den Entwickler und versetzt sich selbst in den Wartemodus für Berechtigungsnachweise. Es liegt in der Verantwortung des Entwicklers, Berechtigungsnachweise zu erfassen und diese durch eine der Methoden des `IMFAuthenticationContext`-Protokolls an das {{site.data.keyword.amashort}}-Client-SDK zurückzumelden, wie nachfolgend beschrieben.

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationSuccess:(NSDictionary *)userInfo;
```

Diese Methode wird nach einer erfolgreichen Authentifizierung aufgerufen. Die Argumente sind IMFAuthenticationContext und ein optionales NSDictionary-Objekt, das Informationen zum Authentifizierungserfolg enthält.

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationFailure:(NSDictionary*)userInfo;
```

Diese Methode wird nach einem Authentifizierungsfehler aufgerufen. Die Argumente sind IMFAuthenticationContext und ein optionales NSDictionary-Objekt, das Informationen zum Authentifizierungsfehler enthält.

## IMFAuthenticationContext-Protokoll
{: #custom-ios-sdk-authcontext}


`IMFAuthenticationContext` wird als Argument für die Methode `authenticationContext:didReceiveAuthenticationChallenge` eines angepassten `IMFAuthenticationHandler` angegeben. Es liegt in der Verantwortung des Entwicklers, Berechtigungsnachweise zu erfassen und diese durch die Methoden von `IMFAuthenticationContext` an das {{site.data.keyword.amashort}}-Client-SDK zurückgeben oder einen Fehler melden. Verwenden Sie eine der folgenden Methoden:

```
-(void) submitAuthenticationChallengeAnswer:(NSDictionary*) answer;

-(void) submitAuthenticationFailure:(NSDictionary*) userInfo;
```

## Beispielimplementierung eines angepassten IMFAuthenticationDelegate
{: #custom-ios-sdk-sample}


Das Beispiel für 'IMFAuthenticationDelegate' ist für die Ausführung mit dem Beispiel für einen angepassten Identitätsprovider gedacht. Sie können dieses Beispiel aus dem [Github-Repository](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample) herunterladen.

Objective-C:

``` Objective-C
CustomAuthenticationDelegate.h
-----------------------------------
#import <Foundation/Foundation.h>

@import IMFCore;
@interface CustomAuthenticationDelegate : NSObject <IMFAuthenticationDelegate>
@end


CustomAuthenticationDelegate.m
-----------------------------------
#import "CustomAuthenticationDelegate.h"

@implementation CustomAuthenticationDelegate

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationChallenge:(NSDictionary *)challenge{

	NSLog(@"didReceiveAuthenticationChallenge :: %@", challenge);

	// In diesem Beispiel gibt IMFAuthenticationDelegate sofort einen fest codierten
	// Satz von Berechtigungsnachweisen zurück. In einem realen Szenario würde der
	// Entwickler hier ein Anmeldefenster anzeigen, Berechtigungsnachweise erfassen
	// und die API [context submitAuthenticationChallengeAnswer:] aufrufen.

	NSDictionary *challengeAnswer = [NSDictionary dictionaryWithObjectsAndKeys:
									 @"john.lennon", @"username",
									 @"12345", @"password", nil];

	[context submitAuthenticationChallengeAnswer:challengeAnswer];

	// Im Fall eines Fehlers beim Erfassen von Berechtigungsnachweisen müssen
	// Sie dies an IMFAuthenticationContext zurückmelden. Andernfalls verbleibt
	// das Mobile Client Access-Client-SDK unbegrenzte Zeit in einem
	// Wartestatus für Berechtigungsnachweise.
}

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationSuccess:(NSDictionary *)userInfo{
	NSLog(@"didReceiveAuthenticationSuccess");


}

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationFailure:(NSDictionary *)userInfo{
	NSLog(@"didReceiveAuthenticationFailure");

}

@end
```

Swift-Implementierung:

```Swift
import Foundation

class CustomAuthenticationDelegate : NSObject, IMFAuthenticationDelegate{

	func authenticationContext(context: IMFAuthenticationContext!,
					didReceiveAuthenticationChallenge challenge: [NSObject : AnyObject]!) {

		NSLog("didReceiveAuthenticationChallenge :: %@", challenge)

		// In diesem Beispiel gibt IMFAuthenticationDelegate sofort einen fest codierten
	// Satz von Berechtigungsnachweisen zurück. In einem realen Szenario würde der
		// Entwickler hier ein Anmeldefenster anzeigen, Berechtigungsnachweise erfassen
		// und die API context.submitAuthenticationChallengeAnswer() aufrufen.

		let challengeAnswer: [String:String] = [
			"username":"john.lennon",
			"password":"12345"
		]

		context.submitAuthenticationChallengeAnswer(challengeAnswer)

		// Im Fall eines Fehlers beim Erfassen von Berechtigungsnachweisen müssen
 	// Sie dies an IMFAuthenticationContext zurückmelden. Andernfalls verbleibt
		// das Mobile Client Access-Client-SDK unbegrenzte Zeit in einem
		// Wartestatus für Berechtigungsnachweise.
	}


	func authenticationContext(context: IMFAuthenticationContext!,
					didReceiveAuthenticationSuccess userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationSuccess")
	}

	func authenticationContext(context: IMFAuthenticationContext!,
					didReceiveAuthenticationFailure userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationFailure")
	}
}
```

## Angepasstes 'IMFAuthenticationDelegate' registrieren

Nachdem Sie ein angepasstes Delegat 'IMFAuthenticationDelegate' erstellt haben, registrieren Sie es im `IMFClient`. Rufen Sie den folgenden Code in Ihrer Anwendung auf, bevor Sie Anforderungen an Ihre geschützten Ressourcen senden. Verwenden Sie den Wert für 'realmName', den Sie im {{site.data.keyword.amashort}}-Dashboard angegeben haben.

Objective-C-Anwendungen:

```Objective-C
[[IMFClient sharedInstance]
				registerAuthenticationDelegate:[CustomAuthenticationDelegate new]
										forRealm:realmName];
```

Swift-Anwendungen:
```Swift
IMFClient.sharedInstance().registerAuthenticationDelegate(CustomAuthenticationDelegate(),
									forRealm: realmName)
```




## Authentifizierung testen
{: #custom-ios-testing}
Nachdem Sie das Client-SDK initialisiert und ein angepasstes Delegat `IMFAuthenticationDelegate` registriert haben, können Sie mit dem Senden von Anforderungen an Ihr mobiles Back-End beginnen.

### Vorbereitungen
{: #custom-ios-testing-before}
 Sie müssen eine Anwendung, die mit der {{site.data.keyword.mobilefirstbp}}-Boilerplate erstellt wurde, sowie eine Ressource, die durch {{site.data.keyword.amashort}} geschützt wird, am Endpunkt `/protected` haben.

1. Senden Sie eine Anforderung an den geschützten Endpunkt Ihres mobilen Back-Ends in Ihrem Browser, indem Sie die Adresse `{applicationRoute}/protected` öffnen (z. B. `http://my-mobile-backend.mybluemix.net/protected`).
  Der Endpunkt `/protected` eines mobilen Back-Ends, das mit der {{site.data.keyword.mobilefirstbp}}-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Auf den Endpunkt können nur mobile Anwendungen zugreifen, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind. Daher wird eine Nachricht `Unauthorized` (Nicht autorisiert) in Ihrem Browser angezeigt.
1. Verwenden Sie Ihre iOS-Anwendung, um eine Anforderung an denselben Endpunkt zu senden. Fügen Sie den folgenden Code hinzu, nachdem Sie `BMSClient` initialisiert und Ihr angepasstes `IMFAuthenticationDelegate` registriert haben:

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
1. 	Wenn Ihre Anforderung erfolgreich ist, wird die folgende Ausgabe in der Xcode-Konsole angezeigt:

	![Bild](images/ios-custom-login-success.png)
	
	
	
	Durch Hinzufügen des folgenden Codes können Sie auch die Abmeldefunktion (logout) hinzufügen:

	Objective-C: 

	```Objective-C
	[[IMFAuthorizationManager sharedInstance] logout : callBack]
	```
	Swift: 

	```Swift
	IMFAuthorizationManager.sharedInstance().logout(callBack)
	```

Wenn Sie diesen Code aufrufen, nachdem sich ein Benutzer angemeldet hat, wird der Benutzer abgemeldet. Wenn der Benutzer versucht, sich wieder anzumelden, muss er auf die vom Server empfangene Anforderung erneut reagieren.
Die Übergabe von `callBack` an die Abmeldefunktion ist optional. Sie können auch `nil` übergeben.

