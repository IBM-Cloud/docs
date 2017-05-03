---

copyright:
  years: 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Erste Schritte mit ASP.NET unter Bluemix
{: #getting_started}

* {: download} Herzlichen Glückwunsch! Sie haben die Hello World-Beispielanwendung unter {{site.data.keyword.Bluemix}} bereitgestellt! Befolgen Sie diesen schrittweisen Leitfaden, um zu starten. Oder laden Sie den <a class="xref" href="http://bluemix.net" target="_blank" title="(Beispielcode herunterladen) "><img class="hidden" src="../../images/btn_starter-code.svg" alt="Beispielcode herunterladen" />Beispielcode herunter</a> und beginnen Sie auf eigene Faust.

Wenn Sie diesem Leitfaden folgen, werden Sie eine Entwicklungsumgebung einrichten, eine App lokal und unter {{site.data.keyword.Bluemix}} bereitstellen und einen {{site.data.keyword.Bluemix}}-Datenbankservice in Ihre App integrieren.

## Voraussetzungen
{: #prereqs}

Sie benötigen Folgendes: 
* [{{site.data.keyword.Bluemix_notm}} Konto](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry-CLI ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://git-scm.com/downloads){: new_window}
* Installieren Sie .NET Core 1.0.0-preview4-004233 SDK von der Downloadseite [preview4 ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://github.com/dotnet/core/blob/master/release-notes/download-archives/preview4-download.md) mithilfe der Anweisungen.
* Installieren Sie die aktuellste .NET Core-Laufzeit von der Website [dot.net ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://www.microsoft.com/net/download/core#/runtime)

## 1. Klonen Sie die Beispielapp.
{: #clone}

Jetzt können Sie beginnen, mit der App zu arbeiten. Klonen Sie das Repository und wechseln Sie in das Verzeichnis, in dem sich die Beispielapp befindet.
  ```
git clone https://github.com/IBM-Bluemix/get-started-aspnet-core
  ```
  {: pre}
  ```
cd get-started-aspnet-core
  ```
  {: pre}

## 2. Führen Sie die App lokal aus.
{: #run_locally}

Führen Sie die App aus.
  ```
cd src/GetStartedDotnet
  ```
  {: pre}
  ```
dotnet restore
  ```
  {: pre}
  ```
dotnet run
  ```
  {: pre}

Ihre App finden Sie unter: http://localhost:5000/

## 3. Bereiten Sie die App für die Bereitstellung vor.
{: #prepare}

Für die Bereitstellung unter {{site.data.keyword.Bluemix_notm}} kann es hilfreich sein, die Datei 'manifest.yml' zu installieren. Die Datei 'manifest.yml' enthält Basisinformationen zu Ihrer App wie den Namen, wieviel Speicher für jede Instanz zugeordnet werden soll und die Route. Wir haben eine Beispieldatei 'manifest.yml' im Verzeichnis `get-started-dotnet` bereitgestellt. 

Öffnen Sie die Datei 'manifest.yml' und ändern Sie die Angabe für `name` von `GetStartedDotnet` in den Namen Ihrer App <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
 applications:
 - name: GetStartedDotnet
   random-route: true
   memory: 256M
  ```
  {: codeblock}

In dieser Datei 'manifest.yml' generiert **random-route: true** eine zufällige Route für Ihre App, um zu verhindern, dass Ihre Route mit anderen Routen kollidiert. Wenn Sie möchten, können Sie **random-route: true** durch **host: myChosenHostName** ersetzen und einen Hostnamen Ihrer Wahl angeben. [Weitere Informationen...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. Stellen Sie die App bereit.
{: #deploy}

Sie können die Cloud Foundry-CLI verwenden, um Apps bereitzustellen.

Melden Sie sich zum Starten bei Ihrem {{site.data.keyword.Bluemix_notm}}-Konto an:
  ```
cf login
```
  {: pre}

Wählen Sie Ihren API-Endpunkt aus.
  ```
cf api <API-endpoint>
  ```
  {: pre}

Ersetzen Sie *API-endpoint* im Befehl durch einen API-Endpunkt aus der folgenden Liste: 

|URL                             |Region          |
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net     | US South       |
| https://api.eu-gb.bluemix.net  | United Kingdom |
| https://api.au-syd.bluemix.net | Sydney         |

**Stellen Sie sicher, dass Sie sich im Hauptverzeichnis 'get-started-aspnet-core' Ihrer Anwendung befinden** und übertragen Sie dann Ihre Anwendung mit einer Push-Operation an {{site.data.keyword.Bluemix_notm}}
  ```
cf push
```
  {: pre}

Dieser Vorgang kann einige Minuten dauern. Falls ein Fehler im Bereitstellungsprozess auftritt, können Sie den Befehl `cf logs <Your-App-Name> --recent` verwenden, um den Fehler zu beheben.

Wenn die Bereitstellung abgeschlossen ist, sollten Sie eine Nachricht sehen, die anzeigt, dass Ihre App ausgeführt wird. Ihre App wird an der URL angezeigt, die in der Ausgabe der Push-Operation aufgelistet ist. Sie können auch den Befehl 
  ```
cf apps
  ```
  {: pre}
  ausgeben, um Ihren Appstatus und die URL anzuzeigen.

## 5. Stellen Sie eine Verbindung zu einer MySQL-Datenbank her.
{: connect_mysql}

Als nächstes werden wir eine ClearDB MySQL-Datenbank zu dieser Anwendung hinzufügen und die Anwendung so einrichten, dass sie lokal und unter Bluemix ausgeführt werden kann.

1. Melden Sie sich in Ihrem Browser bei {{site.data.keyword.Bluemix_notm}} an. Navigieren Sie zum `Dashboard`. Wählen Sie Ihre Anwendung durch Klicken auf den zugehörigen Namen in der Spalte `Name` aus. 
2. Klicken Sie auf `Verbindungen` und dann auf `Neuen verbinden`.
2. Wählen Sie im Abschnitt `Data & Analytics` den Eintrag `ClearDB MySQL Database` aus und erstellen Sie den Service mithilfe von `Erstellen`. 
3. Wählen Sie `Erneutes Staging` aus, wenn Sie dazu aufgefordert werden. {{site.data.keyword.Bluemix_notm}} startet Ihre Anwendung erneut und bietet die Datenbankberechtigungsnachweise für Ihre Anwendung unter Verwendung der Umgebungsvariablen `VCAP_SERVICES`. Diese Umgebungsvariable ist nur dann für die Anwendung verfügbar, wenn sie unter {{site.data.keyword.Bluemix_notm}} ausgeführt wird.

Umgebungsvariablen ermöglichen es Ihnen, die Bereitstellungseinstellungen von Ihrem Quellcode zu trennen. Anstelle der festen Codierung eines Datenbankkennworts können Sie dieses in einer Umgebungsvariablen speichern, auf die Sie in Ihrem Quellcode verweisen. [Weitere Informationen...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 6. Verwenden Sie die Datenbank lokal.
{: #use_database}

Wir werden jetzt Ihren lokalen Code aktualisieren, um auf diese Datenbank zu verweisen. Wir werden die Berechtigungsnachweise für die Services in einer JSON-Datei speichern. Diese Datei wird NUR dann verwendet, wenn die Anwendung lokal ausgeführt wird. Bei der Ausführung in {{site.data.keyword.Bluemix_notm}} werden die Berechtigungsnachweise aus der Umgebungsvariablen VCAP_SERVICES gelesen. 

1. Erstellen Sie die Datei 'src/GetStartedDotnet/vcap-local.json'.

2. Öffnen Sie in Ihrem Browser die Benutzerschnittstelle von {{site.data.keyword.Bluemix_notm}} und wählen Sie Ihre App -> Verbindungen -> ClearDB MySQL Database -> Berechtigungsnachweise anzeigen aus.

3. Kopieren Sie das gesamte JSON-Objekt aus den Berechtigungsnachweisen und fügen Sie es in die Datei `vcap-local.json` ein. Danach speichern Sie die Änderungen. Als Ergebnis erhalten Sie in etwa Folgendes: 
  ```
  {
  "cleardb": [
    {
      "credentials": {
        ...
        "uri": "mysql://user:password@some-hostname.cleardb.net:3306/database-name?reconnect=true",
        ...
      },
      ...
      "name": "My ClearDB service instance name",
      ...
    }
  ]
}
  ```

4. Starten Sie aus dem Verzeichnis `get-started-aspnet-core/src/GetStartedDotnet` Ihre Anwendung mit dem Befehl `dotnet run` erneut.

  Aktualisieren Sie Ihre Browseransicht unter: http://localhost:5000/. Alle Namen, die Sie in die App eingegeben haben, werden jetzt zur Datenbank hinzugefügt. 

  Ihre lokale App und die {{site.data.keyword.Bluemix_notm}}-App verwenden die Datenbank gemeinsam. Ihre {{site.data.keyword.Bluemix_notm}}-App wird an der URL angezeigt, die in der Ausgabe der oben erwähnten Push-Operation aufgelistet ist. Namen, die Sie in einer der Apps eingeben, sollten nach einer Aktualisierung des Browsers in beiden angezeigt werden. 

Denken Sie daran, dass Sie Ihre App stoppen, wenn Sie nicht benötigt wird, damit Ihnen nicht unerwartete Gebühren belastet werden.
{: tip}
