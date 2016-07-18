<!-- Attribute definitions -->
{:codeblock: .codeblock}
{:screen: .screen}

# Einführung in das Beispiel 'HelloWorld'
{: #gettingstarted-ios}
Wenn Sie mit einer neuen iOS-App beginnen möchten, können Sie die App 'HelloWorld' verwenden. Anhand dieser App wird veranschaulicht, wie von einer mobilen App ohne Authentifizierung eine Verbindung zum {{site.data.keyword.Bluemix}}-Back-End aufgebaut wird. Die App ist bereits mit dem SDK installiert. Wenn Sie bereit sind, können Sie die entsprechenden Bibliotheken abrufen, die Sie in der App verwenden möchten.

1. Erstellen Sie ein mobiles Back-End in {{site.data.keyword.Bluemix_notm}}.
<ol>
	<li>Klicken Sie im Abschnitt 'Boilerplates' des {{site.data.keyword.Bluemix_notm}}-Katalogs auf den **Starter für MobileFirst Services**.</li>
    <li>Geben Sie einen Namen und Host für die App ein und klicken Sie auf **Erstellen**.</li>
    <li>Klicken Sie auf **Fertig stellen**. </li>
</ol>
2. Rufen Sie das Projekt von GitHub ab.
Öffnen Sie auf dem Computer das Terminal und geben Sie anschließend den folgenden Befehl ein:
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld
```

3. Initialisieren Sie das Projekt.
Kopieren Sie zum Initialisieren des SDKs den folgenden Code zur Methode `didFinishLaunchingWithOptions` im Anwendungsdelegierten.
   * Objective-C:
```
// SDK mit IBM Bluemix-Anwendungs-ID und -Route initialisieren
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<insert route>" backendGUID:@"<insertGUID>"];
return YES;
```{: codeblock}
   * Swift:
```
// SDK mit IBM Bluemix-Anwendungs-ID und -Route initialisieren
IMFClient.sharedInstance().initializeWithBackendRoute("<insert route>", backendGUID: "<insertGUID>")
return true
```{: codeblock}

4. Führen Sie das Beispiel in der Entwicklungsumgebung aus.
Klicken Sie in Xcode auf **Product &gt; Run**. Ein iOS-Simulator wird gestartet.
Klicken Sie im Simulator auf **Ping {{site.data.keyword.Bluemix_notm}}**. Von der Beispiel-App wird der Berechtigungsheader vom Mobile Client Access-Service abgerufen. Wenn das Pingsignal erfolgreich ist, wird der Text im Simulator aktualisiert.
<br/>Wenn Sie von der mobilen App in Xcode erfolgreich eine Verbindung zu {{site.data.keyword.Bluemix_notm}} aufbauen, wird die Nachricht 'Yay! You are connected' angezeigt:<br/>
![Verbindung von Anwendung 'Hello World' zu {{site.data.keyword.Bluemix_notm}} erfolgreich aufgebaut](images/yayconnected.jpg "Abbildung 1. Verbindung von Anwendung 'Hello World' zu {{site.data.keyword.Bluemix_notm}} erfolgreich aufgebaut")
<br/>
Wenn Sie die Verbindung erfolgreich aufgebaut haben, enthält der Debug-Anmelde-Xcode die folgende Nachricht:
```
You have connected to {{site.data.keyword.Bluemix_notm}} successfully
```
5. Beheben Sie eventuelle Probleme.
Wenn die Verbindung fehlschlägt, wird die Nachricht 'Bummer Something went wrong' angezeigt. Weitere Informationen zum Fehler werden angegeben.<br/>
![Von der Anwendung 'Hello World' wurde keine Verbindung zu {{site.data.keyword.Bluemix_notm}} aufgebaut](images/bummer_android.jpg "Abbildung 2. Von der Anwendung 'Hello World' wurde keine Verbindung zu Bluemix aufgebaut")
<br/>Stellen Sie sicher, dass Sie die Werte für Route und GUID ordnungsgemäß eingefügt haben:
   * Objective-C:
  ```
  [imfClient initializeWithBackendRoute:@"https://hellotest.mybluemix.net"
  backendGUID:@"9d48d73a-0878-4254-test-bdcbe6c79c31"];
  ``` {: codeblock}
   * Swift:
  ```
  IMFClient.sharedInstance().initializeWithBackendRoute("https://hellotest.mybluemix.net", backendGUID: "9d48d73a-0878-4254-test-bdcbe6c79c31")
  ```{: codeblock}


Sie können auch das Debugprotokoll auf weitere Informationen überprüfen.

## Nächste Schritte:
{: #next}
Informationen zum Abrufen und Integrieren des SDKs in die mobile App finden Sie in den Informationen zum Konfigurieren der {{site.data.keyword.Bluemix}}-Services.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# Zugehörige Links

## Beispiele
   * [HelloWorld (iOS)](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld)

## SDK
   * [bms-clientsdk-ios-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-ios-core)

## API
   *
[API-Kerndefinitionen](https://www.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)
