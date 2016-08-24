---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Utilizzo di servizi abilitati a {{site.data.keyword.openwhisk_short}} 
{: #openwhisk_ecosystem}
*Ultimo aggiornamento: 28 marzo 2016*
{: .last-updated}

In {{site.data.keyword.openwhisk}}, un catalogo di pacchetti mette a tua disposizione un modo facile per migliorare la tua applicazione con delle utili funzionalità e di accedere ai servizi interni nell'ecosistema. Sono esempi di servizi esterni con attivazione {{site.data.keyword.openwhisk_short}}: Cloudant, The Weather Company, Slack e GitHub.
{: shortdesc}

Il catalogo è disponibile come pacchetti nello spazio dei nomi `/whisk.system`. Vedi [Esplorazione dei pacchetti](./openwhisk_packages.html#openwhisk_packagedisplay) per informazioni su come esplorare il catalogo utilizzando lo strumento di riga di comando.

I seguenti argomenti documentano alcuni dei pacchetti presenti nel catalogo.

## Utilizzo del pacchetto Cloudant
{: #openwhisk_catalog_cloudant}
Il pacchetto `/whisk.system/cloudant` ti consente di lavorare con un database Cloudant. Include le azioni e i feed di seguito indicati.

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | pacchetto | {{site.data.keyword.Bluemix_notm}}ServiceName, host, username, password, dbname, includeDoc, overwrite | Lavorare con un database Cloudant |
| `/whisk.system/cloudant/read` | azione | dbname, includeDoc, id | Leggere un documento da un database |
| `/whisk.system/cloudant/write` | azione | dbname, overwrite, doc | Scrivere un documento in un database |
| `/whisk.system/cloudant/changes` | feed | dbname, includeDoc, maxTriggers | Attivare degli eventi di trigger in caso di modifiche a un database |

I seguenti argomenti descrivono la configurazione di un database Cloudant, la configurazione di un pacchetto associato e l'utilizzo di azioni e feed nel pacchetto `/whisk.system/cloudant`.

### Configurazione di un database Cloudant in {{site.data.keyword.Bluemix_notm}}

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

  Dovresti vedere il nome completo del bind di pacchetto che corrisponde alla tua istanza del servizio {{site.data.keyword.Bluemix_notm}} Cloudant.

4. Verifica che il bind di pacchetto creato precedentemente sia configurato con il tuo host e le tue credenziali dell'istanza del servizio {{site.data.keyword.Bluemix_notm}} Cloudant.

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

Se non stai utilizzando {{site.data.keyword.openwhisk_short}} in {{site.data.keyword.Bluemix_notm}} o se vuoi configurare il tuo database Cloudant esternamente a {{site.data.keyword.Bluemix_notm}}, devi creare manualmente un bind di pacchetto per il tuo account Cloudant. Ti servono il nome host, il nome utente e la password dell'account Cloudant.

1. Crea un bind di pacchetto configurato per il tuo account Cloudant.

  ```
  wsk package bind /whisk.system/cloudant myCloudant -p username 'MIONOMEUTENTE' -p password 'MIAPASSWORD' -p host 'MIOACCOUNTCLOUDANT.cloudant.com'
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

Puoi utilizzare il feed `changes` per configurare un servizio per attivare un trigger ogni volta che viene apportata una modifica al tuo database Cloudant. I parametri sono i seguenti:

- `dbname`: nome del database Cloudant.
- `includeDoc`: se è impostato su true, ogni evento di trigger che viene attivato include il documento Cloudant modificato. 
- `maxTriggers`: arrestare l'attivazione dei trigger quando viene raggiunto questo limite. Il valore predefinito è 1000. Puoi impostarlo su un massimo di 10.000. Se tenti di impostare più di 10.000, la richiesta viene rifiutata.

1. Crea un trigger con il feed `changes` nel bind di pacchetto che hai creato precedentemente. Accertati di sostituire `/myNamespace/myCloudant` con il tuo nome pacchetto.

  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb --param includeDoc true
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

**Nota**: se non sei in grado di osservare le nuove attivazioni, consulta le sezioni successive relative alla lettura da, e alla scrittura in, un database Cloudant. Verificare i passi relativi alla lettura e alla scrittura qui di seguito aiuterà a verificare che le tue credenziali Cloudant siano corrette.

Puoi ora creare le regole e associarle alle azioni per reagire agli aggiornamenti dei documenti.

Il contenuto degli eventi generati dipende dal valore del parametro `includeDoc` durante la creazione del trigger. Se è impostato su true, ogni evento di trigger che viene attivato include il documento Cloudant modificato. Considera, ad esempio, il seguente documento modificato:

  ```
  {
    "_id": "6ca436c44074c4c2aa6a40c9a188b348",
    "_rev": "3-bc4960fc13aa368afca8c8427a1c18a8",
    "name": "Heisenberg"
  }
  ```
  {: screen}

Il codice in questo esempio genera un evento di trigger con i parametri `_id`, `_rev` e `name` corrispondenti. In effetti, la rappresentazione JSON dell'evento di trigger è identica al documento.

In caso contrario, se `includeDoc` è false, gli eventi includono i seguenti parametri:

- `id`: l'ID documento.
- `seq`: l'identificativo sequenza generato da Cloudant.
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

Puoi utilizzare un'azione per memorizzare un documento in un database Cloudant denominato `testdb`. Assicurati che questo database esista nel tuo account Cloudant.

1. Memorizza un documento utilizzando l'azione `write` nel bind di pacchetto che hai creato precedentemente. Accertati di sostituire `/myNamespace/myCloudant` con il tuo nome pacchetto.

  ```
  wsk action invoke /myNamespace/myCoudant/write --blocking --result --param dbname testdb --param doc '{"_id":"heisenberg", "name":"Walter White"}'
  ```
  {: pre}
  ```
  ok: invoked /myNamespace/myCoudant/write with id 62bf696b38464fd1bcaff216a68b8287
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

Puoi utilizzare un'azione per recuperare un documento da un database Cloudant denominato `testdb`. Assicurati che questo database esista nel tuo account Cloudant.

1. Recupera un documento utilizzando l'azione `read` nel bind di pacchetto che hai creato precedentemente. Accertati di sostituire `/myNamespace/myCloudant` con il tuo nome pacchetto.

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


## Utilizzo del pacchetto Alarm
{: #openwhisk_catalog_alarm}

Il pacchetto `/whisk.system/alarms` può essere utilizzato per attivare un trigger con una specifica frequenza. Ciò è utile per configurare i lavori o le attività ricorrenti, come il richiamo di un'azione di backup del sistema ogni ora.

Il pacchetto include il seguente feed.

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | pacchetto | - | Programma di utilità per gli avvisi e la periodicità |
| `/whisk.system/alarms/alarm` | feed | cron, trigger_payload, maxTriggers | Attivare l'evento di trigger periodicamente |


### Attivazione di un evento di trigger periodicamente

Il feed `/whisk.system/alarms/alarm` configura il servizio Alarm per attivare un evento di trigger con una specifica frequenza. I parametri sono i seguenti:

- `cron`: una stringa, basata sulla sintassi crontab Unix, che indica quando attivare il trigger in UTC (Coordinated Universal Time). La stringa è una sequenza di sei campi separati da spazi: `X X X X X X `. Per ulteriori dettagli sull'utilizzo della sintassi cron, consulta: https://github.com/ncb000gt/node-cron. Ecco alcuni esempi della frequenza indicata dalla stringa:

  - `* * * * * *`: ogni secondo.
  - `0 * * * * *`: all'inizio di ogni minuto.
  - `* 0 * * * *`: all'inizio di ogni ora.
  - `0 0 9 8 * *`: alle 9:00:00 AM (UTC) l'ottavo giorno di ogni mese

- `trigger_payload`: il valore di questo parametro diventa il contenuto del trigger ogni volta che il trigger viene attivato.

- `maxTriggers`: arrestare l'attivazione dei trigger quando viene raggiunto questo limite. Il valore predefinito è 1000. Puoi impostarlo su un massimo di 10.000. Se tenti di impostare più di 10.000, la richiesta viene rifiutata.

Il seguente è un esempio di creazione di un trigger che verrà attivato una volta ogni 20 secondi con i valori `name` e `place` nell'evento di trigger.

  ```
  wsk trigger create periodic --feed /whisk.system/alarms/alarm --param cron '*/20 * * * * *' --param trigger_payload '{"name":"Odin","place":"Asgard"}'
  ```
  {: pre}

Ogni evento generato includerà come parametri le proprietà specificate nel valore `trigger_payload`. In questo caso, ogni evento di trigger avrà i parametri `name=Odin` e `place=Asgard`.


## Utilizzo del pacchetto Weather
{: #openwhisk_catalog_weather}

Con il pacchetto `/whisk.system/weather` è possibile richiamare comodamente l'API IBM Weather Insights.

Il pacchetto include la seguente azione.

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/weather` | pacchetto | apiKey | Servizi dall'API IBM Weather Insights  |
| `/whisk.system/weather/forecast` | azione | apiKey, latitude, longitude, timePeriod | Previsione per il periodo di tempo specificato|

Anche se non è obbligatorio, ti consigliamo di creare un bind di pacchetto con il valore `apiKey`. In questo modo non dovrai specificare la chiave ogni volta che richiami le azioni nel pacchetto.

### Come ottenere una previsione meteo per una località

L'azione `/whisk.system/weather/forecast` restituisce una previsione meteo per una località, richiamando un'API The Weather Company. I parametri sono i seguenti:

- `apiKey`: una chiave API per The Weather Company autorizzata a richiamare l'API di previsione.
- `latitude`: la coordinata della latitudine della località.
- `longitude`: la coordinata della longitudine della località.
- `timeperiod`: periodo di tempo per la previsione. Le opzioni valide sono '10day' (impostazione predefinita): restituisce una previsione giornaliera per un periodo di 10 giorni, '24hour': restituisce una previsione oraria per 2 giorni, 'current': restituisce le condizioni meteorologiche correnti, 'timeseries': restituisce le rilevazioni in tempo reale e quelle delle ultime 24 ore dalla data/ora corrente. 


Il seguente è un esempio di creazione di un bind di pacchetto e di successivo ottenimento di una previsione meteo a 10 giorni.

1. Crea un bind di pacchetto con la tua chiave API.

  ```
  wsk package bind /whisk.system/weather myWeather --param apiKey 'MY_WEATHER_API'
  ```
  {: pre}

2. Richiama l'azione `forecast` nel tuo bind di pacchetto per ottenere la previsione meteo.

  ```
  wsk action invoke myWeather/forecast --blocking --result --param latitude '43.7' --param longitude '-79.4'
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


## Utilizzo del pacchetto Watson
{: #openwhisk_catalog_watson}

Il pacchetto `/whisk.system/watson` offre un pratico modo per richiamare diverse API Watson.

Il pacchetto include le seguenti azioni.

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/watson` | pacchetto | username, password | Azioni per le API di Watson Analytics |
| `/whisk.system/watson/translate` | azione | translateFrom, translateTo, translateParam, username, password | Tradurre il testo |
| `/whisk.system/watson/languageId` | azione | payload, username, password | Identificare la lingua |
| `/whisk.system/watson/speechToText` | azione | payload, content_type, encoding, username, password, continuous, inactivity_timeout, interim_results, keywords, keywords_threshold, max_alternatives, model, timestamps, watson-token, word_alternatives_threshold, word_confidence, X-Watson-Learning-Opt-Out | Convertire audio in testo |
| `/whisk.system/watson/textToSpeech` | azione | payload, voice, accept, encoding, username, password | Convertire testo in audio |

Anche se non è obbligatorio, ti consigliamo di creare un bind di pacchetto con i valori `username` e `password`. In questo modo, non dovrai specificare queste credenziali ogni volta che richiami le azioni nel pacchetto.

### Traduzione di testo

L'azione `/whisk.system/watson/translate` traduce il testo da una lingua a un'altra. I parametri sono i seguenti:

- `username`: il nome utente della API Watson.
- `password`: la password della API Watson.
- `translateParam`: il parametro di input da tradurre. Ad esempio, se `translateParam=payload`, il valore del parametro `payload` passato all'azione viene tradotto.
- `translateFrom`: un codice a due cifre della lingua di origine.
- `translateTo`: un codice a due cifre della lingua di destinazione.

Il seguente è un esempio di creazione di un bind di pacchetto e di traduzione di testo.

1. Crea un bind di pacchetto con le tue credenziali Watson.

  ```
  wsk package bind /whisk.system/watson myWatson --param username 'MIO_NOMEUTENTE_WATSON' --param password 'MIA_PASSWORD_WATSON'
  ```
  {: pre}

2. Richiama l'azione `translate` nel tuo bind di pacchetto per tradurre del testo dall'inglese al francese.

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


### Identificazione della lingua di un testo

L'azione `/whisk.system/watson/languageId` identifica la lingua di un testo. I parametri sono i seguenti:

- `username`: il nome utente della API Watson.
- `password`: la password della API Watson.
- `payload`: il testo da identificare.

Il seguente è un esempio di creazione di un bind di pacchetto e di identificazione della lingua di un testo.

1. Crea un bind di pacchetto con le tue credenziali Watson.

  ```
  wsk package bind /whisk.system/watson myWatson -p username 'MIO_NOMEUTENTE_WATSON' -p password 'MIA_PASSWORD_WATSON'
  ```
  {: pre}

2. Richiama l'azione `languageId` nel tuo bind di pacchetto per identificare la lingua.

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


### Conversione da testo a voce

L'azione `/whisk.system/watson/textToSpeech` converte un testo in un discorso audio. I parametri sono i seguenti:

- `username`: il nome utente della API Watson.
- `password`: la password della API Watson.
- `payload`: il testo da convertire in voce.
- `voice`: la voce dello speaker.
- `accept`: il formato del file audio.
- `encoding`: la codifica dei dati binari del file audio.

Di seguito è riportato un esempio di creazione di un bind di pacchetto e di una conversione da testo a voce.

1. Crea un bind di pacchetto con le tue credenziali Watson.

  ```
  wsk package bind /whisk.system/watson myWatson -p username 'MIO_NOMEUTENTE_WATSON' -p password 'MIA_PASSWORD_WATSON'
  ```
  {: pre}

2. Richiama l'azione `textToSpeech` nel tuo bind di pacchetto per convertire il testo.

  ```
  wsk action invoke myWatson/textToSpeech --blocking --result --param payload 'Hey.' --param voice 'en-US_MichaelVoice' --param accept 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```
  {
    "payload": "<base64 encoding of a .wav file>"
  }
  ```
  {: screen}


### Conversione da voce a testo

L'azione `/whisk.system/watson/speechToText` converte il discorso audio in testo. I parametri sono i seguenti:

- `username`: il nome utente della API Watson.
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
 
Di seguito è riportato un esempio di creazione di un bind di pacchetto e di una conversione da voce a testo.

1. Crea un bind di pacchetto con le tue credenziali Watson.

  ```
  wsk package bind /whisk.system/watson myWatson -p username 'MIO_NOMEUTENTE_WATSON' -p password 'MIA_PASSWORD_WATSON'
  ```
  {: pre}

2. Richiama l'azione `speechToText` nel tuo bind di pacchetto per convertire l'audio codificato.

  ```
  wsk action invoke myWatson/speechToText --blocking --result --param payload <base64 encoding of a .wav file> --param content_type 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```
  {
    "data": "Hello Watson"
  }
  ```
  {: screen}
  
 
## Utilizzo del pacchetto Slack
{: #openwhisk_catalog_slack}

Il pacchetto `/whisk.system/slack` offre un pratico modo per utilizzare le [API Slack](https://api.slack.com/).

Il pacchetto include le seguenti azioni:

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/slack` | pacchetto | url, channel, username | Interagire con la API Slack |
| `/whisk.system/slack/post` | azione | text, url, channel, username | Pubblicare un messaggio su un canale Slack |

Anche se non è obbligatorio, ti consigliamo di creare un bind di pacchetto con i valori `username`, `url` e 'channel'. Con il bind, non dovrai specificare i valori ogni volta che richiami l'azione nel pacchetto.

### Pubblicazione di un messaggio in un canale Slack

L'azione `/whisk.system/slack/post` pubblica un messaggio in uno specifico canale Slack. I parametri sono i seguenti:

- `url`: l'URL del webhook Slack.
- `channel`: il canale Slack nel quale pubblicare il messaggio.
- `username`: il nome con il quale pubblicare il messaggio.
- `text`: un messaggio da pubblicare.

Il seguente è un esempio di configurazione di Slack, creazione di un bind di pacchetto e pubblicazione di un messaggio in un canale.

1. Configura un [webhook in entrata](https://api.slack.com/incoming-webhooks) Slack per il tuo team.

  Dopo che Slack è stato configurato, dovresti ottenere un URL Webhook simile al seguente `https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`. Ti servirà nel prossimo passo.

2. Crea un bind di pacchetto con le tue credenziali Slack, il canale in cui vuoi pubblicare il messaggio e il nome utente con il quale vuoi farlo.

  ```
  wsk package bind /whisk.system/slack mySlack --param url 'https://hooks.slack.com/services/...' --param username 'Bob' --param channel '#MySlackChannel'
  ```
  {: pre}

3. Richiama l'azione `post` nel tuo bind di pacchetto per pubblicare un messaggio nel canale Slack.

  ```
  wsk action invoke mySlack/post --blocking --result --param text 'Salve da OpenWhisk!'
  ```
  {: pre}


## Utilizzo del pacchetto GitHub
{: #openwhisk_catalog_github}

Il pacchetto `/whisk.system/github` offre un pratico modo per utilizzare le [API GitHub](https://developer.github.com/).

Il pacchetto include il seguente feed:

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/github` | pacchetto | username, repository, accessToken | Interagire con la API GitHub |
| `/whisk.system/github/webhook` | feed | events, username, repository, accessToken | Attivare gli eventi di trigger in caso di attività GitHub |

Anche se non è obbligatorio, ti consigliamo di creare un bind di pacchetto con i valori `username`, `repository` e `accessToken`.  Con il bind, non dovrai specificare i valori ogni volta che usi il feed nel pacchetto.

### Attivazione di un evento di trigger in caso di attività GitHub

Il feed `/whisk.system/github/webhook` configura un servizio per attivare un trigger in caso di attività in uno specifico repository GitHub. I parametri sono i seguenti:

- `username`: il nome utente del repository GitHub.
- `repository`: Il repository GitHub.
- `accessToken`: il tuo token di accesso personale GitHub. Quando [crei il tuo token](https://github.com/settings/tokens), assicurati di selezionare gli ambiti repo:status e public_repo. Assicurati inoltre di non avere di Webhook già definiti per il tuo repository.
- `events`: il [tipo di evento GitHub](https://developer.github.com/v3/activity/events/types/) a cui sei interessato.

Il seguente è un esempio di creazione di un trigger che verrà attivato ogni volta che viene eseguito un nuovo commit in un repository GitHub.

1. Genera un [token di accesso personale](https://github.com/settings/tokens) GitHub.

  Il token di accesso verrà utilizzato nel prossimo passo.

2. Crea un bind di pacchetto configurato per il tuo repository GitHub e con il tuo token di accesso.

  ```
  wsk package bind /whisk.system/github myGit --param username myGitUser --param repository myGitRepo --param accessToken aaaaa1111a1a1a1a1a111111aaaaaa1111aa1a1a
  ```
  {: pre}

3. Crea un trigger per il tipo di evento `push` di GitHub utilizzando il tuo feed `myGit/webhook`.

  ```
  wsk trigger create myGitTrigger --feed myGit/webhook --param events push
  ```
  {: pre}

Un commit al repository Github tramite un `git push` causerà l'attivazione del trigger dal webhook. Se è presente una regola che corrisponde al trigger, sarà richiamata l'azione associata.
L'azione riceve il payload del webhook Github come parametro di input. Ogni evento webhook Github ha uno schema JSON simile ma un oggetto payload univoco che è determinato dal proprio tipo di evento.
Per ulteriori informazioni sul contenuto del payload consulta la documentazione API [Github events and payload](https://developer.github.com/v3/activity/events/types/).


## Utilizzo del pacchetto Push
{: #openwhisk_catalog_pushnotifications}

Il pacchetto `/whisk.system/pushnotifications` ti consente di lavorare con un servizio push. 

Il pacchetto include il seguente feed:

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/pushnotifications` | pacchetto | appId, appSecret  | Lavorare con il servizio push |
| `/whisk.system/pushnotifications/sendMessage` | azione | text, url, deviceIds, platforms, tagNames, apnsBadge, apnsCategory, apnsActionKeyTitle, apnsSound, apnsPayload, apnsType, gcmCollapseKey, gcmDelayWhileIdle, gcmPayload, gcmPriority, gcmSound, gcmTimeToLive | Invia una notifica push ai dispositivi specificati. |
| `/whisk.system/pushnotifications/webhook` | feed | events | Attiva gli eventi trigger sulle attività del dispositivo (registrazione(annullamento della registrazione del dispositivo) / sottoscrizione(annullamento della sottoscrizione)) sul servizio push |
Anche se non è obbligatorio, ti consigliamo di creare un bind di pacchetto con i valori `appId` e `appSecret`. In questo modo, non dovrai specificare queste credenziali ogni volta che richiami le azioni nel pacchetto.

### Configurazione del pacchetto IBM Push Notifications

Durante la creazione di un pacchetto IBM Push Notifications devi fornire i seguenti parametri,

-  `appId`: il GUID dell'applicazione Bluemix.
-  `appSecret`: l'appSecret del servizio di notifica push Bluemix.

Il seguente è un esempio di creazione di un bind di pacchetto.

1. Crea un'applicazione Bluemix nel [Dashboard Bluemix](http://console.ng.bluemix.net).

2. Inizializza il servizio di notifica push ed esegui il bind del servizio all'applicazione Bluemix.

3. Configura l'[applicazione IBM Push Notification](https://console.ng.bluemix.net/docs/services/mobilepush/index.html).

  Assicurati di ricordare il `GUID applicazione` e il `Segreto applicazione` dell'applicazione Bluemix che hai creato.


4. Crea un bind al pacchetto con `/whisk.system/pushnotifications`.

  ```
  wsk package bind /whisk.system/pushnotifications myPush -p appId "myAppID" -p appSecret "myAppSecret"
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

L'azione `/whisk.system/pushnotifications/sendMessage` invia notifiche push ai dispositivi registrati. I parametri sono i seguenti:
- `text` - il messaggio della notifica da mostrare all'utente. Esempio: -p text "Hi ,{{site.data.keyword.openwhisk}} send a notification".
- `url`: un URL facoltativo che può essere inviato con l'avviso. Esempio: -p url "https:\\www.w3.ibm.com".
- `gcmPayload` - il payload JSON personalizzato che sarà inviato come parte del messaggio di notifica. Esempio: -p gcmPayload "{"hi":"hello"}"
- `gcmSound` - il file audio (sul dispositivo) che tenterà di essere eseguito quando la notifica arriva al dispositivo.
- `gcmCollapseKey` - questo parametro identifica un gruppo di messaggi
- `gcmDelayWhileIdle` - quando questo parametro è impostato su true, indica che il messaggio non può essere inviato finché il dispositivo non diventa attivo.
- `gcmPriority` - imposta la priorità del messaggio.
- `gcmTimeToLive` - questo parametro specifica il tempo (in secondi) in cui il messaggio viene conservato nell'archivio GCM se il dispositivo è offline.
- `apnsBadge` - il numero da visualizzare come badge dell'icona dell'applicazione.
- `apnsCategory` -  l'identificativo della categoria da utilizzare per le notifiche push interattive.
- `apnsIosActionKey` - il titolo per la chiave azione.
- `apnsPayload` - il payload JSON personalizzato che sarà inviato come parte del messaggio di notifica. 
- `apnsType` - ['DEFAULT', 'MIXED', 'SILENT'].
- `apnsSound` - il nome del file audio nel bundle dell'applicazione. L'audio di questo file viene riprodotto come un avviso.

Questo è un esempio di invio di una notifica push dal pacchetto pushnotification.

1. Invia la notifica push utilizzando l'azione `sendMessage` nel bind di pacchetto che hai precedentemente creato. Accertati di sostituire `/myNamespace/myPush` con il tuo nome pacchetto.

  ```
  wsk action invoke /myNamespace/myPush/sendMessage --blocking --result  -p url https://example.com -p text "this is my message"  -p sound soundFileName -p deviceIds '["T1","T2"]'
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

### Attivazione di un evento di trigger per l'attività del servizio IBM Push Notifications

`/whisk.system/pushnotifications/webhook` configura il servizio IBM Push Notifications per attivare un trigger quando è presente un'attività come la registrazione / l'annullamento della registrazione del dispositivo o la sottoscrizione / annullamento della sottoscrizione in un'applicazione specificata

I parametri sono i seguenti:

- `appId:` l'appSecret del servizio di notifica push Bluemix.
- `appSecret:` il GUID dell'applicazione Bluemix.
- `events:` gli eventi supportati sono `onDeviceRegister`, `onDeviceUnregister`, `onDeviceUpdate`, `onSubscribe`, `onUnsubscribe`.Per ricevere notifiche da tutti gli eventi utilizzare il carattere jolly `*`.

Il seguente è un esempio di creazione di un trigger che verrà attivato ogni volta che viene registrato un nuovo dispositivo con l'applicazione del servizio IBM Push Notifications.

1. Crea un bind di pacchetto configurato per il tuo servizio IBM Push Notifications con il tuo appId e appSecret.

  ```
  wsk package bind /whisk.system/pushnotifications myNewDeviceFeed --param appID myapp --param appSecret myAppSecret --param events onDeviceRegister
  ```
  {: pre}

2. Crea un trigger per il tipo di evento `onDeviceRegister` del servizio IBM Push Notifications utilizzando il tuo feed `myPush/webhook`.

  ```
  wsk trigger create myPushTrigger --feed myPush/webhook --param events onDeviceRegister
  ```
  {: pre}
