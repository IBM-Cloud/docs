---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Einführung in das Beispiel 'Hello Bluemix for iOS'
{: #gettingstarted-android}
*Letzte Aktualisierung: 1. Juni 2016*
{: .last-updated}  

Wenn Sie mit einer neuen iOS-App arbeiten möchten, können Sie die App 'HelloWorld' verwenden. Diese App zeigt, wie Sie ohne Authentifizierung eine Verbindung von einer mobilen App zu Ihrem {{site.data.keyword.Bluemix}}-Back-End herstellen können. Für die App ist das SDK bereits installiert. Wenn Sie bereit sind, können Sie die spezifischen Bibliotheken abrufen, die Sie in Ihrer App verwenden möchten.

1. Erstellen Sie Ihr mobiles Back-End in {{site.data.keyword.Bluemix_notm}}.
    1. Klicken Sie im Abschnitt mit den Boilerplates im {{site.data.keyword.Bluemix_notm}}-Katalog auf 'MobileFirst Services Starter'.
    2. Geben Sie einen Namen und einen Host für Ihre App ein und klicken Sie auf **Erstellen**.
    3. Klicken Sie auf **Fertigstellen**.
2. Rufen Sie das Projekt aus GitHub ab. Sie können zum Abrufen des Projekts optional den Befehl 'git clone' verwenden. Öffnen Sie auf Ihrem Computer das Terminal und geben Sie anschließend den folgenden Befehl ein:
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld.git
    ```

3. Initialisieren Sie das Projekt. Kopieren Sie zum Initialisieren des SDK den folgenden Code in die Methode `didFinishLaunchingWithOptions` im Anwendungs-Delegat.

	###Objective-C
	{: initializeobjc}

	**Wichtig**: Es besteht weiter eine vollständige Unterstützung für das Objective-C-SDK und es wird weiterhin als primäres SDK für {{site.data.keyword.Bluemix}} Mobile Services betrachtet, bis dieses SDK wahrscheinlich zu einem späteren Zeitpunkt in diesem Jahr zugunsten des neuen Swift-SDK eingestellt wird.

	Mit dem Objective-C-SDK werden Überwachungsdaten an die Überwachungskonsole des Service {{site.data.keyword.amashort}} gemeldet. Wenn Sie die Überwachungsfunktionen des Service {{site.data.keyword.amashort}} benötigen, verwenden Sie weiterhin das Objective-C-SDK.

	```
	// initialize SDK with IBM Bluemix application ID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<insert route>" backendGUID:@"<insertGUID>"];
return YES;
	```

	###Swift
	{: initializeswift}
	```
	// initialize SDK with IBM Bluemix application ID and route
IMFClient.sharedInstance().initializeWithBackendRoute("<insert route>", backendGUID: "<insertGUID>")
return true
	```

4. Führen Sie das Beispiel in Ihrer Entwicklungsumgebung aus. Klicken Sie in Xcode auf **Product&gt;Run**. Ein iOS-Simulator wird
gestartet.
5. Klicken Sie im Simulator auf **Ping {{site.data.keyword.Bluemix_notm}}**. Die Beispiel-App
ruft den Berechtigungsheader vom Service 'Mobile Client Access' ab. Wenn
der Pingbefehl erfolgreich ausgeführt wurde, wird der Text im Simulator aktualisiert.

  Wenn Sie in Xcode erfolgreich eine Verbindung zwischen der mobilen App und {{site.data.keyword.Bluemix_notm}} hergestellt haben, wird die folgende Nachricht angezeigt:

  `Yay! You are connected`
  {: screen}

  ![Verbindung zwischen Anwendung 'Hello World' und {{site.data.keyword.Bluemix_notm}} erfolgreich hergestellt](images/yayconnected.jpg "Abbildung 1. Verbindung zwischen Anwendung 'Hello World' und und Bluemix erfolgreich hergestellt")

  Falls die Verbindung fehlschlägt, wird folgende Nachricht angezeigt:
  `Bummer. Something went wrong`
  {: screen}

  ![Verbindung zwischen Anwendung 'Hello World' und Bluemix nicht hergestellt](images/bummer_android.jpg "Abbildung 2. Verbindung zwischen Anwendung 'Hello World' und Bluemix nicht hergestellt")

	Sie können für die fehlgeschlagene Verbindung folgende Fehlerbehebungsmaßnahme durchführen:
	* Überprüfen Sie, dass Sie die Werte für die Route und die GUID ordnungsgemäß eingefügt haben.
		####Objective-C
		{: #objcvals}
		```
		[imfClient initializeWithBackendRoute:@"https://hellotest.mybluemix.net"
  backendGUID:@"9d48d73a-0878-4254-test-bdcbe6c79c31"];
		```

		####Swift
		{: #swiftvals}
		```
		IMFClient.sharedInstance().initializeWithBackendRoute("https://hellotest.mybluemix.net", backendGUID: "9d48d73a-0878-4254-test-bdcbe6c79c31")
		```

	* Weitere Informationen finden Sie im Debugprotokoll.


## Nächste Schritte:
{: #next}
Informationen zum Abrufen des SDK und zum Integrieren in Ihre mobile Anwendung finden Sie in den Informationen zum Einrichten der Bluemix-Services.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# Zugehörige Links

## Beispiele
   * [Hello Bluemix - Beispiel](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld)

## SDK
   * [Core SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## API
   * [Core API](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
