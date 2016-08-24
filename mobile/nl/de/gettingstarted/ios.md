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

Wenn Sie mit einer neuen iOS-App arbeiten möchten, können Sie die App 'Hello Bluemix' verwenden. Diese App zeigt, wie Sie ohne Authentifizierung eine Verbindung von einer mobilen App zu Ihrem {{site.data.keyword.Bluemix}}-Back-End herstellen können. Wenn Sie bereit sind, können Sie die spezifischen Bibliotheken abrufen, die Sie in Ihrer App verwenden möchten.

1. Erstellen Sie Ihr mobiles Back-End in {{site.data.keyword.Bluemix_notm}}.
    1. Klicken Sie im Abschnitt mit den Boilerplates im {{site.data.keyword.Bluemix_notm}}-Katalog auf 'MobileFirst Services Starter'.
    2. Geben Sie einen Namen und einen Host für Ihre App ein und klicken Sie auf **Erstellen**.
    3. Klicken Sie auf **Fertigstellen**.
2. Führen Sie die Beispielanwendung 'Hello Bluemix' aus:
	1. Rufen Sie das Projekt aus GitHub ab. Sie können zum Abrufen des Projekts optional den Befehl 'git clone' verwenden. Öffnen Sie auf Ihrem Computer das Terminal und geben Sie den folgenden Befehl ein:
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellobluemix.git
    ```
	2. Führen Sie den Befehl `pod install` im Verzeichnis `bms-samples-swift-hellobluemix` aus, im dem das Projekt geklont wurde. Wenn Sie Cocoapods noch nicht installiert haben, rufen Sie es unter [https://cocoapods.org](https://cocoapods.org) ab.
	3. Öffnen Sie den Xcode-Arbeitsbereich mit dem Befehl `open HelloBluemix.xcworkspace`.
	4. Aktualisieren Sie in der Datei `AppDelegate.swift` die Werte für 'appRoute' und 'appGuid' so, dass sie denen entsprechen, die aus dem zu einem früheren Zeitpunkt erstellten Bluemix-Back-End stammen.

3. Führen Sie das Beispiel in Ihrer Entwicklungsumgebung aus. Klicken Sie in Xcode auf **Product&gt;Run**. Ein iOS-Simulator wird
gestartet.

	**Wichtig:** Ihre 'appRoute' muss das Protokoll `https` und nicht das Protokoll `http` verwenden; ansonsten kommt es möglicherweise aufgrund der Transportsicherheitseinstellungen der App zu einem Verbindungsfehler. Weitere Informationen zu diesen Einstellungen finden Sie im Blogbeitrag [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/).

4. Klicken Sie im Simulator auf **Ping {{site.data.keyword.Bluemix_notm}}**. Die Beispiel-App
ruft den Berechtigungsheader vom Service 'Mobile Client Access' ab. Wenn
der Pingbefehl erfolgreich ausgeführt wurde, wird der Text im Simulator aktualisiert.

  Wenn Sie in Xcode erfolgreich eine Verbindung zwischen der mobilen App und {{site.data.keyword.Bluemix_notm}} hergestellt haben, wird die folgende Nachricht angezeigt:
  `Yay! You are connected`
  {: screen}

  <!--
  ![Hello World application successfully connected to {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figure 1. Hello World application successfully connected to Bluemix")
-->

  Falls die Verbindung fehlschlägt, wird folgende Nachricht angezeigt:
  `Bummer. Something went wrong`
  {: screen}

 <!--
  ![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")
  -->

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
   * [Hello Bluemix - Beispiel (iOS)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellobluemix)

## SDK
   * [Core SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## API
   * [Core API](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
