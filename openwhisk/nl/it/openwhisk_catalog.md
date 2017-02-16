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

# Utilizzo dei servizi {{site.data.keyword.Bluemix_notm}} abilitati per {{site.data.keyword.openwhisk_short}}
{: #openwhisk_ecosystem}

In {{site.data.keyword.openwhisk}}, un catalogo di pacchetti mette a tua disposizione un modo facile per migliorare la tua applicazione con delle utili funzionalità e di accedere ai servizi interni nell'ecosistema. Sono esempi di servizi esterni con attivazione {{site.data.keyword.openwhisk_short}}: Cloudant, The Weather Company, Slack e GitHub.
{: shortdesc}

Il catalogo è disponibile come pacchetti nello spazio dei nomi `/whisk.system`. Vedi [Esplorazione dei pacchetti](./openwhisk_packages.html#openwhisk_packagedisplay) per informazioni su come esplorare il catalogo utilizzando lo strumento di riga di comando.

I seguenti argomenti documentano alcuni dei pacchetti presenti nel catalogo.

## Utilizzo del pacchetto Cloudant
{: #openwhisk_catalog_cloudant}
Il pacchetto `/whisk.system/cloudant` ti consente di lavorare con un database Cloudant. Include le azioni e i feed di seguito indicati.

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | pacchetto | {{site.data.keyword.Bluemix_notm}}ServiceName, host, username, password, dbname, overwrite | Lavorare con un database Cloudant |
| `/whisk.system/cloudant/read` | azione | dbname, includeDoc, id | Leggere un documento da un database |
| `/whisk.system/cloudant/write` | azione | dbname, overwrite, doc | Scrivere un documento in un database |
| `/whisk.system/cloudant/changes` | feed | dbname, maxTriggers | Attivare degli eventi di trigger in caso di modifiche a un database |

I seguenti argomenti descrivono la configurazione di un database Cloudant, la configurazione di un pacchetto associato e l'utilizzo di azioni e feed nel pacchetto `/whisk.system/cloudant`.

### Configurazione di un database Cloudant in {{site.data.keyword.Bluemix_notm}}
{: #openwhisk_catalog_cloudant_in}

Se stai utilizzando {{site.data.keyword.openwhisk_short}} da {{site.data.keyword.Bluemix}}, {{site.data.keyword.openwhisk_short}} crea automaticamente i bind di pacchetto per le tue istanze del servizio {{site.data.keyword.Bluemix_notm}} Cloudant. Se non stai utilizzando {{site.data.keyword.openwhisk_short}} e Cloudant da {{site.data.keyword.Bluemix_notm}}, vai direttamente al passo successivo.

1. Crea un'istanza del servizio Cloudant nel tuo [dashboard](http://console.ng.{{site.data.keyword.Bluemix_notm}}.net) {{site.data.keyword.Bluemix_notm}}.

  Accertati di tenere a mente il nome dell'istanza del servizio e dell'organizzazione e dello spazio {{site.data.keyword.Bluemix_notm}} in cui ti trovi.

2. Assicurati che la CLI {{site.data.keyword.openwhisk_short}} si trovi nello spazio dei nomi corrispondente all'organizzazione e allo spazio {{site.data.keyword.Bluemix_notm}} che hai utilizzato nel passo precedente.

  ```
  wsk property set --namespace my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space
  ```
  {: pre}

  In alternativa, puoi utilizzare `wsk property set --namespace` per impostare uno spazio dei nomi da un elenco di quelli a cui puoi accedere.

3. Aggiorna i pacchetti nel tuo spazio dei nomi. L'aggiornamento crea automaticamente un bind di pacchetto per l'istanza del servizio Cloudant da te creata.

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

  Viene visualizzato il nome completo del bind di pacchetto che corrisponde alla tua istanza del servizio {{site.data.keyword.Bluemix_notm}} Cloudant.

4. Verifica che il bind di pacchetto creato precedentemente sia configurato con l'host e le credenziali della tua istanza del servizio {{site.data.keyword.Bluemix_notm}} Cloudant.

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

### Configurazione di un database Cloudant esternamente a {{site.data.keyword.Bluemix_notm}}
{: #openwhisk_catalog_cloudant_outside}

Se non stai utilizzando {{site.data.keyword.openwhisk_short}} in {{site.data.keyword.Bluemix_notm}} o se vuoi configurare il tuo database Cloudant esternamente a {{site.data.keyword.Bluemix_notm}}, devi creare manualmente un bind di pacchetto per il tuo account Cloudant. Ti servono il nome host, il nome utente e la password dell'account Cloudant.

1. Crea un bind di pacchetto configurato per il tuo account Cloudant.

  ```
  wsk package bind /whisk.system/cloudant myCloudant -p username MYUSERNAME -p password MYPASSWORD -p host MYCLOUDANTACCOUNT.cloudant.com
  ```
  {: pre}

2. Verifica che il bind di pacchetto esista.

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myNamespace/myCloudant private binding
  ```
  {: screen}


### In ascolto delle modifiche a un database Cloudant
{: #openwhisk_catalog_cloudant_listen}

Puoi utilizzare il feed `changes` per configurare un servizio per attivare un trigger ogni volta che viene apportata una modifica al tuo database Cloudant. I parametri sono i seguenti:

- `dbname`: nome del database Cloudant.
- `maxTriggers`: arrestare l'attivazione dei trigger quando viene raggiunto questo limite. Il valore predefinito è infinito.

1. Crea un trigger con il feed `changes` nel bind di pacchetto che hai creato precedentemente. Accertati di sostituire `/myNamespace/myCloudant` con il tuo nome pacchetto.

  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
  ```
  {: pre}
  ```
  ok: created trigger feed myCloudantTrigger
  ```
  {: screen}

2. Esegui il polling per le attivazioni.

  ```
  wsk activation poll
  ```
  {: pre}

3. Nel tuo dashboard Cloudant, modifica un documento esistente oppure creane uno nuovo.

4. Osserva le nuove attivazioni per il trigger `myCloudantTrigger` trigger per ogni modifica di documento.

**Nota**: se non se in grado di osservare le nuove attivazioni, consulta le sezioni successive relative alla lettura da, e alla scrittura in, un database Cloudant. L'esecuzione di test sulle seguenti procedure di lettura e scrittura aiuterà a verificare la correttezza delle credenziali Cloudant.

Puoi ora creare le regole e associarle alle azioni per reagire agli aggiornamenti dei documenti.

Il contenuto degli eventi generati include i seguenti parametri:

- `id`: l'ID documento.
- `seq`: l'identificativo della sequenza generato da Cloudant.
- `changes`: un array di oggetti, ciascuno dei quali con un campo `rev` che contiene l'ID revisione del documento.

La rappresentazione JSON dell'evento di trigger è la seguente:

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


### Scrittura in un database Cloudant
{: #openwhisk_catalog_cloudant_write}

Puoi utilizzare un'azione per memorizzare un documento in un database Cloudant denominato `testdb`. Assicurati che questo database esista nel tuo account Cloudant.

1. Memorizza un documento utilizzando l'azione `write` nel bind di pacchetto che hai creato precedentemente. Accertati di sostituire `/myNamespace/myCloudant` con il tuo nome pacchetto.

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

2. Verifica che il documento esista sfogliando il tuo dashboard Cloudant per individuarlo.

  L'URL del dashboard per il database `testdb` ha un aspetto simile al seguente: `https://MIOACCOUNTCLOUDANT.cloudant.com/dashboard.html#database/testdb/_all_docs?limit=100`.


### Lettura da un database Cloudant
{: #openwhisk_catalog_cloudant_read}

Puoi utilizzare un'azione per recuperare un documento da un database Cloudant denominato `testdb`. Assicurati che questo database esista nel tuo account Cloudant.

1. Recupera un documento utilizzando l'azione `read` nel bind di pacchetto che hai creato precedentemente. Accertati di sostituire `/myNamespace/myCloudant` con il tuo nome pacchetto.

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

### Utilizzo di una sequenza di azioni e un trigger di modifica per elaborare un documento da un database Cloudant

Puoi utilizzare una sequenza di azioni in una regola per recuperare ed elaborare il documento associato a un evento di modifica Cloudant.

Di seguito è riportato un codice di esempio di un'azione che gestisce un documento:
```
function main(doc){
  return { "isWalter:" : doc.name === "Walter White"};
}
```
{: codeblock}

Crea l'azione per elaborare il documento da Cloudant:
```
wsk action create myAction myAction.js
```
{: pre}

Per leggere un documento dal database, puoi utilizzare l'azione `read` dal pacchetto Cloudant.
L'azione `read` potrebbe essere formata con `myAction` per creare una sequenza di azioni.
```
wsk action create sequenceAction --sequence /myNamespace/myCloudant/read,myAction
```
{: pre}

L'azione `sequenceAction` può essere utilizzata in una regola che attiva l'azione sui nuovi eventi di trigger Cloudant.
```
wsk rule create myRule myCloudantTrigger sequenceAction
```
{: pre}

**Nota** il trigger `changes` Cloudant è utilizzato per supportare il parametro `includeDoc` che non è più supportato.
  Avrai bisogno di ricreare i trigger precedentemente creati con `includeDoc`. Segui queste istruzioni per ricreare il trigger:
  ```
  wsk trigger delete myCloudantTrigger
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
  ```
  {: pre}

  L'esempio di seguito illustrato può essere utilizzato per creare una sequenza di azioni per leggere il documento modificato e chiamare le tue azioni esistenti.
  Ricorda di disabilitare tutte le regole che non sono più valide e creane di nuove utilizzando il modello della sequenza di azioni.

## Utilizzo del pacchetto Alarm
{: #openwhisk_catalog_alarm}

Il pacchetto `/whisk.system/alarms` può essere utilizzato per attivare un trigger con una frequenza specifica. Ciò è utile per configurare i lavori o le attività ricorrenti, come il richiamo di un'azione di backup del sistema ogni ora.

Il pacchetto include il seguente feed.

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | pacchetto | - | Programma di utilità per gli avvisi e la periodicità |
| `/whisk.system/alarms/alarm` | feed | cron, trigger_payload, maxTriggers | Attivare l'evento di trigger periodicamente |


### Attivazione di un evento di trigger periodicamente
{: #openwhisk_catalog_alarm_fire}

Il feed `/whisk.system/alarms/alarm` configura il servizio Alarm per attivare un evento di trigger con una specifica frequenza. I parametri sono i seguenti:

- `cron`: una stringa, basata sulla sintassi crontab Unix, che indica quando attivare il trigger in UTC (Coordinated Universal Time). La stringa è una sequenza di cinque campi separati da spazi: `X X X X X`.
Per ulteriori dettagli sull'utilizzo di sintassi cron, consulta: http://crontab.org. Di seguito sono riportati alcuni esempi della frequenza indicata dalla stringa:

  - `* * * * *`: all'inizio di ogni minuto.
  - `0 * * * *`: all'inizio di ogni ora.
  - `0 */2 * * *`: ogni 2 ore (ad esempio, 02:00:00, 04:00:00, ...)
  - `0 9 8 * *`: alle 9:00:00AM (UTC) l'ottavo giorno di ogni mese

- `trigger_payload`: il valore di questo parametro diventa il contenuto del trigger ogni volta che il trigger viene attivato.

- `maxTriggers`: arrestare l'attivazione dei trigger quando viene raggiunto questo limite. Il valore predefinito è 1.000.000. Puoi impostarlo su infinito (-1).

Di seguito viene riportato un esempio di creazione di un trigger che verrà attivato una volta ogni 2 minuti con i valori `name` e `place` nell'evento di trigger.

  ```
  wsk trigger create periodic --feed /whisk.system/alarms/alarm --param cron "*/2 * * * *" --param trigger_payload "{\"name\":\"Odin\",\"place\":\"Asgard\"}"
  ```
  {: pre}

Ogni evento generato includerà come parametri le proprietà specificate nel valore `trigger_payload`. In questo caso, ogni evento di trigger avrà i parametri `name=Odin` e `place=Asgard`.

**Nota**: il parametro `cron` supporta anche una sintassi personalizzata di sei campi, dove il primo campo rappresenta i secondi. 
Per ulteriori dettagli sull'utilizzo di sintassi cron personalizzata, consulta: https://github.com/ncb000gt/node-cron. 
Di seguito è riportato un esempio che utilizza una notazione di sei campi:
  - `*/30 * * * * *`: ogni trenta secondi.

## Utilizzo del pacchetto Weather
{: #openwhisk_catalog_weather}

Il pacchetto `/whisk.system/weather` offre un pratico modo per richiamare l'API Weather Company Data for IBM Bluemix.

Il pacchetto include la seguente azione.

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/weather` | pacchetto | username, password | Servizi dall'API Weather Company Data for IBM Bluemix  |
| `/whisk.system/weather/forecast` | azione | latitude, longitude, timePeriod | Previsione per il periodo di tempo specificato|

Si consiglia di effettuare la creazione di un bind di pacchetto con i valori `username` e `password`. In questo modo, non dovrai specificare le credenziali ogni volta che richiami le azioni nel pacchetto.

### Come ottenere una previsione meteo per una località
{: #openwhisk_catalog_weather_forecast}

L'azione `/whisk.system/weather/forecast` restituisce una previsione meteo per una località, richiamando un'API The Weather Company. I parametri sono i seguenti:

- `username`: nome utente per The Weather Company Data for IBM Bluemix che ha diritto a richiamare l'API delle previsioni.
- `password`: password per The Weather Company Data for IBM Bluemix che ha diritto a richiamare l'API delle previsioni.
- `latitude`: la coordinata della latitudine della località.
- `longitude`: la coordinata della longitudine della località.
- `timeperiod`: periodo di tempo per la previsione. Le opzioni valide sono '10day' - (impostazione predefinita) restituisce una previsione giornaliera per un periodo di 10 giorni, '48hour' - restituisce una previsione oraria per 2 giorni, 'current' - restituisce le condizioni meteorologiche correnti, 'timeseries' - restituisce le rilevazioni in tempo reale e quelle delle ultime 24 ore dalla data/ora corrente.


Di seguito viene riportato un esempio di creazione di un bind di pacchetto e successiva acquisizione di una previsione meteo di 10 giorni.

1. Crea un bind di pacchetto con la tua chiave API.

  ```
  wsk package bind /whisk.system/weather myWeather --param username MY_USERNAME --param password MY_PASSWORD
  ```
  {: pre}

2. Richiama l'azione `forecast` nel tuo bind di pacchetto per ottenere la previsione meteo.

  ```
  wsk action invoke myWeather/forecast --blocking --result --param latitude 43.7 --param longitude -79.4
  ```
  {: pre}

  ```
  {
      "forecasts": [
          {
              "dow": "Mercoledì",
              "max_temp": -1,
              "min_temp": -16,
              "narrative": "Possibilità di alcuni rovesci. Massime tra i -2°C e 0°C e minime tra -17°C e -15°C.",
              ...
          },
          {
              "class": "fod_long_range_daily",
              "dow": "Giovedì",
              "max_temp": -4,
              "min_temp": -8,
              "narrative": "Prevalentemente soleggiato. Massime tra -5°C e -3°C e minime tra i -9°C e -7°C.",
              ...
          },
          ...
      ],
  }
  ```
  {: screen}


## Utilizzo dei pacchetti Watson
{: #openwhisk_catalog_watson}

I pacchetti Watson offrono una soluzione pratica per richiamare le diverse API Watson.

Sono forniti i seguenti pacchetti Watson:

| Pacchetto | Descrizione |
| --- | --- |
| `/whisk.system/watson-translator`   | Pacchetto per la traduzione del testo e per l'identificazione della lingua |
| `/whisk.system/watson-textToSpeech` | Pacchetto per convertire il testo in voce |
| `/whisk.system/watson-speechToText` | Pacchetto per convertire la voce in testo |

**Nota** il pacchetto `/whisk.system/watson` è attualmente obsoleto; esegui la migrazione ai nuovi pacchetti menzionati sopra. Le nuove azioni forniscono la stessa interfaccia.

### Utilizzo del pacchetto Watson Translator

Il pacchetto `/whisk.system/watson-translator` offre una soluzione pratica per richiamare le diverse API Watson per la traduzione.

Il pacchetto include le seguenti azioni.

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/watson-translator` | pacchetto | username, password | Pacchetto per la traduzione del testo e per l'identificazione della lingua  |
| `/whisk.system/watson-translator/translator` | azione | payload, translateFrom, translateTo, translateParam, username, password | Tradurre il testo |
| `/whisk.system/watson-translator/languageId` | azione | payload, username, password | Identificare la lingua |

**Nota**: il pacchetto `/whisk.system/watson` è obsoleto, incluse le azioni `/whisk.system/watson/translate` e `/whisk.system/watson/languageId`.

#### Configurazione del pacchetto Watson Translator in Bluemix

Se stai utilizzando OpenWhisk da Bluemix, OpenWhisk crea automaticamente i bind di pacchetto per le tue istanze del servizio Bluemix Watson.

1. Crea un'istanza del servizio Watson Translator nel tuo [dashboard](http://console.ng.Bluemix.net) Bluemix.

  Assicurati di ricordare il nome dell'istanza del servizio e dell'organizzazione e dello spazio Bluemix in cui ti trovi.

2. Assicurati che la CLI OpenWhisk si trovi nello spazio dei nomi corrispondente all'organizzazione e allo spazio Bluemix che hai utilizzato nel passo precedente.

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  In alternativa, puoi utilizzare `wsk property set --namespace` per impostare uno spazio dei nomi da un elenco di quelli a cui puoi accedere.

3. Aggiorna i pacchetti nel tuo spazio dei nomi. L'aggiornamento crea automaticamente un bind di pacchetto per l'istanza del servizio Watson da te creata.

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


#### Configurazione del pacchetto Watson Translator esternamente a Bluemix

Se non stai utilizzando OpenWhisk in Bluemix o se vuoi configurare Watson Translator esternamente a Bluemix, devi creare manualmente un bind di pacchetto per il tuo servizio Watson Translator. Ti servono il nome utente e la password del servizio Watson Translator.

- Crea un bind di pacchetto configurato per il tuo servizio Watson Translator.

  ```
  wsk package bind /whisk.system/watson-translator myWatsonTranslator -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### Traduzione di testo
{: #openwhisk_catalog_watson_translate}

L'azione `/whisk.system/watson-translator/translator` traduce il testo da una lingua a un'altra. I parametri sono i seguenti:

- `username`: il nome utente dell'API Watson API.
- `password`: la password della API Watson.
- `payload`: il testo da tradurre.
- `translateParam`: il parametro di input che indica il testo da tradurre. Ad esempio, se `translateParam=payload`, viene tradotto il valore del parametro `payload` che viene passato all'azione.
- `translateFrom`: un codice a due cifre della lingua di origine.
- `translateTo`: un codice a due cifre della lingua di destinazione.

- Richiama l'azione `translator` nel tuo bind di pacchetto per tradurre del testo dall'inglese al francese.

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


#### Identificazione della lingua di un testo
{: #openwhisk_catalog_watson_identifylang}

L'azione `/whisk.system/watson-translator/languageId` identifica la lingua di un testo. I parametri sono i seguenti:

- `username`: il nome utente dell'API Watson API.
- `password`: la password della API Watson.
- `payload`: il testo da identificare.

- Richiama l'azione `languageId` nel tuo bind di pacchetto per identificare la lingua.

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


### Utilizzo del pacchetto Watson Text to Speech
{: #openwhisk_catalog_watson_texttospeech}

Il pacchetto `/whisk.system/watson-textToSpeech` offre una soluzione pratica per richiamare le diverse API Watson per la conversione da testo a voce.

Il pacchetto include le seguenti azioni.

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/watson-textToSpeech` | pacchetto | username, password | Pacchetto per convertire il testo in voce |
| `/whisk.system/watson-textToSpeech/textToSpeech` | azione | payload, voice, accept, encoding, username, password | Convertire testo in audio |

**Nota**: il pacchetto `/whisk.system/watson` è obsoleto, inclusa l'azione `/whisk.system/watson/textToSpeech`.

#### Configurazione del pacchetto Watson Text to Speech in Bluemix

Se stai utilizzando OpenWhisk da Bluemix, OpenWhisk crea automaticamente i bind di pacchetto per le tue istanze del servizio Bluemix Watson.

1. Crea un'istanza del servizio Watson Text to Speech nel tuo [dashboard](http://console.ng.Bluemix.net) Bluemix.

  Assicurati di ricordare il nome dell'istanza del servizio e dell'organizzazione e dello spazio Bluemix in cui ti trovi.

2. Assicurati che la CLI OpenWhisk si trovi nello spazio dei nomi corrispondente all'organizzazione e allo spazio Bluemix che hai utilizzato nel passo precedente.

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  In alternativa, puoi utilizzare `wsk property set --namespace` per impostare uno spazio dei nomi da un elenco di quelli a cui puoi accedere.

3. Aggiorna i pacchetti nel tuo spazio dei nomi. L'aggiornamento crea automaticamente un bind di pacchetto per l'istanza del servizio Watson da te creata.

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


#### Configurazione del pacchetto Watson Text to Speech esternamente a Bluemix

Se non stai utilizzando OpenWhisk in Bluemix o se vuoi configurare Watson Text to Speech esternamente a Bluemix, devi creare manualmente un bind di pacchetto per il tuo servizio Watson Text to Speech. Ti servono il nome utente e la password del servizio Watson Text to Speech.

- Crea un bind di pacchetto configurato per il tuo servizio Watson Speech to Text.

  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonTextToSpeech -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### Conversione da testo a voce
{: #openwhisk_catalog_watson_speechtotext}

L'azione `/whisk.system/watson-speechToText/textToSpeech` converte un testo in audio. I parametri sono i seguenti:

- `username`: il nome utente dell'API Watson API.
- `password`: la password della API Watson.
- `payload`: il testo da convertire in voce.
- `voice`: la voce dello speaker.
- `accept`: il formato del file audio.
- `encoding`: la codifica dei dati binari del file audio.


- Richiama l'azione `textToSpeech` nel tuo bind di pacchetto per convertire il testo.

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


### Utilizzo del pacchetto Watson Speech to Text
{: #openwhisk_catalog_watson_speechtotext}

Il pacchetto `/whisk.system/watson-speechToText` offre una soluzione pratica per richiamare le diverse API Watson per la conversione da voce a testo.

Il pacchetto include le seguenti azioni.

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/watson-speechToText` | pacchetto | username, password | Pacchetto per convertire la voce in testo |
| `/whisk.system/watson-speechToText/speechToText` | azione | payload, content_type, encoding, username, password, continuous, inactivity_timeout, interim_results, keywords, keywords_threshold, max_alternatives, model, timestamps, watson-token, word_alternatives_threshold, word_confidence, X-Watson-Learning-Opt-Out | Convertire audio in testo |

**Nota**: il pacchetto `/whisk.system/watson` è obsoleto, inclusa l'azione `/whisk.system/watson/speechToText`.

#### Configurazione del pacchetto Watson Speech to Text in Bluemix

Se stai utilizzando OpenWhisk da Bluemix, OpenWhisk crea automaticamente i bind di pacchetto per le tue istanze del servizio Bluemix Watson.

1. Crea un'istanza del servizio Watson Speech to Text nel tuo [dashboard](http://console.ng.Bluemix.net) Bluemix.

  Assicurati di ricordare il nome dell'istanza del servizio e dell'organizzazione e dello spazio Bluemix in cui ti trovi.

2. Assicurati che la CLI OpenWhisk si trovi nello spazio dei nomi corrispondente all'organizzazione e allo spazio Bluemix che hai utilizzato nel passo precedente.

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  In alternativa, puoi utilizzare `wsk property set --namespace` per impostare uno spazio dei nomi da un elenco di quelli a cui puoi accedere.

3. Aggiorna i pacchetti nel tuo spazio dei nomi. L'aggiornamento crea automaticamente un bind di pacchetto per l'istanza del servizio Watson da te creata.

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


#### Configurazione del pacchetto Watson Speech to Text esternamente a Bluemix

Se non stai utilizzando OpenWhisk in Bluemix o se vuoi configurare  Watson Speech to Text esternamente a Bluemix, devi creare manualmente un bind di pacchetto per il tuo servizio Watson Speech to Text. Ti servono il nome utente e la password del servizio Watson Speech to Text.

- Crea un bind di pacchetto configurato per il tuo servizio Watson Speech to Text.

  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonSpeechToText -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### Conversione da voce a testo

L'azione `/whisk.system/watson-speechToText/speechToText` converte l'audio in testo. I parametri sono i seguenti:

- `username`: il nome utente dell'API Watson API.
- `password`: la password della API Watson.
- `payload`: i dati binari audio codificati da convertire in testo.
- `content_type`: il tipo MIME dell'audio.
- `encoding`: la codifica dei dati binari del file audio.
- `continuous`: indica se vengono restituiti più risultati finali che rappresentano frasi consecutive separate da pause lunghe.
- `inactivity_timeout`: il tempo, in secondi, dopo il quale viene chiusa la connessione, se nell'audio presentato viene rilevato solo silenzio.
- i`interim_results`: indica se il servizio deve restituire risultati intermedi
- `keywords`: un elenco di parole chiave da individuare nell'audio.
- `keywords_threshold`: un valore di attendibilità corrispondente al limite inferiore per l'individuazione di una parola chiave.
- `max_alternatives`: il numero massimo di trascrizioni alternative da restituire.
- `model`: l'identificativo del modello da utilizzare per la richiesta di riconoscimento.
- `timestamps`: indica se l'allineamento temporale viene restituito per ciascuna parola.
- `watson-token`: fornisce un token di autenticazione per il servizio come alternativa all'immissione delle credenziali del servizio.
- `word_alternatives_threshold`: un valore di attendibilità corrispondente al limite inferiore per l'individuazione di un'ipotesi come possibile parola alternativa.
- `word_confidence`: indica se per ciascuna parola deve essere restituita una misura di attendibilità compresa nell'intervallo da 0 a 1.
- `X-Watson-Learning-Opt-Out`: indica se annullare la selezione della raccolta dati per la chiamata.
 

- Richiama l'azione `speechToText` nel tuo bind di pacchetto per convertire l'audio codificato.

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
 
 
## Utilizzo del pacchetto Message Hub
{: #openwhisk_catalog_message_hub}

Questo pacchetto ti consente di creare trigger che reagiscono quando vengono pubblicati dei messaggi nell'istanza del servizio [Message Hub](https://developer.ibm.com/messaging/message-hub/) su Bluemix.

### Creazione di un trigger in ascolto su un'istanza Message Hub
{: #openwhisk_catalog_message_hub_trigger}
Per creare un trigger che reagisce quando vengono pubblicati i messaggi in un'istanza Message Hub, devi utilizzare il feed denominato `messaging/messageHubFeed`. Questo feed supporta i seguenti parametri:

|Nome|Tipo|Descrizione|
|---|---|---|
|kafka_brokers_sasl|Array JSON di stringhe|Questo parametro è un array di stringhe `<host>:<port>` che comprime i broker nella tua istanza Message Hub|
|user|Stringa|Il tuo nome utente Message Hub|
|password|Stringa|La tua password Message Hub|
|topic|Stringa|L'argomento per cui vuoi che il trigger sia in ascolto|
|kafka_admin_url|Stringa URL|L'URL dell'interfaccia REST di gestione Message Hub|
|api_key|Stringa|La tua chiave API Message Hub|
|isJSONData|Booleano (facoltativo - default=false)|Quando impostato su `true` farà in modo che il feed tenti di analizzare il contenuto del messaggio come JSON prima di trasmetterlo come il payload del trigger.|

Mentre questo elenco di parametri può sembrare scoraggiante, ti possono venire automaticamente impostati utilizzando il comando CLI di aggiornamento del pacchetto:

1. Crea un'istanza del servizio Message Hub nella tua organizzazione e nel tuo spazio correnti che stai utilizzando per OpenWhisk.

2. Verifica che l'argomento che desideri ascoltare già esista in Message Hub o creane uno nuovo per ascoltare i messaggi, come `mytopic`.

2. Aggiorna i pacchetti nel tuo spazio dei nomi. L'aggiornamento crea automaticamente un bind di pacchetto per l'istanza del servizio Message Hub da te creata.

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

  Il tuo bind del pacchetto contiene ora le credenziali associate alla tua istanza Message Hub.

3. Ora, tutto quello di cui hai bisogno, è di creare un trigger da attivare quando vengono pubblicati nuovi messaggi nel tuo Message Hub.

  ```
  wsk trigger create MyMessageHubTrigger -f /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1/messageHubFeed -p topic mytopic
  ```
  {: pre}

### Configurazione di un pacchetto Message Hub esternamente a Bluemix

Se non stai utilizzando OpenWhisk in Bluemix o se desideri configurare il Message Hub esternamente a Bluemix, devi creare manualmente un bind del pacchetto per il tuo servizio Message Hub. Hai bisogno delle credenziali del servizio Message Hub e delle informazioni di connessione.

- Crea un bind di pacchetto configurato per il tuo servizio Message Hub.

  ```
  wsk trigger create MyMessageHubTrigger -f /whisk.system/messaging/messageHubFeed -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p topic mytopic -p user <your Message Hub user> -p password <your Message Hub password> -p kafka_admin_url https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443 -p api_key <your API key>
  ```
  {: pre}

### In ascolto per i messaggi su un'istanza Message Hub
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

Tuttavia, se viene pubblicato lo stesso contenuto del messaggio con `isJSONData` impostato su `false`, il payload del trigger sarà simile a:

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

### I messaggi vengono organizzati
Riceverai una notifica che il payload del trigger contiene un array di messaggi. Ciò significa che stai producendo dei messaggi al tuo sistema di messaggistica molto velocemente, il feed tenterà di organizzare i messaggi pubblicati in una sola attivazione del tuo trigger. Ciò consente ai messaggi di essere pubblicati nel tuo trigger più velocemente ed efficacemente.

Tieni in mente quando codifichi le azioni attivate dal tuo trigger, che il numero di messaggi nel payload è tecnicamente illimitato, ma sarà sempre maggiore di 0.


## Utilizzo del pacchetto Slack
{: #openwhisk_catalog_slack}

Il pacchetto `/whisk.system/slack` offre un pratico modo per utilizzare le [API Slack](https://api.slack.com/).

Il pacchetto include le seguenti azioni:

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/slack` | pacchetto | url, channel, username | Interagire con la API Slack |
| `/whisk.system/slack/post` | azione | text, url, channel, username | Pubblicare un messaggio su un canale Slack |

Si consiglia di effettuare la creazione di un bind di pacchetto con i valori `username`, `url` e `channel`. Con il bind, non dovrai specificare i valori ogni volta che richiami l'azione nel pacchetto.

### Pubblicazione di un messaggio in un canale Slack
{: #openwhisk_catalog_slack_post}

L'azione `/whisk.system/slack/post` pubblica un messaggio in uno specifico canale Slack. I parametri sono i seguenti:

- `url`: l'URL del webhook Slack.
- `channel`: il canale Slack nel quale pubblicare il messaggio.
- `username`: il nome con il quale pubblicare il messaggio.
- `text`: un messaggio da pubblicare.
- `token`: (facoltativo) un [token di accesso](https://api.slack.com/tokens) Slack. Vedi [sotto](./openwhisk_catalog.html#openwhisk_catalog_slack_token) per ulteriori dettagli sull'utilizzo dei token di accesso Slack.

Il seguente è un esempio di configurazione di Slack, creazione di un bind di pacchetto e pubblicazione di un messaggio in un canale.

1. Configura un [webhook in entrata](https://api.slack.com/incoming-webhooks) Slack per il tuo team.

  Dopo che Slack è stato configurato, ottieni un URL webhook simile a `https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`. Ti servirà nel prossimo passo.

2. Crea un bind di pacchetto con le tue credenziali Slack, il canale in cui vuoi pubblicare il messaggio e il nome utente con il quale vuoi farlo.

  ```
  wsk package bind /whisk.system/slack mySlack --param url "https://hooks.slack.com/services/..." --param username Bob --param channel "#MySlackChannel"
  ```
  {: pre}

3. Richiama l'azione `post` nel tuo bind di pacchetto per pubblicare un messaggio nel canale Slack.

  ```
  wsk action invoke mySlack/post --blocking --result --param text "Hello from OpenWhisk!"
  ```
  {: pre}

### Utilizzo dell'API basata sul token Slack
{: #openwhisk_catalog_slack_token}

Se preferisci, puoi scegliere di utilizzare l'API basata su token Slack anziché l'API webhook. Se così fosse, devi passare un parametro `token` che contiene il tuo [token di accesso](https://api.slack.com/tokens) Slack. Puoi quindi utilizzare qualsiasi [metodo API Slack](https://api.slack.com/methods) come tuo parametro `url`. Ad esempio, per pubblicare un messaggio, puoi utilizzare il valore di parametro `url` [slack.postMessage](https://api.slack.com/methods/chat.postMessage).

## Utilizzo del pacchetto GitHub
{: #openwhisk_catalog_github}

Il pacchetto `/whisk.system/github` offre un pratico modo per utilizzare le [API GitHub](https://developer.github.com/).

Il pacchetto include il seguente feed:

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/github` | pacchetto | username, repository, accessToken | Interagire con la API GitHub |
| `/whisk.system/github/webhook` | feed | events, username, repository, accessToken | Attivare gli eventi di trigger in caso di attività GitHub |

Si consiglia di effettuare la creazione di un bind di pacchetto con i valori `username`, `repository` e `accessToken`.  Con il bind, non dovrai specificare i valori ogni volta che usi il feed nel pacchetto.

### Attivazione di un evento di trigger in caso di attività GitHub
{: #openwhisk_catalog_github_fire}

Il feed `/whisk.system/github/webhook` configura un servizio per attivare un trigger in caso di attività in uno specifico repository GitHub. I parametri sono i seguenti:

- `username`: il nome utente del repository GitHub.
- `repository`: Il repository GitHub.
- `accessToken`: il tuo token di accesso personale GitHub. Quando [crei il tuo token](https://github.com/settings/tokens), assicurati di selezionare gli ambiti repo:status e public_repo. Assicurati inoltre di non avere webhook già definiti per il tuo repository.
- `events`: il [tipo di evento GitHub](https://developer.github.com/v3/activity/events/types/) a cui sei interessato.

Il seguente è un esempio di creazione di un trigger che verrà attivato ogni volta che viene eseguito un nuovo commit in un repository GitHub.

1. Genera un [token di accesso personale](https://github.com/settings/tokens) GitHub.

  Il token di accesso verrà utilizzato nel prossimo passo.

2. Crea un bind di pacchetto configurato per il tuo repository GitHub e con il tuo token di accesso.

  ```
  wsk package bind /whisk.system/github myGit --param username myGitUser --param repository myGitRepo --param accessToken aaaaa1111a1a1a1a1a111111aaaaaa1111aa1a1a
  ```
  {: pre}

3. Crea un trigger per il tipo di evento `push` di GitHub utilizzando il feed `myGit/webhook`.

  ```
  wsk trigger create myGitTrigger --feed myGit/webhook --param events push
  ```
  {: pre}

Un commit al repository GitHub mediante `git push` comporta l'attivazione del trigger da parte del webhook. Se è presente una regola che corrisponde al trigger, sarà richiamata l'azione associata.
L'azione riceve il payload del webhook GitHub come parametro di input. Ogni evento webhook Github ha uno schema JSON simile, ma è un oggetto payload univoco che è determinato dal proprio tipo di evento.
Per ulteriori informazioni sul contenuto del payload, consulta la documentazione API [GitHub events and payload](https://developer.github.com/v3/activity/events/types/).


## Utilizzo del pacchetto Push
{: #openwhisk_catalog_pushnotifications}

Il pacchetto `/whisk.system/pushnotifications` ti consente di lavorare con un servizio push. 

Il pacchetto include l'azione e il feed che seguono:

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/pushnotifications` | pacchetto | appId, appSecret  | Lavorare con il servizio push |
| `/whisk.system/pushnotifications/sendMessage` | azione | text, url, deviceIds, platforms, tagNames, apnsBadge, apnsCategory, apnsActionKeyTitle, apnsSound, apnsPayload, apnsType, gcmCollapseKey, gcmDelayWhileIdle, gcmPayload, gcmPriority, gcmSound, gcmTimeToLive | Invia notifica di push a uno o più dispositivi specificati |
| `/whisk.system/pushnotifications/webhook` | feed | events | Attiva gli eventi trigger sulle attività del dispositivo (registrazione, annullamento della registrazione, sottoscrizione o annullamento della sottoscrizione del dispositivo) sul servizio Push |
Si consiglia di effettuare la creazione di un bind di pacchetto con i valori `appId` e `appSecret`. In questo modo, non dovrai specificare queste credenziali ogni volta che richiami le azioni nel pacchetto.

### Creazione di un bind di pacchetto Push
{: #openwhisk_catalog_pushnotifications_create}

Durante la creazione di un bind di pacchetto Notifiche di push, devi specificare i seguenti parametri:

-  `appId`: il GUID dell'applicazione Bluemix.
-  `appSecret`: l'appSecret del servizio di notifica push Bluemix.

Il seguente è un esempio di creazione di un bind di pacchetto.

1. Crea un'applicazione Bluemix nel [Dashboard Bluemix](http://console.ng.bluemix.net).

2. Inizializza il servizio di notifica push ed esegui il bind del servizio all'applicazione Bluemix.

3. Configura l'[applicazione Notifica di push](https://console.ng.bluemix.net/docs/services/mobilepush/index.html).

  Assicurati di ricordare il `GUID applicazione` e il `Segreto applicazione` dell'applicazione Bluemix che hai creato.


4. Crea un bind al pacchetto con `/whisk.system/pushnotifications`.

  ```
  wsk package bind /whisk.system/pushnotifications myPush -p appId myAppID -p appSecret myAppSecret
  ```
  {: pre}

5. Verifica che il bind di pacchetto esista.

  ```
  wsk package list
  ```
  {: pre}

  ```
  packages
  /myNamespace/myPush private binding
  ```
  {: screen}

### Invio di notifiche di push
{: #openwhisk_catalog_pushnotifications_send}

L'azione `/whisk.system/pushnotifications/sendMessage` invia notifiche push ai dispositivi registrati. I parametri sono i seguenti:
- `text`: il messaggio della notifica visualizzato dall'utente. Ad esempio: `-p text "Hi ,OpenWhisk send a notification"`.
- `url`: un URL facoltativo che può essere inviato con l'avviso. Ad esempio: `-p url "https:\\www.w3.ibm.com"`.
- `deviceIds`: l'elenco di dispositivi specificati. Ad esempio: `-p deviceIds "[\"deviceID1\"]"`.
- `platforms`: invia notifiche ai dispositivi delle piattaforme specificate. 'A' per i dispositivi Apple (iOS) e 'G' per i dispositivi Google (Android). Ad esempio `-p platforms "[\"A\"]"`.
- `tagNames`:  invia notifiche ai dispositivi sottoscritti a una di queste tag. Ad esempio `-p tagNames "[\"tag1\"]" `.
- `gcmPayload`: payload JSON personalizzato che verrà inviato come parte del messaggio di notifica. Ad esempio: `-p gcmPayload "{\"hi\":\"hello\"}"`
- `gcmSound`: il file audio (sul dispositivo) che tenterà di essere eseguito quando la notifica arriva al dispositivo.
- `gcmCollapseKey`: questo parametro identifica un gruppo di messaggi.
- `gcmDelayWhileIdle`: quando questo parametro è impostato su true, indica che il messaggio non verrà inviato finché il dispositivo non diventa attivo.
- `gcmPriority`: imposta la priorità del messaggio.
- `gcmTimeToLive`: questo parametro specifica per quanto tempo (in secondi) il messaggio viene conservato nella memoria GCM se il dispositivo è offline.
- `apnsBadge`: il numero da visualizzare come badge dell'icona dell'applicazione.
- `apnsCategory`: l'identificativo della categoria da utilizzare per le notifiche di push interattive.
- `apnsIosActionKey`: il titolo per la chiave Azione.
- `apnsPayload`: payload JSON personalizzato che verrà inviato come parte del messaggio di notifica.
- `apnsType`: ['DEFAULT', 'MIXED', 'SILENT'].
- `apnsSound`: il nome del file audio nel bundle dell'applicazione. L'audio di questo file viene riprodotto come un avviso.

Questo è un esempio di invio di una notifica push dal pacchetto pushnotification.

1. Invia la notifica push utilizzando l'azione `sendMessage` nel bind di pacchetto che hai precedentemente creato. Accertati di sostituire `/myNamespace/myPush` con il tuo nome pacchetto.

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

### Attivazione di un evento di trigger sull'attività push
{: #openwhisk_catalog_pushnotifications_fire}

`/whisk.system/pushnotifications/webhook` configura il servizio Push per attivare un trigger quando, in un'applicazione specificata, si verifica un'attività del dispositivo, ad esempio la registrazione/l'annullamento della registrazione o la sottoscrizione/l'annullamento della sottoscrizione del dispositivo.

I parametri sono i seguenti:

- `appId:` il GUID dell'applicazione Bluemix.
- `appSecret:` l'appSecret del servizio di notifica push Bluemix.
- `events:` gli eventi supportati sono `onDeviceRegister`, `onDeviceUnregister`, `onDeviceUpdate`, `onSubscribe`, `onUnsubscribe`.Per ricevere notifiche da tutti gli eventi utilizzare il carattere jolly `*`.

Di seguito viene riportato un esempio di creazione di un trigger che verrà attivato ogni volta che viene registrato un nuovo dispositivo con l'applicazione del servizio di notifiche di push.

1. Crea un bind di pacchetto configurato per il tuo servizio di notifica di push con i tuoi appId e appSecret.

  ```
  wsk package bind /whisk.system/pushnotifications myNewDeviceFeed --param appID myapp --param appSecret myAppSecret --param events onDeviceRegister
  ```
  {: pre}

2. Crea un trigger per il tipo di evento `onDeviceRegister` del servizio di notifica di push utilizzando il feed `myPush/webhook`.

  ```
  wsk trigger create myPushTrigger --feed myPush/webhook --param events onDeviceRegister
  ```
  {: pre}
