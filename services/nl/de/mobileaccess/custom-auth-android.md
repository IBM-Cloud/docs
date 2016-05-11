---

copyright:
  years: 2015, 2016

---

# {{site.data.keyword.amashort}}-Client-SDK für Android konfigurieren
{: #custom-android}
Konfigurieren Sie Ihre Android-Anwendung, die mit der angepassten Authentifizierung arbeitet, zur Verwendung des {{site.data.keyword.amashort}}-Client-SDKs und verbinden Sie Ihre Anwendung mit {{site.data.keyword.Bluemix}}.

## Vorbereitungen
{: #before-you-begin}
Sie müssen über eine Ressource verfügen, die durch eine Instanz des {{site.data.keyword.amashort}}-Service geschützt wird, die zur Verwendung eines angepassten Identitätsproviders konfiguriert ist.  Ihre mobile App muss außerdem mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sein.  Weitere Informationen finden Sie über die folgenden Links:
 * [Einführung in {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Android-SDK einrichten](https://console.{DomainName}/docs/services/mobileaccess/getting-started-android.html)
 * [Angepassten Identitätsprovider verwenden](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Angepassten Identitätsprovider erstellen](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [{{site.data.keyword.amashort}} für die angepasste Authentifizierung konfigurieren](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## {{site.data.keyword.amashort}}-Client-SDK initialisieren
{: #custom-android-initialize}
1. Öffnen Sie in Ihrem Android-Projekt in Android Studio die Datei `build.gradle` Ihres App-Moduls.
<br/>**Tipp:** Ihr Android-Projekt enthält möglicherweise zwei Dateien `build.gradle`: eine für das Projekt und eine für das Anwendungsmodul. Verwenden Sie die Datei für das Anwendungsmodul.

1. Suchen Sie in der Datei `build.gradle` den Abschnitt `dependencies` und prüfen Sie, ob die folgende Abhängigkeit 'compile' vorhanden ist. Fügen Sie diese Abhängigkeit hinzu, falls sie noch nicht vorhanden ist.

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'core',
        version: '1.+',
        ext: 'aar',
        transitive: true
    	// weitere Abhängigkeiten  
	}
	```

1. Synchronisieren Sie Ihr Projekt mit Gradle. Klicken Sie auf **Tools > Android > Sync Project with Gradle Files**.

1. Öffnen Sie die Datei `AndroidManifest.xml` Ihres Android-Projekts.
Fügen Sie die Internetzugriffsberechtigung unter dem Element `<manifest>` hinzu:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```

1. Initialisieren Sie das SDK.  
Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode `onCreate` der Hauptaktivität in Ihrer Android-Anwendung.
Ersetzen Sie *applicationRoute* und *applicationGUID* durch die Werte für **Route** und **App-GUID**, die angezeigt werden, wenn Sie auf **Mobile Systemerweiterungen** in Ihrer App im {{site.data.keyword.Bluemix_notm}}-Dashboard klicken.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");					
	```

## Schnittstelle 'AuthenticationListener'
{: #custom-android-authlistener}

Das {{site.data.keyword.amashort}}-Client-SDK stellt die Schnittstelle `AuthenticationListener` bereit, mit deren Hilfe Sie einen angepassten Authentifizierungsablauf implementieren können. Die Schnittstelle `AuthenticationListener` macht drei Methoden verfügbar, die in verschiedenen Phasen des Authentifizierungsprozesses aufgerufen werden.

### Methode 'onAuthenticationChallengeReceived'
{: #custom-onAuth}
Rufen Sie diese Methode auf, wenn eine angepasste Authentifizierungsanforderung (Challenge) aus dem {{site.data.keyword.amashort}}-Service empfangen wird.

```Java
void onAuthenticationChallengeReceived(AuthenticationContext authContext, JSONObject challenge, Context context);
```
#### Argumente
{: #custom-android-onAuth-arg}

* `AuthenticationContext`: Wird vom {{site.data.keyword.amashort}}-Client-SDK bereitgestellt, sodass Sie Antworten auf Authentifizierungsanforderungen oder Fehler bei der Erfassung von Berechtigungsnachweisen zurückmelden können.  Dadurch können Sie zum Beispiel reagieren, wenn ein Benutzer die Authentifizierung abbricht.
* `JSONObject`: Enthält eine angepasste Authentifizierungsanforderung, wie sie durch einen angepassten Identitätsprovider zurückgegeben wird.
* `Context`: Eine Referenz auf den Android-Kontext, der beim Senden der Anforderung verwendet wurde. In der Regel stellt dieses Argument eine Android-Aktivität dar.

Durch Aufrufen der Methode `onAuthenticationChallengeReceived` delegiert das {{site.data.keyword.amashort}}-Client-SDK die Steuerung an den Entwickler.  Der Service wartet auf Berechtigungsnachweise. Der Entwickler muss Berechtigungsnachweise erfassen durch eine der Methoden der Schnittstelle `AuthenticationContext` an das {{site.data.keyword.amashort}}-Client-SDK zurückmelden.

### Methode 'onAuthenticationSuccess'
{: #custom-android-authlistener-onsuccess}
Rufen Sie diese Methode nach einer erfolgreichen Authentifizierung auf. Die Argumente sind der Android-Kontext und ein optionales JSONObject- Objekt, das erweiterte Informationen zu dem Authentifizierungserfolg enthält.
```Java
void onAuthenticationSuccess(Context context, JSONObject info);
```

### Methode 'onAuthenticationFailure'
{: #custom-android-authlistener-onfail}
Rufen Sie diese Methode auf, wenn eine Authentifizierung fehlgeschlagen ist. Die Argumente sind der Android-Kontext und ein optionales JSONObject- Objekt, das erweiterte Informationen zu dem Authentifizierungsfehler enthält.
```Java
void onAuthenticationFailure(Context context, JSONObject info);
```

## Schnittstelle 'AuthenticationContext'
{: #custom-android-authcontext}

Die Schnittstelle `AuthenticationContext` wird als Argument für die Methode `onAuthenticationChallengeReceived` einer angepassten Schnittstelle `AuthenticationListener` bereitgestellt. Sie müssen Berechtigungsnachweise erfassen und durch die Methoden der Schnittstelle `AuthenticationContext` an das {{site.data.keyword.amashort}}-Client-SDK zurückgeben oder einen Fehler melden. Verwenden Sie eine der folgenden Methoden.

```Java
void submitAuthenticationChallengeAnswer(JSONObject answer);
```
```Java
void submitAuthenticationFailure (JSONObject info);
```

## Beispielimplementierung einer angepassten Schnittstelle 'AuthenticationListener'
{: #custom-android-samplecustom}

Dieses Beispiel für 'AuthenticationListener' ist für die Ausführung mit einem angepassten Identitätsprovider gedacht. Sie können dieses Beispiel aus dem [Github-Repository](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample) herunterladen.

```Java
package com.ibm.helloworld;
import android.content.Context;
import android.util.Log;
import com.ibm.mobilefirstplatform.clientsdk.android.security.api.AuthenticationContext;
import com.ibm.mobilefirstplatform.clientsdk.android.security.api.AuthenticationListener;
import org.json.JSONException;
import org.json.JSONObject;

public class CustomAuthenticationListener implements AuthenticationListener {
	@Override
	public void onAuthenticationChallengeReceived (AuthenticationContext authContext,
											JSONObject challenge, Context context) {

		log("onAuthenticationChallengeResceived :: " + challenge.toString());

		// In diesem Beispiel gibt AuthenticationListener sofort einen fest codierten
		// Satz von Berechtigungsnachweisen zurück. In einem realen Szenario würde der
		// Entwickler hier ein Anmeldefenster anzeigen, Berechtigungsnachweise erfassen
		// und die API authContext.submitAuthenticationChallengeAnswer() aufrufen.

		JSONObject challengeResponse = new JSONObject();
		try {
			challengeResponse.put("username", "john.lennon");
			challengeResponse.put("password", "12345");
			authContext.submitAuthenticationChallengeAnswer(challengeResponse);
		} catch (JSONException e){

			// Im Fall eines Fehlers beim Erfassen von Berechtigungsnachweisen müssen
			// Sie dies an AuthenticationContext zurückmelden. Andernfalls verbleibt
			// das Mobile Client Access-Client-SDK unbegrenzte Zeit in einem
			// Wartestatus für Berechtigungsnachweise.

			log("This should never happen...");
			authContext.submitAuthenticationFailure(null);
		}
	}

	@Override
	public void onAuthenticationSuccess (Context context, JSONObject info) {
		log("onAuthenticationSuccess :: " + info.toString());
	}

	@Override
	public void onAuthenticationFailure (Context context, JSONObject info) {
		log("onAuthenticationFailure :: " + info.toString());
	}

	private void log(String text){
		Log.d("CustomAuthListener", text);
	}
}
```

## Angepasste Schnittstelle 'AuthenticationListener' registrieren
{: #custom-android-register}

Nach dem Erstellen einer angepassten Schnittstelle 'AuthenticationListener' registrieren Sie sie in `BMSClient`, bevor Sie mit der Verwendung des Listeners beginnen. Fügen Sie Ihrer Anwendung den folgenden Code hinzu. Dieser Code muss aufgerufen werden, bevor Sie Anforderungen an Ihre geschützten Ressourcen senden.

```Java
BMSClient.getInstance().registerAuthenticationListener(realmName,
									new CustomAuthenticationListener());
```

Verwenden Sie den Wert für *realmName*, den Sie im {{site.data.keyword.amashort}}-Dashboard angegeben haben.


## Authentifizierung testen
{: #custom-android-testing}
Nach der Initialisierung des Client-SDK und der Registrierung der angepassten Schnittstelle 'AuthenticationListener' können Sie mit dem Senden von Anforderungen an Ihr mobiles Back-End beginnen.

### Vorbereitungen
{: #custom-android-testing-before}
Sie müssen eine Anwendung, die mit der {{site.data.keyword.mobilefirstbp}}-Boilerplate erstellt wurde, sowie eine Ressource, die durch {{site.data.keyword.amashort}} geschützt wird, am Endpunkt `/protected` haben.


1. Senden Sie eine Anforderung an den geschützten Endpunkt Ihres mobilen Back-Ends in Ihrem Browser, indem Sie die Adresse `{applicationRoute}/protected` öffnen (z. B. `http://my-mobile-backend.mybluemix.net/protected`).

1. Der Endpunkt `/protected` eines mobilen Back-Ends, das mit der {{site.data.keyword.mobilefirstbp}}-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Auf den Endpunkt können nur mobile Anwendungen zugreifen, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind. Daher wird eine Nachricht `Unauthorized` (Nicht autorisiert) in Ihrem Browser angezeigt.

1. Senden Sie eine Anforderung über Ihre Android-Anwendung an denselben Endpunkt. Fügen Sie den folgenden Code hinzu, nachdem Sie `BMSClient` initialisiert und Ihre angepasste Schnittstelle 'AuthenticationListener' registriert haben.

	```Java
	Request request = new Request("/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp", AuthorizationManager.getInstance().getUserIdentity().toString());
		}
		@Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
			if (null != t) {
				Log.d("Myapp", "onFailure :: " + t.getMessage());
			} else if (null != extendedInfo) {
				Log.d("Myapp", "onFailure :: " + extendedInfo.toString());
			} else {
				Log.d("Myapp", "onFailure :: " + response.getResponseText());
			}
		}
	});
```

1. 	Wenn Ihre Anforderung erfolgreich ist, wird die folgende Ausgabe im LogCat-Tool angezeigt:

	![Bild](images/android-custom-login-success.png)

1. Durch Hinzufügen des folgenden Codes können Sie auch die Abmeldefunktion (logout) hinzufügen:

 ```Java
 AuthorizationManager.getInstance().logout(getApplicationContext(), listener);
 ```

 Wenn Sie diesen Code aufrufen, nachdem sich ein Benutzer angemeldet hat, wird der Benutzer abgemeldet. Wenn der Benutzer versucht, sich wieder anzumelden, muss er auf die vom Server empfangene Anforderung erneut reagieren.

 Der Wert für `listener`, der an die Abmeldefunktion übergeben wird, kann null sein.
