---

 

copyright:

  years: 2016, 2017
lastupdated: "2017-01-04"
 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.Bluemix_notm}}-Services für {{site.data.keyword.openwhisk_short}} verwenden
{: #openwhisk_ecosystem}

In {{site.data.keyword.openwhisk}} stellt ein Katalog von Paketen eine einfache Methode bereit, um Ihre App mit nützlichen Funktionen zu erweitern und um auf externe Services im direkten Geschäftsumfeld ('Ökosystem') zuzugreifen. Zu den externen Services, die für {{site.data.keyword.openwhisk_short}} eingerichtet sind, gehören zum Beispiel Cloudant, The Weather Company, Slack und GitHub.
{: shortdesc}

Der Katalog ist in Form von Paketen im Namensbereich `/whisk.system` verfügbar. Informationen dazu, wie sich der Katalog mithilfe des Befehlszeilentools durchsuchen lässt, finden Sie unter [Pakete durchsuchen](./openwhisk_packages.html#openwhisk_packagedisplay).

In den folgenden Abschnitten werden einige der Pakete im Katalog dokumentiert.

## Cloudant-Paket verwenden
{: #openwhisk_catalog_cloudant}
Das Paket `/whisk.system/cloudant` ermöglicht Ihnen die Arbeit mit einer Cloudant-Datenbank. Es enthält die folgenden Aktionen und Feeds.

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | Paket | {{site.data.keyword.Bluemix_notm}}ServiceName, host, username, password, dbname, overwrite | Dient zur Arbeit mit einer Cloudant-Datenbank. |
| `/whisk.system/cloudant/read` | Aktion | dbname, includeDoc, id | Liest ein Dokument aus einer Datenbank. |
| `/whisk.system/cloudant/write` | Aktion | dbname, overwrite, doc | Schreibt ein Dokument in eine Datenbank. |
| `/whisk.system/cloudant/changes` | Feed | dbname, maxTriggers | Aktiviert Auslöserereignisse bei Änderungen an einer Datenbank. |

In den folgenden Abschnitten werden die Einrichtung einer Cloudant-Datenbank, die Konfiguration eines zugeordneten Pakets sowie die Verwendung der Aktionen und Feeds im Paket `/whisk.system/cloudant` schrittweise erläutert.

### Cloudant-Datenbank in {{site.data.keyword.Bluemix_notm}} einrichten
{: #openwhisk_catalog_cloudant_in}

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

  Es wird der vollständig qualifizierte Name der Paketbindung angezeigt, die Ihrer {{site.data.keyword.Bluemix_notm}}-Cloudant-Serviceinstanz entspricht.

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
{: #openwhisk_catalog_cloudant_outside}

Wenn Sie {{site.data.keyword.openwhisk_short}} in {{site.data.keyword.Bluemix_notm}} nicht verwenden oder wenn Sie Ihre Cloudant-Datenbank außerhalb von {{site.data.keyword.Bluemix_notm}} einrichten möchten, müssen Sie manuell eine Paketbindung für Ihr Cloudant-Konto erstellen. Sie benötigen den Hostnamen, den Benutzernamen und das Kennwort des Cloudant-Kontos.

1. Erstellen Sie eine Paketbindung, die für Ihr Cloudant-Konto konfiguriert ist.

  ```
  wsk package bind /whisk.system/cloudant myCloudant -p username MYUSERNAME -p password MYPASSWORD -p host MYCLOUDANTACCOUNT.cloudant.com
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
{: #openwhisk_catalog_cloudant_listen}

Mit dem Feed `changes` können Sie einen Service konfigurieren, der bei jeder Änderung an Ihrer Cloudant-Datenbank einen Auslöser aktiviert. Die folgenden Parameter sind verfügbar:

- `dbname`: Name der Cloudant-Datenbank.
- `maxTriggers`: Stoppt die Aktivierung von Auslösern, wenn dieser Grenzwert erreicht wird. Standardwert: unbegrenzt.

1. Erstellen Sie einen Auslöser mit dem Feed `changes` in der Paketbindung, die Sie zuvor erstellt haben. Stellen Sie sicher, dass Sie `/myNamespace/myCloudant` durch Ihren Paketnamen ersetzen.

  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
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

Der Inhalt der generierten Ereignisse weist die folgenden Parameter auf:

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
{: #openwhisk_catalog_cloudant_write}

Sie können eine Aktion verwenden, um ein Dokument in einer Cloudant-Datenbank mit dem Namen `testdb` speichern. Stellen Sie sicher, dass diese Datenbank in Ihrem Cloudant-Konto vorhanden ist.

1. Speichern Sie ein Dokument mit der Aktion `write` in der Paketbindung, die Sie zuvor erstellt haben. Stellen Sie sicher, dass Sie `/myNamespace/myCloudant` durch Ihren Paketnamen ersetzen.

  ```
  wsk action invoke /myNamespace/myCloudant/write --blocking --result --param dbname testdb --param doc "{\"_id\":\"heisenberg\",\"name\":\"Walter White\"}"
  ```
  {: pre}
  ```
  ok: invoked /myNamespace/myCloudant/write with id 62bf696b38464fd1bcaff216a68b8287
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
{: #openwhisk_catalog_cloudant_read}

Sie können eine Aktion verwenden, um ein Dokument aus einer Cloudant-Datenbank mit dem Namen `testdb` abzurufen. Stellen Sie sicher, dass diese Datenbank in Ihrem Cloudant-Konto vorhanden ist.

1. Rufen Sie ein Dokument mit der Aktion `read` in der Paketbindung ab, die Sie zuvor erstellt haben. Stellen Sie sicher, dass Sie `/myNamespace/myCloudant` durch Ihren Paketnamen ersetzen.

  ```
  wsk action invoke /myNamespace/myCloudant/read --blocking --result --param dbname testdb --param id heisenberg
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

### Aktionssequenz und Änderungsauslöser zur Verarbeitung eines Dokuments aus einer Cloudant-Datenbank verwenden

Sie können eine Aktionssequenz in einer Regel verwenden, um das Dokument, das einem Cloudant-Änderungsereignis zugeordnet ist, abzurufen und zu verarbeiten.

Im Folgenden ist ein Beispielcode einer Aktion aufgeführt, die zur Verarbeitung eines Dokuments dient:
```
function main(doc){
  return { "isWalter:" : doc.name === "Walter White"};
}
```
{: codeblock}

Erstellen Sie die Aktion, um das Dokument aus Cloudant zu verarbeiten:
```
wsk action create myAction myAction.js
```
{: pre}

Um ein Dokument aus der Datenbank zu lesen, können Sie die Aktion `read` aus dem Cloudant-Paket verwenden.
Die Aktion `read` kann mit `myAction` zusammengesetzt werden, um eine Aktionsfolge zu erstellen.
```
wsk action create sequenceAction --sequence /myNamespace/myCloudant/read,myAction
```
{: pre}

Die Aktion `sequenceAction` kann in einer Regel verwendet werden, mit der die Aktion bei neuen Cloudant-Auslöserereignissen aktiviert wird.
```
wsk rule create myRule myCloudantTrigger sequenceAction
```
{: pre}

**Hinweis:** Mit dem Cloudant-Auslöser `changes` wurde der Parameter `includeDoc` unterstützt, der nun nicht mehr unterstützt wird.
  Sie müssen Auslöser, die zuvor mit `includeDoc` erstellt wurden, erneut erstellen. Führen Sie die folgenden Schritte aus, um den Auslöser erneut zu erstellen:
  ```
  wsk trigger delete myCloudantTrigger
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
  ```
  {: pre}

  Das oben dargestellte Beispiel kann verwendet werden, um eine Aktionsfolge zu erstellen, um das geänderte Dokument zu lesen und die vorhandenen Aktionen aufzurufen.
  Denken Sie daran, Regeln zu inaktivieren, die möglicherweise nicht mehr gültig sind, und erstellen Sie mit dem Aktionsfolgemuster neue Regeln.

## Paket für Alarme verwenden
{: #openwhisk_catalog_alarm}

Das Paket `/whisk.system/alarms` kann verwendet werden, um einen Auslöser in einer angegebenen Häufigkeit zu aktivieren. Dies ist nützlich, um sich wiederholende Jobs oder Tasks einzurichten, wie zum Beispiel das stündliche Aufrufen einer Systemsicherungsaktion.

Das Paket enthält den folgenden Feed.

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | Paket | - | Dienstprogramm für Alarme und periodisch wiederkehrende Aktionen |
| `/whisk.system/alarms/alarm` | Feed | cron, trigger_payload, maxTriggers | Auslöserereignis regelmäßig aktivieren |


### Auslöserereignis regelmäßig aktivieren
{: #openwhisk_catalog_alarm_fire}

Der Feed `/whisk.system/alarms/alarm` konfiguriert den Alarm-Service so, dass er ein Auslöserereignis mit einer angegebenen Häufigkeit aktiviert. Die folgenden Parameter sind verfügbar:

- `cron`: Eine Zeichenfolge auf der Basis der UNIX-Syntax 'crontab', die angibt, wann der Auslöser zu aktivieren ist (angegeben in koordinierter Weltzeit, UTC). Die Zeichenfolge besteht aus einer Reihe von fünf durch Leerzeichen getrennten Feldern: `X X X X X`.
Weitere Informationen zur Verwendung der cron-Syntax finden Sie unter 'http://crontab.org'. Beispiele für die von der Zeichenfolge angegebene Häufigkeit:

  - `* * * * *`: zu Beginn jeder Minute.
  - `0 * * * *`: zu Beginn jeder Stunde.
  - `0 */2 * * *`: alle zwei Stunden (z. B. 02:00:00, 04:00:00, ...).
  - `0 9 8 * *`: um 9:00:00 (UTC) am achten Tag jeden Monats.

- `trigger_payload`: Der Wert dieses Parameters wird jedes Mal zum Inhalt des Auslösers, wenn der Auslöser aktiviert wird.

- `maxTriggers`: Stoppt die Aktivierung von Auslösern, wenn dieser Grenzwert erreicht wird. Standardwert: 1.000.000. Der Wert -1 (unbegrenzt) kann verwendet werden.

Das folgende Beispiel zeigt, wie ein Auslöser erstellt wird, der einmal alle 2 Minuten aktiviert wird, wobei das Auslöserereignis die Werte für `name` und `place` enthält.

  ```
  wsk trigger create periodic --feed /whisk.system/alarms/alarm --param cron "*/2 * * * *" --param trigger_payload "{\"name\":\"Odin\",\"place\":\"Asgard\"}"
  ```
  {: pre}

Jedes generierte Ereignis enthält die im Wert von `trigger_payload` angegebenen Eigenschaften als Parameter. In diesem Fall erhält jedes Auslöserereignis die Parameter `name=Odin` und `place=Asgard`.

**Hinweis:** Der Parameter `cron` bietet auch Unterstützung für eine angepasste Syntax mit sechs Feldern, wobei das erste Feld für Sekunden steht. 
Weitere Informationen zur Verwendung dieser angepassten cron-Syntax finden Sie unter 'https://github.com/ncb000gt/node-cron'. 
Im Folgenden ist ein Beispiel für die Notation mit sechs Feldern aufgeführt:
  - `*/30 * * * * *`: alle 30 Sekunden.

## Weather-Paket verwenden
{: #openwhisk_catalog_weather}

Das Paket `/whisk.system/weather` bietet eine komfortable Methode zum Aufrufen der Weather Company Data for IBM Bluemix-API.

Das Paket enthält die folgende Aktion.

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/weather` | Paket | username, password | Services der Weather Company Data for IBM Bluemix-API  |
| `/whisk.system/weather/forecast` | Aktion | latitude, longitude, timePeriod | Vorhersage für angegebenen Zeitraum|

Es wird empfohlen, eine Paketbindung mit den Werten `username` und `password` zu erstellen. Auf diese Weise brauchen Sie die Berechtigungsnachweise nicht jedes Mal anzugeben, wenn Sie die Aktionen im Paket aufrufen.

### Wettervorhersage für einen Standort abrufen
{: #openwhisk_catalog_weather_forecast}

Die Aktion `/whisk.system/weather/forecast` gibt eine Wettervorhersage für einen Standort durch einen Aufruf der API für The Weather Company zurück. Die folgenden Parameter sind verfügbar:

- `username`: Der Benutzername für Weather Company Data for IBM Bluemix, der berechtigt ist, die API für die Vorhersage aufzurufen.
- `password`: Das Kennwort für Weather Company Data for IBM Bluemix, das berechtigt ist, die API für die Vorhersage aufzurufen.
- `latitude`: Die Breitengradkoordinate des Standorts.
- `longitude`: Die Längengradkoordinate des Standorts.
- `timeperiod`: Der Zeitraum für die Vorhersage. Gültige Optionen: '10day' (Standardwert) - Gibt eine tägliche 10-Tage-Vorhersage zurück. '48hour' - Gibt eine stündliche 2-Tage-Vorhersage zurück. 'current' - Gibt die aktuellen Wetterbedingungen zurück. 'timeseries' - Gibt die aktuellen Wetterbeobachtungen und bis zu 24 Stunden zurückliegende Beobachtungen ab dem aktuellen Zeitpunkt (Datum und Uhrzeit) zurück.


Das folgende Beispiel zeigt die Erstellung einer Paketbindung und den anschließenden Abruf einer 10-Tage-Vorhersage.

1. Erstellen Sie eine Paketbindung mit Ihrem API-Schlüssel.

  ```
  wsk package bind /whisk.system/weather myWeather --param username MY_USERNAME --param password MY_PASSWORD
  ```
  {: pre}

2. Rufen Sie die Aktion `forecast` in Ihrer Paketbindung auf, um die Wettervorhersage abzurufen.

  ```
  wsk action invoke myWeather/forecast --blocking --result --param latitude 43.7 --param longitude -79.4
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


## Watson-Pakete verwenden
{: #openwhisk_catalog_watson}

Die Watson-Pakete bieten eine komfortable Möglichkeit zum Aufrufen verschiedener Watson-APIs.

Die folgenden Watson-Pakete werden bereitgestellt:

| Paket | Beschreibung |
| --- | --- |
| `/whisk.system/watson-translator`   | Paket für Textübersetzung und Spracherkennung |
| `/whisk.system/watson-textToSpeech` | Paket zum Umwandeln von Text in Sprache |
| `/whisk.system/watson-speechToText` | Paket zum Umwandeln von Sprache in Text |

**Hinweis:** Das Paket `/whisk.system/watson` wird momentan nicht mehr verwendet. Führen Sie eine Migration auf die hier aufgeführten neuen Pakete durch. Die neuen Aktionen bieten die gleiche Schnittstelle.

### Watson Translator-Paket verwenden

Das Paket `/whisk.system/watson-translator` bietet eine komfortable Methode zum Aufrufen der Watson-APIs für die Übersetzung.

Das Paket enthält die folgenden Aktionen.

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/watson-translator` | Paket | username, password | Paket für Textübersetzung und Spracherkennung  |
| `/whisk.system/watson-translator/translator` | Aktion | payload, translateFrom, translateTo, translateParam, username, password | Übersetzung von Text |
| `/whisk.system/watson-translator/languageId` | Aktion | payload, username, password | Ermittlung einer Sprache |

**Hinweis:** Das Paket `/whisk.system/watson` wird einschließlich der Aktionen `/whisk.system/watson/translate` und `/whisk.system/watson/languageId` nicht mehr verwendet.

#### Watson Translator-Paket in Bluemix einrichten

Wenn Sie OpenWhisk von Bluemix verwenden, dann erstellt OpenWhisk automatisch Paketbindungen für Ihre Bluemix-Watson-Serviceinstanzen.

1. Erstellen Sie eine Watson Translator-Serviceinstanz in Ihrem Bluemix-[Dashboard](http://console.ng.Bluemix.net).

  Stellen Sie sicher, dass Sie sich den Namen der Serviceinstanz sowie der Bluemix-Organisation und den Bereich merken, in dem Sie sich befinden.

2. Stellen Sie sicher, dass sich Ihre OpenWhisk-Befehlszeilenschnittstelle (CLI = Command-Line Interface) in dem Namensbereich befindet, der der Bluemix-Organisation und dem Bereich entspricht, die Sie im vorherigen Schritt verwendet haben.

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  Alternativ können Sie mit dem Befehl `wsk property set --namespace` den Namensbereich mithilfe einer Liste der für sie zugänglichen Namensbereiche festlegen.

3. Aktualisieren Sie die Pakete in Ihrem Namensbereich. Die Aktualisierung erstellt automatisch eine Paketbindung für die Watson-Serviceinstanz, die Sie erstellt haben.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_Translator_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_Translator_Credentials-1 private
  ```
  {: screen}


#### Watson Translator-Paket außerhalb von Bluemix einrichten

Wenn Sie OpenWhisk nicht in Bluemix verwenden oder wenn Sie Watson Translator außerhalb von Bluemix einrichten möchten, müssen Sie manuell eine Paketbindung für Ihren Watson Translator-Service erstellen. Sie benötigen hierzu den Benutzernamen und das Kennwort des Watson Translator-Service.

- Erstellen Sie eine Paketbindung, die für Ihren Watson Translator-Service konfiguriert ist.

  ```
  wsk package bind /whisk.system/watson-translator myWatsonTranslator -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### Text übersetzen
{: #openwhisk_catalog_watson_translate}

Die Aktion `/whisk.system/watson-translator/translator` übersetzt Text aus einer Sprache in eine andere. Die folgenden Parameter sind verfügbar:

- `username`: Der Benutzername für die Watson-API.
- `password`: Das Kennwort für die Watson-API.
- `payload`: Der zu übersetzende Text.
- `translateParam`: Der Eingabeparameter, der den zu übersetzenden Text angibt. Beispiel: Wenn `translateParam=payload` angegeben wird, wird der Wert des Parameters `payload`, der an die Aktion übergeben wird, übersetzt.
- `translateFrom`: Ein zweistelliger Code für die Ausgangssprache.
- `translateTo`: Ein zweistelliger Code für die Zielsprache.

- Rufen Sie die Aktion `translator` in Ihrer Paketbindung auf, um einen Text aus dem Englischen ins Französische zu übersetzen.

  ```
  wsk action invoke myWatsonTranslator/translator --blocking --result --param payload 'Blue skies ahead' --param translateFrom 'en' --param translateTo 'fr'
  ```
  {: pre}

  ```
  {
      "payload": "Ciel bleu a venir"
  }
  ```
  {: screen}


#### Sprache eines Texts ermitteln
{: #openwhisk_catalog_watson_identifylang}

Die Aktion `/whisk.system/watson-translator/languageId` ermittelt die Sprache eines Texts. Die folgenden Parameter sind verfügbar:

- `username`: Der Benutzername für die Watson-API.
- `password`: Das Kennwort für die Watson-API.
- `payload`: Der zu ermittelnde Text.

- Rufen Sie die Aktion `languageId` in Ihrer Paketbindung auf, um die Sprache zu ermitteln.

  ```
  wsk action invoke myWatsonTranslator/languageId --blocking --result --param payload 'Ciel bleu a venir'
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


### Watson-Paket 'Text to Speech' verwenden
{: #openwhisk_catalog_watson_texttospeech}

Das Paket `/whisk.system/watson-textToSpeech` bietet eine komfortable Methode zum Aufrufen der Watson-APIs für die Konvertierung von Text in Sprache.

Das Paket enthält die folgenden Aktionen.

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/watson-textToSpeech` | Paket | username, password | Paket zum Umwandeln von Text in Sprache |
| `/whisk.system/watson-textToSpeech/textToSpeech` | Aktion | payload, voice, accept, encoding, username, password | Umsetzung von Text in Sprache |

**Hinweis:** Das Paket `/whisk.system/watson` wird einschließlich der Aktion `/whisk.system/watson/textToSpeech` nicht mehr verwendet.

#### Watson-Paket 'Text to Speech' in Bluemix einrichten

Wenn Sie OpenWhisk von Bluemix verwenden, dann erstellt OpenWhisk automatisch Paketbindungen für Ihre Bluemix-Watson-Serviceinstanzen.

1. Erstellen Sie eine Watson-Serviceinstanz für 'Text to Speech' in Ihrem Bluemix-[Dashboard](http://console.ng.Bluemix.net).

  Stellen Sie sicher, dass Sie sich den Namen der Serviceinstanz sowie der Bluemix-Organisation und den Bereich merken, in dem Sie sich befinden.

2. Stellen Sie sicher, dass sich Ihre OpenWhisk-Befehlszeilenschnittstelle (CLI = Command-Line Interface) in dem Namensbereich befindet, der der Bluemix-Organisation und dem Bereich entspricht, die Sie im vorherigen Schritt verwendet haben.

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  Alternativ können Sie mit dem Befehl `wsk property set --namespace` den Namensbereich mithilfe einer Liste der für sie zugänglichen Namensbereiche festlegen.

3. Aktualisieren Sie die Pakete in Ihrem Namensbereich. Die Aktualisierung erstellt automatisch eine Paketbindung für die Watson-Serviceinstanz, die Sie erstellt haben.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_TextToSpeech_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_TextToSpeec_Credentials-1 private
  ```
  {: screen}


#### Watson-Paket 'Text to Speech' außerhalb von Bluemix einrichten

Wenn Sie OpenWhisk nicht in Bluemix verwenden oder wenn Sie den Watson-Service 'Text to Speech' außerhalb von Bluemix einrichten möchten, müssen Sie manuell eine Paketbindung für Ihren Watson-Service 'Text to Speech' erstellen. Sie benötigen hierzu den Benutzernamen und das Kennwort des Watson-Service 'Text to Speech'.

- Erstellen Sie eine Paketbindung, die für Ihren Watson-Service 'Text to Speech' konfiguriert ist.

  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonTextToSpeech -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### Umsetzung von Text in Sprache
{: #openwhisk_catalog_watson_speechtotext}

Mit der Aktion `/whisk.system/watson-speechToText/textToSpeech` kann Text in eine Audioansage konvertiert werden. Die folgenden Parameter sind verfügbar:

- `username`: Der Benutzername für die Watson-API.
- `password`: Das Kennwort für die Watson-API.
- `payload`: Der Text, der in Sprache umgesetzt werden soll.
- `voice`: Die Stimme des Sprechers.
- `accept`: Das Format der Sprachdatei.
- `encoding`: Die Codierung der binären Sprachdaten.


- Rufen Sie die Aktion `textToSpeech` in Ihrer Paketbindung auf, um den Text umzusetzen.

  ```
  wsk action invoke myWatsonTextToSpeech/textToSpeech --blocking --result --param payload 'Hey.' --param voice 'en-US_MichaelVoice' --param accept 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```
  {
    "payload": "<base64 encoding of a .wav file>"
  }
  ```
  {: screen}


### Watson-Paket 'Speech to Text' verwenden
{: #openwhisk_catalog_watson_speechtotext}

Das Paket `/whisk.system/watson-speechToText` bietet eine komfortable Methode zum Aufrufen der Watson-APIs für die Konvertierung von Sprache in Text.

Das Paket enthält die folgenden Aktionen.

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/watson-speechToText` | Paket | username, password | Paket zum Umwandeln von Sprache in Text |
| `/whisk.system/watson-speechToText/speechToText` | Aktion | payload, content_type, encoding, username, password, continuous, inactivity_timeout, interim_results, keywords, keywords_threshold, max_alternatives, model, timestamps, watson-token, word_alternatives_threshold, word_confidence, X-Watson-Learning-Opt-Out | Umsetzung von Sprache in Text |

**Hinweis:** Das Paket `/whisk.system/watson` wird einschließlich der Aktion `/whisk.system/watson/speechToText` nicht mehr verwendet.

#### Watson-Paket 'Speech to Text' in Bluemix einrichten

Wenn Sie OpenWhisk von Bluemix verwenden, dann erstellt OpenWhisk automatisch Paketbindungen für Ihre Bluemix-Watson-Serviceinstanzen.

1. Erstellen Sie eine Watson-Serviceinstanz für 'Speech to Text' in Ihrem Bluemix-[Dashboard](http://console.ng.Bluemix.net).

  Stellen Sie sicher, dass Sie sich den Namen der Serviceinstanz sowie der Bluemix-Organisation und den Bereich merken, in dem Sie sich befinden.

2. Stellen Sie sicher, dass sich Ihre OpenWhisk-Befehlszeilenschnittstelle (CLI = Command-Line Interface) in dem Namensbereich befindet, der der Bluemix-Organisation und dem Bereich entspricht, die Sie im vorherigen Schritt verwendet haben.

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  Alternativ können Sie mit dem Befehl `wsk property set --namespace` den Namensbereich mithilfe einer Liste der für sie zugänglichen Namensbereiche festlegen.

3. Aktualisieren Sie die Pakete in Ihrem Namensbereich. Die Aktualisierung erstellt automatisch eine Paketbindung für die Watson-Serviceinstanz, die Sie erstellt haben.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_SpeechToText_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_SpeechToText_Credentials-1 private
  ```
  {: screen}


#### Watson-Paket 'Speech to Text' außerhalb von Bluemix einrichten

Wenn Sie OpenWhisk nicht in Bluemix verwenden oder wenn Sie den Watson-Service 'Speech to Text' außerhalb von Bluemix einrichten möchten, müssen Sie manuell eine Paketbindung für Ihren Watson-Service 'Speech to Text' erstellen. Sie benötigen hierzu den Benutzernamen und das Kennwort des Watson-Service 'Speech to Text'.

- Erstellen Sie eine Paketbindung, die für Ihren Watson-Service 'Text to Speech' konfiguriert ist.

  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonSpeechToText -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### Umsetzung von Sprache in Text

Mit der Aktion `/whisk.system/watson-speechToText/speechToText` kann eine Audioansage in Text konvertiert werden. Die folgenden Parameter sind verfügbar:

- `username`: Der Benutzername für die Watson-API.
- `password`: Das Kennwort für die Watson-API.
- `payload`: Die codierten binären Sprachdaten, die in Text umgesetzt werden sollen.
- `content_type`: Der MIME-Typ der Sprachdaten.
- `encoding`: Die Codierung der binären Sprachdaten.
- `continuous`: Gibt an, ob mehrere Endergebnisse, die durch lange Pausen voneinander getrennte aufeinanderfolgende Phrasen darstellen, zurückgegeben werden.
- `inactivity_timeout`: Die Zeit in Sekunden, nach deren Ablauf die Verbindung geschlossen wird, wenn in den übertragenen Sprachdaten nur Stille festgestellt wird.
- `interim_results`: Gibt an, ob der Service Zwischenergebnisse zurückgeben soll.
- `keywords`: Eine Liste der Schlüsselwörter, die in den Sprachdaten erkannt werden sollen.
- `keywords_threshold`: Ein Übereinstimmungswert, der die Untergrenze für die Erkennung eines Schlüsselworts darstellt.
- `max_alternatives`: Die maximale Anzahl alternativer Aufzeichnungen, die zurückgegeben werden sollen.
- `model`: Die Kennung des Modells für die Erkennungsanforderung.
- `timestamps`: Gibt an, ob für jedes Wort Laufzeitkorrekturen (Time Alignment) zurückgegeben werden.
- `watson-token`: Gibt alternativ zu Serviceberechtigungsnachweisen ein Authentifizierungstoken für den Service an.
- `word_alternatives_threshold`: Ein Übereinstimmungswert, der die Untergrenze für die Angabe einer Hypothese als mögliche Wortalternative darstellt.
- `word_confidence`: Gibt an, ob für jedes Wort ein Übereinstimmungswert im Bereich von 0 bis 1 zurückgegeben wird.
- `X-Watson-Learning-Opt-Out`: Gibt an, ob die Datenerfassung für den Aufruf abgelehnt wird.
 

- Rufen Sie die Aktion `speechToText` in Ihrer Paketbindung auf, um die codierten Sprachdaten umzusetzen.

  ```
  wsk action invoke myWatsonSpeechToText/speechToText --blocking --result --param payload <base64 encoding of a .wav file> --param content_type 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```
  {
    "data": "Hello Watson"
  }
  ```
  {: screen}
 
 
## Message Hub-Paket verwenden
{: #openwhisk_catalog_message_hub}

Mit diesem Paket können Sie Auslöser erstellen, die reagieren, wenn Nachrichten an eine [Message Hub](https://developer.ibm.com/messaging/message-hub/)-Serviceinstanz in Bluemix gesendet werden.

### Für eine Message Hub-Instanz empfangsbereiten Auslöser erstellen
{: #openwhisk_catalog_message_hub_trigger}
Um einen Auslöser zu erstellen, der reagiert, wenn Nachrichten an eine Message Hub-Instanz gesendet werden, müssen Sie den Feed `messaging/messageHubFeed` verwenden. Dieser Feed unterstützt die folgenden Parameter:

|Name|Typ|Beschreibung|
|---|---|---|
|kafka_brokers_sasl|JSON-Array aus Zeichenfolgen|Dieser Parameter ist ein Array aus Zeichenfolgen im Format `<Host>:<Port>`, die die Broker in Ihrer Message Hub-Instanz umfassen.|
|user|Zeichenfolge|Ihr Message Hub-Benutzername|
|password|Zeichenfolge|Ihr Message Hub-Kennwort|
|topic|Zeichenfolge|Das Thema, in dem der Auslöser empfangsbereit sein soll|
|kafka_admin_url|URL-Zeichenfolge|Die URL der Message Hub-REST-Schnittstelle für Administratoren|
|api_key|Zeichenfolge|Ihr Message Hub-API-Schlüssel|
|isJSONData|Boolesch (optional: Standard=false)|Wenn diese Option auf `true` festgelegt ist, versucht der Feed, Nachrichteninhalte als JSON zu analysieren, bevor sie als Nutzdaten für den Auslöser übergeben werden.|

Diese Parameterliste kann zwar abschreckend wirken, jedoch können die Parameter automatisch mit dem CLI-Befehl zum Aktualisieren des Pakets für Sie festgelegt werden:

1. Erstellen Sie eine Instanz des Message Hub-Service unter Ihrer aktuellen Organisation und dem aktuellen Bereich, die bzw. den Sie für OpenWhisk verwenden.

2. Stellen Sie sicher, dass das zu überwachende Thema bereits in Message Hub vorhanden ist, oder erstellen Sie ein neues Thema, das auf Nachrichten überwacht werden soll. Beispiel: `mytopic`.

2. Aktualisieren Sie die Pakete in Ihrem Namensbereich. Die Aktualisierung erstellt automatisch eine Paketbindung für die Message Hub-Serviceinstanz, die Sie erstellt haben.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Message_Hub_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1 private
  ```
  {: screen}

  Ihre Paketbindung enthält nun die Ihrer Message Hub-Instanz zugeordneten Berechtigungsnachweise.

3. Nun müssen Sie nur noch einen Auslöser erstellen, der angewendet werden soll, wenn neue Nachrichten an Ihre Message Hub-Instanz gesendet werden.

  ```
  wsk trigger create MyMessageHubTrigger -f /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1/messageHubFeed -p topic mytopic
  ```
  {: pre}

### Message Hub-Paket außerhalb von Bluemix einrichten

Wenn Sie OpenWhisk nicht in Bluemix verwenden oder wenn Sie Message Hub außerhalb von Bluemix einrichten möchten, müssen Sie manuell eine Paketbindung für Ihren Message Hub-Service erstellen. Dazu benötigen Sie die Berechtigungsnachweise für den Message Hub-Service und die Verbindungsinformationen.

- Erstellen Sie eine Paketbindung, die für Ihren Message Hub-Service konfiguriert ist.

  ```
  wsk trigger create MyMessageHubTrigger -f /whisk.system/messaging/messageHubFeed -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p topic mytopic -p user <Message Hub-Benutzer> -p password <Message Hub-Kennwort> -p kafka_admin_url https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443 -p api_key <eigener API-Schlüssel>
  ```
  {: pre}

### Nachrichten in einer Message Hub-Instanz überwachen
{: #openwhisk_catalog_message_hub_listen}
Nach dem Erstellen eines Auslösers überwacht das System das angegebene Thema in Ihrem Messaging-Service. Wenn neue Nachrichten gesendet werden, wird der Auslöser angewendet.

Die Nutzdaten dieses Auslösers enthalten das Feld `messages`. Dabei handelt es sich um ein Array aus Nachrichten, die seit der letzten Anwendung des Auslösers gesendet wurden. Jedes Nachrichtenobjekt im Array enthält die folgenden Felder:
- topic
- partition
- offset
- key
- value

In Bezug auf Kafka sollten diese Felder selbstverständlich sein. `value` erfordert jedoch besondere Aufmerksamkeit. Wenn der Parameter `isJSONData` bei der Erstellung des Auslösers auf `false` festgelegt (oder überhaupt nicht festgelegt) wurde, enthält das Feld `value` den Rohwert der gesendeten Nachricht. Wenn `isJSONData` bei der Erstellung des Auslösers jedoch auf `true` festgelegt wurde, versucht das System, diesen Wert möglichst als JSON-Objekt zu analysieren. Wenn die Analyse erfolgreich war, ergibt sich aus `value` in den Nutzdaten des Auslösers das entsprechende JSON-Objekt.

Beispiel: Wenn eine Nachricht mit dem Inhalt `{"title": "Some string", "amount": 5, "isAwesome": true}` gesendet wird und dabei `isJSONData` auf `true` festgelegt ist, sehen die Nutzdaten für den Auslöser möglicherweise wie folgt aus:

```
{
  "messages": [
      {
        "partition": 0,
        "key": null,
        "offset": 421760,
        "topic": "mytopic",
        "value": {
            "amount": 5,
            "isAwesome": true,
            "title": "Some string"
        }
      }
  ]
}
```

Wird jedoch derselbe Nachrichteninhalt gesendet, wenn `isJSONData` auf `false` festgelegt ist, sehen die Nutzdaten für den Auslöser wie folgt aus:

```
{
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421761,
      "topic": "mytopic",
      "value": "{\"title\": \"Some string\", \"amount\": 5, \"isAwesome\": true}"
    }
  ]
}
```

### Nachrichten werden stapelweise verarbeitet
Die Nutzdaten für den Auslöser enthalten ein Array aus Nachrichten. Das bedeutet, dass der Feed versucht, für die gesendeten Nachrichten mit einer Stapeloperation eine einzige Anwendung des Auslösers herbeizuführen, wenn sehr schnell Nachrichten in Ihrem Messaging-System erstellt werden. Dadurch können die Nachrichten schneller und effizienter an Ihren Auslöser gesendet werden.

Beachten Sie beim Codieren von Aktionen, die von Ihrem Auslöser gestartet werden, dass die Anzahl der Nachrichten in den Nutzdaten eigentlich nicht begrenzt ist, aber immer größer als 0 ist.


## Slack-Paket verwenden
{: #openwhisk_catalog_slack}

Das Paket `/whisk.system/slack` bietet eine komfortable Methode zur Verwendung der [Slack-APIs](https://api.slack.com/).

Das Paket enthält die folgenden Aktionen:

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/slack` | Paket | url, channel, username | Interaktion mit der Slack-API |
| `/whisk.system/slack/post` | Aktion | text, url, channel, username | Senden einer Nachricht an einen Slack-Kanal |

Es wird empfohlen, eine Paketbindung mit den Werten `username`, `url` und `channel` zu erstellen. Mit der Bindung brauchen Sie die Werte nicht jedes Mal anzugeben, wenn Sie die Aktion im Paket aufrufen.

### Nachricht an einen Slack-Kanal senden
{: #openwhisk_catalog_slack_post}

Die Aktion `/whisk.system/slack/post` sendet eine Nachricht an einen angegebenen Slack-Kanal. Die folgenden Parameter sind verfügbar:

- `url`: Die URL für den Slack-Web-Hook.
- `channel`: Der Slack-Kanal, an den die Nachricht zu senden ist.
- `username`: Der Name, unter dem die Nachricht gesendet werden soll.
- `text`: Ein zu sendender Nachrichtentext.
- `token`: (optional) Ein Slack-[Zugriffstoken](https://api.slack.com/tokens). Weitere Informationen zur Verwendung des Slack-Zugriffstokens finden Sie [unten](./openwhisk_catalog.html#openwhisk_catalog_slack_token).

Das folgende Beispiel zeigt die Konfiguration von Slack, die Erstellung einer Paketbindung und das Senden einer Nachricht an einen Kanal.

1. Konfigurieren Sie für Ihr Team einen [eingehenden Web-Hook](https://api.slack.com/incoming-webhooks) für Slack.

  Nach der Konfiguration von Slack erhalten Sie eine Web-Hook-URL, die ungefähr wie folgt aussieht: `https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`. Sie benötigen diese im nächsten Schritt.

2. Erstellen Sie eine Paketbindung mit Ihren Slack-Berechtigungsnachweisen, mit dem Kanal, an den gesendet werden soll, sowie mit dem Benutzernamen, unter dem gesendet werden soll.

  ```
  wsk package bind /whisk.system/slack mySlack --param url "https://hooks.slack.com/services/..." --param username Bob --param channel "#MySlackChannel"
  ```
  {: pre}

3. Rufen Sie die Aktion `post` in Ihrer Paketbindung auf, um eine Nachricht an Ihren Slack-Kanal zu senden.

  ```
  wsk action invoke mySlack/post --blocking --result --param text "Hello from OpenWhisk!"
  ```
  {: pre}

### Slack-Token-basierte API verwenden
{: #openwhisk_catalog_slack_token}

Sie können auf Wunsch auch die Slack-Token-basierte API statt der Web-Hook-API verwenden. Übergeben Sie in einem solchen Fall in einem `Token` die Parameter, die Ihr Slack-[Zugriffstoken](https://api.slack.com/tokens) enthalten. Sie können dann eine beliebige [Slack-API-Methode](https://api.slack.com/methods) als Parameter `url` verwenden. Um beispielsweise eine Nachricht zu senden, verwenden Sie den Parameterwert `url` von [slack.postMessage](https://api.slack.com/methods/chat.postMessage).

## GitHub-Paket verwenden
{: #openwhisk_catalog_github}

Das Paket `/whisk.system/github` bietet eine komfortable Methode zur Verwendung der [GitHub-APIs](https://developer.github.com/).

Das Paket enthält den folgenden Feed:

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/github` | Paket | username, repository, accessToken | Interaktion mit der GitHub-API |
| `/whisk.system/github/webhook` | Feed | events, username, repository, accessToken | Aktivieren von Auslöserereignissen für GitHub-Aktivitäten |

Es wird empfohlen, eine Paketbindung mit den Werten `username`, `repository` und `accessToken` zu erstellen.  Mit der Bindung brauchen Sie die Werte nicht jedes Mal anzugeben, wenn Sie den Feed im Paket verwenden.

### Auslöserereignis für GitHub-Aktivität aktivieren
{: #openwhisk_catalog_github_fire}

Der Feed `/whisk.system/github/webhook` konfiguriert einen Service so, dass ein Auslöser aktiviert wird, wenn eine Aktivität in einem angegebenen GitHub-Repository stattfindet. Die folgenden Parameter sind verfügbar:

- `username`: Der Benutzername für das GitHub-Repository.
- `repository`: Das GitHub-Repository.
- `accessToken`: Ihr persönliches GitHub-Zugriffstoken. Wenn Sie Ihr [Token erstellen](https://github.com/settings/tokens), stellen Sie sicher, dass Sie die Geltungsbereiche 'repo:status' und 'public_repo' auswählen. Stellen Sie außerdem sicher, dass noch keine Web-Hooks für Ihr Repository definiert sind.
- `events`: Der interessierende [GitHub-Ereignistyp](https://developer.github.com/v3/activity/events/types/).

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

Ein Commit für ein Github-Repository mithilfe von `git push` führt dazu, dass der Auslöser durch den Web-Hook ausgelöst wird. Falls eine Regel zutrifft, die mit dem Auslöser übereinstimmt, wird die zugeordnete Aktion aufgerufen.
Von der Aktion werden die Nutzdaten für den GitHub-Web-Hook als Eingabeparameter empfangen. Jedes GitHub-Web-Hook-Ereignis weist ein ähnliches JSON-Schema und ein eindeutiges Nutzdatenobjekt auf, das vom jeweiligen Ereignistyp abhängt.
Weitere Informationen zum Nutzdateninhalt finden Sie in der API-Dokumentation unter [GitHub-Ereignisse und -Nutzdaten](https://developer.github.com/v3/activity/events/types/).


## Push-Paket verwenden
{: #openwhisk_catalog_pushnotifications}

Das Paket `/whisk.system/pushnotifications` ermöglicht Ihnen die Arbeit mit einem Push-Service. 

Das Paket enthält die folgende Aktion und den folgenden Feed:

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/pushnotifications` | Paket | appId, appSecret  | Arbeit mit Push-Service |
| `/whisk.system/pushnotifications/sendMessage` | Aktion | text, url, deviceIds, platforms, tagNames, apnsBadge, apnsCategory, apnsActionKeyTitle, apnsSound, apnsPayload, apnsType, gcmCollapseKey, gcmDelayWhileIdle, gcmPayload, gcmPriority, gcmSound, gcmTimeToLive | Push-Benachrichtigung an mindestens ein angegebenes Gerät senden |
| `/whisk.system/pushnotifications/webhook` | Feed | events | Löst Auslöserereignisse für Geräteaktivitäten (Registrierung des Geräts, Rücknahme der Registrierung, Abonnement für Gerät, Beendigung des Abonnements) für den Push-Service aus |
Es wird empfohlen, eine Paketbindung mit den Werten `appId` und `appSecret` zu erstellen. Auf diese Weise brauchen Sie diese Berechtigungsnachweise nicht jedes Mal anzugeben, wenn Sie die Aktionen im Paket aufrufen.

### Push-Paketbindung erstellen
{: #openwhisk_catalog_pushnotifications_create}

Bei der Erstellung einer Paketbindung für Push-Benachrichtigungen müssen Sie die folgenden Parameter angeben.

-  `appId`: Die GUID für die Bluemix-App.
-  `appSecret`: Der geheime Schlüssel des Bluemix Push-Benachrichtigungsservice.

Das folgende Beispiel zeigt die Erstellung einer Paketbindung.

1. Erstellen Sie eine Bluemix-Anwendung in einem [Bluemix-Dashboard](http://console.ng.bluemix.net).

2. Initialisieren Sie den Push-Benachrichtigungsservice und binden Sie den Service an die Bluemix-Anwendung.

3. Konfigurieren Sie die [Push Notifications-Anwendung](https://console.ng.bluemix.net/docs/services/mobilepush/index.html).

  Notieren Sie sich die Werte für `App GUID` und `App Secret` der von Ihnen erstellten Bluemix-App.


4. Erstellen Sie eine Paketbindung mit den `/whisk.system/pushnotifications`.

  ```
  wsk package bind /whisk.system/pushnotifications myPush -p appId myAppID -p appSecret myAppSecret
  ```
  {: pre}

5. Prüfen Sie, ob die Paketbindung vorhanden ist.

  ```
  wsk package list
  ```
  {: pre}

  ```
  packages
  /myNamespace/myPush private binding
  ```
  {: screen}

### Push-Benachrichtigungen senden
{: #openwhisk_catalog_pushnotifications_send}

Von der Aktion `/whisk.system/pushnotifications/sendMessage` werden Push-Benachrichtigungen an registrierte Geräte gesendet. Die folgenden Parameter sind verfügbar:
- `text`: Die Benachrichtigung, die dem Benutzer angezeigt wird. Beispiel: `-p text "Hallo, OpenWhisk sendet eine Benachrichtigung"`.
- `url`: Eine optionale URL, die zusammen mit einem Alert gesendet werden kann. Beispiel: `-p url "https:\\www.w3.ibm.com"`.
- `deviceIds` Die Liste der angegebenen Geräte. Beispiel: `-p deviceIds "[\"deviceID1\"]"`.
- `platforms` Zum Senden einer Benachrichtigung an die Geräte der angegebenen Plattformen. 'A' für Apple- (iOS) Geräte und 'G' für Google- (Android) Geräte. Beispiel: `-p platforms "[\"A\"]"`.
- `tagNames` Zum Senden einer Benachrichtigung an die Geräte, die einen dieser Tags subskribiert haben. Beispiel: `-p tagNames "[\"tag1\"]" `.
- `gcmPayload`: Angepasste JSON-Nutzdaten, die als Bestandteil einer Benachrichtigung gesendet werden. Beispiel: `-p gcmPayload "{\"hi\":\"hello\"}"`
- `gcmSound`: Die Audiodatei (auf einem Gerät), die abgespielt werden soll, wenn die Benachrichtigung vom Gerät empfangen wird.
- `gcmCollapseKey`: Dieser Parameter gibt eine Gruppe aus Nachrichten an.
- `gcmDelayWhileIdle`: Wenn für diesen Parameter der Wert 'true' festgelegt wird, gibt dies an, dass die Nachricht erst gesendet werden darf, wenn das Gerät aktiv wird.
- `gcmPriority`: Legt die Priorität der Nachricht fest.
- `gcmTimeToLive`: Dieser Parameter gibt an, wie lange (in Sekunden) die Nachricht im GCM-Speicher aufbewahrt wird, wenn das Gerät offline ist.
- `apnsBadge`: Die Nummer, die als Markierung des Anwendungssymbols angezeigt werden soll.
- `apnsCategory`: Die Kategoriekennung, die für interaktive Push-Benachrichtigungen verwendet werden soll.
- `apnsIosActionKey`: Der Titel für den Aktionsschlüssel.
- `apnsPayload`: Angepasste JSON-Nutzdaten, die als Bestandteil einer Benachrichtigung gesendet werden.
- `apnsType`: ['DEFAULT', 'MIXED', 'SILENT'].
- `apnsSound`: Der Name der Audiodatei im Anwendungsbundle. Die Tonsignale dieser Datei werden als Alert abgespielt.

Nachfolgend ein Beispiel für das Senden einer Push-Benachrichtigung von einem Push Notifications-Paket.

1. Senden Sie die Push-Benachrichtigung mithilfe der Aktion `sendMessage` in der Paketbindung ab, die Sie zuvor erstellt haben. Stellen Sie sicher, dass Sie `/myNamespace/myPush` durch Ihren Paketnamen ersetzen.

  ```
  wsk action invoke /myNamespace/myPush/sendMessage --blocking --result  -p url https://example.com -p text "this is my message"  -p sound soundFileName -p deviceIds "[\"T1\",\"T2\"]"
  ```
  {: pre}

  ```
  {
  "result": {
  "pushResponse": "{"messageId":"11111H","message":{"message":{"alert":"this is my message","url":"http.google.com"},"settings":{"apns":{"sound":"default"},"gcm":{"sound":"default"},"target":{"deviceIds":["T1","T2"]}}}"
  },
      "status": "success",
      "success": true
  }
  ```
  {: screen}

### Auslöserereignis für Push-Aktivität aktivieren
{: #openwhisk_catalog_pushnotifications_fire}

Von `/whisk.system/pushnotifications/webhook` wird der Push-Service so konfiguriert, dass ein Auslöser aktiviert wird, wenn eine Gerätaktivität wie eine Geräteregistrierung bzw. die Rücknahme einer Gerätregistrierung oder ein Abonnement bzw. das Beenden eines Abonnements für eine angegebene Anwendung auftritt.

Die folgenden Parameter sind verfügbar:

- `appId:` Die GUID für die Bluemix-App.
- `appSecret:` Der geheime Schlüssel des Push Notifications-Service von Bluemix.
- `events:` Unterstützte Ereignisse sind `onDeviceRegister`, `onDeviceUnregister`, `onDeviceUpdate`, `onSubscribe` und `onUnsubscribe`. Wenn Sie bei allen Ereignissen benachrichtigt werden möchten, verwenden Sie das Platzhalterzeichen `*`.

Das folgende Beispiel die Erstellung eines Auslösers, der jedes Mal aktiviert wird, wenn ein neues Gerät mit der Push Notifications-Serviceanwendung registriert wird.

1. Erstellen Sie eine Paketbindung, die für den Push Notifications-Service (mit Werten für 'appId' und 'appSecret') konfiguriert ist.

  ```
  wsk package bind /whisk.system/pushnotifications myNewDeviceFeed --param appID myapp --param appSecret myAppSecret --param events onDeviceRegister
  ```
  {: pre}

2. Erstellen Sie mithilfe des Feeds `myPush/webhook` einen Auslöser für den Ereignistyp `onDeviceRegister` des Push Notifications-Service.

  ```
  wsk trigger create myPushTrigger --feed myPush/webhook --param events onDeviceRegister
  ```
  {: pre}
