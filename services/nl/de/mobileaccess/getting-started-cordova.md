---

copyright:
  years: 2015, 2016
  
---

# Cordova-Plug-in einrichten
{: #getting-started-cordova}

Instrumentieren Sie Ihre Cordova-Anwendung mit dem {{site.data.keyword.amashort}}-Client-SDK, initialisieren Sie das SDK und senden Sie Anforderungen an geschützte und nicht geschützte Ressourcen.

## Vorbereitungen
{: #before-you-begin}

- Sie müssen über eine Instanz eines mobilen Back-Ends verfügen, die durch den {{site.data.keyword.amashort}}-Service geschützt wird. Weitere Informationen zur Erstellung eines mobilen Back-Ends finden Sie in der [Einführung](getting-started.html).

- Erstellen Sie eine Cordova-Anwendung oder verwenden Sie ein vorhandenes Projekt. Weitere Informationen zur Einrichtung Ihrer Cordova-Anwendung finden Sie auf der [Cordova-Website](https://cordova.apache.org/).

## Cordova-Plug-in für {{site.data.keyword.amashort}} installieren
{: #getting-started-cordova-plugin}

Das {{site.data.keyword.amashort}}-Client-SDK für Cordova ist ein Cordova-Plug-in, das als Wrapper für die nativen {{site.data.keyword.amashort}}-Client-SDKs fungiert. Es wird mithilfe der Cordova-Befehlszeilenschnittstelle (CLI) und mit `npmjs`, einem Plug-in-Repository für Cordova-Projekte verteilt. Die Cordova-CLI lädt Plug-ins automatisch aus Repositorys herunter und stellt sie Ihrer Cordova-Anwendung zur Verfügung.

1. Fügen Sie Android- und iOS-Plattformen zur Ihrer Cordova-Anwendung hinzu. Führen Sie einen oder beide der folgenden Befehle über die Befehlszeile aus:

	```Bash
	cordova platform add android
	```

	```Bash
	cordova platform add ios
	```

1. Wenn Sie die Android-Plattform hinzugefügt haben, müssen Sie die minimal unterstützte API-Stufe in der Datei `config.xml` Ihrer Cordova-Anwendung hinzufügen. Öffnen Sie die Datei `config.xml` und fügen Sie die folgende Zeile dem Element `<platform name="android">` hinzu:

	```XML
	<platform name="android">  
		<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
		<!-- add minimum and target Android API level declaration -->
	</platform>
	```

	Der Wert für *minSdkVersion* muss höher als `15` sein. Der Wert für *targetSdkVersion* muss das neueste Android-SDK angeben, das über Google verfügbar ist.

1. Wenn Sie das iOS-Betriebssystem hinzugefügt haben, aktualisieren Sie das Element `<platform name="ios">` mit einer Zieldeklaration ('target'):

	```XML
	<platform name="ios">
    <preference name="deployment-target" value="8.0"/>
		<!-- add deployment target declaration -->
	</platform>
	```

1. Installieren Sie das Cordova-Plug-in für {{site.data.keyword.amashort}}:

 	```Bash
	cordova plugin add ibm-mfp-core
	```

1. Konfigurieren Sie Ihre Plattform für Android und/oder iOS.

	* **Android**

		Erstellen Sie vor dem Öffnen Ihres Projekts in Android Studio den Build Ihrer Cordova-Anwendung über Ihre Befehlszeilenschnittstelle (Command-Line Interface, CLI), um Buildfehler zu vermeiden.

		```
		cordova build android
		```

	* **iOS**

		Konfigurieren Sie Ihr Xcode-Projekt wie nachfolgend angegeben, um Buildfehler zu vermeiden.

		1. Öffnen Sie Ihre Xcode-Projektdatei (xcode.proj) mit der neuesten Version von Xcode im Verzeichnis  &lt;*app_name*&gt;/platforms/ios.

		**Wichtig:** Wenn eine Nachricht "Convert to Latest Swift Syntax" ausgegeben wird, klicken Sie auf 'Cancel' (Abbrechen).

		2. Navigieren Sie zu **Build Settings > Swift Compiler - Code Generation > Objective-C Bridging Header** und fügen Sie den folgenden Pfad hinzu:

			```
			<ihr_projektname>/Plugins/ibm-mfp-core/Bridging-Header.h
			```

		3. Navigieren Sie zu **Build settings > Linking > Runpath Search Paths** und fügen Sie den folgenden Parameter 'Frameworks' hinzu:

			```
			@executable_path/Frameworks
			```

		4. Erstellen Sie den Build mit Xcode und führen Sie Ihre Anwendung mit Xcode aus.

1. Überprüfen Sie, ob das Plug-in erfolgreich installiert wurde, indem Sie den folgenden Befehl ausführen:

	```Bash
	cordova plugin list
	```

## {{site.data.keyword.amashort}}-Client-Plug-in initialisieren
{: #getting-started-cordova-initialize}

Zur Verwendung des {{site.data.keyword.amashort}}-Client-SDK müssen Sie das SDK initialisieren, indem Sie die Parameter *applicationGUID* und *applicationRoute* übergeben.

1. Ermitteln Sie Ihre Werte für die Route und die GUID der Anwendung auf der Hauptseite des {{site.data.keyword.Bluemix_notm}}-Dashboards. Klicken Sie auf den Namen Ihrer App und anschließend auf **Mobile Systemerweiterungen**, um die Wert für die **Anwendungsroute** und die **Anwendungs-GUID** zum Initialisieren des SDK anzuzeigen.

3. Fügen Sie Ihrer Datei `index.js` den folgenden Aufruf hinzu, um das {{site.data.keyword.amashort}}-Client-SDK zu initialisieren. Ersetzen Sie die Werte für *applicationRoute* und *applicationGUID* durch die Werte aus **Mobile Systemerweiterungen** im {{site.data.keyword.Bluemix_notm}}-Dashboard.

	```JavaScript
	BMSClient.initialize("applicationRoute", "applicationGUID");
	```

## Anforderung an das mobile Back-End senden
{: #getting-started-request}

Nach der Initialisierung des {{site.data.keyword.amashort}}-Client-SDK können Sie mit dem Senden von Anforderungen an Ihr mobiles Back-End beginnen.

1. Versuchen Sie, eine Anforderung an den Endpunkt '/protected' Ihres mobilen Back-Ends zu senden. Öffnen Sie in Ihrem Browser die folgende URL: `{applicationRoute}/protected`. Beispiel:

	```
	http://my-mobile-backend.mybluemix.net/protected
	```

	Der Endpunkt `/protected` eines mobilen Back-Ends, der mit der Boilerplate 'MobileFirst Services Starter' erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Eine Nachricht `Unauthorized` (Nicht autorisiert) wird in Ihrem Browser zurückgegeben. Diese Nachricht wird deshalb zurückgegeben, weil auf diesen Endpunkt nur mobile Anwendungen zugreifen, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind.

1. Verwenden Sie Ihre Cordova-Anwendung, um eine Anforderung an denselben Endpunkt zu senden. Fügen Sie den folgenden Code hinzu, nachdem Sie `BMSClient` initialisiert haben:

	```Javascript
	var success = function(data){
	console.log("success", data);
	}

	var failure = function(error){
		console.log("failure", error);
	}

	var request = new MFPRequest("/protected", MFPRequest.GET);

	request.send(success, failure);
	```

1. Wenn Ihre Anforderung erfolgreich ist, wird die folgende Ausgabe in der LogCat- oder Xcode-Konsole (abhängig von der verwendeten Plattform) angezeigt:

	![Bild](images/getting-started-android-success.png)

	## Nächste Schritte
	{: #next-steps}

	Wenn Sie eine Verbindung zu dem geschützten Endpunkt hergestellt haben, waren keine Berechtigungsnachweise erforderlich. Wenn Sie die Benutzer zur Anmeldung bei Ihrer Anwendung veranlassen wollen, müssen Sie eine Authentifizierung über Facebook oder Google oder eine angepasste Authentifizierung konfigurieren.
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [Angepasst](custom-auth-cordova.html)
