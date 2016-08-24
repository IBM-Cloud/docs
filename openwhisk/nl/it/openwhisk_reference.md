---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock:.codeblock}
{:screen:.screen}
{:pre: .pre}

# Dettagli del sistema {{site.data.keyword.openwhisk_short}}
{: #openwhisk_reference}
*Ultimo aggiornamento: 14 aprile 2016*
{: .last-updated}

Le seguenti sezioni forniscono ulteriori dettagli sul sistema {{site.data.keyword.openwhisk}}.
{: shortdesc}

## Entità di {{site.data.keyword.openwhisk_short}}
{: #openwhisk_entities}

### Spazi dei nomi e pacchetti

Azioni, trigger e regole {{site.data.keyword.openwhisk_short}} appartengono a uno spazio dei nomi e, facoltativamente, a un pacchetto.

I pacchetti possono contenere azioni e feed. Un pacchetto non può contenerne un altro, pertanto la nidificazione dei pacchetti non è consentita. Inoltre, le entità non devono essere contenute in un pacchetto.

In Bluemix, uno spazio dei nomi {{site.data.keyword.openwhisk_short}} corrisponde a una coppia organizzazione/spazio. Ad esempio, l'organizzazione `BobsOrg` e lo spazio `dev` corrisponderebbero allo spazio dei nomi {{site.data.keyword.openwhisk_short}} `/BobsOrg_dev`.

Se autorizzato, puoi creare il tuo spazio dei nomi personale. Lo spazio dei nomi `/whisk.system` è riservato alle entità distribuite con il sistema {{site.data.keyword.openwhisk_short}}.


### Nomi completi

Il nome completo di un'entità è
`/nomeSpazioNomi[/nomePacchetto]/nomeEntità`. Nota che `/` viene utilizzato per delimitare
gli spazi dei nomi, i pacchetti e le entità. Inoltre, gli spazi dei nomi devono essere preceduti da un `/`.

Per comodità, lo spazio dei nomi può essere tralasciato se è lo *spazio dei nomi predefinito*
dell'utente.

Ad esempio, considera un utente il cui spazio dei nomi predefinito è `/myOrg`. Di seguito
sono riportati esempi di nomi completi di una serie di entità e i rispettivi alias.

| Nome completo | Alias | Spazio dei nomi | Pacchetto | Nome |
| --- | --- | --- | --- | --- |
| `/whisk.system/cloudant/read` |  | `/whisk.system` | `cloudant` | `read` |
| `/myOrg/video/transcode` | `video/transcode` | `/myOrg` | `video` | `transcode` |
| `/myOrg/filter` | `filter` | `/myOrg` |  | `filter` |

Userai questo schema di denominazione quando utilizzi, ad esempio, la CLI {{site.data.keyword.openwhisk_short}}.

### Nomi delle entità

I nomi di tutte le entità, inclusi azioni, trigger, regole, pacchetti e spazi dei nomi, sono una sequenza di caratteri aventi il seguente formato:

* Il primo carattere deve essere un carattere alfanumerico, una cifra o un carattere di sottolineatura.
* I caratteri successivi possono essere alfanumerici, cifre, spazi o i seguenti: `_`, `@`, `.`, `-`.
* L'ultimo carattere non può essere uno spazio.

Più precisamente, un nome deve corrispondere alla seguente espressione regolare (indicata utilizzando la sintassi metacharacter Java): `\A([\w]|[\w][\w@ .-]*[\w@.-])\z`.


## Semantica delle azioni
{: #openwhisk_semantics}

Le seguenti sezioni forniscono informazioni dettagliate sulle azioni {{site.data.keyword.openwhisk_short}}.

### Assenza di stato

Le implementazioni delle azioni devono essere senza stato o *idempotenti*. Mentre il sistema non applica questa proprietà, non vi è alcuna garanzia che qualsiasi stato gestito da un'azione sia disponibile tra le chiamate.

Inoltre, potrebbero esistere più creazioni di istanze di un'azione, ciascuna delle quali con il proprio stato. La chiamata di un'azione potrebbe essere inviata a una qualsiasi di queste creazioni di istanze.

### Input e output delle chiamate

L'input da/l'output verso un'azione costituiscono un dizionario di coppie chiave/valore. La chiave è una stringa e il valore è un valore JSON valido.

### Ordinamento delle chiamate delle azioni
{: #openwhisk_ordering}

Le chiamate di un'azione non sono ordinate. Se l'utente richiama un'azione due volte dalla riga di comando o dall'API REST, la seconda chiamata potrebbe essere eseguita prima della precedente. Se le azioni hanno effetti secondari, questi potrebbero essere osservati in qualsiasi ordine.

Inoltre, non vi è alcuna garanzia che le azioni vengano eseguire automaticamente. Due azioni possono essere eseguite contemporaneamente e avere effetti secondari interfoliati.  OpenWhisk non garantisce uno specifico modello di coerenza simultanea per gli effetti secondari. Qualsiasi effetto secondario dipenderà dall'implementazione.

### Semantica at most once
{: #openwhisk_atmostonce}

Il sistema supporta la chiamata at most one di azioni.

Alla ricezione di una richiesta di chiamata, il sistema registra la richiesta e
invia un'attivazione.

Il sistema restituisce un ID di attivazione (in caso di chiamata non bloccante) per
confermare la ricezione della chiamata. Nota che anche in assenza di
tale risposta (dovuta, ad esempio, all'interruzione di una connessione di rete), è possibile
che la chiamata sia stata ricevuta.

Il sistema tenta di richiamare l'azione una volta, ottenendo uno dei quattro seguenti risultati:
- *success*: la chiamata dell'azione è stata completata correttamente.
- *application error*: la chiamata dell'azione è stata eseguita correttamente, ma l'azione ha restituito un valore di errore sullo scopo, ad esempio perché non è stata soddisfatta una precondizione sugli argomenti.
- *action developer error*: l'azione è stata richiamata, ma è stata completata in maniera anomala; ad esempio, l'azione non ha colto un'eccezione o era presente un errore di sintassi.
- *whisk internal error*: il sistema non è stato in grado di richiamare l'azione.
Il risultato viene registrato nel campo `stato` del record di attivazione, come illustrato in una delle seguenti sezioni.

Per ogni chiamata ricevuta correttamente, e che potrebbe
essere addebitata all'utente, ci sarà infine un record di attivazione.


## Record di attivazione
{: #openwhisk_ref_activation}

Ogni chiamata di un'azione e ogni trigger che attiva risultati in un record di attivazione.

Un record di attivazione contiene i seguenti campi:

- *activationId*: l'ID dell'attivazione.
- *start* e *end*: data/ora di inizio e fine dell'attivazione. I valori sono espressi nel [formato temporale UNIX](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap04.html#tag_04_15).
- *namespace* e `nome`: lo spazio dei nomi e il nome dell'entità.
- *logs*: un array di stringhe con i log prodotti dall'azione durante la sua attivazione. Ogni elemento dell'array corrisponde a un riga di output emessa dall'azione in stdout o stderr e include il tempo e il flusso dell'output del log. La struttura è la seguente: ```TIMESTAMP STREAM: LOG_OUTPUT```.
- *response*: un dizionario che definisce le chiavi `success`, `status` e `result`:
  - *status*: il risultato dell'attivazione, che può assumere uno dei seguenti valori: "success", "application error", "action developer error", "whisk internal error".
  - *success*: è `true` se, e solo se, lo stato è `"success"`
- *result*: un dizionario che contiene il risultato dell'attivazione. Se l'attivazione è stata eseguita correttamente, contiene il valore restituito dall'azione. Se l'attivazione non è stata eseguita correttamente, `result` contiene sicuramente la chiave `error`, generalmente accompagnata da una spiegazione dell'errore.


## Azioni JavaScript
{: #openwhisk_ref_javascript}

### Prototipo della funzione

Azioni JavaScript {{site.data.keyword.openwhisk_short}} eseguite in un runtime Node.js, attualmente alla versione 0.12.9.

Le azioni scritte in JavaScript devono essere circoscritte in un unico file. Tale file può contenere più funzioni, ma per convenzione deve essere presente una funzione denominata `main`, che è quella richiamata con l'azione. Segue un esempio di azione con più funzioni.

```
function main() {
    return { payload: helper() }
}

function helper() {
    return new Date();
}
```
{: codeblock}

I parametri di input dell'azione vengono trasmessi come oggetto JSON come parametri della funzione `main`. Il risultato di un'attivazione eseguita correttamente è anch'esso un oggetto JSON, che viene tuttavia restituito in modo differente a seconda che l'azione sia sincrona o asincrona, come descritto nella seguente sezione.


### Funzionamento sincrono e asincrono

Le funzioni JavaScript proseguono comunemente la loro esecuzione in una funzione di callback anche dopo che vengono restituite. Per risolvere questo problema, l'attivazione di un'azione JavaScript può essere *sincrona* o *asincrona*.

Un'attivazione dell'azione JavaScript è **sincrona** se la funzione principale termina in una delle seguenti condizioni:

- La funzione principale termina senza eseguire un'istruzione ```return```.
- La funzione principale termina con l'esecuzione di un'istruzione ```return``` che restituisce ogni valore *eccetto* ```whisk.async()```.

Seguono due esempi di azioni sincrone.

```
// un'azione sincrona
function main() {
  return {payload: 'Hello, World!'};
}
```
{: codeblock}

```
// un'azione in cui ciascun percorso comporta un'attivazione sincrona
function main(params) {
  if (params.payload == 0) {
     return;
  } else if (params.payload == 1) {
     return whisk.done();    // indicate un completamento normale
  } else if (params.payload == 2) {
    return whisk.error();   // indica un completamento anomalo
  }
}
```
{: codeblock}

Un'attivazione dell'azione JavaScript è **asincrona** se la funzione principale termina richiamando ```return whisk.async();```.  In questo caso, il sistema presuppone che l'azione sia ancora in esecuzione, finché essa non esegue:
- ```return whisk.done();```
- ```return whisk.error();```

Di seguito è riportato un esempio di azione eseguita in modo asincrono.

```
function main() {
    setTimeout(function() {
        return whisk.done({done: true});
    }, 100);
    return whisk.async();
}
```
{: codeblock}

Un'azione può essere sincrona rispetto ad alcuni input e asincrona rispetto ad altri. Segue un esempio.

```
  function main(params) {
      if (params.payload) {
         setTimeout(function() {
            return whisk.done({done: true});
         }, 100);
         return whisk.async();  // attivazione asincrona
      }  else {
         return whisk.done();   // attivazione sincrona
      }
  }
```
{: codeblock}

- In questo caso, la funzione `main` dovrà restituire `whisk.async()`. Quando il risultato dell'attivazione è disponibile, la funzione `whisk.done()` deve essere richiamata con il risultato trasmesso come oggetto JSON. Questo tipo di attivazione viene detto *asincrono*.

Nota che indipendentemente dal fatto che un'attivazione sia sincrona o asincrona, la chiamata dell'azione può essere bloccante o non bloccante.

### Ulteriori metodi SDK

La funzione `whisk.invoke()` richiama un'altra azione. Essa prende come argomento un dizionario che definisce i seguenti parametri:

- *name*: il nome completo dell'azione da richiamare,
- *parameters*: un oggetto JSON che rappresenta l'input dell'azione richiamata. Se omesso, il valore predefinito è un oggetto vuoto.
- *apiKey*: la chiave di autorizzazione con cui richiamare l'azione. Il valore predefinito è `whisk.getAuthKey()`.
- *blocking*: indica se l'azione deve essere richiamata in modalità bloccante o non bloccante. Il valore predefinito è `false`, che indica una chiamata non bloccante.
- *next*: una funzione di callback facoltativa da eseguire al completamento della chiamata.

La firma per `next` è `function(error, activation)`, dove:

- `error` è `false` se la chiamata è stata eseguita correttamente o truthy se ha avuto esito negativo; di norma una stringa descrive l'errore.
- In caso di errori, a seconda della modalità di errore, `activation` può non essere definito.
- Se definito, `activation` è un dizionario con i seguenti campi:
  - *activationId*: l'ID attivazione:
  - *result*: se l'azione è stata richiamata in modalità bloccante, il risultato dell'azione è un oggetto JSON, altrimenti è `undefined`.

La funzione `whisk.trigger()` attiva un trigger. Prende come argomento un oggetto JSON con i seguenti parametri:

- *name*: il nome completo del trigger da richiamare.
- *parameters*: un oggetto JSON che rappresenta l'input del trigger. Se omesso, il valore predefinito è un oggetto vuoto.
- *apiKey*: la chiave di autorizzazione con cui attivare il trigger. Il valore predefinito è `whisk.getAuthKey()`.
- *next*: una callback facoltativo da eseguire al completamento dell'attivazione.

La firma per `next` è `function(error, activation)`, dove:

- `error` è `false` se l'attivazione è stata eseguita correttamente o truthy se ha avuto esito negativo; di norma una stringa descrive l'errore.
- In caso di errori, a seconda della modalità di errore, `activation` può non essere definito.
- Se definito, `activation` è un dizionario con un campo `activationId` contenente l'ID di attivazione.

La funzione `whisk.getAuthKey()` restituisce la chiave di autorizzazione con cui viene eseguita l'azione. Di solito, non serve richiamare questa funzione direttamente, poiché viene utilizzato implicitamente dalle funzioni `whisk.invoke()` e `whisk.trigger()`.

### Ambiente runtime
{: #openwhisk_ref_runtime_environment}

Le azioni JavaScript vengono eseguite in un ambiente Node.js versione 0.12.14 con i seguenti pacchetti utilizzabili dall'azione:

- apn
- async
- body-parser
- btoa
- cheerio
- cloudant
- commander
- consul
- cookie-parser
- cradle
- errorhandler
- express
- express-session
- gm
- jade
- log4js
- unire
- moment
- mustache
- nano
- node-uuid
- oauth2-server
- process
- request
- rimraf
- semver
- serve-favicon
- socket.io
- socket.io-client
- superagent
- swagger-tools
- tmp
- watson-developer-cloud
- when
- ws
- xml2js
- xmlhttprequest
- yauzl


## Azioni Docker
{: #openwhisk_ref_docker}

Le azioni Docker eseguono un file binario fornito dall'utente in un contenitore Docker. Il file binario viene eseguito in un'immagine Docker basata su Ubuntu 14.04 LTD, perciò il file binario deve essere compatibile con questa distribuzione.

Il parametro "payload" di input dell'azione viene trasmesso al programma binario come argomento posizionale e l'output standard dell'esecuzione del programma viene restituito nel parametro "result".

La struttura di base Docker può essere opportunamente utilizzata per la creazione di immagini Docker compatibili con {{site.data.keyword.openwhisk_short}}. Puoi installare la struttura di base con il comando CLI `wsk sdk install docker`.

Il programma binario principale deve essere copiato sul file `dockerSkeleton/client/action`. Qualsiasi libreria o file complementare può risiedere nella directory `dockerSkeleton/client`.

Puoi anche includere qualsiasi procedura di compilazione o dipendenza modificando il `dockerSkeleton/Dockerfile`. Ad esempio, se la tua azione è uno script Python, puoi installare Python.


## API REST
{: #openwhisk_ref_restapi}

Tutte le funzionalità del sistema sono disponibili tramite API REST. Sono presenti endpoint di raccolta e di entità per le azioni, i trigger, le regole, i pacchetti, le attivazioni e gli spazi dei nomi.

Gli endpoint di raccolta sono:

- `https://{BASE URL}/api/v1/namespaces`
- `https://{BASE URL}/api/v1/namespaces/{namespace}/actions`
- `https://{BASE URL}/api/v1/namespaces/{namespace}/triggers`
- `https://{BASE URL}/api/v1/namespaces/{namespace}/rules`
- `https://{BASE URL}/api/v1/namespaces/{namespace}/packages`
- `https://{BASE URL}/api/v1/namespaces/{namespace}/activations`

`{BASE URL}` è il nome host API OpenWhisk (ad es. openwhisk.ng.bluemix.net, 172.17.0.1, ecc..)

Per `{namespace}` può essere utilizzato il carattere `_` per specificare lo *spazio dei nomi
predefinito* dell'utente (ad es. l'indirizzo email)

Puoi effettuare una richiesta GET sugli endpoint di raccolta per richiamare un elenco di entità della raccolta.

Sono presenti endpoint per ciascun tipo di entità:

- `https://{BASE URL}/api/v1/namespaces/{namespace}`
- `https://{BASE URL}/api/v1/namespaces/{namespace}/actions/[{packageName}/]{actionName}`
- `https://{BASE URL}/api/v1/namespaces/{namespace}/triggers/{triggerName}`
- `https://{BASE URL}/api/v1/namespaces/{namespace}/rules/{ruleName}`
- `https://{BASE URL}/api/v1/namespaces/{namespace}/packages/{packageName}`
- `https://{BASE URL}/api/v1/namespaces/{namespace}/activations/{activationName}`

Gli endpoint namespace e activation supportano solo richieste GET. Gli endpoint actions, triggers, rules e packages supportano richieste GET, PUT e DELETE. Gli endpoint actions, triggers e rules supportano richieste POST, che vengono utilizzate per richiamare le azioni e i trigger e abilitare o disabilitare le regole. Per informazioni dettagliate, consulta la [Guida di riferimento API](https://new-console.{DomainName}/apidocs/98).

Tutte le API sono protette tramite autenticazione base HTTP. Le credenziali per l'autenticazione di base si trovano nella proprietà `AUTH` del tuo file `~/.wskprops` e sono delimitate dai due punti. Puoi richiamarle anche nella [procedura di configurazione della CLI](../README.md#setup-cli).

Di seguito viene riportato un esempio che utilizza il comando cURL per ottenere un elenco di tutti i pacchetti dello spazio dei nomi `whisk.system`:

```
curl -u USERNAME:PASSWORD https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/packages
```
{: pre}
```
[
  {
    "name": "slack",
    "binding": false,
    "publish": true,
    "annotations": [
      {
        "key": "description",
        "value": "Package which contains actions to interact with the Slack messaging service"
      }
    ],
    "version": "0.0.9",
    "namespace": "whisk.system"
  },
  ...
]
```
{: screen}

L'API OpenWhisk supporta chiamate di richiesta-risposta dai client web. OpenWhisk risponde alle richieste `OPTIONS` con le intestazione Cross-Origin Resource Sharing. Al momento, sono consentite tutte le origini (ad es., Access-Control-Allow-Origin è "`*`") e Access-Control-Allow-Headers produce Authorization and Content-Type.

**Visto che OpenWhisk supporta al momento solo una chiave per account, ti raccomandiamo di utilizzare CORS al di fuori degli esperimenti semplici. La tua chiave ha bisogno di essere integrata nel codice del lato client rendendola visibile al pubblico. Utilizzarla con cautela.**

## Limiti di sistema
{: #openwhisk_syslimits}

{{site.data.keyword.openwhisk_short}} ha dei limiti di sistema, tra cui la quantità di memoria utilizzata da un'azione e il numero di chiamate di azioni consentite per ciascuna ora. La seguente tabella elenca i limiti predefiniti.

| limite | descrizione | configurabile | unità | valore predefinito |
| ----- | ----------- | ------------ | -----| ------- |
| timeout | un contenitore non può essere eseguito per più di N millisecondi | per azione |  millisecondi | 60000 |
| memory | a un contenitore non possono essere assegnati più di N MB di memoria | per azione | MB | 256 |
| concurrent | non può avere più di N attivazioni contemporanee per spazio dei nomi | per spazio dei nomi | numero | 100 |
| minuteRate | un utente non può richiamare un numero di azioni al minuto superiore a questo | per utente | numero | 120 |
| hourRate | un utente non può richiamare un numero di azioni all'ora superiore a questo | per utente | numero | 3600 |

### Timeout per azione (ms) (valore predefinito: 60 secondi)
* Il limite di timeout N è compreso nell'intervallo [100 ms - 300000 ms] ed è impostato per azione in millisecondi.
* L'utente può modificare il limite durante la creazione dell'azione.
* Un contenitore in esecuzione per più di N millisecondi viene terminato.

### Memoria per azione (MB) (valore predefinito: 256 MB)
* Il limite di memoria M è compreso nell'intervallo [128 MB - 512 MB] ed è impostato per ciascuna azione in MB.
* L'utente può modificare il limite durante la creazione dell'azione.
* A un contenitore non può essere assegnata una quantità di memoria superiore al limite.

### Risorsa per azione (MB) (valore fisso: 1MB)
* La dimensione del codice massima per l'azione è 1MB.
* Per un'azione Java ti raccomandiamo di utilizzare uno strumento per concatenare tutto il codice di origine incluse le dipendenze in un singolo file di bundle.

### Dimensione payload di attivazione (MB) (valore fisso: 1MB)
* La dimensione del contenuto POST massima più tutti i parametri sottoposti a currying per la chiamata di un'azione o l'attivazione di un trigger è 1MB.

### Chiamata simultanea per lo spazio dei nomi (valore predefinito: 100)
* Il numero di attivazioni attualmente elaborate per uno spazio dei nomi non essere maggiore di 100.
* Il limite predefinito può essere configurato statisticamente da Whisk in consul kvstore.
* L'utente non può attualmente modificare questi limiti.

### Chiamate al minuto/all'ora (valore fisso: 120/3600)
* Il limite di frequenza N è impostato su 120/3600 e limita il numero di chiamate di azioni possibili in un'unica finestra temporale espressa in minuti/ore.
* L'utente non può modificare questo limite durante la creazione dell'azione.
* Una chiamata CLI che superi questo limite riceverà un codice di errore corrispondente a TOO_MANY_REQUESTS.

### Numero limite dei file aperti dall'azione Docker (valore fisso: 64:64)
* Il numero massimo di file aperti è 64 (si applica sia ai limiti hard che soft).
* Il comando docker run utilizza l'argomento `--ulimit nofile=64:64`.
* Per ulteriori informazioni sul numero limite di file aperti consulta la documentazione [docker run](https://docs.docker.com/engine/reference/commandline/run).

### Numero limite del numero di processi dell'azione Docker (valore fisso: 512:512)
* Il numero massimo di processi disponibili per un utente è 512 (si applica sia ai limiti hard che soft).
* Il comando docker run utilizza l'argomento `--ulimit nproc=512:512`.
* Per ulteriori informazioni sul numero limite di processi consulta la documentazione [docker run](https://docs.docker.com/engine/reference/commandline/run).
