---

copyright:
  years: 2015, 2016

---

# Google-Authentifizierung für Android-Apps aktivieren
{: #google-auth-android}

## Vorbereitungen
{: #before-you-begin}
Voraussetzungen:

* Android-Projekt in Android Studio, das für das Arbeiten mit Gradle konfiguriert ist. Das Projekt muss nicht mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sein.  
* Instanz einer {{site.data.keyword.Bluemix_notm}}-Anwendung, die durch den {{site.data.keyword.amashort}}-Service geschützt ist. Weitere Informationen zur Erstellung eines {{site.data.keyword.Bluemix_notm}}-Back-Ends finden Sie in der [Einführung](index.html).

Das Einrichten der Google-Authentifizierung für Ihre {{site.data.keyword.amashort}}-Android-App erfordert außerdem die Konfiguration der folgenden Komponenten:
* {{site.data.keyword.Bluemix_notm}}-Anwendung
* Android Studio-Projekt

## Projekt in Google Developer Console erstellen
{: #create-google-project}

Erstellen Sie zur Verwendung von Google als Identitätsprovider ein Projekt in der Entwicklerkonsole von Google '[Google Developer Console](https://console.developers.google.com)'.
Zur Erstellung eines Projekts gehört das Anfordern einer Google-Client-ID. Die Google-Client-ID ist eine eindeutige Kennung für Ihre Anwendung, die von der Google-Authentifizierung verwendet wird und zum Einrichten der {{site.data.keyword.Bluemix_notm}}-Anwendung erforderlich ist.

Führen Sie die folgenden Schritte von der Konsole aus:

1. Erstellen Sie ein Projekt mithilfe der **Google+**-API.
2. Fügen Sie den Benutzerzugriff **OAuth** hinzu.
3. Vor dem Hinzufügen der Berechtigungsnachweise müssen Sie die Plattform auswählen (Android).
4. Fügen Sie die Berechtigungsnachweise hinzu. Zum Abschließen der Erstellung der Berechtigungsnachweise müssen Sie den **Fingerabdruck für das Signaturzertifikat** hinzufügen.



### Signaturzertifikat einrichten
Damit Google Ihre Anwendungsauthentizität überprüfen kann, müssen Sie einen Fingerabdruck für das Signaturzertifikat angeben.

Das Android-Betriebssystem erfordert, dass alle Anwendungen, die auf einem Android-Gerät installiert sind, mit einem Entwicklerzertifikat signiert sind. Eine Android-Anwendung kann in zwei Modi erstellt werden: Debugmodus und Freigabemodus (Release). Es wird gewöhnlich empfohlen, zwei unterschiedliche Zertifikate für den Debugmodus und den Freigabemodus zu haben.  Zertifikate, die zum Signieren von Android-Anwendungen im Debugmodus verwendet werden, werden in das Android-SDK gepackt.  Das Android-SDK wird in der Regel von Android Studio automatisch installiert. Wenn Sie Ihre Anwendung für Google Play freigeben möchten, müssen Sie die App mit einem anderen Zertifikat signieren, das Sie normalerweise selbst generieren. Weitere Informationen finden Sie unter [Android-Anwendungen signieren](http://developer.android.com/tools/publishing/app-signing.html).

Ein Keystore (Schlüsselspeicher), der ein Zertifikat für Entwicklungsumgebungen enthält, ist in der Datei `~/.android/debug.keystore` gespeichert. Das Standardkennwort für den Keystore ist `android`. Dieses Zertifikat dient zum Erstellen (Build) von Anwendungen im Debugmodus.

1. Rufen Sie Ihren Fingerabdruck für das Signaturzertifikat von Ihrer Client-Entwicklungsumgebung ab:

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore -list -v
	```
	Mit derselben Syntax können Sie auch den Schlüsselhashwert Ihres Freigabemoduszertifikats abrufen. Ersetzen Sie in dem Befehl den Alias- und den Keystorepfad entsprechend.

1. Suchen Sie im Dialog 'Google Console Credential' die Zeile, die unter **Certificate Fingerprints** mit `SHA1` beginnt. Kopieren Sie den Fingerabdruck, der durch Ausführen des Befehls **keytool** abgerufen wurde, in das Textfeld.

###Paketname

1. Geben Sie im Dialog 'Credentials' den Paketnamen Ihrer Android-Anwendung ein. 

  Zur Ermittlung des Paketnamens Ihrer Android-Anwendung öffnen Sie die Datei `AndroidManifest.xml` in Android Studio und suchen nach: `<manifest package="{your-package-name}">`. 

1. Wenn Sie dies erledigt haben, klicken Sie auf **Create**. **Damit ist die Erstellung der Berechtigungsnachweise abgeschlossen.**

###Google-Client-ID

Wenn die Berechtigungsnachweise erfolgreich erstellt wurden, wird auf der Seite für Berechtigungsnachweise Ihre Google-Client-ID angezeigt. Notieren Sie sich diesen Wert. Sie müssen diesen Wert in der {{site.data.keyword.Bluemix}}-Anwendung registrieren.


## {{site.data.keyword.amashort}} für die Google-Authentifizierung konfigurieren
{: #google-auth-android-config}

Jetzt, da Sie eine Google-Client-ID für Android haben, können Sie die Google-Authentifizierung im {{site.data.keyword.amashort}}-Dashboard aktivieren.

1. Öffnen Sie Ihre App im {{site.data.keyword.Bluemix_notm}}-Dashboard.

1. Klicken Sie auf **Mobile Systemerweiterungen** und notieren Sie die Werte für **Route** (`applicationRoute`) und **App-GUID** (`applicationGUID`). Sie benötigen diese Werte, wenn Sie das SDK initialisieren.

1. Klicken Sie auf die Kachel für {{site.data.keyword.amashort}}. Das {{site.data.keyword.amashort}}-Dashboard wird geladen.

1. Klicken Sie auf die Kachel für **Google**.

1. Geben Sie bei **Application ID for Android** Ihre Google-Client-ID für Android an und klicken Sie auf **Save**.

## {{site.data.keyword.amashort}}-Client-SDK für Android konfigurieren
{: #google-auth-android-sdk}

1. Kehren Sie zu Android Studio zurück.

1. Öffnen Sie die Datei `build.gradle` Ihres App-Moduls.

	Ihr Android-Projekt enthält möglicherweise zwei Dateien `build.gradle`: eine für das Projekt und eine für das Anwendungsmodul. Verwenden Sie die Datei für das Anwendungsmodul.

  Suchen Sie den Abschnitt für Abhängigkeiten ('dependencies') und fügen Sie eine neue Abhängigkeit 'compile' für das Client-SDK hinzu:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'googleauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// weitere Abhängigkeiten  
	}
	```

	**Hinweis:** Sie können die Abhängigkeit vom Modul `core` der Gruppe `com.ibm.mobilefirstplatform.clientsdk.android` entfernen, wenn diese vorhanden ist. Das Modul `googleauthentication` lädt sie automatisch für Sie herunter. Das Modul `googleauthentication` lädt das Google-SDK herunter und installiert es in Ihrem Android-Projekt.

1. Synchronisieren Sie Ihr Projekt mit Gradle, indem Sie auf **Tools > Android > Sync Project with Gradle Files** klicken.

1. Öffnen Sie die Datei `AndroidManifest.xml` Ihres Android-Projekts.

1. Fügen Sie die Internetzugriffsberechtigung unter dem Element `<manifest>` hinzu:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	```

1. Zur Verwendung des {{site.data.keyword.amashort}}-Client-SDK müssen Sie es initialisieren, indem Sie die Parameter für Kontext, 'applicationGUID' und 'applicationRoute' übergeben.

	Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode 'onCreate' der Hauptaktivität in Ihrer Android-Anwendung.

1. Initialisieren Sie das Client-SDK und registrieren Sie den Google-Authentifizierungsmanager. Ersetzen Sie *applicationRoute* und *applicationGUID* durch die Werte für **Route** und **App-GUID** aus dem Abschnitt **Mobile Systemerweiterungen** im Dashboard.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");

	GoogleAuthenticationManager.getInstance().register(this);
	```

1. Fügen Sie Ihrer Aktivität den folgenden Code hinzu:

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		GoogleAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```

## Authentifizierung testen
{: #google-auth-android-test}
Nach der Initialisierung des Client-SDK und der Registrierung des Google-Authentifizierungsmanagers können Sie mit dem Senden von Anforderungen an Ihre mobile Back-End-Anwendung beginnen.

### Vorbereitungen
{: #google-auth-android-testing-before}
Sie müssen über eine mobile Back-End-Anwendung verfügen, die mit der MobileFirst Services Starter-Boilerplate erstellt wurde. Außerdem müssen Sie bereits eine Ressource haben, die durch {{site.data.keyword.amashort}} am Endpunkt `/protected` geschützt wird. Weitere Informationen finden Sie in [Ressourcen schützen](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Versuchen Sie, in Ihrem Desktop-Browser eine Anforderung an den geschützten Endpunkt Ihrer mobilen Back-End-Anwendung zu senden, indem Sie `{applicationRoute}/protected` öffnen (z. B. `http://my-mobile-backend.mybluemix.net/protected`).
 Der Endpunkt `/protected` einer mobilen Back-End-Anwendung, die mit der Boilerplate 'MobileFirst Services' erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Daher können nur mobile Anwendungen auf den Endpunkt zugreifen, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind. Infolgedessen wird eine Nachricht `Unauthorized` (Nicht autorisiert) in Ihrem Desktop-Browser angezeigt.

1. Senden Sie eine Anforderung über Ihre Android-Anwendung an denselben Endpunkt. Fügen Sie den folgenden Code hinzu, nachdem Sie die `BMSClient`-Instanz initialisiert und `GoogleAuthenticationManager` registriert haben.

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

1. Führen Sie Ihre Anwendung aus. Eine Google-Anmeldeanzeige wird geöffnet. Nach der Anmeldung fordert die App eine Berechtigung für den Zugriff auf Ressourcen an:

	![Bild](images/android-google-login.png)

	Abhängig von Ihrem Android-Gerät sowie davon, ob Sie gerade bei Google angemeldet sind, erhalten Sie möglicherweise eine andere Benutzerschnittstelle.

  Indem Sie auf **OK** klicken, berechtigen Sie {{site.data.keyword.amashort}} Ihre Google-Benutzeridentität zu Authentifizierungszwecken zu nutzen.

1. 	Wenn Ihre Anforderung erfolgreich ist, wird die folgende Ausgabe im LogCat-Tool angezeigt:

	![Bild](images/android-google-login-success.png)

 Durch Hinzufügen des folgenden Codes können Sie auch die Abmeldefunktion (logout) hinzufügen:

 ```Java
 GoogleAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
 ```

 Wenn Sie diesen Code aufrufen, nachdem sich ein Benutzer bei Google angemeldet hat, wird der Benutzer bei Google abgemeldet. Wenn der Benutzer versucht, sich wieder anzumelden, muss er ein Google-Konto auswählen, mit dem er wieder angemeldet wird. Wird die Anmeldung mit einer zuvor angemeldeten Google-ID versucht, wird der Benutzer nicht noch einmal zur Eingabe der Berechtigungsnachweise aufgefordert. Um erneut zur Eingabe der Anmeldeberechtigungsnachweise aufgefordert zu werden, muss der Benutzer sein Google-Konto von dem Android-Gerät entfernen.

 Der Wert für `listener`, der an die Abmeldefunktion übergeben wird, kann `null` sein.
