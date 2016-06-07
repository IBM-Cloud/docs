---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}}-Pakete verwenden und erstellen
{: #openwhisk_packages}
*Letzte Aktualisierung: 28. März 2016*

In {{site.data.keyword.openwhisk}} können Sie Pakete verwenden, um eine Gruppe zusammengehöriger Aktionen zu bündeln und diese zur gemeinsamen Nutzung mit anderen Benutzern bereitzustellen.

Ein Paket kann *Aktionen* und *Feeds* enthalten.
- Eine Aktion ist ein Stück Code, das in {{site.data.keyword.openwhisk_short}} ausgeführt wird. Zum Beispiel enthält das Cloudant-Paket Aktionen zum Lesen und Schreiben von Datensätzen in einer Cloudant-Datenbank.
- Ein Feed dient zum Konfigurieren einer externen Ereignisquelle zum Aktivieren von Auslöserereignissen. Zum Beispiel enthält das Paket für Alarme einen Feed, der einen Auslöser mit einer angegebenen Häufigkeit auslösen kann.

Jede {{site.data.keyword.openwhisk_short}}-Entität, einschließlich Paketen, gehört in einen *Namensbereich*. Der vollständig qualifizierte Name einer Entität setzt sich dementsprechend wie folgt zusammen: `/Namensbereichsname[/Paketname]/Entitätsname`. Weitere Informationen finden Sie unter [Benennungsrichtlinien](./openwhisk_reference.html#openwhisk_entities).

In den folgenden Abschnitten wird beschrieben, wie Pakete durchsucht und die in ihnen enthaltenen Auslöser (Trigger) und Feeds verwendet werden. Wenn Sie daran interessiert sind, eigene Pakete für den Katalog beizutragen, lesen Sie außerdem die Abschnitte zur Erstellung und gemeinsamen Nutzung von Paketen.

## Pakete durchsuchen
{: #openwhisk_packagedisplay}

In {{site.data.keyword.openwhisk_short}} sind verschiedene Pakete registriert. Sie können eine Liste der Pakete in einem Namensbereich abrufen, die Entitäten in einem Paket auflisten und eine Beschreibung der einzelnen Entitäten in einem Paket abrufen.

1. Rufen Sie eine Liste der Pakete im Namensbereich `/whisk.system` ab.

  ```
  wsk package list /whisk.system
  ```
  {: pre}
  ```
  packages
  /whisk.system/alarms                                              shared
  /whisk.system/cloudant                                            shared
  /whisk.system/github                                              shared
  /whisk.system/samples                                             shared
  /whisk.system/slack                                               shared
  /whisk.system/util                                                shared
  /whisk.system/watson                                              shared
  /whisk.system/weather                                             shared
  ```
  {: screen}

2. Rufen Sie eine Liste der Entitäten im Paket `/whisk.system/cloudant` ab.

  ```
  wsk package get --summary /whisk.system/cloudant
  ```
  {: pre}
  ```
  package /whisk.system/cloudant: Cloudant database service
     (params: {{site.data.keyword.Bluemix_notm}}ServiceName host username password dbname includeDoc overwrite)
   action /whisk.system/cloudant/read: Read document from database
   action /whisk.system/cloudant/write: Write document to database
   feed   /whisk.system/cloudant/changes: Database change feed
  ```
  {: screen}

  Diese Ausgabe zeigt, dass das Cloudant-Paket zwei Aktionen, `read` und `write`, sowie einen Auslöserfeed mit dem Namen `changes` bereitstellt. Der Feed `changes` bewirkt, dass Auslöser ausgelöst werden, wenn Dokumente der angegebenen Cloudant-Datenbank hinzugefügt werden.

  Das Cloudant-Paket definiert außerdem die Parameter `username`, `password`, `host` und `port`. Diese Parameter müssen für die Aktionen und Feeds angegeben werden, damit diese aussagekräftig sind. Durch die Parameter können Aktionen zum Beispiel auf einem bestimmten Cloudant-Konto operieren.

3. Rufen Sie eine Beschreibung der Aktion `/whisk.system/cloudant/read` ab.

  ```
  wsk action get --summary /whisk.system/cloudant/read
  ```
  {: pre}
  ```
  action /whisk.system/cloudant/read: Read document from database
     (params: dbname includeDoc id)
  ```
  {: screen}

  Diese Ausgabe zeigt, dass die Cloudant-Aktion `read` drei Parameter erfordert, zu denen die Datenbank und die abzurufende Dokument-ID gehören.


## Aktionen in einem Paket aufrufen
{: #openwhisk_package_invoke}

Sie können Aktionen in einem Paket ebenso wie bei anderen Aktionen aufrufen. Die nächsten Schritte zeigen, wie die Aktion `greeting` im Paket `/whisk.system/samples` mit verschiedenen Parametern aufgerufen wird.

1. Rufen Sie eine Beschreibung der Aktion `/whisk.system/samples/greeting` ab.

  ```
  wsk action get --summary /whisk.system/samples/greeting
  ```
  {: pre}
  ```
  action /whisk.system/samples/greeting: Print a friendly greeting
     (params: name place)
  ```
  {: screen}

  Beachten Sie, dass die Aktion `greeting` zwei Parameter hat: `name` und `place`.

2. Rufen Sie die Aktion ohne Parameter auf.

  ```
  wsk action invoke --blocking --result /whisk.system/samples/greeting
  ```
  {: pre}
  ```
  {
      "payload": "Hello, stranger from somewhere!"
  }
  ```
  {: screen}

  Die Ausgabe ist eine generische Nachricht, da keine Parameter angegeben wurden.

3. Rufen Sie die Aktion mit Parametern auf.

  ```
  wsk action invoke --blocking --result /whisk.system/samples/greeting --param name Mork --param place Ork
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Mork from Ork!"
  }
  ```
  {: screen}

  Beachten Sie, dass die Ausgabe die Parameter `name` und `place` verwendet, die an die Aktion übergeben wurden.


## Paketbindungen erstellen und verwenden
{: #openwhisk_package_bind}

Sie können die Entitäten in einem Paket immer direkt verwenden, was jedoch bedeuten kann, dass Sie jedes Mal dieselben Parameter an die Aktion übergeben. Sie können dies vermeiden, indem Sie eine Bindung an ein Paket erstellen und Standardparameter angeben. Diese Parameter werden von den Aktionen im Paket übernommen.

Beispiel: Im Paket `/whisk.system/cloudant` können Sie Standwerte für die Parameter `username`, `password` und `dbname` in einer Paketbindung festlegen, sodass diese Werte automatisch an alle Aktionen in dem Paket übergeben werden.

In dem folgenden einfachen Beispiel erstellen Sie eine Bindung an das Paket `/whisk.system/samples`.

1. Erstellen Sie eine Bindung an das Paket `/whisk.system/samples` und legen Sie einen Standardwert für den Parameter `place` fest.

  ```
  wsk package bind /whisk.system/samples valhallaSamples --param place Valhalla
  ```
  {: pre}
  ```
  ok: created binding valhallaSamples
  ```
  {: screen}

2. Rufen Sie eine Beschreibung der Paketbindung ab.

  ```
  wsk package get --summary valhallaSamples
  ```
  {: pre}
  ```
  package /myNamespace/valhallaSamples
   action /myNamespace/valhallaSamples/greeting: Print a friendly greeting
   action /myNamespace/valhallaSamples/wordCount: Count words in a string
   action /myNamespace/valhallaSamples/helloWorld: Print to the console
   action /myNamespace/valhallaSamples/echo: Returns the input arguments, unchanged
  ```
  {: screen}

  Beachten Sie, dass alle Aktionen im Paket `/whisk.system/samples` in der Paketbindung `valhallaSamples` verfügbar sind.

3. Rufen Sie eine Aktion in der Paketbindung auf.

  ```
  wsk action invoke --blocking --result valhallaSamples/greeting --param name Odin
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Odin from Valhalla!"
  }
  ```
  {: screen}

  Beachten Sie im Ergebnis, dass die Aktion den Parameter `place` übernimmt, den Sie beim Erstellen der Paketbindung `valhallaSamples` festgelegt haben.

4. Rufen Sie eine Aktion auf und überschreiben Sie den Standardparameterwert.

  ```
  wsk action invoke --blocking --result valhallaSamples/greeting --param name Odin --param place Asgard
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Odin from Asgard!"
  }
  ```
  {: screen}

  Beachten Sie, dass der Wert des Parameters `place`, der im Aktionsaufruf angegeben wird, den Standardwert überschreibt, der in der Paketbindung `valhallaSamples` festgelegt wurde.


## Auslöserfeed erstellen und verwenden
{: #openwhisk_package_trigger}

Feeds sind eine bequeme Methode zum Konfigurieren einer externen Ereignisquelle zum Auslösen von Ereignissen für einen {{site.data.keyword.openwhisk_short}}-Auslöser. Das folgende Beispiel zeigt, wie ein Feed im Paket für Alarme verwendet wird, um einen Auslöser jede Sekunde zu aktivieren und eine Regel zu verwenden, um jede Sekunde eine Aktion aufzurufen.

1. Rufen Sie eine Beschreibung des Feeds im Paket `/whisk.system/alarms` ab.

  ```
  wsk package get --summary /whisk.system/alarms
  ```
  {: pre}
  ```
  package /whisk.system/alarms
   feed   /whisk.system/alarms/alarm
  ```
  {: screen}

  ```
  wsk action get --summary /whisk.system/alarms/alarm
  ```
  {: pre}
  ```
  action /whisk.system/alarms/alarm: Fire trigger when alarm occurs
     (params: cron trigger_payload)
  ```
  {: screen}

  Der Feed `/whisk.system/alarms/alarm` hat zwei Parameter:
  - `cron`: Eine crontab-Angabe für den Zeitpunkt, wann der Auslöser zu aktivieren ist.
  - `trigger_payload`: Der Payload-Parameterwert, der in jedem Auslöserereignis festgelegt werden soll.

2. Erstellen Sie einen Auslöser, der alle acht Sekunden aktiviert wird.

  ```
  wsk trigger create everyEightSeconds --feed /whisk.system/alarms/alarm -p cron '*/8 * * * * *' -p trigger_payload '{"name":"Mork", "place":"Ork"}'
  ```
  {: pre}
  ```
  ok: created trigger feed everyEightSeconds
  ```
  {: screen}

3. Erstellen Sie eine Datei 'hello.js' mit dem folgenden Aktionscode.

  ```
  function main(params) {
      return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

4. Stellen Sie sicher, dass die Aktion vorhanden ist.

  ```
  wsk action update hello hello.js
  ```
  {: pre}

5. Erstellen Sie eine Regel, die die Aktion `hello` jedes Mal aufruft, wenn der Auslöser `everyEightSeconds` aktiviert wird.

  ```
  wsk rule create --enable myRule everyEightSeconds hello
  ```
  {: pre}
  ```
  ok: created rule myRule
  ok: rule myRule is activating
  ```
  {: screen}

6. Prüfen Sie, ob die Aktion aufgerufen wird, indem Sie die Aktivierungsprotokolle durch Polling abfragen.

  ```
  wsk activation poll
  ```
  {: pre}

  Es sollten Aktivierungen alle acht Sekunden für den Auslöser, die Regel und die Aktion angezeigt werden. Die Aktion empfängt die Parameter `{"name":"Mork", "place":"Ork"}` bei jedem Aufruf.


## Paket erstellen
{: #openwhisk_packages_create}

Ein Paket dient dazu, eine Gruppe von zusammengehörigen Aktionen und Feed zu organisieren.
Es bietet außerdem die Möglichkeit, Parameter über alle Entitäten in dem Paket hinweg gemeinsam zu nutzen.

Versuchen Sie das folgende Beispiel, um ein angepasstes Paket mit einer einfachen Aktion zu erstellen:

1. Erstellen Sie ein Paket mit dem Namen "custom".

  ```
  wsk package create custom
  ```
  {: pre}
  ```
  ok: created package custom
  ```
  {: screen}

2. Rufen Sie eine Zusammenfassung des Pakets ab.

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /myNamespace/custom
  ```
  {: screen}

  Beachten Sie, dass das Paket leer ist.

3. Erstellen Sie eine Datei mit dem Namen `identity.js`, die den folgenden Aktionscode enthält. Diese Aktion gibt alle Eingabeparameter zurück.

  ```
  function main(args) { return args; }
  ```
  {: codeblock}

4. Erstellen Sie eine Aktion `identity` im Paket `custom`.

  ```
  wsk action create custom/identity identity.js
  ```
  {: pre}
  ```
  ok: created action custom/identity
  ```
  {: screen}

  Zum Erstellen einer Aktion in einem Paket müssen Sie dem Aktionsnamen einen Paketnamen als Präfix voranstellen. Eine Verschachtelung von Paketen ist nicht zulässig. Ein Paket kann nur Aktionen, jedoch kein anderes Paket enthalten.

5. Rufen Sie erneut eine Zusammenfassung des Pakets ab.

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /myNamespace/custom
   action /myNamespace/custom/identity
  ```
  {: screen}

  Die Aktion `custom/identity` wird jetzt in Ihrem Namensbereich angezeigt.

6. Rufen Sie die Aktion in dem Paket auf.

  ```
  wsk action invoke --blocking --result custom/identity
  ```
  {: pre}
  ```
  {}
  ```
  {: screen}


Sie können Standardparameter für alle Entitäten in einem Paket festlegen. Dazu legen Sie Parameter auf Paketebene fest, die von allen Aktionen in dem Paket übernommen werden. Versuchen Sie das folgende Beispiel, um zu erfahren, wie dies funktioniert:

1. Aktualisieren Sie das Paket `custom` mit zwei Parametern: `city` und `country`.

  ```
  wsk package update custom --param city Austin --param country USA
  ```
  {: pre}
  ```
  ok: updated package custom
  ```
  {: screen}

2. Zeigen Sie die Parameter in dem Paket und in der Aktion an und beachten Sie, wie die Aktion `identity` in dem Paket die Parameter aus dem Paket übernimmt.

  ```
  wsk package get custom parameters
  ```
  {: pre}
  ```
  ok: got package custom, projecting parameters
  [
      {
          "key": "city",
          "value": "Austin"
      },
      {
          "key": "country",
          "value": "USA"
      }
  ]
  ```
  {: screen}

  ```
  wsk action get custom/identity parameters
  ```
  {: pre}
  ```
  ok: got action custom/identity, projecting parameters
  [
      {
          "key": "city",
          "value": "Austin"
      },
      {
          "key": "country",
          "value": "USA"
      }
  ]
  ```
  {: screen}

3. Rufen Sie die Aktion 'identity' ohne Parameter auf, um zu prüfen, ob die Aktion die Parameter tatsächlich übernimmt.

  ```
  wsk action invoke --blocking --result custom/identity
  ```
  {: pre}
  ```
  {
      "city": "Austin",
      "country": "USA"
  }
  ```
  {: screen}

4. Rufen Sie die Aktion 'identity' mit Parametern auf. Die Aufrufparameter werden mit den Paketparametern gemischt, wobei die Aufrufparameter die Paketparameter überschreiben.

  ```
  wsk action invoke --blocking --result custom/identity --param city Dallas --param state Texas
  ```
  {: pre}
  ```
  {
      "city": "Dallas",
      "country": "USA",
      "state": "Texas"
  }
  ```
  {: screen}


## Paket gemeinsam nutzen
{: #openwhisk_packages_share}

Wenn die Aktionen und Feeds, die ein Paket bilden, auf Fehler geprüft und getestet wurden, kann das Paket zur gemeinsamen Nutzung durch alle {{site.data.keyword.openwhisk_short}}-Benutzer bereitgestellt werden. Durch die gemeinsame Nutzung haben Benutzer die Möglichkeit, das Paket zu binden, Aktionen in dem Paket aufzurufen sowie {{site.data.keyword.openwhisk_short}}-Regeln zu verfassen und Aktionsfolgen zu erstellen.

1. Stellen Sie das Paket zur gemeinsamen Nutzung durch alle Benutzer bereit:

  ```
  wsk package update custom --shared
  ```
  {: pre}
  ```
  ok: updated package custom
  ```
  {: screen}

2. Zeigen Sie die Eigenschaft `publish` des Pakets an, um zu prüfen, ob sie jetzt den Wert 'true' hat.

  ```
  wsk package get custom publish
  ```
  {: pre}
  ```
  ok: got package custom, projecting publish
  true
  ```
  {: screen}


Andere Benutzer können Ihr Paket `custom` jetzt verwenden, indem sie Bindungen an das Paket erstellen oder eine Aktion in dem Paket direkt aufrufen. Andere Benutzer müssen die vollständig qualifizierten Namen des Pakets kennen, um es binden zu können oder um Aktionen in dem Paket aufrufen zu können. Aktionen und Feed in einem gemeinsam genutzten Paket sind *öffentlich*. Wenn ein Paket privat ist, ist auch sein gesamter Inhalt privat.

1. Rufen Sie eine Beschreibung des Pakets ab, um die vollständig qualifizierten Namen des Pakets und der Aktion anzuzeigen.

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /myNamespace/custom
   action /myNamespace/custom/identity
  ```
  {: screen}

  Im obigen Beispiel wird der Namensbereich `myNamespace` verwendet und dieser Namensbereich ist in dem vollständig qualifizierten Namen enthalten.

