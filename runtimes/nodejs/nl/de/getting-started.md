---

copyright:
  years: 2017
lastupdated: "2017-03-22"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}


# Erste Schritte mit Node.js unter Bluemix

* {: download} Herzlichen Glückwunsch! Sie haben die Hello World-Beispielanwendung unter {{site.data.keyword.Bluemix}} bereitgestellt! Befolgen Sie diesen schrittweisen Leitfaden, um zu starten. Oder laden Sie den <a class="xref" href="http://bluemix.net" target="_blank" title="(Beispielcode herunterladen) "><img class="hidden" src="../../images/btn_starter-code.svg" alt="Beispielcode herunterladen" />Beispielcode herunter</a> und beginnen Sie auf eigene Faust.

Wenn Sie diesem Leitfaden folgen, werden Sie eine Entwicklungsumgebung einrichten, eine App lokal und unter {{site.data.keyword.Bluemix}} bereitstellen und einen {{site.data.keyword.Bluemix}}-Datenbankservice in Ihre App integrieren.

## Voraussetzungen
{: #prereqs}

Sie benötigen die folgenden Konten und Tools: 
* [{{site.data.keyword.Bluemix_notm}} Konto](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry-CLI ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://git-scm.com/downloads){: new_window}
* [Node ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://nodejs.org/en/){: new_window}


## 1. Klonen Sie die Beispielapp.
{: #clone}

Klonen Sie zuerst die *hello world*-Beispielapp von Node.js 'GitHub repo'.
  ```
git clone https://github.com/IBM-Bluemix/get-started-node
  ```
  {: pre}

## 2. Führen Sie die App lokal aus.
{: #run_locally}

Verwenden Sie den npm-Paketmanager, um Abhängigkeiten zu installieren und führen Sie Ihre App aus.

1. Wechseln Sie mithife der Befehlszeile das Verzeichnis, in dem sich die Beispielapp befindet.
  ```
cd get-started-node
```
  {: pre}

1. Installieren Sie die Abhängigkeiten, die in der Datei [package.json ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://docs.npmjs.com/files/package.json) aufgelistet sind, um die App lokal auszuführen.  
  ```
npm install
```
  {: pre}

1. Führen Sie die App aus.
  ```
npm start  
  ```
  {: pre}

Ihre App finden Sie unter: http://localhost:3000.

Verwenden Sie [nodemon](https://nodemon.io/) für den automatischen Neustart der Anwendung bei Dateiänderungen.
{: tip}


## 3. Bereiten Sie die App für die Bereitstellung vor.
{: #prepare}

Für die Bereitstellung unter {{site.data.keyword.Bluemix_notm}} kann es hilfreich sein, die Datei 'manifest.yml' zu installieren. Die Datei 'manifest.yml' enthält Basisinformationen zu Ihrer App wie den Namen, wieviel Speicher für jede Instanz zugeordnet werden soll und die Route. Wir haben eine Beispieldatei 'manifest.yml' im Verzeichnis `get-started-node` bereitgestellt.

Öffnen Sie die Datei 'manifest.yml' und ändern Sie die Angabe für `name` von `GetStartedNode` in den Namen Ihrer App <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

```
applications:
- name: GetStartedNode
  random-route: true
  memory: 128M
```
{: codeblock}

In dieser Datei 'manifest.yml' generiert **random-route: true** eine zufällige Route für Ihre App, um zu verhindern, dass Ihre Route mit anderen Routen kollidiert. Wenn Sie möchten, können Sie **random-route: true** durch **host: myChosenHostName** ersetzen und einen Hostnamen Ihrer Wahl angeben. [Weitere Informationen...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. Stellen Sie die App bereit.
{: #deploy}

Sie können die Cloud Foundry-CLI verwenden, um Apps für {{site.data.keyword.Bluemix_notm}} bereitzustellen.

Führen Sie den folgenden Befehl aus, um Ihren API-Endpunkt festzulegen, wobei Sie den Wert *API-endpoint* durch den API-Endpunkt für Ihren Bereich ersetzen.
   ```
cf api <API-endpoint>
   ```
   {: pre}

|API-Endpunkt                    | Bereich        |
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net     | USA (Süden)    |
| https://api.eu-gb.bluemix.net  | Großbritannien |
| https://api.au-syd.bluemix.net | Sydney         |

Melden Sie sich an Ihrem {{site.data.keyword.Bluemix_notm}}-Konto an.

  ```
cf login
```
  {: pre}

Übertragen Sie Ihre App mit einer Push-Operation aus dem Verzeichnis *get-started-node* zu {{site.data.keyword.Bluemix_notm}}.
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

## 5. Fügen Sie eine Datenbank hinzu. 
{: #add_database}

Als nächstes werden wir eine NoSQL-Datenbank zu dieser Anwendung hinzufügen und die Anwendung so einrichten, dass sie lokal und unter {{site.data.keyword.Bluemix_notm}} ausgeführt werden kann.

1. Melden Sie sich in Ihrem Browser bei {{site.data.keyword.Bluemix_notm}} an und wechseln Sie in das Dashboard. Wählen Sie Ihre Anwendung durch Klicken auf den zugehörigen Namen in der Spalte **Name** aus. 
2. Klicken Sie auf **Verbindungen** und dann auf **Neuen verbinden**.
2. Wählen Sie im Abschnitt **Data & Analytics** den Eintrag `Cloudant NoSQL DB` aus und erstellen Sie dann den Service.
3. Wählen Sie **Erneutes Staging** aus, wenn Sie dazu aufgefordert werden. {{site.data.keyword.Bluemix_notm}} startet Ihre Anwendung erneut und bietet die Datenbankberechtigungsnachweise für Ihre Anwendung unter Verwendung der Umgebungsvariablen `VCAP_SERVICES`. Diese Umgebungsvariable ist nur dann für die Anwendung verfügbar, wenn Sie unter {{site.data.keyword.Bluemix_notm}} ausgeführt wird.

Umgebungsvariablen ermöglichen es Ihnen, die Bereitstellungseinstellungen von Ihrem Quellcode zu trennen. Anstelle der festen Codierung eines Datenbankkennworts können Sie dieses in einer Umgebungsvariablen speichern, auf die Sie in Ihrem Quellcode verweisen. [Weitere Informationen...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 6. Verwenden Sie die Datenbank. 
{: #use_database}
Wir werden jetzt Ihren lokalen Code aktualisieren, um auf diese Datenbank zu verweisen. Wir erstellen nun eine JSON-Datei, die die Berechtigungsnachweise für die Services speichert, die die Anwendung verwendet. Diese Datei wird NUR dann verwendet, wenn die Anwendung lokal ausgeführt wird. Bei der Ausführung in {{site.data.keyword.Bluemix_notm}} werden die Berechtigungsnachweise aus der Umgebungsvariablen `VCAP_SERVICES` gelesen. 

1. Erstellen Sie im Verzeichnis `get-started-node` eine Datei mit dem Namen `vcap-local.json` mit dem folgenden Inhalt: 
  ```
  {
    "services": {
      "cloudantNoSQLDB": [
        {
          "credentials": {
            "url":"CLOUDANT_DATABASE_URL"
          },
          "label": "cloudantNoSQLDB"
        }
      ]
    }
  }
  ```
  {: codeblock}

2. Wechseln Sie in Ihrem Browser zu {{site.data.keyword.Bluemix_notm}} und wählen Sie **Apps > _your app_ > Verbindungen > Cloudant > Berechtigungsnachweise anzeigen** aus.

3. Kopieren Sie einfach die `url` aus den Berechtigungsnachweisen in das Feld `url` der Datei `vcap-local.json` und ersetzen Sie dabei **CLOUDANT_DATABASE_URL**.

4. Führen Sie Ihre Anwendung lokal aus.
  ```
npm start  
  ```
  {: pre}

  Ihre lokale App finden Sie unter http://localhost:3000. Alle Namen, die Sie in die App eingegeben haben, werden jetzt zur Datenbank hinzugefügt. 

  Ihre lokale App und die {{site.data.keyword.Bluemix_notm}}-App verwenden die Datenbank gemeinsam. Namen, die Sie in einer der Apps eingeben, werden nach einer Aktualisierung des Browsers in beiden angezeigt.

Denken Sie daran, dass Sie Ihre App unter {{site.data.keyword.Bluemix_notm}} stoppen, wenn Sie nicht benötigt wird, damit Ihnen nicht unerwartete Gebühren belastet werden.
{: tip}
