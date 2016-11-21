---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Benutzer und Shield-Zuordnungen erstellen
{: #gettingstartedtemplate}
Letzte Aktualisierung: 15. September 2016
{: .last-updated}

Wenn Sie den Service {{site.data.keyword.iotinsurance_short}} erstellt und die erforderlichen unterstützenden Services und Apps bereitgestellt haben, können Sie den Service testen, indem Sie einen berechtigten Benutzer und eine Shield-Zuordnung erstellen.
{:shortdesc}

**Voraussetzungen:** Stellen Sie zunächst sicher, dass folgende Voraussetzungen erfüllt sind:

- [Node.js](https://nodejs.org/en/) ist auf Ihrem Computer installiert.  
- Eine Node.js-fähige Laufzeitumgebung wie z. B. Eclipse ist vorhanden.
- Git-Software und Zugriff auf das [GitHub-Quellcode-Repository für die API-Beispiele ist vorhanden](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs).   Alternativ können Sie das [Archiv mit den Quellcodedateien herunterladen](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/archive/master.zip).
- Vorbereiteter Quellcode.  
  Führen Sie die folgenden Schritte aus, um den Quellcode vorzubereiten:
  1. Klonen Sie das [GitHub-Quellcode-Repository](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs) oder laden Sie es auf Ihren Computer herunter.
  2. Installieren Sie die Open-Source-Voraussetzungen des Projekts, indem Sie über eine Eingabeaufforderung in den Ordner wechseln, der die geklonten Quellcodedateien enthält, und dort den Befehl `npm install` ausführen.

Erstellen Sie einen Benutzer, den Sie verwenden können, um die Features des Dashboards und die mobile Beispiel-App zu testen.

1. Erstellen Sie einen Benutzer im {{site.data.keyword.iotinsurance_short}}-System.
  1. Bearbeiten Sie die Datei createUser.js, um die Werte in der Variablen **user** durch eindeutige Benutzerinformationen zu ersetzen.
  2. Speichern Sie die Datei.
  3. Führen Sie `node createUser.js` aus. Der Prozess nimmt eine gewisse Zeit in Anspruch.
  4. Notieren Sie sich den Benutzernamen. Sie benötigen ihn im nächsten Schritt.
2. Erstellen Sie eine Shield-Zuordnung für den Benutzer.
  1. Bearbeiten Sie die Datei createUserShieldAssociation.js, um den Benutzernamen aus dem vorherigen Schritt in der Variablen **username** hinzuzufügen.
  2. Speichern Sie die Datei.
  3. Führen Sie `node createUserShieldAssociation.js` aus. Weitere Informationen zu Shields finden Sie im Abschnitt [Komponenten](iotinsurance_overview.html#components).
3. (Optional) Die Analyseengine wird automatisch aktualisiert. Wenn aber nicht die richtigen Daten angezeigt werden, können Sie die Analyseengine durch Ausführen von `node updateAnalyticsEngine.js` aktualisieren.
4. (Optional) Simulieren Sie ein Gefahrenereignis für den Benutzer.
  1. Bearbeiten Sie die Datei simulateHazard.js, um den Benutzernamen aus den vorherigen Schritten in der Variablen **usr** hinzuzufügen.
  2. Speichern Sie die Datei.
  3. Führen Sie `node simulateHazard.js` aus.
5. (Optional) Erstellen Sie simulierte Langzeitdaten, indem Sie `node createHistoricalData.js` ausführen.


# Zugehörige Links
{: #rellinks}

## API-Referenz
{: #api}
* [{{site.data.keyword.iotinsurance_short}}-API-Beispiele](https://iot4i-docs-api.mybluemix.net/dist/){:new_window}

## Zugehörige Links
{: #general}
* [Support-Forum für Entwickler](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Stack Overflow-Support-Forum](http://stackoverflow.com/questions/tagged/ibm-bluemix)
