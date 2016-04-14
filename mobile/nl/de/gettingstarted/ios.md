<!-- Attribute definitions -->
{:codeblock: .codeblock}
{:screen: .screen}

# Einführung in das Beispiel 'HelloWorld'
{: #gettingstarted-ios}
*Letzte Aktualisierung: 28. Januar 2016*
Wenn Sie mit einer neuen iOS-App arbeiten möchten, können Sie die App 'HelloWorld' verwenden. Diese App zeigt, wie Sie ohne Authentifizierung eine Verbindung von einer mobilen App zu Ihrem {{site.data.keyword.Bluemix}}-Back-End herstellen können. Für die App ist das SDK bereits installiert. Wenn Sie bereit sind, können Sie die spezifischen Bibliotheken abrufen, die Sie in Ihrer App verwenden möchten.

1. Erstellen Sie Ihr mobiles Back-End in {{site.data.keyword.Bluemix_notm}}.
<ol>
	<li>Klicken Sie im Abschnitt für Boilerplates im {{site.data.keyword.Bluemix_notm}}-Katalog auf **MobileFirst Services Starter**.</li>
    <li>Geben Sie einen Namen und einen Host für Ihre App ein und klicken Sie auf **Erstellen**.</li>
    <li>Klicken Sie auf **Fertigstellen**. </li>
</ol>
2. Rufen Sie das Projekt aus GitHub ab.
Öffnen Sie auf Ihrem Computer das Terminal und geben Sie den folgenden Befehl ein:
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld
```

3. Initialisieren Sie das Projekt.
Kopieren Sie zum Initialisieren des SDK den folgenden Code in die Methode `didFinishLaunchingWithOptions` im Anwendungs-Delegat.
   * Objective-C:
```
// initialize SDK with IBM Bluemix application ID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<insert route>" backendGUID:@"<insertGUID>"];
return YES;
```{: codeblock}
   * Swift:
```
// initialize SDK with IBM Bluemix application ID and route
IMFClient.sharedInstance().initializeWithBackendRoute("<insert route>", backendGUID: "<insertGUID>")
return true
```{: codeblock}

4. Führen Sie das Beispiel in Ihrer Entwicklungsumgebung aus.
Klicken Sie in Xcode auf **Product&gt;Run**. Ein iOS-Simulator wird
gestartet.
Klicken Sie im Simulator auf **Ping {{site.data.keyword.Bluemix_notm}}**. Die Beispiel-App
ruft den Berechtigungsheader vom Service 'Mobile Client Access' ab. Wenn
der Pingbefehl erfolgreich ausgeführt wurde, wird der Text im Simulator aktualisiert.
<br/>Wenn Sie erfolgreich eine Verbindung von der mobilen App in Xcode zu {{site.data.keyword.Bluemix_notm}} hergestellt haben, wird folgende Nachricht angezeigt: "Yay! You are connected".:<br/>
![Verbindung zwischen Anwendung 'Hello World' und {{site.data.keyword.Bluemix_notm}} erfolgreich hergestellt](images/yayconnected.jpg "Bild 1. Verbindung zwischen Anwendung 'Hello World' und {{site.data.keyword.Bluemix_notm}} erfolgreich hergestellt")
<br/>
Wenn die Verbindung erfolgreich hergestellt wurde, enthält das Debugprotokoll in Xcode die folgende Nachricht:
```You have connected to {{site.data.keyword.Bluemix_notm}} successfully```
5. Beheben Sie eventuelle Probleme.
Wenn die Verbindung fehlschlägt, wird die Nachricht 'Bummer Something went wrong' angezeigt. Außerdem werden weitere Informationen zu dem Fehler angegeben.<br/>
![Verbindung zwischen Anwendung 'Hello World' und {{site.data.keyword.Bluemix_notm}} nicht hergestellt](images/bummer_android.jpg "Bild 2. Verbindung zwischen Anwendung 'Hello World' und Bluemix nicht hergestellt")
<br/>Überprüfen Sie, dass Sie die Route und die GUID ordnungsgemäß eingefügt haben:
   * Objective-C:
  ```
  [imfClient initializeWithBackendRoute:@"https://hellotest.mybluemix.net"
  backendGUID:@"9d48d73a-0878-4254-test-bdcbe6c79c31"];
  ``` {: codeblock}
   * Swift:
  ```
  IMFClient.sharedInstance().initializeWithBackendRoute("https://hellotest.mybluemix.net", backendGUID: "9d48d73a-0878-4254-test-bdcbe6c79c31")
  ```{: codeblock}


Weitere Informationen finden Sie auch im Debugprotokoll.

## Nächste Schritte:
{: #next}
Informationen zum Abrufen des SDK und zum Integrieren in Ihre mobile Anwendung finden Sie in den Informationen zum Einrichten der {{site.data.keyword.Bluemix}}-Services.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# Zugehörige Links

## Beispiele
   * [Beispiel 'HelloWorld'](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld)

## SDK
   * [Core SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-ios-core)

## API
   *
[Core API](https://classicdocs.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)
