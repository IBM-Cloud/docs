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

# Google-Authentifizierung für Android-Apps aktivieren
{: #google-auth-android}

Sie können Benutzer über Google für Ihre {{site.data.keyword.amafull}}-Android-Anwendung authentifizieren. Fügen Sie die Sicherheitsfunktionalität von {{site.data.keyword.amashort}} hinzu.

## Vorbereitungen
{: #before-you-begin}

Voraussetzungen:

* Eine Instanz einer {{site.data.keyword.amafull}} service and {{site.data.keyword.Bluemix_notm}}-Anwendung. Weitere Informationen zur Erstellung einer {{site.data.keyword.Bluemix_notm}}-Back-End-Anwendung finden Sie in der [Einführung](index.html).
* Die URL der Back-End-Anwendung (**App-Route**). Sie benötigen diese Werte zum Senden von Anforderungen an die geschützten Endpunkte der Back-End-Anwendung.
* Der Wert für die **Tenant-ID**. Öffnen Sie den Service im {{site.data.keyword.amashort}}-Dashboard. Klicken Sie auf die Schaltfläche **Mobile Systemerweiterungen**. Im Feld **App-GUID/TenantId** wird der Wert `tenantId` (auch als `appGUID` bezeichnet) angezeigt. Sie benötigen diesen Wert für die Initialisierung von Authorization Manager.
* Die {{site.data.keyword.Bluemix_notm}}-**Region**. Ihre aktuelle {{site.data.keyword.Bluemix_notm}}-Region finden Sie im Header neben dem Symbol **Avatar** ![Avatarsymbol](images/face.jpg "Avatarsymbol"). Der Regionswert, der angezeigt wird, sollte einer der folgenden sein: `USA (Süden)`, `Vereinigtes Königreich` oder `Sydney`. Außerdem sollte er den im WebView-JavaScript-Code erforderlichen SDK-Werten entsprechen: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` oder `BMSClient.REGION_UK`. Sie benötigen diesen Wert für die Initialisierung des {{site.data.keyword.amashort}}-Clients.
* Android-Projekt, das für das Arbeiten mit Gradle konfiguriert ist. Das Projekt muss nicht mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sein.  

Das Einrichten der Google-Authentifizierung für Ihre {{site.data.keyword.amashort}}-Android-App erfordert außerdem die Konfiguration der folgenden Komponenten:

* {{site.data.keyword.Bluemix_notm}}-Anwendung
* Android Studio-Projekt

## Projekt in Google Developer Console erstellen
{: #create-google-project}

Erstellen Sie zur Verwendung von Google als Identitätsprovider ein Projekt in [Google Developer Console ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.developers.google.com "Symbol für externen Link"){: new_window}. Zur Erstellung eines Projekts gehört das Anfordern einer Google-Client-ID.  Die Google-Client-ID ist eine eindeutige Kennung für Ihre Anwendung, die von der Google-Authentifizierung verwendet wird und zum Einrichten des {{site.data.keyword.amashort}}-Service erforderlich ist.

Führen Sie die folgenden Schritte von der Konsole aus:

1. Erstellen Sie ein Projekt mithilfe der **Google+**-API.
2. Fügen Sie den Benutzerzugriff **OAuth** hinzu.
3. Vor dem Hinzufügen der Berechtigungsnachweise müssen Sie die Plattform auswählen (Android).
4. Fügen Sie die Berechtigungsnachweise hinzu.

Zum Abschließen der Erstellung der Berechtigungsnachweise müssen Sie den **Fingerabdruck für das Signaturzertifikat** hinzufügen.


### Signaturzertifikat einrichten
{: #signing_cert}

Damit Google Ihre Anwendungsauthentizität überprüfen kann, müssen Sie einen Fingerabdruck für das Signaturzertifikat angeben.

Das Android-Betriebssystem erfordert, dass alle Anwendungen, die auf einem Android-Gerät installiert sind, mit einem Entwicklerzertifikat signiert sind. Eine Android-Anwendung kann in zwei Modi erstellt werden: Debugmodus und Freigabemodus (Release). Es wird gewöhnlich empfohlen, zwei unterschiedliche Zertifikate für den Debugmodus und den Freigabemodus zu haben.  Zertifikate, die zum Signieren von Android-Anwendungen im Debugmodus verwendet werden, werden in das Android-SDK gepackt.  Das Android-SDK wird in der Regel von Android Studio automatisch installiert. Wenn Sie Ihre Anwendung für Google Play freigeben möchten, müssen Sie die App mit einem anderen Zertifikat signieren, das Sie normalerweise selbst generieren. Weitere Informationen finden Sie in [Android-Anwendungen signieren ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://developer.android.com/tools/publishing/app-signing.html "Symbol für externen Link"){: new_window}.

Ein Keystore (Schlüsselspeicher), der ein Zertifikat für Entwicklungsumgebungen enthält, ist in der Datei `~/.android/debug.keystore` gespeichert. Das Standardkennwort für den Keystore ist `android`. Dieses Zertifikat dient zum Erstellen (Build) von Anwendungen im Debugmodus.

1. Rufen Sie Ihren Fingerabdruck für das Signaturzertifikat von Ihrer Client-Entwicklungsumgebung ab:

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore -list -v
	```
	{: codeblock}

	Mit derselben Syntax können Sie auch den Schlüsselhashwert Ihres Freigabemoduszertifikats abrufen. Ersetzen Sie in dem Befehl den Alias- und den Keystorepfad entsprechend.

1. Suchen Sie im Dialog 'Google Console Credential' die Zeile, die unter **Certificate Fingerprints** mit `SHA1` beginnt. Kopieren Sie den Fingerabdruck, der durch Ausführen des Befehls **keytool** abgerufen wurde, in das Textfeld.

###Paketname

1. Geben Sie im Dialog 'Credentials' den Paketnamen Ihrer Android-Anwendung ein.

	Zur Ermittlung des Paketnamens Ihrer Android-Anwendung öffnen Sie die Datei `AndroidManifest.xml` in Android Studio und suchen nach:

	```
	<manifest package="{your-package-name}">
	```
	{: codeblock}

1. Wenn Sie dies erledigt haben, klicken Sie auf **Create**. Damit ist die Erstellung der Berechtigungsnachweise abgeschlossen.

###Google-Client-ID
{: #google-client-id}

Wenn die Berechtigungsnachweise erfolgreich erstellt wurden, wird auf der Seite für Berechtigungsnachweise Ihre Google-Client-ID angezeigt. Notieren Sie sich diesen Wert. Sie müssen diesen Wert in der {{site.data.keyword.Bluemix}}-Anwendung registrieren.


## {{site.data.keyword.amashort}} für die Google-Authentifizierung konfigurieren
{: #google-auth-android-config}

Jetzt, da Sie eine Google-Client-ID für Android haben, können Sie die Google-Authentifizierung im {{site.data.keyword.amashort}}-Dashboard aktivieren.

1. Öffnen Sie den Service im {{site.data.keyword.amashort}}-Dashboard.
1. Aktivieren Sie auf der Registerkarte **Verwalten** die Option **Berechtigung**.
1. Erweitern Sie den Abschnitt **Google**.
1. Geben Sie in **Client-ID für Android** Ihre Google-Client-ID für Android an und klicken Sie auf **Speichern**.

## {{site.data.keyword.amashort}}-Client-SDK für Android konfigurieren
{: #google-auth-android-sdk}

Über das Android Studio-Projekt.

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
    	// andere Abhängigkeiten
	}
	```
	{: codeblock}

	**Hinweis:** Sie können die Abhängigkeit vom Modul `core` der Gruppe `com.ibm.mobilefirstplatform.clientsdk.android` entfernen, wenn diese vorhanden ist. Das Modul `googleauthentication` lädt sie automatisch für Sie herunter. Das Modul `googleauthentication` lädt das Google+-SDK herunter und installiert es in Ihrem Android-Projekt.

1. Synchronisieren Sie Ihr Projekt mit Gradle, indem Sie auf **Tools > Android > Sync Project with Gradle Files** klicken.

1. Öffnen Sie die Datei `AndroidManifest.xml` Ihres Android-Projekts.

1. Fügen Sie die Internetzugriffsberechtigung unter dem Element `<manifest>` hinzu:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	```
	{: codeblock}

1. Zur Verwendung des {{site.data.keyword.amashort}}-Client-SDK müssen Sie es initialisieren, indem Sie die Parameter **context** und **region** übergeben.

	Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode `onCreate` der Hauptaktivität in Ihrer Android-Anwendung.

1. Initialisieren Sie das Client-SDK und registrieren Sie den Google-Authentifizierungsmanager.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

	BMSClient.getInstance().setAuthorizationManager(
					MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));

	GoogleAuthenticationManager.getInstance().register(this);
	```
	{: codeblock}

	* Ersetzen Sie `BMSClient.REGION_UK` durch Ihre {{site.data.keyword.Bluemix_notm}}-**Region**.
	* Ersetzen Sie `<MCAServiceTenantId>` durch den Wert der **Tenant-ID**.

	Informationen zum Abrufen dieser Werte finden Sie unter [Vorbereitungen](##before-you-begin).

	**Hinweis:** Wenn Ihre Android-Anwendung als Ziel Android Version 6.0 (API-Stufe 23) oder höher ausgewählt hat, müssen Sie sicherstellen, dass die Anwendung über einen `android.permission.GET_ACCOUNTS`-Aufruf verfügt, bevor `register` aufgerufen wird. Weitere Informationen finden Sie in [Berechtigungen für Android anfordern ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.android.com/training/permissions/requesting.html "Symbol für externen Link"){: new_window}.

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

## Authentifizierung testen
{: #google-auth-android-test}

Nach der Initialisierung des Client-SDK und der Registrierung des Google-Authentifizierungsmanagers können Sie mit dem Senden von Anforderungen an Ihre Back-End-Anwendung beginnen.

Bevor Sie mit dem Test beginnen, müssen Sie über eine mobile Back-End-Anwendung verfügen, die mit der **MobileFirst Services Starter**-Boilerplate erstellt wurde. Außerdem müssen Sie bereits eine Ressource haben, die durch den Endpunkt `/protected` von {{site.data.keyword.amashort}} geschützt wird. Weitere Informationen finden Sie in [Ressourcen schützen](protecting-resources.html).

1. Versuchen Sie, in Ihrem Desktop-Browser eine Anforderung an den geschützten Endpunkt Ihrer mobilen Back-End-Anwendung zu senden, indem Sie `{applicationRoute}/protected` öffnen (z. B. `http://my-mobile-backend.mybluemix.net/protected`).  Informationen zum Abrufen des Wertes für `{applicationRoute}` finden Sie unter [Vorbereitungen](#before-you-begin).

	Der Endpunkt `/protected` einer mobilen Back-End-Anwendung, die mit der Boilerplate 'MobileFirst Services' erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Daher können nur mobile Anwendungen auf den Endpunkt zugreifen, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind. Infolgedessen wird eine Nachricht `Unauthorized` (Nicht autorisiert) in Ihrem Desktop-Browser angezeigt.

1. Verwenden Sie Ihre Android-Anwendung, um eine Anforderung an denselben geschützten Endpunkt zu senden. Fügen Sie den folgenden Code hinzu, nachdem Sie die `BMSClient`-Instanz initialisiert und `GoogleAuthenticationManager` registriert haben.

	```Java
	Request request = new Request("{applicationRoute}/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp", MCAAuthorizationManager.getInstance().getUserIdentity().toString());
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
	{: codeblock}

1. Führen Sie Ihre Anwendung aus. Eine Google-Anmeldeanzeige wird geöffnet. Nach der Anmeldung fordert die App eine Berechtigung für den Zugriff auf Ressourcen an:

	![Bild](images/android-google-login.png)

	Abhängig von Ihrem Android-Gerät sowie davon, ob Sie gerade bei Google angemeldet sind, wird möglicherweise eine andere Benutzerschnittstelle angezeigt.

	Indem Sie auf **OK** klicken, berechtigen Sie {{site.data.keyword.amashort}} Ihre Google-Benutzeridentität zu Authentifizierungszwecken zu nutzen.

1. 	Wenn Ihre Anforderung erfolgreich ist, wird die folgende Ausgabe im LogCat-Tool angezeigt:

	![Bild](images/android-google-login-success.png)

	Durch Hinzufügen des folgenden Codes können Sie auch die Abmeldefunktion (logout) hinzufügen:

	```Java
 GoogleAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
	```
	{: codeblock}

	Wenn Sie diesen Code aufrufen, nachdem sich ein Benutzer bei Google angemeldet hat, wird der Benutzer bei Google abgemeldet. Wenn der Benutzer versucht, sich wieder anzumelden, muss er ein Google-Konto für die erneute Anmeldung auswählen. Wird die Anmeldung mit einer zuvor angemeldeten Google-ID versucht, wird der Benutzer nicht noch einmal zur Eingabe der Berechtigungsnachweise aufgefordert. Um erneut zur Eingabe der Anmeldeberechtigungsnachweise aufgefordert zu werden, muss der Benutzer sein Google-Konto von dem Android-Gerät entfernen.

	Der Wert für `listener`, der an die Abmeldefunktion übergeben wird, kann `null` sein.
