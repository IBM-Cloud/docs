---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Einführung in das Beispiel 'Hello Bluemix for Android'
{: #gettingstarted-android}
*Letzte Aktualisierung: 27. Mai 2016*
{: .last-updated}  

Wenn Sie mit einer neuen Android-Anwendung arbeiten möchten, können Sie die App 'HelloWorld' verwenden. Diese App zeigt, wie Sie ohne Authentifizierung eine Verbindung von einer mobilen App zu Ihrem {{site.data.keyword.Bluemix}}-Back-End herstellen können. Für die App
ist das SDK bereits installiert. Wenn Sie bereit sind, können Sie die spezifischen Bibliotheken abrufen, die Sie in Ihrer App verwenden möchten.

1. Erstellen Sie Ihr mobiles Back-End in {{site.data.keyword.Bluemix_notm}}.
    1. Klicken Sie im Abschnitt mit den Boilerplates im {{site.data.keyword.Bluemix_notm}}-Katalog auf 'MobileFirst Services Starter'.
    2. Geben Sie einen Namen und einen Host für Ihre App ein und klicken Sie auf **Erstellen**.
    3. Klicken Sie auf **Fertigstellen**.
2. Rufen Sie das Projekt aus GitHub ab. Sie können zum Abrufen des Projekts optional den Befehl 'git clone' verwenden. Öffnen Sie auf Ihrem Computer das Terminal und geben Sie anschließend den folgenden Befehl ein:
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld.git
    ```

3. Initialisieren Sie das Projekt, indem Sie &lt;ANWENDUNGSROUTE&gt; und &lt;ANWENDUNGS-ID&gt; durch Ihre Anwendungsroute und GUID im Block `try` innerhalb der Funktion `BMSClient.getInstance().initialize()` ersetzen:
```
// initialize SDK with IBM Bluemix application ID and route
BMSClient.getInstance().initialize(this, "<ANWENDUNGSROUTE>", "<ANWENDUNGS-ID>");
```
4. Führen Sie das Beispiel in Ihrer Entwicklungsumgebung aus.
Klicken Sie in der Symbolleiste von Android Studio auf die Schaltfläche zur Wiedergabe und wählen Sie einen Simulator aus.
5. Klicken Sie im Simulator auf **Ping {{site.data.keyword.Bluemix_notm}}**. Die Beispiel-App sendet eine GET-Anforderung an die `Node.js`-Laufzeit in {{site.data.keyword.Bluemix_notm}}. Wenn die Anforderung erfolgreich ist, wird die Verbindung bestätigt und der Text im Simulator wird aktualisiert.

  **Anmerkung:** Der Code der `Node.js`-Laufzeit wird in der Boilerplate 'MobileFirst Services Starter' bereitgestellt. Wenn die Back-End-Anwendung nicht mit der Boilerplate 'MobileFirst Services Starter' erstellt wurde, ist das Herstellen einer Verbindung durch die Anwendung nicht erfolgreich.

  Wenn Sie in Android Studio erfolgreich eine Verbindung zwischen der mobilen App und {{site.data.keyword.Bluemix_notm}} hergestellt haben, wird die folgende Nachricht angezeigt:

  `Yay! You are connected`
  {: screen}

  ![Verbindung zwischen Anwendung 'Hello World' und {{site.data.keyword.Bluemix_notm}} erfolgreich hergestellt](images/yayconnected.jpg "Abbildung 1. Verbindung zwischen Anwendung 'Hello World' und und Bluemix erfolgreich hergestellt")

  Falls die Verbindung fehlschlägt, wird folgende Nachricht angezeigt:
  `Bummer. Something went wrong`
  {: screen}

  ![Verbindung zwischen Anwendung 'Hello World' und Bluemix nicht hergestellt](images/bummer_android.jpg "Abbildung 2. Verbindung zwischen Anwendung 'Hello World' und Bluemix nicht hergestellt")

  Sie können für die fehlgeschlagene Verbindung folgende Fehlerbehebungsmaßnahme durchführen:
   * Überprüfen Sie, dass Sie die Werte für die Route und die GUID ordnungsgemäß eingefügt haben.
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
