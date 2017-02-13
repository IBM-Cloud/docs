---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Google-Authentifizierung für Cordova-Apps aktivieren
{: #google-auth-cordova}

Um Ihre {{site.data.keyword.amafull}}-Cordova-Anwendungen für die Google-Authentifizierung zu integrieren, müssen Sie Änderungen am nativen Plattformcode (Java oder Objective-C) der Cordova-Anwendung sowie im Cordova-WebView (JavaScript) vornehmen. Jede Plattform muss separat konfiguriert werden. Verwenden Sie die native Entwicklungsumgebung, um Änderungen an nativem Code vorzunehmen, wie zum Beispiel Android Studio oder Xcode.

## Vorbereitungen
{: #before-you-begin}

Voraussetzungen:

* Cordova-Projekt, das mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert ist.  Weitere Informationen finden Sie in [Cordova-Plug-in einrichten](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html).  
* Instanz einer {{site.data.keyword.Bluemix_notm}}-Anwendung, die durch den {{site.data.keyword.amashort}}-Service geschützt ist. Weitere Informationen zur Erstellung eines {{site.data.keyword.Bluemix_notm}}-Back-End-Service finden Sie in der [Einführung](index.html).
* Anwendungsroute. Dies ist die URL Ihrer Back-End-Anwendung.
* **Tenant-ID**. Öffnen Sie den Service im {{site.data.keyword.Bluemix_notm}}-Dashboard. Klicken Sie auf **Mobile Systemerweiterungen**. Im Feld **App-GUID/TenantId** wird der Wert `tenantId` (auch als `appGUID` bezeichnet) angezeigt. Sie benötigen diesen Wert für die Initialisierung von Authorization Manager.
*  Suchen Sie die Region, in der Ihre {{site.data.keyword.Bluemix_notm}}-Anwendung gehostet wird. Ihre aktuelle Bluemix-Region finden Sie im Header neben dem Symbol **Avatar** ![Avatarsymbol](images/face.jpg "Avatarsymbol"). Der Regionswert muss einer der folgenden sein: **USA (Süden)**, **Sydney** oder **Vereinigtes Königreich**. Die genauen konstanten Werte des SDK, die diesen Namen entsprechen, sind in den Codebeispielen angegeben.
* (Optional) Machen Sie sich mit den folgenden Abschnitten vertraut:
   * [Google-Authentifizierung für Android-Apps aktivieren](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)
   * [Google-Authentifizierung für iOS-Apps aktivieren](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html)


## Android-Plattform konfigurieren
{: #google-auth-cordova-android}

Die Schritte, die zur Konfiguration der Android-Plattform einer Cordova-Anwendung für die Google-Authentifizierung erforderlich sind, sind den Schritten, die für native Anwendungen erforderlich sind, sehr ähnlich. Weitere Informationen finden Sie in [Google-Authentifizierung in Android-Apps aktivieren](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html); richten Sie Folgendes ein:

   * [Projekt in Google Developer Console erstellen](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html#create-google-project). Hier erfahren Sie, wie Sie den Authentifizierungsservice auf der Google Developers-Website einrichten.
   * [MCA für die Google-Authentifizierung konfigurieren](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html#google-auth-android-config). Hier erfahren Sie, wie Sie {{site.data.keyword.amashort}} für die Google-Authentifizierung einrichten.

### {{site.data.keyword.amashort}}-Client-SDK fur Android (Cordova) konfigurieren

1. Öffnen Sie in Ihrem Android-Projektordner die Datei `build.gradle` für das Anwendungsmodul (**nicht** die Projektdatei `build.gradle`).
	Suchen Sie den Abschnitt für Abhängigkeiten ('dependencies') und fügen Sie eine neue Abhängigkeit 'compile' für das Client-SDK hinzu:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',
        name:'googleauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// andere Abhängigkeiten
	}
	```
	{: codeblock}

1. Synchronisieren Sie Ihr Projekt mit Gradle, indem Sie auf **Tools > Android > Sync Project with Gradle Files** klicken.

1. Die API `GoogleAuthenticationManager` muss trotzdem in Ihrem nativen Code registriert werden. Fügen Sie diesen Code zur Methode `onCreate` für Hauptaktivitäten hinzu:

	```Java
	String tenantId = "<tenantId>";
	MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
	BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
	GoogleAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
	```
	{: codeblock}

1. Fügen Sie Ihrer Aktivität den folgenden Code hinzu:

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		GoogleAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}

## iOS-Plattform konfigurieren
{: #google-auth-cordova-ios}

Die Schritte, die zur Konfiguration der iOS-Plattform einer Cordova-Anwendung für die Integration der Google-Authentifizierung erforderlich sind, sind den Schritten für native Anwendungen ähnlich. Der Hauptunterschied besteht darin, dass die Cordova-CLI gegenwärtig den CocoaPods-Abhängigkeitenmanager nicht unterstützt. Sie müssen die erforderlichen Dateien für die Integration in die Google-Authentifizierung manuell hinzufügen. Weitere Informationen finden Sie in [Google-Authentifizierung für iOS-Apps aktivieren (Swift-SDK)](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html). Führen Sie die folgenden Schritte aus:

   * [App für Google-Anmeldung vorbereiten](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-sign-in-ios): Bereitet die Google-Anmeldung für die Authentifizierung von {{site.data.keyword.amashort}}-iOS-Anwendungen vor.

   * [MCA für die Google-Authentifizierung konfigurieren](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-auth-ios-config): Konfiguriert den {{site.data.keyword.amashort}}-Service für die Verwendung mit der Google-Anmeldung.

   * [MCA-Client-SDK für iOS konfigurieren](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-auth-ios-sdk): Konfiguriert den {{site.data.keyword.amashort}}-Client für die Verwendung mit der Google-Anmeldung.


### Gemeinsame Nutzung der Schlüsselkette (Keychain) für iOS aktivieren
{: #enable_keychain}

Aktivieren Sie `Keychain Sharing`. Rufen Sie dazu die Registerkarte `Capabilities` auf und setzen Sie `Keychain Sharing` in Ihrem Xcode-Projekt auf `On`.


### Authorization Manager im iOS-Code initialisieren

Initialisieren Sie {{site.data.keyword.amashort}} Authorization Manager in Objective-C in der Datei `AppDelgate.m`.

```
#import "<your_module_name>-Swift.h"

- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

{
	[CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];

	[[GoogleAuthenticationManager sharedInstance] register];

	self.viewController = [[MainViewController alloc] init];

	[[GoogleAuthenticationManager sharedInstance] onFinishLaunchingWithApplication:application withOptions:launchOptions];

	return [super application:application didFinishLaunchingWithOptions:launchOptions];
}

- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url
					sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {
	return [[GoogleAuthenticationManager sharedInstance] onOpenURLWithApplication:application url:url 
	sourceApplication:sourceApplication annotation:annotation];
}
```
{: codeblock}

**Hinweis:**

* Ersetzen Sie `<ihr_modulname>` mit dem Modulnamen des Projekts. Wenn beispielsweise der Modulname `Cordova` ist, sollte die Importzeile `#import "Cordova-Swift.h"` lauten. Suchen Sie den Modulnamen und wechseln Sie zu
`Build Settings`, `Packaging` > `Product Module Name`.
* Ersetzen Sie `<tenantId>` durch Ihre Tenant-ID (siehe [Vorbereitungen](#before-you-begin)).


## {{site.data.keyword.amashort}}-Client-SDK im Cordova-WebView initialisieren
{: #google-auth-cordova-initialize}

Verwenden Sie für alle Plattformen den folgenden JavaScript-Code in Ihrer Cordova-Anwendung, um das {{site.data.keyword.amashort}}-Client-SDK zu initialisieren.

```JavaScript
BMSClient.initialize("<applicationBluemixRegion>");
```
{: codeblock}

Ersetzen Sie `<applicationBluemixRegion>` durch Ihre Region (siehe [Vorbereitungen](#before-you-begin)).

## Authentifizierung testen
{: #google-auth-cordova-test}

Nach der Initialisierung des Client-SDK können Sie mit dem Senden von Anforderungen an Ihre mobile Back-End-Anwendung beginnen.

### Vorbereitungen
{: #google-auth-cordova-testing-before}

Sie müssen über eine Back-End-Anwendung verfügen, die durch {{site.data.keyword.amashort}} am Endpunkt `/protected` geschützt wird. Wenn Sie einen Endpunkt `/protected` einrichten müssen, finden Sie weitere Informationen in [Ressourcen schützen](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Versuchen Sie, in Ihrem Desktop-Browser eine Anforderung an den geschützten Endpunkt Ihrer mobilen Back-End-Anwendung zu senden, indem Sie `{applicationRoute}/protected` öffnen (z. B. `http://my-mobile-backend.mybluemix.net/protected`).

1. Der Endpunkt `/protected` einer mobilen Back-End-Anwendung, die mit der MobileFirst Services-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Deshalb kann auf ihn nur mit mobilen Anwendungen zugegriffen werden, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert wurden. Infolgedessen wird eine Nachricht `Unauthorized` (Nicht autorisiert) in Ihrem Desktop-Browser angezeigt.

1. Verwenden Sie Ihre Cordova-Anwendung, um eine Anforderung an denselben Endpunkt zu senden. Verwenden Sie dabei die vollständige URL (z. B. `http://my-mobile-backend.mybluemix.net/protected`). Fügen Sie den folgenden Code hinzu, nachdem Sie `BMSClient` initialisiert haben.

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new BMSRequest("<your-application-route>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}

1. Führen Sie Ihre Anwendung aus. Die Google-Anmeldeanzeige wird geöffnet.

	![Google-Anmeldebildschirm](images/android-google-login.png)

	![Google-Anmeldebildschirm](images/ios-google-login.png)

	Diese Anzeige sieht möglicherweise geringfügig anders aus, wenn Sie die Facebook-App nicht auf Ihrem Gerät installiert haben oder wenn Sie zurzeit nicht bei Facebook angemeldet sind.

1. Indem Sie auf **OK** klicken, berechtigen Sie {{site.data.keyword.amashort}}, Ihre Google-Benutzeridentität zu Authentifizierungszwecken zu nutzen.

1. Ihre Anforderung sollte erfolgreich ausgeführt werden. Abhängig von der verwendeten Plattform sollte die folgende Ausgabe in der LogCat/Xcode-Konsole angezeigt werden:

	![Code-Snippet von Android](images/android-google-login-success.png)

	![Code-Snippet von iOS](images/ios-google-login-success.png)
