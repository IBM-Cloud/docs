---

copyright:
  years: 2015, 2016

---

# {{site.data.keyword.amashort}}-Client-SDK für Cordova konfigurieren
{: #custom-cordova}
Konfigurieren Sie Ihre Cordova-Anwendung, die mit der angepassten Authentifizierung arbeitet, zur Verwendung des {{site.data.keyword.amashort}}-Client-SDKs und verbinden Sie Ihre Anwendung mit {{site.data.keyword.Bluemix}}.


## Vorbereitungen
{: #before-you-begin}
Sie müssen über eine Ressource verfügen, die durch eine Instanz des {{site.data.keyword.amashort}}-Service geschützt wird, die zur Verwendung eines angepassten Identitätsproviders konfiguriert ist.  Ihre mobile App muss außerdem mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sein.  Weitere Informationen finden Sie über die folgenden Links:
 * [Einführung in {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Cordova-SDK einrichten](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)
 * [Angepassten Identitätsprovider verwenden](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Angepassten Identitätsprovider erstellen](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [{{site.data.keyword.amashort}} für die angepasste Authentifizierung konfigurieren](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)

## {{site.data.keyword.amashort}}-Client-SDK initialisieren
{: #custom-cordova-sdk}
Initialisieren Sie das SDK, indem Sie die Parameter 'applicationGUID' und 'applicationRoute' übergeben.

1. Ermitteln Sie Ihre Werte für die Anwendungsparameter. Öffnen Sie Ihre App im {{site.data.keyword.Bluemix_notm}}-Dashboard. Klicken Sie auf **Mobile Systemerweiterungen**. Die Werte für **Route** (`applicationRoute`) und **App-GUID** (`applicationGUID`) werden angezeigt.
1. Initialisieren Sie das Client-SDK.

	```JavaScript
	BMSClient.initialize(applicationRoute, applicationGUID);

	```
 Ersetzen Sie *applicationRoute* und *applicationGUID* durch die Werte für **Route** und **App-GUID** aus der Anzeige **Mobile Systemerweiterungen** Ihrer Anwendung im {{site.data.keyword.Bluemix_notm}}-Dashboard.

## Schnittstelle 'AuthenticationListener'
{: #custom-cordva-auth}

Das {{site.data.keyword.amashort}}-Client-SDK stellt eine Schnittstelle für einen Authentifizierungslistener zur Implementierung eines angepassten Authentifizierungsablaufs bereit. Sie müssen die folgenden Methoden hinzufügen, die in verschiedenen Phasen eines Authentifizierungsprozesses aufgerufen werden.

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...},
	onAuthenticationSuccess: function(info){...},
	onAuthenticationFailure: function(info){...}
}
```

Jede Methode verarbeitet eine andere Phase eines Authentifizierungsprozesses.

### Methode 'onAuthenticationChallengeReceived'
{: #onAuthenticationChallengeReceived}
Diese Methode wird aufgerufen, wenn eine angepasste Authentifizierungsanforderung (Challenge) aus dem {{site.data.keyword.amashort}}-Service empfangen wird.
```JavaScript
onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...}
```

#### Argumente
{: #onAuthenticationChallengeReceived-args}
* `authenticationContext`: Wird vom {{site.data.keyword.amashort}}-Client-SDK bereitgestellt, sodass der Entwickler Antworten auf Authentifizierungsanforderungen oder Fehler, die bei der Erfassung von Berechtigungsnachweisen auftreten, wie zum Beispiel, ein Abbruch der Authentifizierungsanforderung durch den Benutzer, zurückmelden kann.
* `challenge`: Ein JSON-Objekt, das eine angepasste Authentifizierungsanforderung enthält, wie sie durch einen angepassten Identitätsprovider zurückgegeben wird.

Durch das Aufrufen der Methode `onAuthenticationChallengeReceived` delegiert das {{site.data.keyword.amashort}}-Client-SDK die Steuerung an den Entwickler. Der {{site.data.keyword.amashort}}-Service wartet auf Berechtigungsnachweise. Der Entwickler muss Berechtigungsnachweise erfassen und durch eine der folgenden Methoden der Schnittstelle `authContext` an das {{site.data.keyword.amashort}}-Client-SDK zurückmelden.

```JavaScript
onAuthenticationSuccess: function(info){...}
```

Diese Methode wird nach einer erfolgreichen Authentifizierung aufgerufen. Die Argumente sind ein optionales JSONObject, das erweiterte Informationen zu dem Authentifizierungserfolg enthält.

```JavaScript
onAuthenticationFailure: function(info){...}
```

Diese Methode wird nach einem Authentifizierungsfehler aufgerufen. Die Argumente sind ein optionales JSONObject, das erweiterte Informationen zu dem Authentifizierungsfehler enthält.

## authenticationContext
{: #custom-cordova-authcontext}

Der Wert von `authenticationContext` wird als Argument für die Methode `onAuthenticationChallengeReceived` eines angepassten Authentifizierungslisteners bereitgestellt. Der Entwickler muss Berechtigungsnachweise erfassen und durch die Methoden der Schnittstelle `authenticationContext` an das {{site.data.keyword.amashort}}-Client-SDK zurückgeben oder einen Fehler melden. Verwenden Sie eine der folgenden Methoden:

```JavaScript
authenticationContext.submitAuthenticationChallengeAnswer(challengeAnswer);

authenticationContext.submitAuthenticationFailure(info);
```

## Beispielimplementierung eines angepassten Authentifizierungslisteners
{: #custom-cordova-authlisten-sample}

Dieses Beispiel für einen Authentifizierungslistener ist für die Ausführung mit einem angepassten Identitätsprovider gedacht. Sie können den angepassten Identitätsprovider aus [diesem Github-Repository](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample) herunterladen.

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

## Angepassten Authentifizierungslistener registrieren
{: #custom-cordova-authreg}

Nach dem Erstellen eines angepassten Authentifizierungslisteners registrieren Sie diesen in `BMSClient`, bevor Sie mit seiner Verwendung beginnen. Fügen Sie Ihrer Anwendung den folgenden Code hinzu.  Rufen Sie diesen Code auf, bevor Sie Anforderungen an Ihre geschützten Ressourcen senden.

```Java
BMSClient.registerAuthenticationListener(realmName, customAuthenticationListener);
```
 Verwenden Sie den Wert für *realmName*, den Sie im {{site.data.keyword.amashort}}-Dashboard angegeben haben.


## Authentifizierung testen
{: #custom-cordova-test}
Nach der Initialisierung des Client-SDK und der Registrierung der angepassten Schnittstelle 'AuthenticationListener' können Sie mit dem Senden von Anforderungen an Ihr mobiles Back-End beginnen.

### Vorbereitungen
{: #custom-cordova-testing-before}
Sie müssen eine Anwendung, die mit der {{site.data.keyword.mobilefirstbp}}-Boilerplate erstellt wurde, sowie eine Ressource, die durch {{site.data.keyword.amashort}} geschützt wird, am Endpunkt `/protected` haben.


1. Senden Sie eine Anforderung an den geschützten Endpunkt Ihres mobilen Back-Ends in Ihrem Browser, indem Sie die Adresse `{applicationRoute}/protected` öffnen (z. B. `http://my-mobile-backend.mybluemix.net/protected`).
 Der Endpunkt `/protected` eines mobilen Back-Ends, das mit der {{site.data.keyword.mobilefirstbp}}-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Auf den Endpunkt können nur mobile Anwendungen zugreifen, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind. Daher wird eine Nachricht `Unauthorized` (Nicht autorisiert) in Ihrem Browser angezeigt.

1. Senden Sie eine Anforderung über Ihre Cordova-Anwendung an denselben Endpunkt. Fügen Sie den folgenden Code hinzu, nachdem Sie `BMSClient` initialisiert und Ihre angepasste Schnittstelle 'AuthenticationListener' registriert haben.

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new MFPRequest("/protected", MFPRequest.GET);
	request.send(success, failure);
	```

1. 	Wenn Ihre Anforderung erfolgreich ist, wird die folgende Ausgabe in der LogCat- oder Xcode-Konsole angezeigt:

	![Bild](images/android-custom-login-success.png)

	![Bild](images/ios-custom-login-success.png)
