---

copyright:
  years: 2015, 2016
  
---

# Android-SDK einrichten
{: #getting-started-android}

Instrumentieren Sie Ihre Android-Anwendung mit dem {{site.data.keyword.amashort}}-Client-SDK, initialisieren Sie das SDK und senden Sie Anforderungen an geschützte und nicht geschützte Ressourcen.

## Vorbereitungen
{: #before-you-begin}
* Sie müssen über eine Instanz eines mobilen Back-Ends verfügen, die durch den {{site.data.keyword.amashort}}-Service geschützt wird. Weitere Informationen zur Erstellung eines mobilen Back-Ends finden Sie in der [Einführung](getting-started.html).
* Richten Sie Android Studio und das Android Studio-SDK ein. Weitere Informationen zur Einrichtung Ihrer Android-Entwicklungsumgebung finden Sie in [Google Developer Tools](http://developer.android.com/sdk/index.html).


## {{site.data.keyword.amashort}}-Client-SDK installieren
{: #install-mca-sdk}

Das {{site.data.keyword.amashort}}-Client-SDK wird mit Gradle, einem Abhängigkeitenmanager für Android-Projekte, verteilt. Gradle lädt automatisch Artefakte aus Repositorys herunter und stellt sie Ihrer Android-Anwendung zur Verfügung.

1. Erstellen Sie ein Android Studio-Projekt oder öffnen Sie ein vorhandenes Projekt.

1. Öffnen Sie die Datei `build.gradle`.
**Tipp**: Ihr Android-Projekt enthält möglicherweise zwei Dateien `build.gradle`: eine für das Projekt und eine für das Anwendungsmodul. Verwenden Sie die Datei für das Anwendungsmodul.

1. Suchen Sie den Abschnitt **dependencies** in der Datei `build.gradle`.  Fügen Sie eine Abhängigkeit 'compile' für das {{site.data.keyword.amashort}}-Client-SDK hinzu:

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

1. Synchronisieren Sie Ihr Projekt mit Gradle. Klicken Sie auf **Tools &gt; Android &gt; Sync Project with Gradle Files**.

1. Öffnen Sie die Datei `AndroidManifest.xml` für Ihr Android-Projekt. Fügen Sie die Internetzugriffsberechtigung unter dem Element `<manifest>` hinzu:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
```

## {{site.data.keyword.amashort}}-Client-SDK initialisieren
{: #initalize-mca-sdk}

Initialisieren Sie das SDK, indem Sie die Parameter für den Kontext, für 'applicationGUID' und 'applicationRoute' an die Methode `initialize` übergeben.


1. Klicken Sie auf der Hauptseite des {{site.data.keyword.Bluemix_notm}}-Dashboards auf Ihre App. Klicken Sie auf **Mobile Systemerweiterungen**. Sie benötigen die Werte für die **Anwendungsroute** und die **Anwendungs-GUID** für die Initialisierung des SDK.

2. Initialisieren Sie das {{site.data.keyword.amashort}}-Client-SDK in Ihrer Android-Anwendung.  Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode `onCreate` der Hauptaktivität in Ihrer Android-Anwendung.
<br/>Ersetzen Sie die Werte *applicationRoute* und *applicationGUID* durch die Werte unter **Mobile Systemerweiterungen** im {{site.data.keyword.Bluemix_notm}}-Dashboard.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");
```


## Anforderung an das mobile Back-End senden
{: #request}

Nach der Initialisierung des {{site.data.keyword.amashort}}-Client-SDK können Sie mit dem Senden von Anforderungen an Ihr mobiles Back-End beginnen.

1. Versuchen Sie, eine Anforderung an den Endpunkt '/protected' Ihres mobilen Back-Ends zu senden. Öffnen Sie in Ihrem Browser die folgende URL: `{applicationRoute}/protected`. Beispiel: `http://my-mobile-backend.mybluemix.net/protected`
<br/>Der Endpunkt `/protected` eines mobilen Back-Ends, der mit der MobileFirst Services Starter-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Eine Nachricht `Unauthorized` (Nicht autorisiert) wird in Ihrem Browser zurückgegeben, weil auf diesen Endpunkt nur mobile Anwendungen zugreifen können, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind.

1. Verwenden Sie Ihre Android-Anwendung, um eine Anforderung an denselben Endpunkt zu senden. Fügen Sie den folgenden Code hinzu, nachdem Sie `BMSClient` initialisiert haben:

	```Java
	Request request = new Request("/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
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

1. Wenn Ihre Anforderung erfolgreich ist, wird die folgende Ausgabe im Dienstprogramm LogCat angezeigt:

	![Bild](images/getting-started-android-success.png)

## Nächste Schritte
{: #next-steps}

Wenn Sie eine Verbindung zu dem geschützten Endpunkt hergestellt haben, waren keine Berechtigungsnachweise erforderlich. Wenn Sie die Benutzer zur Anmeldung bei Ihrer Anwendung veranlassen wollen, müssen Sie eine Authentifizierung über Facebook oder Google oder eine angepasste Authentifizierung konfigurieren.
* [Facebook](facebook-auth-android.html)
* [Google](google-auth-android.html)
* [Angepasst](custom-auth-android.html)
