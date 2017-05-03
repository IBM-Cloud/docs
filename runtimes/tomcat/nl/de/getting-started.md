---

copyright:
  years: 2017
lastupdated: "2017-04-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Erste Schritte mit Tomcat unter Bluemix
{: #getting_started}

* {: download} Herzlichen Glückwunsch! Sie haben die Hello World-Beispielanwendung unter {{site.data.keyword.Bluemix}} bereitgestellt! Befolgen Sie diesen schrittweisen Leitfaden, um zu starten. Oder laden Sie den <a class="xref" href="http://bluemix.net" target="_blank" title="(Beispielcode herunterladen) "><img class="hidden" src="../../images/btn_starter-code.svg" alt="Beispielcode herunterladen" />Beispielcode herunter</a> und beginnen Sie auf eigene Faust.

Wenn Sie diesem Leitfaden folgen, werden Sie eine Entwicklungsumgebung einrichten, eine App lokal und unter {{site.data.keyword.Bluemix}} bereitstellen und einen {{site.data.keyword.Bluemix}}-Datenbankservice in Ihre App integrieren.

## Voraussetzungen
{: #prereqs}

Sie benötigen Folgendes: 
* [{{site.data.keyword.Bluemix_notm}} Konto](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry-CLI ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Eclipse IDE for Java EE Developers ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}
* [Git ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://git-scm.com/downloads){: new_window}
* [Maven ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://maven.apache.org/download.cgi){: new_window}
* [Apache Tomcat Version 8.0.41 ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://tomcat.apache.org/download-80.cgi#8.0.41 ){: new_window}


## 1. Klonen Sie die Beispielapp.
{: #clone}

Jetzt können Sie beginnen, mit der Tomcat-Beispielapp zu arbeiten. Klonen Sie das Repository und wechseln Sie in das Verzeichnis, in dem sich die Beispielapp befindet. 
```
git clone https://github.com/IBM-Bluemix/get-started-tomcat
```
{: pre}

```
cd get-started-tomcat
```
{: pre}

Lesen Sie die Dateien im Verzeichnis *get-started-tomcat*, um sich mit deren Inhalt vertraut zu machen. 

## 2. Führen Sie die App lokal aus.
{: #run_locally}

Sie müsen die Abhängigkeiten installieren und wie in der Datei 'pom.xml' definiert eine .war-Datei erstellen, um die App auszuführen. 

Installieren Sie die Abhängigkeiten.

```
mvn clean install  
```
{: pre}


Kopieren Sie die Datei 'GetStartedTomcat.war' vom Verzeichnis `target` in Ihr `webapps`-Verzeichnis `tomcat-install-dir`. 

Führen Sie die App aus.  
```
<tomcat-install-dir>/bin/startup.bat|.sh
```
{: screen}

Ihre App finden Sie unter: http://localhost:8080/GetStartedTomcat/

Verwenden Sie `shutdown.bat|.sh`, um Ihre App zu stoppen. Beachten Sie, dass Sie möglicherweise den Befehlen eine Ausführungsberechtigung erteilen müssen.
{: tip}

## 3. Bereiten Sie die App für die Bereitstellung unter {{site.data.keyword.Bluemix_notm}} vor.
{: #prepare}

Für die Bereitstellung unter {{site.data.keyword.Bluemix_notm}} kann es hilfreich sein, die Datei 'manifest.yml' zu installieren. Die Datei 'manifest.yml' enthält Basisinformationen zu Ihrer App wie den Namen, wieviel Speicher für jede Instanz zugeordnet werden soll und die Route. Wir haben eine Beispieldatei 'manifest.yml' im Verzeichnis `get-started-tomcat` bereitgestellt. 

Öffnen Sie die Datei 'manifest.yml' und ändern Sie die Angabe für `name` von `GetStartedTomcat` in den Namen Ihrer App <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
  - name: GetStartedTomcat
    random-route: true
    memory: 256M
    path: target/TomcatHelloWorldApp.war
    buildpack: java_buildpack
  ```
  {: codeblock}

In dieser Datei 'manifest.yml' generiert **random-route: true** eine zufällige Route für Ihre App, um zu verhindern, dass Ihre Route mit anderen Routen kollidiert. Wenn Sie möchten, können Sie **random-route: true** durch **host: myChosenHostName** ersetzen und einen Hostnamen Ihrer Wahl angeben. [Weitere Informationen...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. Stellen Sie die App bereit.
{: #deploy}

Sie können die Cloud Foundry-CLI verwenden, um Apps bereitzustellen.

Wählen Sie Ihren API-Endpunkt aus.

```
cf api <API-endpoint>
```
{:pre}

Ersetzen Sie *API-endpoint* im Befehl durch einen API-Endpunkt aus der folgenden Liste: 

|URL                             | Bereich        |
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net     | USA (Süden)    |
| https://api.eu-gb.bluemix.net  | Großbritannien |
| https://api.au-syd.bluemix.net | Sydney         |


Melden Sie sich bei Ihrem {{site.data.keyword.Bluemix_notm}}-Konto an: 

```
cf login
```
{: pre}

Übertragen Sie Ihre App mit einer Push-Operation aus dem Verzeichnis *get-started-tomcat* zu {{site.data.keyword.Bluemix_notm}}
```
cf push
```
{: pre}

Dieser Vorgang kann ungefähr zwei Minuten dauern. Falls ein Fehler im Bereitstellungsprozess auftritt, können Sie den Befehl `cf logs <Your-App-Name> --recent` verwenden, um den Fehler zu beheben.

Wenn die Bereitstellung abgeschlossen ist, sollten Sie eine Nachricht sehen, die anzeigt, dass Ihre App ausgeführt wird. Ihre App wird an der URL angezeigt, die in der Ausgabe der Push-Operation aufgelistet ist. Sie können auch den Befehl 
  ```
cf apps
  ```
  {: pre}
  ausgeben, um Ihren Appstatus und die URL anzuzeigen.

## 6. In Eclipse entwickeln
{: #developing_in_eclipse}

IBM® Eclipse Tools für {{site.data.keyword.Bluemix}} bieten Plug-ins, die in einer vorhandenen Eclipse-Umgebung installiert werden können, um die Integration der IDE (Integrated Development Environment) der Anwendungsentwickler in {{site.data.keyword.Bluemix_notm}} zu unterstützen.

Laden Sie die [IBM Eclipse Tools for Bluemix](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix) herunter und installieren Sie sie.

Importieren Sie dieses Beispiel mithilfe der Optionen `Datei` -> `Importieren` -> `Maven` -> `Vorhandene Maven-Projekte` in Eclipse.

Erstellen Sie eine Tomcat-Serverdefinition:
  - Klicken Sie in der Ansicht `Server` mit der rechten Maustaste auf -> `Neu` -> `Server`.
  - Wählen Sie `Apache` -> `Tomcat v8.0 Server` aus.
  - Wählen Sie Ihr Verzeichnis `tomcat-install-dir` aus.
  - Setzen Sie den Assistenten mit Standardoptionen fort, um zum Abschluss zu gelangen.

Führen Sie Ihre Anwendung lokal auf dem Apache-Server aus:
  - Klicken Sie mit der rechten Maustaste auf das Beispiel `GetStartedTomcat` und wählen Sie die Optionen `Ausführen als` -> `Auf Server ausführen` aus. 
  - Suchen Sie den Tomcat-Server als lokalen Host, wählen Sie ihn aus und klicken Sie auf die Option zum Fertigstellen.
  - In wenigen Sekunden sollte Ihre Anwendung unter folgender Adresse betriebsbereit sein: http://localhost:8080/TomcatHelloWorldApp/

Erstellen Sie eine {{site.data.keyword.Bluemix_notm}}-Serverdefinition:
  - Klicken Sie in der Ansicht `Server` mit der rechten Maustaste auf -> `Neu` -> `Server`.
  - Wählen Sie `IBM` -> `IBM Bluemix` aus und folgen Sie den Schritten im Wizard.
  - Geben Sie Ihre Berechtigungsnachweise ein und klicken Sie auf `Weiter`
  - Wählen Sie Ihre Angaben für `org` und `space` aus und klicken Sie auf die Option zum `Fertigstellen`

Führen Sie Ihre Anwendung unter {{site.data.keyword.Bluemix_notm}} aus:
  - Klicken Sie mit der rechten Maustaste auf das Beispiel `GetStartedTomcat` und wählen Sie die Optionen `Ausführen als` -> `Auf Server ausführen` aus. 
  - Suchen Sie `IBM Bluemix` und wählen Sie diesen Eintrag aus. Klicken Sie anschließend auf die Option zum Fertigstellen.
  - Ein Assistent wird Sie durch die Bereitstellungsoptionen führen. Stellen Sie sicher, dass Sie unter `Name` einen eindeutigen Namen für Ihre Anwendung angeben.
  - In wenigen Minuten sollte Ihre Anwendung unter der von Ihnen ausgewählten URL ausgeführt werden. 

Jetzt haben Sie Ihren Code lokal und in der Cloud ausgeführt!

## 7. Fügen Sie eine Datenbank hinzu. 
{: #add_database}

Als nächstes werden wir eine NoSQL-Datenbank zu dieser Anwendung hinzufügen und die Anwendung so einrichten, dass sie lokal und unter Bluemix ausgeführt werden kann. 

1. Melden Sie sich in Ihrem Browser bei {{site.data.keyword.Bluemix_notm}} an. Navigieren Sie zum `Dashboard`. Wählen Sie Ihre Anwendung durch Klicken auf den zugehörigen Namen in der Spalte `Name` aus. 
2. Klicken Sie auf `Verbindungen` und dann auf `Neuen verbinden`.
2. Wählen Sie im Abschnitt `Data & Analytics` den Eintrag `Cloudant NoSQL DB` aus und erstellen Sie den Service mithilfe von `Erstellen`. 
3. Wählen Sie `Erneutes Staging` aus, wenn Sie dazu aufgefordert werden. {{site.data.keyword.Bluemix_notm}} startet Ihre Anwendung erneut und bietet die Datenbankberechtigungsnachweise für Ihre Anwendung unter Verwendung der Umgebungsvariablen `VCAP_SERVICES`. Diese Umgebungsvariable ist nur dann für die Anwendung verfügbar, wenn sie unter {{site.data.keyword.Bluemix_notm}} ausgeführt wird.

Umgebungsvariablen ermöglichen es Ihnen, die Bereitstellungseinstellungen von Ihrem Quellcode zu trennen. Anstelle der festen Codierung eines Datenbankkennworts können Sie dieses in einer Umgebungsvariablen speichern, auf die Sie in Ihrem Quellcode verweisen. [Weitere Informationen...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 8. Verwenden Sie die Datenbank.
{: #use_database}
Wir werden jetzt Ihren lokalen Code aktualisieren, um auf diese Datenbank zu verweisen. Wir werden die Berechtigungsnachweise für die Services in einer Eigenschaftendatei speichern. Diese Datei wird NUR dann verwendet, wenn die Anwendung lokal ausgeführt wird. Bei der Ausführung in {{site.data.keyword.Bluemix_notm}} werden die Berechtigungsnachweise aus der Umgebungsvariablen VCAP_SERVICES gelesen. 

1. Öffnen Sie zuerst Eclipse und dann die Datei 'src/main/resources/cloudant.properties':
  ```
  cloudant_url=
  ```
  {: pre}

2. Öffnen Sie in Ihrem Browser die Benutzerschnittstelle von {{site.data.keyword.Bluemix_notm}}, wählen Sie Ihre App -> Verbindungen -> Cloudant -> Berechtigungsnachweise anzeigen aus.

3. Kopieren Sie einfach die `url` aus den Berechtigungsnachweisen in das Feld `url` der Datei `cloudant.properties` und speichern Sie die Änderungen. Als Ergebnis erhalten Sie in etwa Folgendes: 
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```

4. Starten Sie den Tomcat-Server in Eclipse erneut aus der Ansicht `Server`.

  Aktualisieren Sie Ihre Browseransicht unter: http://localhost:8080/GetStartedTomcat/. Alle Namen, die Sie in die App eingegeben haben, werden jetzt zur Datenbank hinzugefügt. 

  Ihre lokale App und die {{site.data.keyword.Bluemix_notm}}-App verwenden die Datenbank gemeinsam. Ihre {{site.data.keyword.Bluemix_notm}}-App wird an der URL angezeigt, die in der Ausgabe der oben erwähnten Push-Operation aufgelistet ist. Namen, die Sie in einer der Apps eingeben, sollten nach einer Aktualisierung des Browsers in beiden angezeigt werden. 

Denken Sie daran, dass Sie Ihre App unter {{site.data.keyword.Bluemix_notm}} stoppen, wenn Sie nicht benötigt wird, damit Ihnen nicht unerwartete Gebühren belastet werden.
{: tip}  
