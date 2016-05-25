---

copyright:
  years: 2015, 2016

---

# Facebook-Authentifizierung in Android-Apps aktivieren
{: #facebook-auth-android}
Wenn Sie Facebook als Identitätsprovider in Ihren Android-Anwendungen verwenden möchten, müssen Sie die Android-Plattform für Ihre Facebook-Anwendung hinzufügen und konfigurieren.

## Vorbereitungen
{: #facebook-auth-android-before}
 * Sie müssen über eine Ressource verfügen, die von {{site.data.keyword.amashort}} geschützt wird, und ein Android-Projekt haben, das mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert ist.  Weitere Informationen finden Sie in [Einführung in {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) und [Android-SDK einrichten](https://console.{DomainName}/docs/services/mobileaccess/getting-started-android.html).  
 * Schützen Sie Ihre Back-End-Anwendung manuell mit dem {{site.data.keyword.amashort}}-Server-SDK. Weitere Informationen finden Sie in [Ressourcen schützen](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).
 * Erstellen Sie eine Facebook-Anwendungs-ID. Weitere Informationen finden Sie in [Facebook-Anwendungs-ID vom Facebook-Entwicklerportal anfordern](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).


## Facebook-Anwendung für die Android-Plattform konfigurieren
{: #facebook-auth-android-config}
Zur Verwendung von Facebook als Identitätsprovider in Ihren Android-Anwendungen müssen Sie die Android-Plattform für Ihre Facebook-Anwendung hinzufügen und konfigurieren.

1. Öffnen Sie Ihre Facebook-Anwendung im Facebook-Entwicklerportal (Facebook Developer Portal).

1. Klicken Sie auf **Settings &gt; Add Platform &gt; Android**.

1. Geben Sie den Paketnamen Ihrer Android-Anwendung in die Eingabeaufforderung für 'Google Play Package Name'. Zur Ermittlung des Paketnamens Ihrer Android-Anwendung öffnen Sie die Dateien `AndroidManifest.xml` in Android Studio und suchen nach `<manifest ..... package="{your-package-name}">`.

1. Geben Sie den Klassennamen Ihrer Hauptaktivität (Main) in der Eingabeaufforderung **Class Name** an. Zur Ermittlung des Namens der Hauptaktivitätsklasse Ihrer Android-Anwendung öffnen Sie die Datei `AndroidManifest.xml` und such nach der Aktivitätsdeklaration mit einem Intent-Filter ähnlich wie im folgenden Code-Snippet:

	```XML
	<activity
		android:name=".MainActivity"
		android:label="@string/app_name">
		<intent-filter>
			<action android:name="android.intent.action.MAIN"/>
			<category android:name="android.intent.category.LAUNCHER"/>
		</intent-filter>
	</activity>
	```

1. Damit Facebook Ihre Anwendungsauthentizität sicherstellt, müssen Sie einen Hashwert Ihres Entwicklerzertifikats SHA1 angeben.

	**Weitere Informationen zur Android-Sicherheit:** Das Android-Betriebssystem erfordert, dass alle Anwendungen, die auf einem Android-Gerät installiert sind, mit einem Entwicklerzertifikat signiert sind. Die Android-Anwendung kann in zwei Modi erstellt werden: Debugmodus und Freigabemodus (Release). <br/>
  Verwenden Sie verschiedene Zertifikate für den Debugmodus und den Freigabemodus.  Zertifikate, die zum Signieren von Android-Anwendungen im Debugmodus verwendet werden, werden in das Android-SDK gepackt, das von Android Studio in der Regel automatisch installiert wird. Wenn Sie Ihre App für den Google Play-Store freigeben möchten, müssen Sie Ihre App mit einem anderen Zertifikat signieren, das Sie normalerweise selbst generieren. <br/>Sie können zwei Gruppen von Schlüsselhashwerten mit Facebook eingeben: ein Schlüsselhashwert für Anwendungen, die mit einem Debugzertifikat im Debugmodus erstellt werden, und ein weiterer Schlüsselhashwert für Anwendungen, die mit einem Freigabezertifikat im Freigabemodus erstellt werden. Weitere Informationen finden Sie unter [Android-Anwendungen signieren](http://developer.android.com/tools/publishing/app-signing.html).

1. Der Keystore (Schlüsselspeicher), der das Zertifikat enthält, das Sie für die Entwicklungsumgebung verwenden, wird in der Datei `~/.android/debug.keystore` gespeichert. Das Standardkennwort für den Keystore ist: `android`. Verwenden Sie dieses Zertifikat zum Erstellen von Anwendungen im Debugmodus.

1. Rufen Sie den Schlüsselhashwert Ihres Debugmoduszertifikats ab:

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore | openssl sha1 -binary | openssl base64
	```

	**Tipp**: Mit derselben Syntax können Sie auch den Schlüsselhashwert Ihres Freigabemoduszertifikats abrufen. Ersetzen Sie in dem Befehl den Alias- und den Keystorepfad entsprechend.

1. Kopieren Sie den Schlüsselhashwert, den Sie mit dem Befehl **keytool** abgerufen haben, und fügen Sie ihn in eine Eingabeaufforderung 'Development/Release Key Hashes' im Facebook-Entwicklerportal ein.

	**Tipp**: Wenn Sie planen, dieses Feature zu verwenden, sollten Sie in Betracht ziehen, die Single-Sign-on-Funktion zu aktivieren.

1. Klicken Sie auf **Save Settings** (Einstellungen speichern).

## {{site.data.keyword.amashort}} für die Facebook-Authentifizierung konfigurieren
{: #facebook-auth-android-mca}
Nachdem Sie über eine Facebook-Anwendungs-ID verfügen und Ihre Facebook-Anwendung zur Bedienung von Android-Clients konfiguriert haben, können Sie die Facebook-Authentifizierung im Dashboard von {{site.data.keyword.amashort}} aktivieren.

1. Öffnen Sie Ihre App im {{site.data.keyword.Bluemix_notm}}-Dashboard.

1. Klicken Sie auf **Mobile Systemerweiterungen** und notieren Sie die Werte für **Route** (`applicationRoute`) und **App-GUID** (`applicationGUID`). Sie benötigen diese Werte, wenn Sie das SDK initialisieren.

1. Klicken Sie auf die Kachel für {{site.data.keyword.amashort}}. Das {{site.data.keyword.amashort}}-Dashboard wird geladen.

1. Klicken Sie auf die Kachel **Facebook**.

1. Geben Sie die Facebook-Anwendungs-ID an und klicken Sie auf **Speichern**.

## {{site.data.keyword.amashort}}-Client-SDK für Android konfigurieren
{: #facebook-auth-android-sdk}
Verwenden Sie den Gradle-Abhängigkeitenmanager in Android Studio, um das Client-SDK für Android zu konfigurieren.

1.  Öffnen Sie die Datei `build.gradle` Ihres App-Moduls.
Ihr Android-Projekt enthält möglicherweise zwei Dateien `build.gradle`: eine für das Projekt und eine für das Anwendungsmodul. Verwenden Sie die Datei für das Anwendungsmodul.

1. Suchen Sie den Abschnitt für Abhängigkeiten ('dependencies') in der Datei `build.gradle` und fügen Sie eine neue Abhängigkeit 'compile' für das Client-SDK hinzu:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'facebookauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// weitere Abhängigkeiten  
	}
```

	Sie können die Abhängigkeit vom Modul `core` der Gruppe `com.ibm.mobilefirstplatform.clientsdk.android` entfernen, wenn diese sich in Ihrer Datei befindet. Das Modul `facebookauthentication` lädt das Modul `core` automatisch herunter.

  Nach dem Speichern Ihrer Aktualisierungen lädt das Modul `facebookauthentication` das Facebook-SDK herunter und installiert es in Ihrem Android-Projekt.


1. Synchronisieren Sie Ihr Projekt mit Gradle. Klicken Sie auf **Tools > Android > Sync project with Gradle Files**.

1. Öffnen Sie die Datei `res/values/strings.xml` und fügen Sie eine Zeichenfolge `facebook_app_id` hinzu, die Ihre Facebook-Anwendungs-ID enthält:

	```XML
	<resources>
		<string name="app_name">HelloWorld</string>
		<string name="action_settings">Settings</string>
		<string name="facebook_app_id">522733366802111</string>
	</resources>
```

1. Gehen Sie in der Datei `AndroidManifest.xml` Ihres Android-Projekts wie folgt vor:
   1. Fügen Sie die Internetzugriffsberechtigung unter dem Element `<manifest>` hinzu:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
```
  2. Fügen Sie die erforderlichen Metadaten für das Facebook-SDK dem Element `<application>` hinzu:

	```XML
	<application .......>

		<meta-data
			android:name="com.facebook.sdk.ApplicationId"
			android:value="@string/facebook_app_id"/>

		<activity ...../>
		<activity ...../>
	</application>
```

   1. Fügen unter Ihren vorhandenen Aktivitäten ein Facebook-Aktivitätselement hinzu:

	```XML
	<application .....>
		<activity ...../>
		<activity ...../>

		<activity 	android:name="com.facebook.FacebookActivity"
					android:configChanges=
						"keyboard|keyboardHidden|screenLayout|screenSize|orientation"
					android:theme="@android:style/Theme.Translucent.NoTitleBar"
					android:label="@string/app_name" />

	</application>
```

1. Initialisieren Sie das Client-SDK und registrieren Sie den Facebook-Authentifizierungsmanager. Initialisieren Sie das {{site.data.keyword.amashort}}-Client-SDK, indem Sie die Parameter für Kontext, App-GUID (`applicationGUID`) und Route (`applicationRoute`) übergeben.<br/>
 Eine gängige, jedoch nicht verbindliche, Position für den Initialisierungscode ist die Methode `onCreate` der Hauptaktivität in Ihrer Android-Anwendung.<br/>
 Ersetzen Sie *applicationRoute* und *applicationGUID* durch die Werte für **Route** und **App-GUID** aus dem Menü **Mobile Systemerweiterungen** auf der Hauptseite Ihrer App im Bluemix-Dashboard.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");

	FacebookAuthenticationManager.getInstance().register(this);
```


1. Fügen Sie Ihrer Aktivität den folgenden Code hinzu:

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
```

## Authentifizierung testen
Nach der Initialisierung des Client-SDK und der Registrierung des Facebook-Authentifizierungsmanagers können Sie mit dem Senden von Anforderungen an Ihr mobiles Back-End beginnen.

### Vorbereitungen
{: #facebook-auth-android-testing-before}
Sie müssen die {{site.data.keyword.mobilefirstbp}}-Boilerplate verwenden und bereits eine durch {{site.data.keyword.amashort}} geschützte Ressource am Endpunkt `/protected` haben. Wenn Sie einen Endpunkt `/protected` einrichten müssen, finden Sie weitere Informationen in [Ressourcen schützen](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Versuchen Sie, in Ihrem Browser eine Anforderung an den Endpunkt '/protected' Ihres neu erstellten mobilen Back-Ends zu senden. Öffnen Sie die folgende URL: `{applicationRoute}/protected`. Beispiel: `http://my-mobile-backend.mybluemix.net/protected`
<br/>Der Endpunkt `/protected` eines mobilen Back-Ends, der mit der MobileFirst Services Starter-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Eine Nachricht `Unauthorized` (Nicht autorisiert) wird in Ihrem Browser zurückgegeben. Diese Nachricht wird deshalb zurückgegeben, weil auf diesen Endpunkt nur mobile Anwendungen zugreifen können, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind.

1. Senden Sie eine Anforderung über Ihre Android-Anwendung an denselben Endpunkt. Fügen Sie den folgenden Code hinzu, nachdem Sie `BMSClient` initialisiert und `FacebookAuthenticationManager` registriert haben.

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

1. Führen Sie Ihre Anwendung aus. Es wird eine Facebook-Anmeldeanzeige angezeigt.

	![Bild](images/android-facebook-login.png)

	Diese Anzeige sieht möglicherweise geringfügig anders aus, wenn Sie die Facebook-App nicht auf Ihrem Gerät installiert haben oder wenn Sie zurzeit nicht bei Facebook angemeldet sind.

1. Klicken Sie auf **OK**, um {{site.data.keyword.amashort}} zu berechtigen, Ihre Facebook-Benutzeridentität zu Authentifizierungszwecken zu nutzen.

1. 	Wenn Ihre Anforderung erfolgreich ist, wird die folgende Ausgabe im Dienstprogramm LogCat angezeigt:

	![Bild](images/android-facebook-login-success.png)

1. Durch Hinzufügen des folgenden Codes können Sie auch die Abmeldefunktion (logout) hinzufügen:

 ```
FacebookAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
 ```

 Wenn Sie diesen Code aufrufen, nachdem sich ein Benutzer bei Facebook angemeldet hat, wird der Benutzer bei Facebook abgemeldet. Wenn der Benutzer versucht, sich wieder anzumelden, muss er seine Facebook-Berechtigungsnachweise eingeben.

 Der Wert für `listener`, der an die Abmeldefunktion übergeben wird, kann null sein.
