---

copyright:
  years: 2017
lastupdated: "2017-05-04"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# OpenWhisk-REST-APIs verwenden
{: #openwhisk_rest_api}

Nachdem Ihre OpenWhisk-Umgebung aktiviert ist, können Sie OpenWhisk mit den Web-Apps oder mobilen Apps mit REST-API-Aufrufen verwenden.

Weitere Informationen zu den APIs für Aktionen, Aktivierungen, Pakete, Regeln und Auslöser finden Sie in der [OpenWhisk-API-Dokumentation](http://petstore.swagger.io/?url=https://raw.githubusercontent.com/openwhisk/openwhisk/master/core/controller/src/main/resources/apiv1swagger.json).


Alle Funktionen im System stehen über eine REST-API zur Verfügung. Es gibt Sammlungs- und Entitätsendpunkte für Aktionen, Auslöser, Regeln, Pakete, Aktivierungen und Namensbereiche.

Die Sammlungsendpunkte lauten wie folgt:
- `https://{APIHOST}/api/v1/namespaces`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/actions`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/triggers`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/rules`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/packages`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/activations`

`{APIHOST}` ist der OpenWhisk-API-Hostname (z. B. openwhisk.ng.bluemix.net, 172.17.0.1, 192.168.99.100, 192.168.33.13 usw.).
Für `{namespace}` kann das Zeichen `_` verwendet werden, um den *Standardnamensbereich* des Benutzers anzugeben.

Sie können eine GET-Anforderung für die Sammlungsendpunkte ausführen, um eine Liste der Entitäten in der Sammlung abzurufen.

Für jeden Entitätstyp gibt es Entitätsendpunkte:
- `https://{APIHOST}/api/v1/namespaces/{namespace}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/actions/[{packageName}/]{actionName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/triggers/{triggerName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/rules/{ruleName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/packages/{packageName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/activations/{activationName}`

Die Endpunkte für Namensbereiche und Aktivierungen unterstützen nur GET-Anforderungen. Die Endpunkte für Aktionen, Auslöser, Regeln und Pakete unterstützen GET-, PUT- und DELETE-Anforderungen. Die Endpunkte für Aktionen, Auslöser und Regeln unterstützen auch POST-Anforderungen, die zum Aufrufen von Aktionen und Auslösern sowie zum Aktivieren und Inaktivieren von Regeln verwendet werden. 

Alle APIs sind mit der HTTP-Basisauthentifizierung geschützt. 
Sie können das Tool [wskadmin](../tools/admin/wskadmin) verwenden, um einen neuen Namensbereich und eine neue Authentifizierung zu generieren. Die durch einen Doppelpunkt voneinander getrennten Basic-Berechtigungsnachweise zur Authentifizierung befinden sich in der Eigenschaft `AUTH` in der `~/.wskprops`-Datei. 
Sie können diese Berechtigungsnachweise auch über die Befehlszeilenschnittstelle (CLI) abrufen, indem Sie `wsk property get --auth` ausführen.


Das folgende Beispiel zeigt, wie Sie mit dem Befehlstool [cURL](https://curl.haxx.se) eine Liste aller Pakete im Namensbereich `whisk.system` abrufen können:

```bash
curl -u USERNAME:PASSWORD https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/packages
```
{: pre}

```json
  [
  {
    "name": "slack",
    "binding": false,
    "publish": true,
    "annotations": [
      {
        "key": "description",
        "value": "Package that contains actions to interact with the Slack messaging service"
      }
    ],
    "version": "0.0.1",
    "namespace": "whisk.system"
  }
]
```

In diesem Beispiel wurde die Authentifizierung mithilfe des Flags `-u` übergeben; Sie können diesen Wert auch als Teil der URL als `https://$AUTH@{APIHOST}` übergeben.

Von der OpenWhisk-API werden Anforderung/Antwort-Aufrufe von Web-Clients unterstützt. Von OpenWhisk wird auf `OPTIONS`-Anforderungen mit CORS-Headern (CORS - Cross-Origin Resource Sharing) geantwortet. Derzeit sind alle Ursprünge zulässig (d. h. Access-Control-Allow-Origin ist "`*`") und Access-Control-Allow-Header sorgen für die Autorisierung und den Inhaltstyp.

**Achtung:** Da von OpenWhisk derzeit nur ein Schlüssel pro Namensbereich unterstützt wird, wird empfohlen, CORS nur für einfache Experimente und nicht darüber hinaus zu verwenden. Verwenden Sie [Webaktionen](webactions.md) oder das [API-Gateway](apigateway.md), um Ihre Aktionen der Öffentlichkeit zugänglich zu machen und nicht die OpenWhisk-Berechtigungsschlüssel für Clientanwendungen zu verwenden, für die CORS erforderlich ist.

## Ausführlichen CLI-Modus verwenden
{: #openwhisk_rest_api_cli_v}
Die OpenWhisk-Befehlszeilenschnittstelle (CLI) ist eine Schnittstelle zur OpenWhisk-REST-API.
Sie können die Befehlszeilenschnittstelle im ausführlichen Modus mit dem Flag `-v` ausführen. Dadurch werden alle Informationen zur HTTP-Anforderung und Antwort gedruckt.

Lassen Sie uns nun versuchen, den Wert des Namensbereichs für den aktuellen Benutzer abzurufen.
```
wsk namespace list -v
```
{: pre}
```
REQUEST:
[GET]	https://openwhisk.ng.bluemix.net/api/v1/namespaces
Req Headers
{
  "Authorization": [
    "Basic XXXYYYY"
  ]
}
RESPONSE:Got response with code 200
Resp Headers
{
  "Content-Type": [
    "application/json; charset=UTF-8"
  ]
}
Response body size is 28 bytes
Response body received:
["john@example.com_dev"]
```

Wie Sie sehen, stellen die gedruckten Informationen die Eigenschaften der HTTP-Anforderung bereit. Außerdem wird die HTTP-Methode `GET` mithilfe des BASIC-Berechtigungsheaders `Basic XXXYYYY` auf die URL `https://openwhisk.ng.bluemix.net/api/v1/namespaces` angewendet.
Beachten Sie, dass der Berechtigungswert die base64-codierte OpenWhisk-Berechtigungszeichenfolge ist.
Die Antwort weist den Inhaltstyp `application/json` auf.

## Aktionen
{: #openwhisk_rest_api_actions}
Zum Erstellen oder Aktualisieren einer Aktion senden Sie eine HTTP-Anforderung mit der Methode `PUT` für die Aktionssammlung. Verwenden Sie beispielsweise den folgenden Code, um eine Aktion des Typs `nodejs:6` mit dem Namen `hello` mithilfe des Inhalts einer einzelnen Datei zu erstellen:
```bash
curl -u $AUTH -d '{"namespace":"_","name":"hello","exec":{"kind":"nodejs:6","code":"function main(params) { return {payload:\"Hello \"+params.name}}"}}' -X PUT -H "Content-Type: application/json" https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?overwrite=true
```
{: pre}

Um einen Blockierungsaufruf für eine Aktion durchzuführen, senden Sie folgendermaßen eine HTTP-Anforderung mit der Methode `POST` und einem Hauptteil mit dem Eingabeparameter `name`:
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?blocking=true \
-X POST -H "Content-Type: application/json" \
-d '{"name":"John"}'  
```
{: pre}
Sie erhalten die folgende Antwort:
```json
{
  "duration": 2,
  "name": "hello",
  "subject": "john@example.com_dev",
  "activationId": "c7bb1339cb4f40e3a6ccead6c99f804e",
  "publish": false,
  "annotations": [{
    "key": "limits",
    "value": {
      "timeout": 60000,
      "memory": 256,
      "logs": 10
    }
  }, {
    "key": "path",
    "value": "john@example.com_dev/hello"
  }],
  "version": "0.0.1",
  "response": {
    "result": {
      "payload": "Hello John"
    },
    "success": true,
    "status": "success"
  },
  "end": 1493327653769,
  "logs": [],
  "start": 1493327653767,
  "namespace": "john@example.com_dev"
}
```
Wenn Sie nur die Antwort (`response.result`) abrufen möchten, führen Sie den Befehl erneut mit dem Abfrageparameter `result=true` aus:
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?blocking=true&result=true" \
-X POST -H "Content-Type: application/json" \
-d '{"name":"John"}' 
```
{: pre}
Sie erhalten die folgende Antwort:
```json
{
  "payload": "hello John"
}
```

## Annotationen und Webaktionen
{: #openwhisk_rest_api_webactions}
Um eine Aktion als Webaktion zu erstellen, müssen Sie eine [Annotation](annotations.md) des Typs `web-export=true` für Webaktionen hinzufügen. Da Webaktionen öffentlich zugänglich sind, sollten Sie vordefinierte Parameter mithilfe der Annotation `final=true` schützen (d. h., sie als final behandeln). Wenn Sie eine Aktion mithilfe des CLI-Flags `--web true` erstellen oder aktualisieren, werden mit diesem Befehl sowohl die Annotation `web-export=true` als auch die Annotation `final=true` hinzugefügt.

Führen Sie den curl-Befehl aus und stellen Sie eine vollständige Liste der Annotationen bereit, die für die Aktion festgelegt werden sollen:
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"hello","exec":{"kind":"nodejs:6","code":"function main(params) { return {payload:\"Hello \"+params.name}}"},"annotations":[{"key":"web-export","value":true},{"key":"raw-http","value":false},{"key":"final","value":true}]}'
```
{: pre}
Sie können diese Aktion jetzt als öffentliche URL ohne OpenWhisk-Berechtigung aufrufen. Verwenden Sie dabei die öffentliche URL der Webaktion einschließlich einer optionalen Erweiterung wie `.json` oder `.http` am Ende der URL:
```bash
curl https://openwhisk.ng.bluemix.net/api/v1/web/john@example.com_dev/default/hello.json?name=John
```
{: pre}
```json
{
  "payload": "Hello John"
}
```
Beachten Sie, dass dieser Beispielquellcode nicht mit `.http` funktioniert. Informationen über entsprechende Änderungen finden Sie in der Dokumentation zu [Webaktionen](webactions.md).

## Sequenzen
{: #openwhisk_rest_api_sequences}
Um eine Aktionssequenz zu erstellen, geben Sie die Namen der Aktionen, aus denen sich die Sequenz zusammensetzt, in der gewünschten Reihenfolge an, sodass die Ausgabe der ersten Aktion als Eingabe an die nächste Aktion übergeben wird.

$ wsk action create sequenceAction --sequence /whisk.system/utils/split,/whisk.system/utils/sort

Erstellen Sie eine Sequenz mit den Aktionen `/whisk.system/utils/split` und `/whisk.system/utils/sort`.
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/sequenceAction?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"sequenceAction","exec":{"kind":"sequence","components":["/whisk.system/utils/split","/whisk.system/utils/sort"]},"annotations":[{"key":"web-export","value":true},{"key":"raw-http","value":false},{"key":"final","value":true}]}' 
```
{: pre}

Berücksichtigen Sie bei der Angabe der Namen der Aktionen, dass diese vollständig qualifiziert sein müssen.

## Auslöser
{: #openwhisk_rest_api_triggers}
Um einen Auslöser zu erstellen, müssen Sie als Mindestanforderung einen Namen für den Auslöser angeben. Sie können auch Standardparameter einschließen, die beim Aktivieren des Auslösers anhand einer Regel an die Aktion übergeben werden.

Erstellen Sie einen Auslöser mit dem Namen `events` mit einem Standardparameter `type`, für den der Wert `webhook` festgelegt ist.
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/events?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"events","parameters":[{"key":"type","value":"webhook"}]}' 
```
{: pre}

Wann immer Sie ein Ereignis haben, das diesen Auslöser anwenden muss, benötigen Sie jetzt nur eine HTTP-Anforderung mit einer Methode `POST`, die den OpenWhisk-Berechtigungsschlüssel verwendet.

Senden Sie die folgende HTTP-Anforderung, um den Auslöser `events` mit dem Parameter `temperature` anzuwenden.

```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/events \
-X POST -H "Content-Type: application/json" \
-d '{"temperature":60}' 
```
{: pre}

### Auslöser mit Feedaktionen
{: #openwhisk_rest_api_triggers_feed}
Es gibt spezielle Auslöser, die mit einer Feedaktion erstellt werden können. Die Feedaktion ist eine Aktion, mit der die Konfiguration eines Feedanbieters unterstützt wird, der beim Auftreten eines Ereignisses für den Auslöser für die Aktivierung des Auslösers verantwortlich ist. Weitere Informationen zu diesen Feedanbietern finden Sie in der Dokumentation zu [feeds.md].

Einige der verfügbaren Auslöser, die eine Feedaktion nutzen, sind regelmäßige Auslöser bzw. Alarme, Slack, Github, Cloudant/Couchdb und messageHub/Kafka. Sie können auch Ihre eigenen Feedaktionen und Feedanbieter erstellen.

Erstellen Sie einen Auslöser namens `periodic`, der alle zwei Stunden (z. B. 02:00:00, 04:00:00, ...) aktiviert werden soll.

Über die Befehlszeilenschnittstelle können Sie dies mit einem einzigen Befehl erreichen.
```bash
wsk trigger create periodic --feed /whisk.system/alarms/alarm \
  --param cron "0 */2 * * *" -v
```
{: pre}
Da das Flag `-v` verwendet wird, werden zwei HTTP-Anforderungen gesendet: Eine ist zum Erstellen des Auslösers `periodic` und die andere zum Aufrufen einer Feedaktion `/whisk.system/alarms/alarm` mit den erforderlichen Parametern zum Konfigurieren des Feedanbieters, um den Auslöser alle zwei Stunden anzuwenden.

Für das gleiche Szenario mit der REST-API erstellen Sie zunächst den Auslöser:
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/periodic?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"periodic","annotations":[{"key":"feed","value":"/whisk.system/alarms/alarm"}]}'  
```
{: pre}

Wie Sie sehen, ist die Annotation `feed` im Auslöser gespeichert. Sie verwenden diese Annotation später, um zu ermitteln, mit welcher Feedaktion Sie den Auslöser löschen können.

Nachdem Sie den Auslöser erstellt haben, können Sie die Feedaktion aufrufen.
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/actions/alarms/alarm?blocking=true&result=false" \
-X POST -H "Content-Type: application/json" \
-d "{\"authKey\":\"$AUTH\",\"cron\":\"0 */2 * * *\",\"lifecycleEvent\":\"CREATE\",\"triggerName\":\"/_/periodic\"}" 
```
{: pre}

Sie können den Auslöser in ähnlicher Form löschen, wie Sie ihn erstellt haben. Löschen Sie den Auslöser und konfigurieren Sie mithilfe der Feedaktion den Feedanbieter zum Löschen des Handlers für den Auslöser.

Rufen Sie die Feedaktion zum Löschen des Auslösehandlers aus dem Feedanbieter auf.
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/actions/alarms/alarm?blocking=true&result=false" \
-X POST -H "Content-Type: application/json" \
-d "{\"authKey\":\"$AUTH\",\"lifecycleEvent\":\"DELETE\",\"triggerName\":\"/_/periodic\"}"  
```
{: pre}

Löschen Sie nun den Auslöser mit einer HTTP-Anforderung mit der Methode `DELETE`.
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/periodic \
-X DELETE -H "Content-Type: application/json" 
```
{: pre}

## Regeln
{: #openwhisk_rest_api_rules}
Um eine Regel zu erstellen, die einen Auslöser zu einer Aktion zuordnet, senden Sie eine HTTP-Anforderung mit einer Methode `PUT`, die den Auslöser und die Aktion im Hauptteil der Anforderung angibt.
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/rules/t2a?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"t2a","status":"","trigger":"/_/events","action":"/_/hello"}' 
```
{: pre}

Regeln können aktiviert oder inaktiviert werden und Sie können den Status der Regel durch eine Aktualisierung der Statuseigenschaft ändern. Um beispielsweise die Regel `t2a` zu inaktivieren, senden Sie `status: "inactive"` mit einer Methode `POST` im Hauptanteil der Anforderung.
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/rules/t2a?overwrite=true \
-X POST -H "Content-Type: application/json" \
-d '{"status":"inactive","trigger":null,"action":null}'  
```
{: pre}

## Pakete
{: #openwhisk_rest_api_packages}
Um eine Aktion in einem Paket zu erstellen, müssen Sie zuerst das Paket erstellen. Senden Sie zum Erstellen eines Pakets namens `iot` eine HTTP-Anforderung mit einer Methode `PUT`.

```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/packages/iot?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"iot"}' 
```
{: pre}

## Aktivierungen
{: #openwhisk_rest_api_activations}
Um die Liste der letzten drei Aktivierungen abzurufen, verwenden Sie eine HTTP-Anforderung mit einer Methode `GET` und übergeben Sie den Abfrageparameter `limit=3`.
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/activations?limit=3
```
{: pre}

Um alle Details einer Aktivierung, einschließlich Ergebnisse und Protokolle, abzurufen, senden Sie eine HTTP-Anforderung mit einer Methode `GET` und übergeben Sie die Aktivierungskennung als Pfadparameter.
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/activations/f81dfddd7156401a8a6497f2724fec7b
```
{: pre}
