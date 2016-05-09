---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Für {{site.data.keyword.openwhisk_short}} eingerichtete Services verwenden 
{: #openwhisk_ecosystem}
*Letzte Aktualisierung: 28. März 2016*

In {{site.data.keyword.openwhisk}} stellt ein Katalog von Paketen eine einfache Methode bereit, um Ihre App mit nützlichen Funktionen zu erweitern und um auf externe Services im direkten Geschäftsumfeld ('Ökosystem') zuzugreifen. Zu den externen Services, die für {{site.data.keyword.openwhisk_short}} eingerichtet sind, gehören zum Beispiel Cloudant, The Weather Company, Slack und GitHub.
{: shortdesc}

Der Katalog ist in Form von Paketen im Namensbereich `/whisk.system` verfügbar. Informationen dazu, wie sich der Katalog mithilfe des Befehlszeilentools durchsuchen lässt, finden Sie unter [Pakete durchsuchen](./openwhisk_packages.html#openwhisk_packagedisplay).

In den folgenden Abschnitten werden einige der Pakete im Katalog dokumentiert.

## Cloudant-Paket verwenden
{: #openwhisk_catalog_cloudant}
Das Paket `/whisk.system/cloudant` ermöglicht Ihnen die Arbeit mit einer Cloudant-Datenbank. Es enthält die folgenden Aktionen und Feeds.

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | Paket | {{site.data.keyword.Bluemix_notm}}ServiceName, host, username, password, dbname, includeDoc, overwrite | Dient zur Arbeit mit einer Cloudant-Datenbank. |
| `/whisk.system/cloudant/read` | Aktion | dbname, includeDoc, id | Liest ein Dokument aus einer Datenbank. |
| `/whisk.system/cloudant/write` | Aktion | dbname, overwrite, doc | Schreibt ein Dokument in eine Datenbank. |
| `/whisk.system/cloudant/changes` | Feed | dbname, includeDoc | Aktiviert Auslöserereignisse bei Änderungen an einer Datenbank. |

In den folgenden Abschnitten werden die Einrichtung einer Cloudant-Datenbank, die Konfiguration eines zugeordneten Pakets sowie die Verwendung der Aktionen und Feeds im Paket `/whisk.system/cloudant` schrittweise erläutert.

### Cloudant-Datenbank in {{site.data.keyword.Bluemix_notm}} einrichten

Wenn Sie {{site.data.keyword.openwhisk_short}} aus {{site.data.keyword.Bluemix}} verwenden, erstellt {{site.data.keyword.openwhisk_short}} automatisch Paketbindungen für Ihre {{site.data.keyword.Bluemix_notm}}-Cloudant-Serviceinstanzen. Verwenden Sie {{site.data.keyword.openwhisk_short}} und Cloudant aus {{site.data.keyword.Bluemix_notm}} nicht, fahren Sie mit dem nächsten Schritt fort.

1. Erstellen Sie eine Cloudant-Serviceinstanz in Ihrem {{site.data.keyword.Bluemix_notm}}-[Dashboard](http://console.ng.{{site.data.keyword.Bluemix_notm}}.net).

  Stellen Sie sicher, dass Sie sich den Namen der Serviceinstanz sowie die {{site.data.keyword.Bluemix_notm}}-Organisation und den Bereich merken, in dem Sie sich befinden.

2. Stellen Sie sicher, dass sich Ihre {{site.data.keyword.openwhisk_short}}-Befehlszeilenschnittstelle (CLI) in dem Namensbereich befindet, der der {{site.data.keyword.Bluemix_notm}}-Organisation und dem Bereich entspricht, die Sie im vorherigen Schritt verwendet haben.

  ```
  wsk property set --namespace my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space
  ```
  {: pre}

  Alternativ können Sie mit dem Befehl `wsk property set --namespace` den Namensbereich mithilfe einer Liste der für sie zugänglichen Namensbereiche festlegen.

3. Aktualisieren Sie die Pakete in Ihrem Namensbereich. Die Aktualisierung erstellt automatisch eine Paketbindung für die Cloudant-Serviceinstanz, die Sie erstellt haben.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  {{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1 private binding
  ```
  {: screen}

  Es sollte der vollständig qualifizierte Name der Paketbindung angezeigt werden, die Ihrer {{site.data.keyword.Bluemix_notm}}-Cloudant-Serviceinstanz entspricht.

4. Prüfen Sie, ob die zuvor erstellte Paketbindung mit dem Host und den Berechtigungsnachweisen für Ihre {{site.data.keyword.Bluemix_notm}}-Cloudant-Serviceinstanz konfiguriert ist.

  ```
  wsk package get /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1
  ```
  {: pre}
  ```
  ok: got package /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1, projecting parameters
  [
      ...
      {
          "key": "username",
          "value": "cdb18832-2bbb-4df2-b7b1-{{site.data.keyword.Bluemix_notm}}"
      },
      {
          "key": "host",
          "value": "cdb18832-2bbb-4df2-b7b1-{{site.data.keyword.Bluemix_notm}}.cloudant.com"
      },
      {
          "key": "password",
          "value": "c9088667484a9ac827daf8884972737"
      }
      ...
  ]
  ```
  {: screen}

### Cloudant-Datenbank außerhalb von {{site.data.keyword.Bluemix_notm}} einrichten

Wenn Sie {{site.data.keyword.openwhisk_short}} in {{site.data.keyword.Bluemix_notm}} nicht verwenden oder wenn Sie Ihre Cloudant-Datenbank außerhalb von {{site.data.keyword.Bluemix_notm}} einrichten möchten, müssen Sie manuell eine Paketbindung für Ihr Cloudant-Konto erstellen. Sie benötigen den Hostnamen, den Benutzernamen und das Kennwort des Cloudant-Kontos.

1. Erstellen Sie eine Paketbindung, die für Ihr Cloudant-Konto konfiguriert ist.

  ```
  wsk package bind /whisk.system/cloudant myCloudant -p username 'MYUSERNAME' -p password 'MYPASSWORD' -p host 'MYCLOUDANTACCOUNT.cloudant.com'
  ```
  {: pre}

2. Prüfen Sie, ob die Paketbindung vorhanden ist.

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myNamespace/myCloudant private binding
  ```
  {: screen}


### Änderungen an einer Cloudant-Datenbank empfangen

Mit dem Feed `changes` können Sie einen Service konfigurieren, der bei jeder Änderung an Ihrer Cloudant-Datenbank einen Auslöser aktiviert.

1. Erstellen Sie einen Auslöser mit dem Feed `changes` in der Paketbindung, die Sie zuvor erstellt haben. Stellen Sie sicher, dass Sie `/myNamespace/myCloudant` durch Ihren Paketnamen ersetzen.

  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb --param includeDocs true
  ```
  {: pre}
  ```
  ok: created trigger feed myCloudantTrigger
  ```
  {: screen}

2. Fragen Sie Aktivierungen mit der Pollingfunktion ab.

  ```
  wsk activation poll
  ```
  {: pre}

3. Ändern Sie in Ihrem Cloudant-Dashboard ein vorhandenes Dokument oder erstellen Sie ein neues Dokument.

4. Beobachten Sie die neuen Aktivierungen für den Auslöser `myCloudantTrigger` für jede Dokumentänderung.

**Hinweis:** Wenn Sie keine neuen Aktivierungen beobachten können, lesen Sie die nachfolgenden Abschnitte über das Lesen und Schreiben in einer Cloudant-Datenbank. Durch Testen der nachfolgenden Schritte zum Lesen und Schreiben können Sie prüfen, ob Ihre Cloudant-Berechtigungsnachweise korrekt sind.

Sie können jetzt Regeln erstellen und diese Aktionen zuordnen, um auf die Dokumentaktualisierungen zu reagieren.

Der Inhalt der generierten Ereignisse hängt von dem Wert des Parameters `includeDocs` beim Erstellen des Auslösers ab. Wenn der Parameter den Wert 'true' hat, enthält jedes Auslöserereignis, das aktiviert wird, das geänderte Cloudant-Dokument. Betrachten Sie zum Beispiel das folgende geänderte Dokument:

  ```
  {
    "_id": "6ca436c44074c4c2aa6a40c9a188b348",
    "_rev": "3-bc4960fc13aa368afca8c8427a1c18a8",
    "name": "Heisenberg"
  }
  ```
  {: screen}

Der Code in diesem Beispiel generiert ein Auslöserereignis mit den entsprechenden Parametern `_id`, `_rev` und `name`. Tatsächlich ist die JSON-Darstellung des Auslöserereignisses mit dem Dokument identisch.

Andernfalls, wenn der Parameter `includeDocs` den Wert 'false' hat, enthalten die Ereignisse die folgenden Parameter:

- `id`: Die Dokument-ID.
- `seq`: Die von Cloudant generierte Sequenz-ID.
- `changes`: Ein Array von Objekten, die jeweils ein Feld `rev` haben, das die Revisions-ID des Dokuments enthält.

Die JSON-Darstellung des Auslöserereignisses sieht wie folgt aus:

  ```
  {
      "id": "6ca436c44074c4c2aa6a40c9a188b348",
      "seq": "2-g1AAAAL9aJyV-GJCaEuqx4-BktQkYp_dmIfC",
      "changes": [
          {
              "rev": "2-da3f80848a480379486fb4a2ad98fa16"
          }
      ]
  }
  ```


### In eine Cloudant-Datenbank schreiben

Sie können eine Aktion verwenden, um ein Dokument in einer Cloudant-Datenbank mit dem Namen `testdb` speichern. Stellen Sie sicher, dass diese Datenbank in Ihrem Cloudant-Konto vorhanden ist.

1. Speichern Sie ein Dokument mit der Aktion `write` in der Paketbindung, die Sie zuvor erstellt haben. Stellen Sie sicher, dass Sie `/myNamespace/myCloudant` durch Ihren Paketnamen ersetzen.

  ```
  wsk action invoke /myNamespace/myCoudant/write --blocking --result --param dbname testdb --param doc '{"_id":"heisenberg", "name":"Walter White"}'
  ```
  {: pre}
  ```
  ok: invoked /myNamespace/myCoudant/write with id 62bf696b38464fd1bcaff216a68b8287
  response:
  {
    "id": "heisenberg",
    "ok": true,
    "rev": "1-9a94fb93abc88d8863781a248f63c8c3"
  }
  ```
  {: screen}

2. Prüfen Sie, ob das Dokument vorhanden ist, indem Sie in Ihrem Cloudant-Dashboard danach suchen.

  Die Dashboard-URL für die Datenbank `testdb` sieht in etwa wie folgt aus: `https://MYCLOUDANTACCOUNT.cloudant.com/dashboard.html#database/testdb/_all_docs?limit=100`.


### Aus einer Cloudant-Datenbank lesen

Sie können eine Aktion verwenden, um ein Dokument aus einer Cloudant-Datenbank mit dem Namen `testdb` abzurufen. Stellen Sie sicher, dass diese Datenbank in Ihrem Cloudant-Konto vorhanden ist.

1. Rufen Sie ein Dokument mit der Aktion `read` in der Paketbindung ab, die Sie zuvor erstellt haben. Stellen Sie sicher, dass Sie `/myNamespace/myCloudant` durch Ihren Paketnamen ersetzen.

  ```
  wsk action invoke /myNamespace/myCoudant/read --blocking --result --param dbname testdb --param id heisenberg
  ```
  {: pre}
  ```
  {
    "_id": "heisenberg",
    "_rev": "1-9a94fb93abc88d8863781a248f63c8c3"
    "name": "Walter White"
  }
  ```
  {: screen}


## Paket für Alarme verwenden
{: #openwhisk_catalog_alarm}

Das Paket `/whisk.system/alarms` kann verwendet werden, um Auslöser in einer angegebenen Häufigkeit zu aktivieren. Dies ist nützlich, um sich wiederholende Jobs oder Tasks einzurichten, wie zum Beispiel das stündliche Aufrufen einer Systemsicherungsaktion.

Das Paket enthält den folgenden Feed.

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | Paket | - | Dienstprogramm für Alarme und periodisch wiederkehrende Aktionen |
| `/whisk.system/alarms/alarm` | Feed | cron, trigger_payload, maxTriggers | Auslöserereignis regelmäßig aktivieren |


### Auslöserereignis regelmäßig aktivieren

Der Feed `/whisk.system/alarms/alarm` konfiguriert den Alarm-Service so, dass er ein Auslöserereignis mit einer angegebenen Häufigkeit aktiviert. Die folgenden Parameter sind verfügbar:

- `cron`: Eine Zeichenfolge auf der Basis der Unix-Syntax 'crontab', die angibt, wann der Auslöser zu aktivieren ist (angegebenen in koordinierter Weltzeit, UTC). Die Zeichenfolge besteht aus einer Reihe von sechs durch Leerzeichen getrennten Feldern: `X X X X X X `. Weitere Informationen zur Verwendung der cron-Syntax finden Sie in https://github.com/ncb000gt/node-cron.

- `trigger_payload`: Der Wert dieses Parameters wird jedes Mal zum Inhalt des Auslösers, wenn der Auslöser aktiviert wird.

- `maxTriggers`: Stoppt die Aktivierung von Auslösern, wenn dieser Grenzwert erreicht wird. Standardwert: 1000.

Das folgende Beispiel zeigt, wie ein Auslöser erstellt wird, der einmal alle 20 Sekunden aktiviert wird, wobei das Auslöserereignis die Werte für `name` und `place` enthält.

  ```
  wsk trigger create periodic --feed /whisk.system/alarms/alarm --param cron '/20 * * * * *' --param trigger_payload '{"name":"Odin","place":"Asgard"}'
  ```
  {: pre}

Jedes generierte Ereignis enthält die im Wert von `trigger_payload` angegebenen Eigenschaften als Parameter. In diesem Fall erhält jedes Auslöserereignis die Parameter `name=Odin` und `place=Asgard`.


## Weather-Paket verwenden
{: #openwhisk_catalog_weather}

Das Paket `/whisk.system/weather` bietet eine komfortable Methode zum Aufrufen der The Weather Company-API.

Das Paket enthält die folgende Aktion.

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/weather` | Paket | apiKey | Services von The Weather Company |
| `/whisk.system/weather/forecast` | Aktion | apiKey, latitude, longitude | 10-Tage-Vorhersage von Weather.com |

Obgleich dies nicht erforderlich ist, wird empfohlen, eine Paketbindung mit dem Wert `apiKey` zu erstellen. Auf diese Weise brauchen Sie den Schlüssel nicht jedes Mal anzugeben, wenn Sie die Aktionen im Paket aufrufen.

### Wettervorhersage für einen Standort abrufen

Die Aktion `/whisk.system/weather/forecast` gibt eine 10-Tage-Wettervorhersage für einen Standort durch einen Aufruf der API für The Weather Company zurück. Die folgenden Parameter sind verfügbar:

- `apiKey`: Ein API-Schlüssel für The Weather Company, der berechtigt ist, die API für die 10-Tage-Vorhersage aufzurufen.
- `latitude`: Die Breitengradkoordinate des Standorts.
- `longitude`: Die Längengradkoordinate des Standorts.

Das folgende Beispiel zeigt die Erstellung einer Paketbindung und den anschließenden Abruf einer 10-Tage-Vorhersage.

1. Erstellen Sie eine Paketbindung mit Ihrem API-Schlüssel.

  ```
  wsk package bind /whisk.system/weather myWeather --param apiKey 'MY_WEATHER_API'
  ```
  {: pre}

2. Rufen Sie die Aktion `forecast` in Ihrer Paketbindung auf, um die Wettervorhersage abzurufen.

  ```
  wsk action invoke myWeather/forecast --blocking --result --param latitude '43.7' --param longitude '-79.4'
  ```
  {: pre}

  ```
  {
      "forecasts": [
          {
              "dow": "Wednesday",
              "max_temp": -1,
              "min_temp": -16,
              "narrative": "Chance of a few snow showers. Highs -2 to 0C and lows -17 to -15C.",
              ...
          },
          {
              "class": "fod_long_range_daily",
              "dow": "Thursday",
              "max_temp": -4,
              "min_temp": -8,
              "narrative": "Mostly sunny. Highs -5 to -3C and lows -9 to -7C.",
              ...
          },
          ...
      ],
  }
  ```
  {: screen}


## Watson-Paket verwenden
{: #openwhisk_catalog_watson}

Das Paket `/whisk.system/watson` bietet eine komfortable Methode zum Aufrufen verschiedener Watson-APIs.

Das Paket enthält die folgenden Aktionen.

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/watson` | Paket | username, password | Aktionen für die Watson-Analyse-APIs |
| `/whisk.system/watson/translate` | Aktion | translateFrom, translateTo, translateParam, username, password | Übersetzung von Text |
| `/whisk.system/watson/languageId` | Aktion | payload, username, password | Ermittlung einer Sprache |

Obgleich dies nicht erforderlich ist, wird empfohlen, eine Paketbindung mit den Werten `username` und `password` zu erstellen. Auf diese Weise brauchen Sie diese Berechtigungsnachweise nicht jedes Mal anzugeben, wenn Sie die Aktionen im Paket aufrufen.

### Text übersetzen

Die Aktion `/whisk.system/watson/translate` übersetzt Text aus einer Sprache in eine andere. Die folgenden Parameter sind verfügbar:

- `username`: Der Benutzername für die Watson-API.
- `password`: Das Kennwort für die Watson-API.
- `translateParam`: Der zu übersetzende Eingabeparameter. Beispiel: Wenn `translateParam=payload` angegeben wird, wird der Wert des Parameters `payload`, der an die Aktion übergeben wird, übersetzt.
- `translateFrom`: Ein zweistelliger Code für die Ausgangssprache.
- `translateTo`: Ein zweistelliger Code für die Zielsprache.

Das folgende Beispiel zeigt die Erstellung einer Paketbindung und die Übersetzung eines Texts.

1. Erstellen Sie eine Paketbindung mit Ihren Watson-Berechtigungsnachweisen.

  ```
  wsk package bind /whisk.system/watson myWatson --param username 'MY_WATSON_USERNAME' --param password 'MY_WATSON_PASSWORD'
  ```
  {: pre}

2. Rufen Sie die Aktion `translate` in Ihrer Paketbindung auf, um einen Text aus dem Englischen ins Französische zu übersetzen.

  ```
  wsk action invoke myWatson/translate --blocking --result --param payload 'Blue skies ahead' --param translateParam 'payload' --param translateFrom 'en' --param translateTo 'fr'
  ```
  {: pre}

  ```
  {
      "payload": "Ciel bleu a venir"
  }
  ```
  {: screen}


### Sprache eines Texts ermitteln

Die Aktion `/whisk.system/watson/languageId` ermittelt die Sprache eines Texts. Die folgenden Parameter sind verfügbar:

- `username`: Der Benutzername für die Watson-API.
- `password`: Das Kennwort für die Watson-API.
- `payload`: Der zu ermittelnde Text.

Das folgende Beispiel zeigt die Erstellung einer Paketbindung und die Ermittlung der Sprache eines Texts.

1. Erstellen Sie eine Paketbindung mit Ihren Watson-Berechtigungsnachweisen.

  ```
  wsk package bind /whisk.system/watson myWatson -p username 'MY_WATSON_USERNAME' -p password 'MY_WATSON_PASSWORD'
  ```
  {: pre}

2. Rufen Sie die Aktion `languageId` in Ihrer Paketbindung auf, um die Sprache zu ermitteln.

  ```
  wsk action invoke myWatson/languageId --blocking --result --param payload 'Ciel bleu a venir'
  ```
  {: pre}
  ```
  {
    "payload": "Ciel bleu a venir",
    "language": "fr",
    "confidence": 0.710906
  }
  ```
  {: screen}


## Slack-Paket verwenden
{: #openwhisk_catalog_slack}

Das Paket `/whisk.system/slack` bietet eine komfortable Methode zur Verwendung der [Slack-APIs](https://api.slack.com/).

Das Paket enthält die folgenden Aktionen:

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/slack` | Paket | url, channel, username | Interaktion mit der Slack-API |
| `/whisk.system/slack/post` | Aktion | text, url, channel, username | Senden einer Nachricht an einen Slack-Kanal |

Obgleich dies nicht erforderlich ist, wird empfohlen, eine Paketbindung mit den Werten `username`, `url` und 'channel' zu erstellen. Mit der Bindung brauchen Sie die Werte nicht jedes Mal anzugeben, wenn Sie die Aktion im Paket aufrufen.

### Nachricht an einen Slack-Kanal senden

Die Aktion `/whisk.system/slack/post` sendet eine Nachricht an einen angegebenen Slack-Kanal. Die folgenden Parameter sind verfügbar:

- `url`: Die URL für den Slack-Web-Hook.
- `channel`: Der Slack-Kanal, an den die Nachricht zu senden ist.
- `username`: Der Name, unter dem die Nachricht gesendet werden soll.
- `text`: Ein zu sendender Nachrichtentext.

Das folgende Beispiel zeigt die Konfiguration von Slack, die Erstellung einer Paketbindung und das Senden einer Nachricht an einen Kanal.

1. Konfigurieren Sie für Ihr Team einen [eingehenden Web-Hook](https://api.slack.com/incoming-webhooks) für Slack.

  Nach der Konfiguration von Slack sollten Sie eine Web-Hook-URL erhalten, die ungefähr wie folgt aussieht: `https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`. Sie benötigen diese im nächsten Schritt.

2. Erstellen Sie eine Paketbindung mit Ihren Slack-Berechtigungsnachweisen, mit dem Kanal, an den gesendet werden soll, sowie mit dem Benutzernamen, unter dem gesendet werden soll.

  ```
  wsk package bind /whisk.system/slack mySlack --param url 'https://hooks.slack.com/services/...' --param username 'Bob' --param channel '#MySlackChannel'
  ```
  {: pre}

3. Rufen Sie die Aktion `post` in Ihrer Paketbindung auf, um eine Nachricht an Ihren Slack-Kanal zu senden.

  ```
  wsk action invoke mySlack/post --blocking --result --param text 'Hallo von OpenWhisk!'
  ```
  {: pre}


## GitHub-Paket verwenden
{: #openwhisk_catalog_github}

Das Paket `/whisk.system/github` bietet eine komfortable Methode zur Verwendung der [GitHub-APIs](https://developer.github.com/).

Das Paket enthält den folgenden Feed:

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/github` | Paket | username, repository, accessToken | Interaktion mit der GitHub-API |
| `/whisk.system/github/webhook` | Feed | events, username, repository, accessToken | Aktivieren von Auslöserereignissen für GitHub-Aktivitäten |

Obgleich dies nicht erforderlich ist, wird empfohlen, eine Paketbindung mit den Werten `username`, `repository` und `accessToken` zu erstellen.  Mit der Bindung brauchen Sie die Werte nicht jedes Mal anzugeben, wenn Sie den Feed im Paket verwenden.

### Auslöserereignis für GitHub-Aktivität aktivieren

Der Feed `/whisk.system/github/webhook` konfiguriert einen Service so, dass ein Auslöser aktiviert wird, wenn eine Aktivität in einem angegebenen GitHub-Repository stattfindet. Die folgenden Parameter sind verfügbar:

- `username`: Der Benutzername für das GitHub-Repository.
- `repository`: Das GitHub-Repository.
- `accessToken`: Ihr persönliches GitHub-Zugriffstoken. Wenn Sie Ihr [Token erstellen](https://github.com/settings/tokens), stellen Sie sicher, dass Sie die Geltungsbereiche 'repo:status' und 'public_repo' auswählen. Stellen Sie außerdem sicher, dass noch keine Web-Hooks für Ihr Repository definiert sind.
- `events`: Der interessierende [GitHub-Aktivitätstyp](https://developer.github.com/v3/activity/events/types/).

Das folgende Beispiel zeigt, wie ein Auslöser erstellt wird, der jedes Mal aktiviert wird, wenn eine neue Festschreibung (Commit) in einem GitHub-Repository erfolgt.

1. Generieren Sie ein [persönliches Zugriffstoken](https://github.com/settings/tokens) für GitHub.

  Das Zugriffstoken wird im nächsten Schritt verwendet.


2. Erstellen Sie eine Paketbindung, die für Ihr GitHub-Repository und mit Ihrem Zugriffstoken konfiguriert ist.

  ```
  wsk package bind /whisk.system/github myGit --param username myGitUser --param repository myGitRepo --param accessToken aaaaa1111a1a1a1a1a111111aaaaaa1111aa1a1a
  ```
  {: pre}

3. Erstellen Sie einen Auslöser für den GitHub-Ereignistyp `push` unter Verwendung Ihres Feeds `myGit/webhook`.

  ```
  wsk trigger create myGitTrigger --feed myGit/webhook --param events push
  ```
  {: pre}

