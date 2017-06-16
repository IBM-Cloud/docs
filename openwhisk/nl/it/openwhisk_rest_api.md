---

copyright:
  years: 2017
lastupdated: "2017-05-04"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilizzo delle API REST OpenWhisk
{: #openwhisk_rest_api}

Una volta abilitato il tuo ambiente OpenWhisk, puoi utilizzare OpenWhisk con le tue applicazioni web o mobili utilizzando le chiamate API REST.

Per ulteriori dettagli sull'utilizzo delle API per azioni, attivazioni, pacchetti, regole e trigger, consulta la [documentazione API OpenWhisk](http://petstore.swagger.io/?url=https://raw.githubusercontent.com/openwhisk/openwhisk/master/core/controller/src/main/resources/apiv1swagger.json).


Tutte le capacità nel sistema sono disponibili mediante un'API REST. Sono presenti endpoint di raccolta e di entità per le azioni, i trigger, le regole, i pacchetti, le attivazioni e gli spazi dei nomi.

Gli endpoint di raccolta sono:
- `https://{APIHOST}/api/v1/namespaces`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/actions`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/triggers`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/rules`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/packages`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/activations`

`{APIHOST}` è il nome host dell'API OpenWhisk (ad esempio, openwhisk.ng.bluemix.net, 172.17.0.1, 192.168.99.100, 192.168.33.13 e così via).
Per `{namespace}`, il carattere `_` può essere utilizzato per specificare lo *spazio dei nomi
predefinito* dell'utente.

Puoi effettuare una richiesta GET sugli endpoint di raccolta per richiamare un elenco di entità della raccolta.

Sono presenti endpoint per ciascun tipo di entità:
- `https://{APIHOST}/api/v1/namespaces/{namespace}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/actions/[{packageName}/]{actionName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/triggers/{triggerName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/rules/{ruleName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/packages/{packageName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/activations/{activationName}`

Gli endpoint di spazio dei nomi e attivazione supportano solo le richieste GET. Gli endpoint di azioni, trigger, regole e pacchetti supportano le richieste GET, PUT e DELETE. Gli endpoint di azioni, trigger e regole supportano inoltre le richieste POST, che vengono utilizzate per richiamare azioni e trigger e per abilitare o disabilitare le regole. 

Tutte le API sono protette tramite autenticazione base HTTP. 
Puoi utilizzare lo strumento [wskadmin](../tools/admin/wskadmin) per generare un nuovo spazio dei nomi e l'autenticazione.
Le credenziali per l'autenticazione di base si trovano nella proprietà `AUTH` all'interno del file `~/.wskprops`, delimitate da due punti. 
Puoi anche recuperare queste credenziali con la CLI eseguendo `wsk property get --auth`.


Di seguito viene riportato un esempio che utilizza lo strumento di comando [cURL](https://curl.haxx.se) per richiamare l'elenco di tutti i pacchetti nello spazio dei nomi `whisk.system`:

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

In questo esempio, l'autenticazione è stata trasmessa utilizzando l'indicatore `-u`, puoi passare questo valore anche come parte dell'URL, ad esempio `https://$AUTH@{APIHOST}`

L'API OpenWhisk supporta chiamate di richiesta-risposta dai client web. OpenWhisk risponde alle richieste `OPTIONS` con le intestazione Cross-Origin Resource Sharing. Al momento, sono consentite tutte le origini (ad esempio, Access-Control-Allow-Origin è "`*`") e Access-Control-Allow-Headers produce Authorization e Content-Type.

**Attenzione:** poiché OpenWhisk supporta al momento una sola chiave per spazio dei nomi, non si consiglia di utilizzare CORS al di là di semplici esperimenti. Utilizza [Azioni web](webactions.md) o [Gateway API](apigateway.md) per esporre le tue azioni al pubblico e non utilizzare la chiave di autorizzazione OpenWhisk per le applicazioni client che richiedono CORS.

## Utilizzo della modalità dettagliata della CLI
{: #openwhisk_rest_api_cli_v}
La CLI OpenWhisk è un'interfaccia per l'API REST OpenWhisk.
Puoi eseguire la CLI in modalità dettagliata con l'indicatore `-v`: questa operazione stamperà tutte le informazioni sulla richiesta e sulla risposta HTTP.

Proviamo a richiamare il valore dello spazio dei nomi per l'utente corrente.
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

Come puoi vedere, le informazioni stampate forniscono le proprietà della richiesta HTTP, viene eseguito il metodo HTTP `GET` sull'URL `https://openwhisk.ng.bluemix.net/api/v1/namespaces` utilizzando un'intestazione di autorizzazione di base `Basic XXXYYYY`.
Nota che il valore dell'autorizzazione è la tua stringa di autorizzazione OpenWhisk codificata in base64.
La risposta è di tipo di contenuto `application/json`.

## Azioni
{: #openwhisk_rest_api_actions}
Per creare o aggiornare un'azione, invia una richiesta HTTP con il metodo `PUT` sulla raccolta di azioni. Ad esempio, per creare un'azione `nodejs:6` con il nome `hello` utilizzando un singolo contenuto di file, usa quanto segue:
```bash
curl -u $AUTH -d '{"namespace":"_","name":"hello","exec":{"kind":"nodejs:6","code":"function main(params) { return {payload:\"Hello \"+params.name}}"}}' -X PUT -H "Content-Type: application/json" https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?overwrite=true 
```
{: pre}

Per eseguire una chiamata bloccante su un'azione, invia una richiesta HTTP con un metodo `POST` e il corpo contenente il parametro di input `name` utilizzando quanto segue:
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?blocking=true \
-X POST -H "Content-Type: application/json" \
-d '{"name":"John"}'  
```
{: pre}
Ricevi la seguente risposta:
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
Se vuoi solo ottenere `response.result`, esegui di nuovo il comando con il parametro di query `result=true`
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?blocking=true&result=true" \
-X POST -H "Content-Type: application/json" \
-d '{"name":"John"}' 
```
{: pre}
Ricevi la seguente risposta:
```json
{
  "payload": "hello John"
}
```

## Annotazioni e azioni web
{: #openwhisk_rest_api_webactions}
Per creare un'azione come azione web, devi aggiungere l'[annotazione](annotations.md) `web-export=true` per le azioni web. Poiché le azioni web sono pubblicamente accessibili, devi proteggere i parametri predefiniti (ad esempio, trattarli come finali) utilizzando l'annotazione `final=true`. Se crei o aggiorni un'azione utilizzando l'indicatore della CLI `--web true`, questo comando aggiungerà entrambe le annotazioni `web-export=true` e `final=true`.

Esegui il comando curl fornendo l'elenco completo di annotazioni da impostare sull'azione.
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"hello","exec":{"kind":"nodejs:6","code":"function main(params) { return {payload:\"Hello \"+params.name}}"},"annotations":[{"key":"web-export","value":true},{"key":"raw-http","value":false},{"key":"final","value":true}]}'
```
{: pre}
Puoi ora richiamare questa azione come URL pubblico senza autorizzazione OpenWhisk. Prova il richiamo utilizzando l'URL pubblico dell'azione web che include un'estensione facoltativa come `.json` o `.http` ad esempio alla fine dell'URL.
```bash
curl https://openwhisk.ng.bluemix.net/api/v1/web/john@example.com_dev/default/hello.json?name=John
```
{: pre}
```json
{
  "payload": "Hello John"
}
```
Nota che questo codice sorgente di esempio non funzionerà con `.http`; consulta la documentazione delle [azioni web](webactions.md) per informazioni sulle modifiche.

## Sequenze
{: #openwhisk_rest_api_sequences}
Per creare una sequenza di azioni, devi fornire i nomi delle azioni che compongono la sequenza nell'ordine desiderato e quindi l'output dalla prima azione viene passato come input all'azione successiva.

$ wsk action create sequenceAction --sequence /whisk.system/utils/split,/whisk.system/utils/sort

Crea una sequenza con le azioni `/whisk.system/utils/split` e `/whisk.system/utils/sort`.
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/sequenceAction?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"sequenceAction","exec":{"kind":"sequence","components":["/whisk.system/utils/split","/whisk.system/utils/sort"]},"annotations":[{"key":"web-export","value":true},{"key":"raw-http","value":false},{"key":"final","value":true}]}' 
```
{: pre}

Tieni in considerazione che quando si specificano i nomi delle azioni, questi devono essere completi.

## Trigger
{: #openwhisk_rest_api_triggers}
Per creare un trigger, l'informazione minima che ti serve è un nome per il trigger. Puoi anche includere i parametri predefiniti che vengono passati all'azione tramite una regola quando il trigger viene attivato.

Crea un trigger con il nome `events`, con un parametro predefinito `type` e con il valore `webhook` impostato.
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/events?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"events","parameters":[{"key":"type","value":"webhook"}]}' 
```
{: pre}

Ora ogni volta che hai un evento che deve attivare questo trigger, viene effettuata una richiesta HTTP con un metodo `POST` utilizzando la chiave di autorizzazione OpenWhisk.

Per attivare il trigger `events` con un parametro `temperature`, invia la seguente richiesta HTTP.

```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/events \
-X POST -H "Content-Type: application/json" \
-d '{"temperature":60}' 
```
{: pre}

### Trigger con azioni di feed
{: #openwhisk_rest_api_triggers_feed}
Esistono dei trigger speciali che possono essere creati utilizzando un'azione di feed. L'azione di feed è un'azione che aiuta a configurare un provider di feed che sarà incaricato di attivare il trigger ogni volta che c'è un evento per il trigger. Per ulteriori informazioni su questi provider di feed, consulta la documentazione [feeds.md].

Alcuni dei trigger disponibili che sfruttano un'azione di feed sono periodic/alarms, Slack, Github, Cloudant/Couchdb e messageHub/Kafka. Puoi anche creare la tua propria azione di feed e il tuo provider di feed.

Creiamo un trigger con nome `periodic` da attivare a una frequenza specificata, ossia ogni 2 ore (ad esempio, 02:00:00, 04:00:00, ...).

Utilizzando la CLI, questa operazione sarà eseguita con un solo comando
```bash
wsk trigger create periodic --feed /whisk.system/alarms/alarm \
  --param cron "0 */2 * * *" -v
```
{: pre}
Come vedrai, poiché stiamo utilizzando l'indicatore `-v` vengono inviate due richieste HTTP, una per creare un trigger `periodic` e l'altra per richiamare un'azione di feed `/whisk.system/alarms/alarm` con i parametri per configurare il provider di feed per l'attivazione del trigger ogni 2 ore.

Per fare la stessa cosa con l'API REST, creiamo prima il trigger
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/periodic?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"periodic","annotations":[{"key":"feed","value":"/whisk.system/alarms/alarm"}]}'  
```
{: pre}

Come puoi vedere, l'annotazione `feed` viene memorizzata nel trigger. In seguito utilizzeremo questa annotazione per sapere quale azione di feed utilizzare quando si elimina il trigger.

Ora che il trigger è stato creato, richiamiamo l'azione di feed
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/actions/alarms/alarm?blocking=true&result=false" \
-X POST -H "Content-Type: application/json" \
-d "{\"authKey\":\"$AUTH\",\"cron\":\"0 */2 * * *\",\"lifecycleEvent\":\"CREATE\",\"triggerName\":\"/_/periodic\"}" 
```
{: pre}

L'operazione di eliminazione del trigger è simile a quella della sua creazione. Questa volta eliminiamo il trigger e utilizziamo l'azione di feed per configurare il provider di feed per eliminare il gestore per il trigger.

Richiama l'azione di feed per eliminare il gestore del trigger dal provider di feed
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/actions/alarms/alarm?blocking=true&result=false" \
-X POST -H "Content-Type: application/json" \
-d "{\"authKey\":\"$AUTH\",\"lifecycleEvent\":\"DELETE\",\"triggerName\":\"/_/periodic\"}"  
```
{: pre}

Ora elimina il trigger con una richiesta HTTP utilizzando il metodo `DELETE`
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/periodic \
-X DELETE -H "Content-Type: application/json" 
```
{: pre}

## Regole
{: #openwhisk_rest_api_rules}
Per creare una regola che associa un trigger a un'azione, invia una richiesta HTTP con un metodo `PUT` fornendo il trigger e l'azione nel corpo della richiesta.
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/rules/t2a?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"t2a","status":"","trigger":"/_/events","action":"/_/hello"}' 
```
{: pre}

Le regole possono essere abilitate o disabilitate e puoi modificare lo stato della regola aggiornando la sua proprietà stato. Ad esempio, per disabilitare la regola `t2a`, invia nel corpo della richiesta `status: "inactive"` con un metodo `POST`.
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/rules/t2a?overwrite=true \
-X POST -H "Content-Type: application/json" \
-d '{"status":"inactive","trigger":null,"action":null}'  
```
{: pre}

## Pacchetti
{: #openwhisk_rest_api_packages}
Per creare un'azione in un pacchetto, devi prima creare un pacchetto. Per creare un pacchetto con nome `iot`, invia una richiesta HTTP con un metodo `PUT`

```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/packages/iot?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"iot"}' 
```
{: pre}

## Attivazioni
{: #openwhisk_rest_api_activations}
Per ottenere l'elenco delle ultime 3 attivazioni, utilizza una richiesta HTTP con un metodo `GET`, passando il parametro di query `limit=3`
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/activations?limit=3
```
{: pre}

Per ottenere tutti i dettagli di un'attivazione, inclusi risultati e log, invia una richiesta HTTP con un metodo `GET`, passando l'identificativo dell'attivazione come parametro di percorso
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/activations/f81dfddd7156401a8a6497f2724fec7b
```
{: pre}
