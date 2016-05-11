---

copyright:
  years: 2015, 2016

---

# Google-Authentifizierung in Android-Apps aktivieren
{: #google-auth-android}

## Vorbereitungen
{: #before-you-begin}

* Sie müssen über eine Ressource verfügen, die von {{site.data.keyword.amashort}} geschützt wird, und ein Android-Projekt haben, das mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert ist.  Weitere Informationen finden Sie in [Einführung in {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) und [Android-SDK einrichten](https://console.{DomainName}/docs/services/mobileaccess/getting-started-android.html).  
* Schützen Sie Ihre Back-End-Anwendung manuell mit dem {{site.data.keyword.amashort}}-Server-SDK. Weitere Informationen finden Sie in [Ressourcen schützen](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

## Google-Projekt für die Android-Plattform konfigurieren
{: #google-auth-android-project}
Zur Verwendung von Google als Identitätsprovider erstellen Sie ein Projekt in Google Developer Console. Zur Erstellung eines Projekts gehört das Anfordern einer Google-Client-ID.  Die Google-Client-ID ist eine eindeutige Kennung für Ihre Anwendung, die von der Google-Authentifizierung verwendet wird.

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
     


1. Wählen Sie einen Anwendungstyp aus. Klicken Sie auf **Android**. Geben Sie einen aussagekräftigen Namen für Ihren Android-Client an.

1. Damit Google Ihre Anwendungsauthentizität überprüfen kann, müssen Sie einen Fingerabdruck für das Signaturzertifikat angeben.

	 **Weitere Informationen zur Android-Sicherheit:** Das Android-Betriebssystem erfordert, dass alle Anwendungen, die auf einem Android-Gerät installiert sind, mit einem Entwicklerzertifikat signiert sind. Eine Android-Anwendung kann in zwei Modi erstellt werden: Debugmodus und Freigabemodus (Release). Es wird gewöhnlich empfohlen, zwei unterschiedliche Zertifikate für den Debugmodus und den Freigabemodus zu haben.  Zertifikate, die zum Signieren von Android-Anwendungen im Debugmodus verwendet werden, werden in das Android-SDK gepackt.  Das Android-SDK wird in der Regel von Android Studio automatisch installiert. Wenn Sie Ihre Anwendung für Google Play freigeben möchten, müssen Sie die App mit einem anderen Zertifikat signieren, das Sie normalerweise selbst generieren. Weitere Informationen finden Sie unter [Android-Anwendungen signieren](http://developer.android.com/tools/publishing/app-signing.html).

1. Ein Keystore (Schlüsselspeicher), der ein Zertifikat für Entwicklungsumgebungen enthält, ist in der Datei `~/.android/debug.keystore` gespeichert. Das Standardkennwort für den Keystore ist `android`. Dieses Zertifikat dient zum Erstellen (Build) von Anwendungen im Debugmodus.

     1. Rufen Sie Ihren Fingerabdruck für das Signaturzertifikat ab:

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore -list -v
	```
	Mit derselben Syntax können Sie auch den Schlüsselhashwert Ihres Freigabemoduszertifikats abrufen. Ersetzen Sie in dem Befehl den Alias- und den Keystorepfad entsprechend.

1. Suchen Sie die Zeile, die mit `SHA1` beginnt, unter **Certificate Fingerprints**. Kopieren Sie den Fingerabdruck, den Sie mit dem **keytool**-Befehl ermittelt haben, in Google Developer Console.

1. Geben Sie den Paketnamen Ihrer Android-Anwendung an. Zur Ermittlung des Paketnamens Ihrer Android-Anwendung öffnen Sie die Datei `AndroidManifest.xml` in Android Studio und suchen nach: `<manifest package="{your-package-name}">`. Wenn Sie dies erledigt haben, klicken Sie auf **Create**.

Es wird ein Dialogfenster mit Ihrer Google-Client-ID angezeigt. Notieren Sie sich diesen Wert. Sie müssen diesen Wert bei {{site.data.keyword.Bluemix}} registrieren.


## {{site.data.keyword.amashort}} für die Google-Authentifizierung konfigurieren
{: #google-auth-android-config}

Jetzt, da Sie eine Google-Client-ID für Android haben, können Sie die Google-Authentifizierung im {{site.data.keyword.amashort}}-Dashboard aktivieren.

1. Öffnen Sie Ihre App im {{site.data.keyword.Bluemix_notm}}-Dashboard.

1. Klicken Sie auf **Mobile Systemerweiterungen** und notieren Sie die Werte für **Route** (`applicationRoute`) und **App-GUID** (`applicationGUID`). Sie benötigen diese Werte, wenn Sie das SDK initialisieren.

1. Klicken Sie auf die Kachel für {{site.data.keyword.amashort}}. Das {{site.data.keyword.amashort}}-Dashboard wird geladen.

1. Klicken Sie auf die Kachel für **Google**.

1. Geben Sie in **Application ID for Android** Ihre Google-Client-ID für Android an und klicken Sie auf **Save**.

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

	Sie können die Abhängigkeit vom Modul `core` der Gruppe `com.ibm.mobilefirstplatform.clientsdk.android` entfernen, wenn diese vorhanden ist. Das Modul `googleauthentication` lädt sie automatisch für Sie herunter. Das Modul `googleauthentication` lädt das Google-SDK herunter und installiert es in Ihrem Android-Projekt.

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
Nach der Initialisierung des Client-SDK und der Registrierung des Google-Authentifizierungsmanagers können Sie mit dem Senden von Anforderungen an Ihr mobiles Back-End beginnen.

### Vorbereitungen
{: #google-auth-android-testing-before}
Sie müssen ein mobiles Back-End haben, das mit der Boilerplate 'MobileFirst Services Starter' erstellt wurde, und eine Ressource, die durch {{site.data.keyword.amashort}} geschützt wird, am Endpunkt `/protected` haben. Weitere Informationen finden Sie in [Ressourcen schützen](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Versuchen Sie, in Ihrem Desktop-Browser eine Anforderung an den geschützten Entpunkt Ihres mobilen Back-Ends zu senden, indem Sie `{applicationRoute}/protected` öffnen (z. B. `http://my-mobile-backend.mybluemix.net/protected`).
 Der Endpunkt `/protected` eines mobilen Back-Ends, das mit der Boilerplate 'MobileFirst Services' erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Daher können nur mobile Anwendungen auf den Endpunkt zugreifen, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind. Infolgedessen wird eine Nachricht `Unauthorized` (Nicht autorisiert) in Ihrem Desktop-Browser angezeigt.

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

1. Durch Hinzufügen des folgenden Codes können Sie auch die Abmeldefunktion (logout) hinzufügen:

 ```Java
 GoogleAuthenticationManager.getInstance().logout(getApplicationContext(),, listener);
 ```

 Wenn Sie diesen Code aufrufen, nachdem sich ein Benutzer bei Google angemeldet hat, wird der Benutzer bei Google abgemeldet. Wenn der Benutzer versucht, sich wieder anzumelden, muss er ein Google-Konto auswählen, mit dem er wieder angemeldet wird. Wird die Anmeldung mit einer zuvor angemeldeten Google-ID versucht, wird der Benutzer nicht noch einmal zur Eingabe der Berechtigungsnachweise aufgefordert. Um erneut zur Eingabe der Anmeldeberechtigungsnachweise aufgefordert zu werden, muss der Benutzer sein Google-Konto von dem Android-Gerät entfernen.

 Der Wert für `listener`, der an die Abmeldefunktion übergeben wird, kann null sein.
