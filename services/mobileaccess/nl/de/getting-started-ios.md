---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"

---
{:shortdesc: .shortdesc}

# iOS-Objective-C-SDK einrichten
{: #getting-started-ios}

Instrumentieren Sie Ihre iOS-Anwendung mit dem {{site.data.keyword.amafull}}-SDK, initialisieren Sie das SDK und senden Sie Anforderungen an geschützte und nicht geschützte Ressourcen.

{:shortdesc}

**Wichtig:** Das Objective-C-SDK wird zwar weiterhin vollständig unterstützt und gilt noch als primäres SDK für {{site.data.keyword.Bluemix_notm}} Mobile Services, die Verwendung und Unterstützung dieses SDK sollen jedoch zugunsten des neuen Swift-SDK noch dieses Jahr eingestellt werden. Für neue Anwendungen wird dringend die Verwendung von Swift-SDK empfohlen (Informationen dazu siehe [iOS-Swift-SDK einrichten](getting-started-ios-swift-sdk.html)).

## Vorbereitungen
{: #before-you-begin}
Voraussetzungen:
* Instanz einer {{site.data.keyword.Bluemix_notm}}-Anwendung, die durch den {{site.data.keyword.amashort}}-Service geschützt ist. Weitere Informationen zur Erstellung einer {{site.data.keyword.Bluemix_notm}}-Back-End-Anwendung finden Sie in der [Einführung](index.html).
* **Tenant-ID**. Öffnen Sie den Service im {{site.data.keyword.amashort}}-Dashboard. Klicken Sie auf **Mobile Systemerweiterungen**. Im Feld **App-GUID/TenantId** wird der Wert `tenantId` (auch als `appGUID` bezeichnet) angezeigt. Sie benötigen diesen Wert für die Initialisierung von {{site.data.keyword.amashort}} Authorization Manager.
* **Anwendungsroute**. Dies ist die URL Ihrer Back-End-Anwendung. Sie benötigen diesen Wert zum Senden von Anforderungen an die geschützten Endpunkte der Anwendung.
* Xcode-Projekt  


## {{site.data.keyword.amashort}}-Client-SDK installieren
{: #install-mca-sdk-ios}
Das {{site.data.keyword.amashort}}-SDK wird mit CocoaPods, einem Abhängigkeitenmanager für iOS-Projekte, verteilt. CocoaPods lädt automatisch Artefakte aus Repositorys herunter und stellt sie für Ihre iOS-Anwendung zur Verfügung.


### CocoaPods installieren
{: #install-cocoapods}

1. Öffnen Sie das Terminal und führen Sie den Befehl **pod --version** aus. Wenn CocoaPods bereits installiert ist, wird die Versionsnummer angezeigt. Fahren Sie mit dem nächsten Abschnitt fort, um das SDK zu installieren.

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


	`pod 'IMFCore'`

1. Speichern Sie die `Podfile`-Datei und führen Sie den Befehl `pod install` über die Befehlszeile aus. <br/>Cocoapods installiert hinzugefügte Abhängigkeiten und zeigt die hinzugefügten Komponenten an.<br/>

	**Wichtig**: CocoaPods generiert eine Datei `xcworkspace`.  Sie müssen diese Datei öffnen, um mit Ihrem Projekt in Zukunft arbeiten zu können.

1. Öffnen Sie Ihren iOS-Projektarbeitsbereich. Öffnen Sie die `xcworkspace`-Datei, die von CocoaPods generiert wurde. Beispiel: `{your-project-name}.xcworkspace`. Führen Sie den Befehl `open {your-project-name}.xcworkspace` aus.

## {{site.data.keyword.amashort}}-Client-SDK initialisieren
{: #init-mca-sdk-ios}

1. Importieren Sie das Framework `IMFCore` in die Klasse, in der Sie das {{site.data.keyword.amashort}}-Client-SDK verwenden möchten, indem Sie den folgenden Header hinzufügen:

	####Objective-C
	{: #imfcore-objc}

	```Objective-C
	  #import <IMFCore/IMFCore.h>
	```

	####Swift
	{: #sdk-swift}

	Das {{site.data.keyword.amashort}}-Client-SDK ist mit Objective-C implementiert. Sie müssen Ihrem Swift-Projekt möglicherweise einen Überbrückungsheader hinzufügen:
	1. Klicken Sie mit der rechten Maustaste auf Ihr Projekt in Xcode und wählen Sie **New File** aus.
	1. Wählen Sie in der Kategorie **iOS Source** die Option **Header file** aus. Geben Sie der Datei den Namen `BridgingHeader.h`.
	1. Fügen Sie Ihrem Überbrückungsheader die folgende Zeile hinzu: `#import <IMFCore/IMFCore.h>`.
	1. Klicken Sie auf Ihr Projekt in Xcode und wählen Sie die Registerkarte **Build Settings**aus.
	1. Suchen Sie nach `Objective-C Bridging Header`.
	1. Setzen Sie den Wert auf die Position Ihrer Datei `BridgingHeader.h`. Beispiel: `$(SRCROOT)/MyApp/BridgingHeader.h`.
	1. Stellen Sie sicher, dass Ihr Überbrückungsheader von Xcode aufgenommen wird, indem Sie Ihr Projekt erstellen (Build). Dabei sollten keine Fehlernachrichten angezeigt werden.

1. Verwenden Sie den folgenden Code, um das {{site.data.keyword.amashort}}-Client-SDK zu initialisieren.  Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode `application:didFinishLaunchingWithOptions` Ihres Anwendungsdelegats. <br/>
Informationen zum Abrufen der Werte für `applicationRoute` und `applicationGUID` finden Sie unter [Vorbereitungen](#before-you-begin). 

	####Objective-C
	{: #sharedinstance-objc}

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	####Swift
	{: #sharedinstance-swift}
	```Swift
 		MFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",backendGUID: "applicationGUID")
	```

## AuthorizationManager initialisieren
Initialisieren Sie den `AuthorizationManager` durch Übergeben des Parameters `tenantId` des {{site.data.keyword.amashort}}-Service. Informationen zum Abrufen dieser Werte finden Sie unter [Vorbereitungen](#before-you-begin). 

#### Objective-C

```Objective-C
[[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"<tenantId>"];
```

#### Swift

```Swift
IMFAuthorizationManager.sharedInstance().initializeWithTenantId("<tenantId>")
```

	
## Anforderung an mobile Back-End-Anwendung senden
{: #request}

Nach der Initialisierung des {{site.data.keyword.amashort}}-Client-SDK können Sie mit dem Senden von Anforderungen an Ihre mobile Back-End-Anwendung beginnen.

1. Versuchen Sie, in Ihrem Browser eine Anforderung an einen geschützten Endpunkt in Ihrer mobilen Back-End-Anwendung zu senden. Öffnen Sie die folgende URL: `{applicationRoute}/protected`. Beispiel: `http://my-mobile-backend.mybluemix.net/protected`
<br/>Der Endpunkt `/protected` einer mobilen Back-End-Anwendung, die mit der MobileFirst Services Starter-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Eine Nachricht des Typs `Unauthorized` (Nicht autorisiert) wird in Ihrem Browser zurückgegeben, weil auf diesen Endpunkt nur mobile Anwendungen zugreifen können, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind.

1. Verwenden Sie Ihre iOS-Anwendung, um eine Anforderung an denselben Endpunkt zu senden. Fügen Sie den folgenden Code hinzu, nachdem Sie `IMFClient` initialisiert haben:

	####Objective-C
	{: #nsstring-objc}

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
		}
	}];
	```

	####Swift
	{: #imfclientrequestpath-swift}

	```Swift
	let requestPath = IMFClient.sharedInstance().backendRoute + "/protected"

	let request = IMFResourceRequest(path: requestPath, method: "GET");
	request.sendWithCompletionHandler { (response, error) -> Void in
		if (nil != error){
			NSLog("Error :: %@", error.description)
		} else {
			NSLog("Response :: %@", response.responseText)
		}
	};

	```

1.  Wenn Ihre Anforderung erfolgreich ist, wird die folgende Ausgabe in der Xcode-Konsole angezeigt:

	![Bild](images/getting-started-ios-success.png)

## Nächste Schritte
{: #next-steps}
Wenn Sie eine Verbindung zu dem geschützten Endpunkt hergestellt haben, waren keine Berechtigungsnachweise erforderlich. Wenn Sie die Benutzer zur Anmeldung bei Ihrer Anwendung veranlassen wollen, müssen Sie eine Authentifizierung über Facebook oder Google oder eine angepasste Authentifizierung konfigurieren.
  * [Facebook](facebook-auth-ios.html)
  * [Google](google-auth-ios.html)
  * [Angepasst](custom-auth-ios.html)
