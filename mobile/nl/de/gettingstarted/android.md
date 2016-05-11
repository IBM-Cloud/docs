<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Einführung in das Beispiel 'HelloWorld'
{: #gettingstarted-android}
*Letzte Aktualisierung: 28. Januar 2016*  

Wenn Sie mit einer neuen Android-Anwendung arbeiten möchten, können Sie die App 'HelloWorld' verwenden. Diese App zeigt, wie Sie ohne Authentifizierung eine Verbindung von einer mobilen App zu Ihrem {{site.data.keyword.Bluemix}}-Back-End herstellen können. Für die App
ist das SDK bereits installiert. Wenn Sie bereit sind, können Sie die spezifischen Bibliotheken abrufen, die Sie in Ihrer App verwenden möchten.

1. Erstellen Sie Ihr mobiles Back-End in {{site.data.keyword.Bluemix_notm}}.
    1. Klicken Sie im Abschnitt für Boilerplates im {{site.data.keyword.Bluemix_notm}}-Katalog auf 'MobileFirst Services Starter'.
    2. Geben Sie einen Namen und einen Host für Ihre App ein und klicken Sie auf **Erstellen**.
    3. Klicken Sie auf **Fertigstellen**.
2. Rufen Sie das Projekt aus GitHub ab. Sie können zum Abrufen des Projekts optional den Befehl 'git clone' verwenden. Öffnen Sie auf Ihrem Computer das Terminal und geben Sie anschließend den folgenden Befehl ein:
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld.git
```
Laden Sie vor dem Start die Datei `Gradle.zip` herunter und installieren Sie Gradle durch Extrahieren der heruntergeladenen komprimierten Datei in ein Verzeichnis Ihrer Wahl. Von Android Studio werden Sie beim ersten Importieren des Beispiels möglicherweise nach dem Ausgangsverzeichnis GRADLE HOME gefragt. Geben Sie hierfür den Pfad zum Verzeichnis 'bin' in der extrahierten Datei `Gradle.zip` an. Die Datei `build.gradle` erstellt Ihr Projekt durch automatisches Anziehen der erforderlichen Abhängigkeiten.
3. Initialisieren Sie das Projekt.
Ersetzen Sie zum Initialisieren des SDK &lt;ANWENDUNGSROUTE&gt; und &lt;ANWENDUNGS-ID&gt; durch Ihre Anwendungsroute und GUID im Block 'try' innerhalb der Funktion `BMSClient.getInstance().initialize()`:
```
// initialize SDK with IBM Bluemix application ID and route
BMSClient.getInstance().initialize(this, "<ANWENDUNGSROUTE>", "<ANWENDUNGS-ID>");
```{: codeblock}

4. Führen Sie das Beispiel in Ihrer Entwicklungsumgebung aus.
Klicken Sie in der Android Studio-Symbolleiste auf die Wiedergabetaste und wählen Sie einen Simulator aus.
Klicken Sie im Simulator auf **Ping {{site.data.keyword.Bluemix_notm}}**. Die Beispielanwendung sendet eine GET-Anforderung an eine geschützte Ressource in der Node.js-Laufzeit in {{site.data.keyword.Bluemix_notm}}. Wenn die Anforderung erfolgreich ist, wird die Verbindung bestätigt und der Text im Simulator wird aktualisiert.
<br/>**Hinweis:** Der Code der Node.js-Laufzeit wird in der Boilerplate 'MobileFirst Services Starter' bereitgestellt. Wenn die Back-End-Anwendung nicht mit der Boilerplate 'MobileFirst Services Starter' erstellt wurde, ist das Herstellen einer Verbindung durch die Anwendung nicht erfolgreich.<br/>
Wenn Sie erfolgreich eine Verbindung zwischen der mobilen App und {{site.data.keyword.Bluemix_notm}} in Adroid Studio hergestellt haben, wird die folgende Nachricht angezeigt: 'Yay! You are connected'.<br/>
![Verbindung zwischen Anwendung 'Hello World' und {{site.data.keyword.Bluemix_notm}} erfolgreich hergestellt](images/yayconnected.jpg "Bild 1. Verbindung zwischen Anwendung 'Hello World' und Bluemix erfolgreich hergestellt")

5. Beheben Sie eventuelle Probleme.<br/>Wenn die Verbindung fehlschlägt, wird die Nachricht 'Bummer. Something went wrong' angezeigt:</br>
![Verbindung zwischen Anwendung 'Hello World' und Bluemix nicht hergestellt](images/bummer_android.jpg "Bild 2. Verbindung zwischen Anwendung 'Hello World' und Bluemix nicht hergestellt")
<br/>
Prüfen Sie die folgenden Punkte:
 * Überprüfen Sie, dass Sie die Werte für die Route und die GUID ordnungsgemäß eingefügt haben.
 * Weitere Informationen finden Sie auch im Debugprotokoll.

## Nächste Schritte:
{: #next}
Informationen zum Abrufen des SDK und zum Integrieren in Ihre mobile Anwendung finden Sie in den Informationen zum Einrichten der Bluemix-Services.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# Zugehörige Links

## Beispiele
   * [Beispiel 'HelloWorld'](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld)

## SDK
   * [Core SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## API
   * [Core API](https://classicdocs.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
