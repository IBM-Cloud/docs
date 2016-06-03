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
| `/whisk.system/cloudant/changes` | feed | dbname, includeDoc | Attivare degli eventi di trigger in caso di modifiche a un database |

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

Puoi utilizzare il feed `changes` per configurare un servizio per attivare un trigger ogni volta che viene apportata una modifica al tuo database Cloudant.

1. Crea un trigger con il feed `changes` nel bind di pacchetto che hai creato precedentemente. Accertati di sostituire `/myNamespace/myCloudant` con il tuo nome pacchetto.

```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb --param includeDocs true
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

**Nota**: se non se in grado di osservare le nuove attivazioni, consulta le sezioni successive relative alla lettura da, e alla scrittura in, un database Cloudant. Verificare i passi relativi alla lettura e alla scrittura qui di seguito aiuterà a verificare che le tue credenziali Cloudant siano corrette.

Puoi ora creare le regole e associarle alle azioni per reagire agli aggiornamenti dei documenti.

Il contenuto degli eventi generati dipende dal valore del parametro `includeDocs` quando si crea il trigger. Se è impostato su true, ogni evento di trigger che viene attivato include il documento Cloudant modificato. Considera, ad esempio, il seguente documento modificato:

```
  {
    "_id": "6ca436c44074c4c2aa6a40c9a188b348",
    "_rev": "3-bc4960fc13aa368afca8c8427a1c18a8",
    "name": "Heisenberg"
  }
```
  {: screen}

Il codice in questo esempio genera un evento di trigger con i parametri `_id`, `_rev` e `name` corrispondenti. In effetti, la rappresentazione JSON dell'evento di trigger è identica al documento.

Altrimenti, se `includeDocs` è false, gli eventi includono i seguenti parametri:

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
  response:
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
| `/whisk.system/alarms` | package | - | Programma di utilità per gli avvisi e la periodicità |
| `/whisk.system/alarms/alarm` | feed | cron, trigger_payload, maxTriggers | Attivare l'evento di trigger periodicamente |


### Attivazione di un evento di trigger periodicamente

Il feed `/whisk.system/alarms/alarm` configura il servizio Alarm per attivare un evento di trigger con una specifica frequenza. I parametri sono i seguenti:

- `cron`: una stringa, basata sulla sintassi crontab Unix, che indica quando attivare il trigger in UTC (Coordinated Universal Time). La stringa è una sequenza di sei campi separati da spazi: `X X X X X X `. Per ulteriori dettagli sull'utilizzo della sintassi cron, consulta: https://github.com/ncb000gt/node-cron.

- `trigger_payload`: il valore di questo parametro diventa il contenuto del trigger ogni volta che il trigger viene attivato.

- `maxTriggers`: arrestare l'attivazione dei trigger quando viene raggiunto questo limite. Il valore predefinito è 1000.

Il seguente è un esempio di creazione di un trigger che verrà attivato una volta ogni 20 secondi con i valori `name` e `place` nell'evento di trigger.

```
  wsk trigger create periodic --feed /whisk.system/alarms/alarm --param cron '/20 * * * * *' --param trigger_payload '{"name":"Odin","place":"Asgard"}'
```
  {: pre}

Ogni evento generato includerà come parametri le proprietà specificate nel valore `trigger_payload`. In questo caso, ogni evento di trigger avrà i parametri `name=Odin` e `place=Asgard`.


## Utilizzo del pacchetto Weather
{: #openwhisk_catalog_weather}

Il pacchetto `/whisk.system/weather` offre un pratico modo per richiamare la API di The Weather Company.

Il pacchetto include la seguente azione.

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/weather` | pacchetto | apiKey | Servizi dalla The Weather Company |
| `/whisk.system/weather/forecast` | azione | apiKey, latitude, longitude | Previsioni meteo a 10 giorni di Weather.com |

Anche se non è obbligatorio, ti consigliamo di creare un bind di pacchetto con il valore `apiKey`. In questo modo non dovrai specificare la chiave ogni volta che richiami le azioni nel pacchetto.

### Come ottenere una previsione meteo per una località

L'azione `/whisk.system/weather/forecast` restituisce una previsione meteo a 10 giorni per una località richiamando una API dalla The Weather Company. I parametri sono i seguenti:

- `apiKey`: una chiave API per la The Weather Company autorizzata a richiamare la API di previsione meteo a 10 giorni.
- `latitude`: l coordinata della latitudine della località.
- `longitude`: La coordinata della longitudine della località.

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
- `events`: il [tipo di attività GitHub](https://developer.github.com/v3/activity/events/types/) a cui sei interessato.

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

