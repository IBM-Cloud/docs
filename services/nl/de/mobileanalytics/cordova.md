<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Einführung in das Beispiel 'HelloWorld'
{: #gettingstarted-cordova}

Wenn Sie mit einer neuen Cordova-Anwendung beginnen möchten, können Sie die App 'HelloWorld' verwenden. Anhand dieser App wird veranschaulicht, wie von einer mobilen App ohne Authentifizierung eine Verbindung zum Bluemix-Back-End aufgebaut wird. Die App ist bereits mit dem SDK installiert. Wenn Sie bereit sind, können Sie die entsprechenden Bibliotheken abrufen, die Sie in der App verwenden möchten.

1. Erstellen Sie ein mobiles Back-End in Bluemix.
<ol>
	<li>Klicken Sie im Abschnitt 'Boilerplates' des Bluemix-Katalogs auf den Starter für MobileFirst Services.</li>
    	<li>Geben Sie einen Namen und Host für die App ein und klicken Sie auf **Erstellen**.</li>
    	<li>Klicken Sie auf **Fertig stellen**. </li>
</ol>
2. Rufen Sie das Projekt von GitHub ab. Optional können Sie den Befehl 'git clone' zum Abrufen des Projekts verwenden. Öffnen Sie auf dem Computer das Terminal und geben Sie den folgenden Befehl ein:
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld
```

3. Führen Sie die folgenden Befehle im Projektverzeichnis aus, um die Android- und iOS-Plattformumgebungen hinzuzufügen:

Android:
```
cordova platform add android
```

iOS:
```
cordova platform add ios
```

4. Fügen Sie das Cordova-Plug-in mit dem folgenden Befehl hinzu:
```
cordova plugin add ibm-mfp-core
```

5. Konfigurieren Sie die Cordova-App für Android, iOS oder beide Betriebssysteme.

 * Android

	 Erstellen Sie vor dem Öffnen des Projekts in Android Studio die Cordova-Anwendung und führen Sie sie in der Befehlszeilenschnittstelle (CLI) aus, um Buildfehler zu vermeiden.

	 ```
	 cordova build android
	 ```

	 ```
	 cordova run android
	 ```

 * iOS

	 Konfigurieren Sie das Xcode-Projekt wie folgt, um Buildfehler zu vermeiden.

	    1. Verwenden Sie die neueste Version von Xcode zum Öffnen der Datei 'xcode.proj' im Verzeichnis '&lt;app_name&gt;/platforms/ios'.

			**Wichtig:** Wenn Sie die Nachricht 'Convert to Latest Swift Syntax' empfangen, klicken Sie auf die Schaltfläche zum Abbrechen.

		2. Wechseln Sie zu **Build Settings > Swift Compiler - Code Generation > Objective-C Bridging Header** und fügen Sie den folgenden Pfad hinzu:

		```
		<your_project_name>/Plugins/ibm-mfp-core/Bridging-Header.h
		```
		3. Wechseln Sie zu **Build settings > Linking > Runpath Search Paths** und fügen Sie die folgenden Frameworks-Parameter hinzu:

		```
		@executable_path/Frameworks
		```
		4. Erstellen Sie die Anwendung mit Xcode und führen Sie sie aus.

6. Beispiel 'HelloWorld' konfigurieren
<ol>
	<li>Wechseln Sie in das Verzeichnis, in dem Sie das Projekt geklont haben.</li>
	<li>Öffnen Sie die Datei '&lt;your_app_dir&gt;/www/js/index.js' und ersetzen Sie &lt;APPLICATION_ROUTE&gt; und &lt;APPLICATION_ID&gt; durch die Werte für die Bluemix-Anwendungs-ID und -Route.</li>
</ol>

Hinweis: Stellen Sie sicher, dass von &lt;APPLICATION_ROUTE&gt; das sichere HTTPS-Protokoll verwendet wird.

```
// Bluemix-Berechtigungsnachweise
route: "<APPLICATION_ROUTE>",
GUID: "<APPLICATION_GUID>",
```

7. Führen Sie das Beispiel im mobilen Emulator oder auf dem Mobilgerät aus.

   Erstellen Sie die Cordova-App mit den folgenden Befehlen:
	 ```
	 cordova build ios
	 ```
	 ```
	 cordova build android
	 ```

   Führen Sie die Beispiel-App mit den folgenden Befehlen aus:
	 ```
	 cordova run ios
	 ```
   ```
	 cordova run android
	 ```


Eine Gesamtansichtanwendung mit der Schaltfläche **PING BLUEMIX** wird angezeigt. Wenn Sie die Schaltfläche antippen, wird von der Anwendung die Verbindung vom Client zur Back-End-Bluemix-Anwendung getestet. Die Verbindung wird unter Verwendung der Anwendungsroute getestet, die Sie in der Datei 'index.js' angegeben haben.


![Verbindung von Anwendung 'Hello World' zu Bluemix erfolgreich aufgebaut](images/yayconnected.jpg "Abbildung 1. Verbindung von Anwendung 'Hello World' zu Bluemix erfolgreich aufgebaut")

Wenn Sie von der mobilen App erfolgreich eine Verbindung zu Bluemix aufgebaut haben, wird die Nachricht 'Yay! You are connected' angezeigt.
8. Beheben Sie eventuelle Probleme.

<!--![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")-->

Wenn die Verbindung fehlschlägt, wird die Nachricht 'Bummer Something went wrong' angezeigt. Weitere Informationen zum Fehler werden angegeben.
Überprüfen Sie Folgendes:
 * Stellen Sie sicher, dass Sie die Werte für Route und GUID ordnungsgemäß eingefügt haben.
 * Zeigen Sie das Xcode- oder Android-Debugprotokoll an.
 * Überprüfen Sie den Status der App in Bluemix.

## Nächste Schritte:
{: #next}
Informationen zum Abrufen und Integrieren des SDKs in die mobile App finden Sie in den Informationen zum Konfigurieren des Cordova-Client-SDKs.

# Zugehörige Links

## Beispiele
   * [HelloWorld (Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld)

## SDK
   * [bms-clientsdk-cordova-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

<!--## api
   * [Core API](https://www.{DomainName}/docs/api/content/api/mobilefirst/cordova/core-api-doc/overview-summary.html)
-->
