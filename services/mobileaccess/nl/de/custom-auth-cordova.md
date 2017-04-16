---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Angepasste Authentifizierung für {{site.data.keyword.amashort}}-Cordova-App konfigurieren
{: #custom-cordova}

Instrumentieren Sie die Cordova-Anwendung für die Verwendung der angepassten Authentifizierung und des {{site.data.keyword.amafull}}-Client-SDKs für den Zugriff auf die geschützte Anwendung.

## Vorbereitungen
{: #before-you-begin}
* Eine Ressource, die durch eine Instanz des {{site.data.keyword.amashort}}-Service geschützt wird, die zur Verwendung eines angepassten Identitätsproviders konfiguriert ist (siehe die Veröffentlichung zur [Konfiguration der angepassten Authentifizierung](custom-auth-config-mca.html)).  
* Der Wert für die Tenant-ID. Öffnen Sie den Service im {{site.data.keyword.amashort}}-Dashboard. Klicken Sie auf die Schaltfläche **Mobile Systemerweiterungen**. Im Feld **App-GUID/TenantId** wird der Wert `tenantId` (auch als `appGUID` bezeichnet) angezeigt. Sie benötigen diesen Wert für die Initialisierung von Authorization Manager.
* Der Realname. Dies ist der Wert, den Sie im Feld **Realmname** des Abschnitts **Angepasst** auf der Registerkarte **Management** des {{site.data.keyword.amashort}}-Dashboards angegeben haben.
* Die {{site.data.keyword.Bluemix_notm}}-**Region**. Ihre aktuelle {{site.data.keyword.Bluemix_notm}}-Region finden Sie im Header neben dem Symbol **Avatar** ![Avatarsymbol](images/face.jpg "Avatarsymbol"). Der angezeigte Regionswert muss einer der folgenden sein: `USA (Süden)`, `Vereinigtes Königreich` oder `Sydney`. Die genaue Syntax der entsprechenden SDK-Konstanten finden Sie in den Codebeispielen.

Weitere Informationen finden Sie über die folgenden Links:

 * [{{site.data.keyword.amashort}} für die angepasste Authentifizierung konfigurieren](custom-auth-config-mca.html). Hier erfahren Sie, wie Sie den {{site.data.keyword.amashort}}-Service für die angepasste Authentifizierung einrichten. Außerdem wird der Wert für **Realm** definiert.
 * [Cordova-SDK einrichten](getting-started-cordova.html). Hier finden Sie Informationen zur Einrichtung der Cordova-Client-App.
 * [Angepassten Identitätsprovider verwenden](custom-auth.html). Hier erfahren Sie, wie Sie Benutzer mit einem angepassten Identitätsprovider authentifizieren.
 * [Angepassten Identitätsprovider erstellen](custom-auth-identity-provider.html). Hier finden Sie einige Beispiele zur Funktionsweise eines angepassten Identitätsproviders.

## Cordova-WebView-Code konfigurieren
### {{site.data.keyword.amashort}}-Client-SDK im Cordova-WebView initialisieren
{: #custom-cordova-sdk}
Initialisieren Sie das SDK, indem Sie den Parameter `<applicationBluemixRegion>` in der Datei `index.js` übegeben.

```JavaScript
BMSClient.initialize("<applicationBluemixRegion>");
```
{: codeblock}

Ersetzen Sie `<applicationBluemixRegion>` durch Ihre Region (siehe [Vorbereitungen](#before-you-begin)).


### Schnittstelle 'AuthenticationListener'
{: #custom-cordva-auth}

Das {{site.data.keyword.amashort}}-Client-SDK stellt eine Schnittstelle für einen Authentifizierungslistener zur Implementierung eines angepassten Authentifizierungsablaufs bereit. Sie müssen die folgenden Methoden hinzufügen, die in verschiedenen Phasen eines Authentifizierungsprozesses aufgerufen werden.

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...},
	onAuthenticationSuccess: function(info){...},
	onAuthenticationFailure: function(info){...}
}
```
{: codeblock}

Jede Methode verarbeitet eine andere Phase eines Authentifizierungsprozesses.

### Methode 'onAuthenticationChallengeReceived'
{: #onAuthenticationChallengeReceived}
Diese Methode wird aufgerufen, wenn eine angepasste Authentifizierungsanforderung (Challenge) aus dem {{site.data.keyword.amashort}}-Service empfangen wird.
```JavaScript
onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...}
```
{: codeblock}

* `authenticationContext`: Wird vom {{site.data.keyword.amashort}}-Client-SDK bereitgestellt, sodass der Entwickler Antworten auf Authentifizierungsanforderungen oder Fehler, die bei der Erfassung von Berechtigungsnachweisen auftreten, wie zum Beispiel, ein Abbruch der Authentifizierungsanforderung durch den Benutzer, zurückmelden kann.
* `challenge`: Ein JSON-Objekt, das eine angepasste Authentifizierungsanforderung enthält, wie sie durch einen angepassten Identitätsprovider zurückgegeben wird.

Durch das Aufrufen der Methode `onAuthenticationChallengeReceived` delegiert das {{site.data.keyword.amashort}}-Client-SDK die Steuerung an den Entwickler. Der {{site.data.keyword.amashort}}-Service wartet auf Berechtigungsnachweise. Der Entwickler muss Berechtigungsnachweise erfassen und durch eine der folgenden Methoden der Schnittstelle `authContext` an das {{site.data.keyword.amashort}}-Client-SDK zurückmelden.

```JavaScript
onAuthenticationSuccess: function(info){...}
```
{: codeblock}

Diese Methode wird nach einer erfolgreichen Authentifizierung aufgerufen. Die Argumente umfassen ein optionales JSON-Objekt, das erweiterte Informationen zu dem Authentifizierungserfolg enthält.

```JavaScript
onAuthenticationFailure: function(info){...}
```
{: codeblock}

Diese Methode wird nach einem Authentifizierungsfehler aufgerufen. Die Argumente umfassen ein optionales JSON-Objekt, das erweiterte Informationen zu dem Authentifizierungsfehler enthält.

### authenticationContext
{: #custom-cordova-authcontext}

Der Wert von `authenticationContext` wird als Argument für die Methode `onAuthenticationChallengeReceived` eines angepassten Authentifizierungslisteners bereitgestellt. Der Entwickler muss Berechtigungsnachweise erfassen und durch die Methoden der Schnittstelle `authenticationContext` an das {{site.data.keyword.amashort}}-Client-SDK zurückgeben oder einen Fehler melden. Verwenden Sie eine der folgenden Methoden:

```JavaScript
authenticationContext.submitAuthenticationChallengeAnswer(challengeAnswer);
```
{: codeblock}

```JavaScript
authenticationContext.submitAuthenticationFailure(info);
```
{: codeblock}

Der folgende Code zeigt, wie ein Authentifizierungslistener eines Kunden Berechtigungsnachweise erfassen, Anforderungen (Challenges) verarbeiten und Authentifizierungsantworten bereitstellen kann.

## Workflow für die Beispielimplementierung eines angepassten Authentifizierungslisteners
{: #custom-cordova-authlisten-sample}

Dieses Beispiel für einen Authentifizierungslistener ist für die Ausführung mit einem angepassten Identitätsprovider gedacht. Sie können den angepassten Identitätsprovider aus [diesem Github-Repository ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "Symbol für externen Link"){: new_window} herunterladen.

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {
		console.log("onAuthenticationChallengeReceived :: ", challenge);

		// In diesem Beispiel gibt der Authentifizierungslistener sofort einen fest codierten
		// Satz von Berechtigungsnachweisen zurück. In einem realen Szenario würde der
		// Entwickler hier ein Anmeldefenster anzeigen, Berechtigungsnachweise erfassen
		// und die API authenticationContext.submitAuthenticationChallengeAnswer() aufrufen.

		var challengeResponse = {
			username: "john.lennon",
			password: "12345"
		}

		authenticationContext.submitAuthenticationChallengeAnswer(challengeResponse);

		// Im Fall eines Fehlers beim Erfassen von Berechtigungsnachweisen müssen
		// Sie dies an authenticationContext zurückmelden. Andernfalls verbleibt
		// das Mobile Client Access-Client-SDK unbegrenzte Zeit in einem
		// Wartestatus für Berechtigungsnachweise.

	},

	onAuthenticationSuccess: function(info){
		console.log("onAuthenticationSuccess :: ", info);
	},

	onAuthenticationFailure: function(info){
		console.log("onAuthenticationFailure :: ", info);
	}
}
```
{: codeblock}

## Angepassten Authentifizierungslistener im Cordova-WebView registrieren
{: #custom-cordova-authreg}

Nach dem Erstellen eines angepassten Authentifizierungslisteners müssen Sie diesen in `BMSClient` registrieren, bevor Sie mit seiner Verwendung beginnen. Fügen Sie Ihrer Anwendung den folgenden Code hinzu.  Rufen Sie diesen Code auf, bevor Sie Anforderungen an Ihre geschützten Ressourcen senden.

```Java
BMSClient.registerAuthenticationListener(<realmName>, customAuthenticationListener);
```
{: codeblock}
 Verwenden Sie den Wert für `realmName`, den Sie im {{site.data.keyword.amashort}}-Dashboard angegeben haben.

## Authorization Manager im nativen Code angeben

{{site.data.keyword.amashort}} Authorization Manager muss in Ihrem nativen Plattformcode registriert werden.

**Android** (zu `onCreate` in der Hauptaktivität hinzufügen)

```
String tenantId = "<tenantId>";
MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
```
{: codeblock}

**iOS Objective-C** (zu `AppDelegate.m` hinzufügen)

Registrieren Sie Authorization Manager gemäß Ihrer Version von Xcode hinzu.

```
# import "<your_module_name>-Swift.h"

- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

{  

    //[CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];
 }
```
{: codeblock}

Hinweis: Um den korrekten Namen für die Swift-Headerdatei zu erhalten, ersetzen Sie `your_module_name` durch den Modulnamen Ihres Projekts. Wenn der Modulname beispielsweise `Cordova` ist, sollte der Code `#import "Cordova-Swift.h"` lauten. Um nach dem Modulnamen zu suchen, wechseln Sie zu **Build Settings > Packagin` > Product Module Name**.

**Hinweis:** Ersetzen Sie `tenantId` durch Ihre Tenant-ID aus **Mobile Systemerweiterungen** im {{site.data.keyword.amashort}}-Service-Dashboard.


## Gemeinsame Nutzung der Schlüsselkette (Keychain) für iOS aktivieren

Aktivieren Sie `Keychain Sharing`, indem Sie die Registerkarte `Capabilities` aufrufen und `Keychain Sharing` in Ihrem Xcode-Projekt auf `On` setzen.


## Authentifizierung testen
{: #custom-cordova-test}
Nach der Initialisierung des Client-SDK und der Registrierung der angepassten Schnittstelle `AuthenticationListener` können Sie mit dem Senden von Anforderungen an Ihre mobile Back-End-Anwendung beginnen.

### Vorbereitungen
{: #custom-cordova-testing-before}
Sie müssen eine Anwendung, die mit der {{site.data.keyword.mobilefirstbp}}-Boilerplate erstellt wurde, sowie eine Ressource, die durch {{site.data.keyword.amashort}} geschützt wird, am Endpunkt `/protected` haben.


1. Senden Sie eine Anforderung an den geschützten Endpunkt Ihrer mobilen Back-End-Anwendung in Ihrem Browser, indem Sie die Adresse `{applicationRoute}/protected` öffnen (z. B. `http://my-mobile-backend.mybluemix.net/protected`).
 Der Endpunkt `/protected` einer mobilen Back-End-Anwendung, die mit der {{site.data.keyword.mobilefirstbp}}-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Auf den Endpunkt können nur mobile Anwendungen zugreifen, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind. Daher wird eine Nachricht `Unauthorized` (Nicht autorisiert) in Ihrem Browser angezeigt.

1. Senden Sie eine Anforderung über Ihre Cordova-Anwendung an denselben Endpunkt. Fügen Sie den folgenden Code hinzu, nachdem Sie `BMSClient` initialisiert und Ihre angepasste Schnittstelle 'AuthenticationListener' registriert haben.

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

	Ersetzen Sie `<your-application-route>` durch die URL Ihrer Back-End-Anwendung (siehe [Vorbereitungen](#before-you-begin)).

1. 	Wenn Ihre Anforderung erfolgreich ist, wird die folgende Ausgabe in der `LogCat`- oder Xcode-Konsole angezeigt:

	![Bild](images/android-custom-login-success.png)

	![Bild](images/ios-custom-login-success.png)
