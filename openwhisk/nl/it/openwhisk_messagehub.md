---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilizzo del pacchetto Message Hub
{: #openwhisk_catalog_message_hub}

Questo pacchetto ti consente di comunicare con le istanze di [Message Hub](https://developer.ibm.com/messaging/message-hub) per l'utilizzo dei messaggi utilizzando l'API Kafka nativa dalle elevate presentazioni.
{: shortdesc}

## Creazione di un trigger in ascolto su un'istanza IBM MessageHub
{: #openwhisk_catalog_message_hub_trigger}

Per creare un trigger che reagisca quando vengono pubblicati i messaggi in un'istanza Message Hub, devi utilizzare il feed denominato `/messaging/messageHubFeed`. Questa azione del feed supporta i seguenti parametri:

|Nome|Tipo|Descrizione|
|---|---|---|
|kafka_brokers_sasl|Array JSON di stringhe|Questo parametro è un array di stringhe `<host>:<port>` che comprime i broker nella tua istanza Message Hub|
|user|Stringa|Il tuo nome utente Message Hub|
|password|Stringa|La tua password Message Hub|
|topic|Stringa|L'argomento per cui vuoi che il trigger sia in ascolto|
|kafka_admin_url|Stringa URL|L'URL dell'interfaccia REST di gestione Message Hub|
|isJSONData|Booleano (facoltativo - default=false)|Quando impostato su `true`, il provider tenterà di analizzare il valore del messaggio come JSON prima di trasmetterlo come il payload del trigger.|


Mentre questo elenco di parametri può sembrare scoraggiante, ti possono venire automaticamente impostati utilizzando il comando CLI di aggiornamento del pacchetto:

1. Crea un'istanza del servizio Message Hub nella tua organizzazione e nel tuo spazio correnti che stai utilizzando per OpenWhisk.
  
2. Verifica che l'argomento che desideri ascoltare esista già in Message Hub o creane uno nuovo, ad esempio `mytopic`.
  
3. Aggiorna i pacchetti nel tuo spazio dei nomi. L'aggiornamento crea automaticamente un bind di pacchetto per l'istanza del servizio Message Hub da te creata.
  
  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Message_Hub_Credentials-1
  ```
  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1 private
  ```
  
  Il tuo bind del pacchetto contiene ora le credenziali associate alla tua istanza Message Hub.

4. A questo punto, dovrai solo creare un trigger che verrà attivato quando vengono pubblicati nuovi messaggi nel tuo argomento di Message Hub.
  
  ```
  wsk trigger create MyMessageHubTrigger -f /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1/messageHubFeed -p topic mytopic
  ```
  {: pre}

## Configurazione di un pacchetto Message Hub esternamente a Bluemix

Se vuoi configurare il tuo Message Hub esternamente a Bluemix, devi creare manualmente un bind del pacchetto per il tuo servizio Message Hub.  Hai bisogno delle credenziali del servizio Message Hub e delle informazioni di connessione.

1. Crea un bind di pacchetto configurato per il tuo servizio Message Hub.
  
  ```
  wsk package bind /whisk.system/messaging myMessageHub -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p user <your Message Hub user> -p password <your Message Hub password> -p kafka_admin_url https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443
  ```
  
2. Adesso puoi creare un trigger con il tuo nuovo pacchetto che verrà attivato quando vengono pubblicati nuovi messaggi nel tuo argomento di Message Hub.
  
  ```
  wsk trigger create MyMessageHubTrigger -f myMessageHub/messageHubFeed -p topic mytopic -p isJSONData true
  ```
  {: pre}
  

## In ascolto per i messaggi
{: #openwhisk_catalog_message_hub_listen}

Dopo aver creato un trigger, il sistema monitorerà l'argomento specificato nel tuo servizio di messaggistica. Quando vengono pubblicati nuovi messaggi, il trigger sarà attivato.

Il payload di questo trigger conterrà un campo `messages` che è un array di messaggi che sono stati pubblicati dall'ultima volta in cui è stato attivato il tuo trigger. Ogni oggetto del messaggio nell'array conterrà i seguenti campi:
- topic
- partition
- offset
- key
- value

In termini Kafka, questi campi devono essere evidenti. Tuttavia, `value` richiede una considerazione speciale. Se il parametro `isJSONData` è stato impostato su `false` (o non impostato affatto) quando il trigger è stato creato, il campo `value` sarà il valore non elaborato nel messaggio pubblicato. Tuttavia, se `isJSONData` è stato impostato su `true` quando è stato creato il trigger, il sistema tenterà di analizzare questo valore come un oggetto JSON, con il principio del massimo impegno. Se l'analisi ha esito positivo, `value` nel payload del trigger sarà il risultante oggetto JSON.

Ad esempio, se viene pubblicato un messaggio `{"title": "Some string", "amount": 5, "isAwesome": true}` con `isJSONData` impostato su `true`, il payload del trigger sarà simile a:

```json
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

Tuttavia, se viene pubblicato lo stesso contenuto del messaggio con `isJSONData` impostato su `false`, il payload del trigger sarà simile a:

```json
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

## I messaggi vengono organizzati
Riceverai una notifica che il payload del trigger contiene un array di messaggi. Ciò significa che stai producendo dei messaggi al tuo sistema di messaggistica molto velocemente, il feed tenterà di organizzare i messaggi pubblicati in una sola attivazione del tuo trigger. Ciò consente ai messaggi di essere pubblicati nel tuo trigger più velocemente ed efficacemente.

Ricorda che, durante la codifica delle azioni che vengono attivate dal tuo trigger, il numero di messaggi nel payload è tecnicamente illimitato, ma sarà sempre maggiore di 0. Quello che segue è un esempio di messaggio in batch (nota la modifica nel valore *offset*):
 
 ```json
 {
   "messages": [
    {
         "partition": 0,
         "key": null,
         "offset": 100,
         "topic": "mytopic",
         "value": {
             "amount": 5
         }
       },
       {
         "partition": 0,
         "key": null,
         "offset": 101,
         "topic": "mytopic",
         "value": {
             "amount": 1
         }
       },
       {
         "partition": 0,
         "key": null,
         "offset": 102,
         "topic": "mytopic",
         "value": {
             "amount": 999
         }
       }
   ]
 }
 ```
