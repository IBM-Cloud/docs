---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Erste Schritte mit Liberty unter Bluemix

* {: download} Herzlichen Glückwunsch! Sie haben die Hello World-Beispielanwendung unter {{site.data.keyword.Bluemix}} bereitgestellt! Befolgen Sie diesen schrittweisen Leitfaden, um zu starten. Oder laden Sie den <a class="xref" href="http://bluemix.net" target="_blank" title="(Beispielcode herunterladen) "><img class="hidden" src="../../images/btn_starter-code.svg" alt="Beispielcode herunterladen" />Beispielcode herunter</a> und beginnen Sie auf eigene Faust.

Wenn Sie diesem Leitfaden folgen, werden Sie eine Entwicklungsumgebung einrichten, eine App lokal und unter {{site.data.keyword.Bluemix}} bereitstellen und einen {{site.data.keyword.Bluemix}}-Datenbankservice in Ihre App integrieren.

## Voraussetzungen
{: #prereqs}

Sie benötigen die folgenden Konten und Tools: 
* [{{site.data.keyword.Bluemix_notm}} Konto](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry-CLI ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Eclipse IDE for Java EE Developers ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}
* [Git ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://git-scm.com/downloads){: new_window}
* [Maven ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://maven.apache.org/download.cgi){: new_window}

Für die Entwicklung in Eclipse mit {{site.data.keyword.eclipsetoolsfull}} müssen Sie ferner [die Tools herunterladen. ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix){: new_window}

## 1. Klonen Sie die Beispielapp.
{: #clone}

Klonen Sie zuerst die Beispielapp 'GitHub repo'.
  ```bash
git clone https://github.com/IBM-Bluemix/get-started-java
  ```
  {: pre}


## 2. Führen Sie die App lokal über die Befehlszeile aus. 
{: #run_locally}

Verwenden Sie Maven, um Ihren Sourcecode zu erstellen und führen Sie die daraus resultierende App aus.

1. Wechseln Sie mithife der Befehlszeile das Verzeichnis, in dem sich die Beispielapp befindet.

  ```
cd get-started-java
  ```
  {: pre}

1. Verwenden Sie Maven, um Abhängigkeiten zu installieren und die .war-Datei zu erstellen. 

  ```
mvn clean install
  ```
  {: pre}

1. Führen Sie die App lokal unter Liberty aus.
  ```
mvn install liberty:run-server
  ```
  {: pre}

Wenn Sie die Nachricht *The server defaultServer is ready to run a smarter planet.* sehen, finden Sie Ihre App unter folgender Adresse: http://localhost:9080/GetStartedJava.

Um Ihre App zu stoppen, drücken Sie *Strg-C* in dem Befehlszeilenfenster, in dem Sie die App gestartet haben. 

## 3. Bereiten Sie die App für die Bereitstellung vor. 
{: #prepare}

Für die Bereitstellung unter {{site.data.keyword.Bluemix_notm}} kann es hilfreich sein, die Datei 'manifest.yml' zu installieren. Die Datei 'manifest.yml' enthält Basisinformationen zu Ihrer App wie den Namen, wieviel Speicher für jede Instanz zugeordnet werden soll und die Route. Wir haben eine Beispieldatei 'manifest.yml' im Verzeichnis `get-started-java` bereitgestellt. 

Öffnen Sie die Datei 'manifest.yml' und ändern Sie die Angabe für `name` von `GetStartedJava` in den Namen Ihrer App <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
   - name: GetStartedJava
     random-route: true
     path: target/GetStartedJava.war
     memory: 512M
     instances: 1
  ```
  {: codeblock}

In dieser Datei 'manifest.yml' generiert **random-route: true** eine zufällige Route für Ihre App, um zu verhindern, dass Ihre Route mit anderen Routen kollidiert. Wenn Sie möchten, können Sie **random-route: true** durch **host: myChosenHostName** ersetzen und einen Hostnamen Ihrer Wahl angeben. [Weitere Informationen...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. Stellen Sie die App unter {{site.data.keyword.Bluemix_notm}} bereit.
{: #deploy}

Stellen Sie Ihre App in einem der folgenden Bluemix-Bereiche bereit. Für die optimale Latenzzeit wählen Sie einen Bereich, der Ihren Benutzern am nächsten liegt. 

|Bereich         |API-Endpunkt                    |
|:---------------|:-------------------------------|
| USA (Süden)    | https://api.ng.bluemix.net     |
| Großbritannien | https://api.eu-gb.bluemix.net  |
| Sydney         | https://api.au-syd.bluemix.net |

1. Legen Sie den API-Endpunkt fest, indem Sie `<API-endpoint>` durch den Endpunkt Ihres Bereichs ersetzen.
  ```
cf api <API-endpoint>
  ```
  {: pre}

1. Melden Sie sich an Ihrem {{site.data.keyword.Bluemix_notm}}-Konto an.
  ```
cf login
```
  {: pre}

1. Übertragen Sie Ihre App mit einer Push-Operation aus dem Verzeichnis `get-started-java` zu {{site.data.keyword.Bluemix_notm}}.
  ```
cf push
```
  {: pre}

Das Bereitstellen Ihrer Anwendung kann einige Minuten dauern. Wenn die Bereitstellung abgeschlossen ist, sehen Sie eine Nachricht darüber, dass Ihre App ausgeführt wird. Ihre App wird an der URL angezeigt, die in der Ausgabe des Push-Befehls aufgelistet ist. Sie können aber auch den App-Bereitstellungsstatus und die URL anzeigen, indem Sie folgenden Befehl ausführen:
  ```
cf apps
  ```
  {: pre}

Sie können Fehler im Bereitstellungsprozess beheben, indem Sie den Befehl `cf logs <Your-App-Name> --recent` verwenden.
{: tip}  

## 5. Mit Eclipse entwickeln
{: #eclipse}

{{site.data.keyword.eclipsetoolsfull}} bietet Plug-ins, die in einer vorhandenen Eclipse-Umgebung installiert werden können, um die Integration Ihrer IDE (Integrated Development Environment) in {{site.data.keyword.Bluemix_notm}} zu unterstützen.

1. Stellen Sie sicher, dass Sie über [IBM Eclipse Tools for Bluemix](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix) verfügen.

2. Importieren Sie das Beispiel `get-started-java` in Eclipse, indem Sie zu **Datei > Importieren > Maven > Vorhandene Maven-Projekte** wechseln.

3. Erstellen Sie eine Liberty-Serverdefinition. Die folgenden Schritte werden einen neuen Liberty-Server herunterladen.
  - Klicken Sie in der Ansicht **Fenster > Ansicht anzeigen > Server** mit der rechten Maustaste und wählen Sie **Neu > Server** aus.
  - Wählen Sie **IBM > WebSphere Application Server Liberty** aus.
  - Wählen Sie **Von einem Archiv oder einem Repository installieren** aus.
  - Wenn Sie dazu aufgefordert werden, geben Sie einen Zielpfad zu einem neuen Ordner ein (/Users/username/liberty), in dem Sie Liberty installieren möchten.
  - Wählen Sie **Neue Laufzeitumgebung von ibm.com herunterladen und installieren** aus.
  - Wählen Sie **Webprofil für WAS-Liberty mit Java EE 7** aus.
  - Setzen Sie den Assistenten mit Standardoptionen fort, um zum Abschluss zu gelangen.

4. Führen Sie Ihre Anwendung lokal unter Liberty aus:
  - Ändern Sie die Einstellungen für den Web-Browser in den Systemstandardwert, indem Sie **Fenster > Web-Browser > Standard-Web-Browser des Systems** auswählen.
  - Klicken Sie mit der rechten Maustaste auf das Beispiel `GetStartedJava` und wählen Sie **Ausführen als > Auf Server ausführen** aus.
  - Suchen Sie den Liberty-Server als lokalen Host, wählen Sie ihn aus und klicken Sie auf die Option zum **Fertigstellen**.

  In wenigen Sekunden wird Ihre Anwendung unter folgender Adresse ausgeführt: http://localhost:9080/GetStartedJava.

5. Code aktualisieren:
  - Öffnen Sie die Datei `src/main/webapp/index.html` und ändern Sie die Kopfzeile von `<h1>Welcome.</h1>` in `<h1>Welcome Jane.</h1>`.
  - Speichern Sie Ihre Änderungen. Liberty wird Ihre Änderungen automatisch übernehmen.
  - Aktualisieren Sie Ihren Browser (http://localhost:9080/GetStartedJava), um die Änderungen anzuzeigen.

6. Übergeben Sie Ihre Änderungen mit einer Push-Operation an {{site.data.keyword.Bluemix_notm}}:
  - Erstellen Sie in der Befehlszeile aus dem Verzeichnis `get-started-java` die .war-Datei erneut: 
    ```
mvn clean install
    ```
    {: pre}
  - Übergeben Sie Ihre Anwendung mit einer Push-Operation an {{site.data.keyword.Bluemix_notm}}.
    ```
cf push
```
    {: pre}

Jetzt haben Sie Ihren Code sowohl lokal als auch in der Cloud ausgeführt!

## 6. Fügen Sie eine Datenbank hinzu.
{: #add_database}

Als nächstes werden wir eine NoSQL-Datenbank zu dieser Anwendung hinzufügen und die Anwendung so einrichten, dass sie lokal und unter {{site.data.keyword.Bluemix_notm}} ausgeführt werden kann.

1. Melden Sie sich in Ihrem Browser bei {{site.data.keyword.Bluemix_notm}} an und wechseln Sie in das Dashboard. Wählen Sie Ihre Anwendung durch Klicken auf den zugehörigen Namen in der Spalte **Name** aus. 
2. Klicken Sie auf **Verbindungen** und dann auf **Neuen verbinden**.
3. Wählen Sie im Abschnitt **Data & Analytics** den Eintrag **Cloudant NoSQL DB** aus und erstellen Sie dann den Service.
4. Wählen Sie **Erneutes Staging** aus, wenn Sie dazu aufgefordert werden. {{site.data.keyword.Bluemix_notm}} startet Ihre Anwendung erneut und bietet die Datenbankberechtigungsnachweise für Ihre Anwendung unter Verwendung der Umgebungsvariablen `VCAP_SERVICES`. Diese Umgebungsvariable ist nur dann für die Anwendung verfügbar, wenn Sie unter {{site.data.keyword.Bluemix_notm}} ausgeführt wird.

Umgebungsvariablen ermöglichen es Ihnen, die Bereitstellungseinstellungen von Ihrem Quellcode zu trennen. Anstelle der festen Codierung eines Datenbankkennworts können Sie dieses in einer Umgebungsvariablen speichern, auf die Sie in Ihrem Quellcode verweisen. [Weitere Informationen...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 7. Verwenden Sie die Datenbank.
{: #use_database}
Wir werden jetzt Ihren lokalen Code aktualisieren, um auf diese Datenbank zu verweisen. Wir werden die Berechtigungsnachweise für die Services in einer Eigenschaftendatei speichern. Diese Datei wird NUR dann verwendet, wenn die Anwendung lokal ausgeführt wird. Bei der Ausführung in {{site.data.keyword.Bluemix_notm}} werden die Berechtigungsnachweise aus der Umgebungsvariablen `VCAP_SERVICES` gelesen. 

1. Öffnen Sie in Eclipse die Datei 'src/main/resources/cloudant.properties':
  ```
  cloudant_url=
  ```
  {: pre}

2. Wechseln Sie in Ihrem Browser zu {{site.data.keyword.Bluemix_notm}} und wählen Sie **Apps > _your app_ > Verbindungen > Cloudant > Berechtigungsnachweise anzeigen** aus.

3. Kopieren Sie einfach die `url` aus dem Feld `url` der Datei `cloudant.properties` und speichern Sie die Änderungen.
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:pre}

4. Starten Sie den Liberty-Server in Eclipse erneut aus der Ansicht `Server`.

  Aktualisieren Sie Ihre Browseransicht unter: http://localhost:9080/GetStartedJava/. Alle Namen, die Sie in die App eingegeben haben, werden jetzt zur Datenbank hinzugefügt. 

  Ihre lokale App und die {{site.data.keyword.Bluemix_notm}}-App verwenden die Datenbank gemeinsam. Namen, die Sie in einer der Apps eingeben, werden nach einer Aktualisierung des Browsers in beiden angezeigt.


Denken Sie daran, dass Sie Ihre App unter {{site.data.keyword.Bluemix_notm}} stoppen, wenn Sie nicht benötigt wird, damit Ihnen nicht unerwartete Gebühren belastet werden.
{: tip}  
