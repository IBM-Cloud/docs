---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-10"
---
{:shortdesc: .shortdesc}
{:screen:.screen}


# Android-SDK einrichten
{: #getting-started-android}

Instrumentieren Sie Ihre Android-Anwendung mit dem {{site.data.keyword.amafull}}-Client-SDK, initialisieren Sie das SDK und senden Sie Anforderungen an geschützte und nicht geschützte Ressourcen.

{:shortdesc}

## Vorbereitungen
{: #before-you-begin}
Voraussetzungen:
* Instanz einer {{site.data.keyword.Bluemix_notm}}-Anwendung, die durch den {{site.data.keyword.amashort}}-Service geschützt ist. Weitere Informationen zur Erstellung einer {{site.data.keyword.Bluemix_notm}}-Back-End-Anwendung finden Sie in der [Einführung](index.html).
* Die Parameterwerte Ihres Service. Öffnen Sie den Service im {{site.data.keyword.Bluemix_notm}}-Dashboard. Klicken Sie auf **Mobile Systemerweiterungen**. In den Feldern **Route** und **App-GUID/TenantId** werden die Werte `applicationRoute` und `tenantId` (auch als `appGUID` bezeichnet) angezeigt. Diese Werte benötigen Sie für die Initialisierung des SDK und zum Senden von Anforderungen an die Back-End-Anwendung.
* Android Studio-Projekt, das für das Arbeiten mit Gradle eingerichtet ist. Weitere Informationen zur Einrichtung Ihrer Android-Entwicklungsumgebung finden Sie in [Google Developer Tools](http://developer.android.com/sdk/index.html).

## {{site.data.keyword.amashort}}-Client-SDK installieren
{: #install-mca-sdk}

Das {{site.data.keyword.amashort}}-Client-SDK wird mit Gradle, einem Abhängigkeitenmanager für Android-Projekte, verteilt. Gradle lädt automatisch Artefakte aus Repositorys herunter und stellt sie Ihrer Android-Anwendung zur Verfügung.

1. Erstellen Sie ein Android Studio-Projekt oder öffnen Sie ein vorhandenes Projekt.

1. Öffnen Sie die Datei `build.gradle` für Ihre Anwendung (**nicht** die Datei `build.gradle` für das Projekt).

1. Suchen Sie den Abschnitt **dependencies** in der Datei `build.gradle`.  Fügen Sie eine Abhängigkeit 'compile' für das {{site.data.keyword.amashort}}-Client-SDK hinzu:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',
        name:'core',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// andere Abhängigkeiten
}
```

1. Synchronisieren Sie Ihr Projekt mit Gradle. Klicken Sie auf **Tools &gt; Android &gt; Sync Project with Gradle Files**.

1. Öffnen Sie die Datei `AndroidManifest.xml` für Ihr Android-Projekt. Fügen Sie die Internetzugriffsberechtigung unter dem Element `<manifest>` hinzu:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
```

## {{site.data.keyword.amashort}}-Client-SDK initialisieren
{: #initalize-mca-sdk}

Initialisieren Sie das SDK, indem Sie die Parameter **context** und **region** an die Methode `initialize` übergeben. Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode `onCreate` der Hauptaktivität in Ihrer Android-Anwendung.

```Java
  BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);
					
  BMSClient.getInstance().setAuthorizationManager(
                 MCAAuthorizationManager.createInstance(this, "MCAServiceTenantId"));

```

   * Ersetzen Sie `BMSClient.REGION_UK` durch die entsprechende Region.  Klicken Sie zur Anzeige der {{site.data.keyword.Bluemix_notm}}-Region auf das Symbol **Avatar** ![Avatarsymbol](images/face.jpg "Avatarsymbol") in der Menüleiste, um das Widget **Konto und Unterstützung** zu öffnen. Der Regionswert muss einer der folgenden sein: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` oder `BMSClient.REGION_UK`.
   * Ersetzen Sie "MCAServiceTenantId" durch den Wert **tenantId** (siehe [Vorbereitungen](#before-you-begin)). 

## Anforderung an mobile Back-End-Anwendung senden
{: #request}

Nach der Initialisierung des {{site.data.keyword.amashort}}-Client-SDK können Sie mit dem Senden von Anforderungen an Ihre mobile Back-End-Anwendung beginnen.

1. Versuchen Sie, eine Anforderung an den geschützten Endpunkt Ihrer neuen mobilen Back-End-Anwendung zu senden. Öffnen Sie in Ihrem Browser die folgende URL: `{applicationRoute}/protected` (z. B. `http://my-mobile-backend.mybluemix.net/protected`).   Informationen zum Abrufen des Wertes für `{applicationRoute}` finden Sie unter [Vorbereitungen](#before-you-begin). 
	
	Der Endpunkt `/protected` einer mobilen Back-End-Anwendung, die mit der MobileFirst Services Starter-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Eine Nachricht des Typs `Unauthorized` (Nicht autorisiert) wird in Ihrem Browser zurückgegeben, weil auf diesen Endpunkt nur mobile Anwendungen zugreifen können, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind.

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
