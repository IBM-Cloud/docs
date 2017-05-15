---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-24"

---

{:shortdesc: .shortdesc}
{:codeblock:.codeblock}
{:screen:.screen}
{:pre: .pre}

# Dettagli del sistema {{site.data.keyword.openwhisk_short}}
{: #openwhisk_reference}


Le seguenti sezioni forniscono ulteriori dettagli sul sistema {{site.data.keyword.openwhisk}}.
{: shortdesc}

## Entità di {{site.data.keyword.openwhisk_short}}
{: #openwhisk_entities}

### Spazi dei nomi e pacchetti
{: #openwhisk_entities_namespaces}

Azioni, trigger e regole {{site.data.keyword.openwhisk_short}} appartengono a uno spazio dei nomi e, facoltativamente, a un pacchetto.

I pacchetti possono contenere azioni e feed. Un pacchetto non può contenerne un altro, pertanto la nidificazione dei pacchetti non è consentita. Inoltre, le entità non devono essere contenute in un pacchetto.

In Bluemix, uno spazio dei nomi {{site.data.keyword.openwhisk_short}} corrisponde a una coppia organizzazione/spazio. Ad esempio, l'organizzazione `BobsOrg` e lo spazio `dev` corrisponderebbero allo spazio dei nomi {{site.data.keyword.openwhisk_short}} `/BobsOrg_dev`.

Se autorizzato, puoi creare il tuo spazio dei nomi personale. Lo spazio dei nomi `/whisk.system` è riservato alle entità distribuite con il sistema {{site.data.keyword.openwhisk_short}}.


### Nomi completi
{: #openwhisk_entities_fullyqual}

Il nome completo di un'entità è
`/nomeSpazioNomi[/nomePacchetto]/nomeEntità`. Nota che `/` viene utilizzato per delimitare
gli spazi dei nomi, i pacchetti e le entità. Inoltre, gli spazi dei nomi devono essere preceduti da `/`.

Per praticità, lo spazio dei nomi può essere tralasciato se è lo  *spazio dei nomi predefinito* dell'utente.

Ad esempio, considera un utente il cui spazio dei nomi predefinito è `/myOrg`. Di seguito sono riportati esempi di nomi completi di una serie di entità e i rispettivi alias.

| Nome completo | Alias | Spazio dei nomi | Pacchetto | Nome |
| --- | --- | --- | --- | --- |
| `/whisk.system/cloudant/read` |  | `/whisk.system` | `cloudant` | `read` |
| `/myOrg/video/transcode` | `video/transcode` | `/myOrg` | `video` | `transcode` |
| `/myOrg/filter` | `filter` | `/myOrg` |  | `filter` |

Userai questo schema di denominazione quando utilizzi, ad esempio, la CLI {{site.data.keyword.openwhisk_short}}.

### Nomi delle entità
{: #openwhisk_entities_names}

I nomi di tutte le entità, inclusi azioni, trigger, regole, pacchetti e spazi dei nomi, sono una sequenza di caratteri aventi il seguente formato:

* Il primo carattere deve essere un carattere alfanumerico o un carattere di sottolineatura.
* I caratteri successivi possono essere alfanumerici, spazi o i seguenti: `_`, `@`, `.`, `-`.
* L'ultimo carattere non può essere uno spazio.

Più precisamente, un nome deve corrispondere alla seguente espressione regolare (indicata utilizzando la sintassi metacharacter Java): `\A([\w]|[\w][\w@ .-]*[\w@.-]+)\z`.


## Semantica delle azioni
{: #openwhisk_semantics}

Le seguenti sezioni forniscono informazioni dettagliate sulle azioni {{site.data.keyword.openwhisk_short}}.

### Assenza di stato
{: #openwhisk_semantics_stateless}

Le implementazioni delle azioni devono essere senza stato o *idempotenti*. Mentre il sistema non applica questa proprietà, non vi è alcuna garanzia che qualsiasi stato gestito da un'azione sia disponibile tra le chiamate.

Inoltre, potrebbero esistere più creazioni di istanze di un'azione, ciascuna delle quali con il proprio stato. La chiamata di un'azione potrebbe essere inviata a una qualsiasi di queste creazioni di istanze.

### Input e output delle chiamate
{: #openwhisk_semantics_invocationio}

L'input da/l'output verso un'azione costituiscono un dizionario di coppie chiave/valore. La chiave è una stringa e il valore è un valore JSON valido.

### Ordinamento delle chiamate delle azioni
{: #openwhisk_ordering}

Le chiamate di un'azione non sono ordinate. Se l'utente richiama un'azione due volte dalla riga di comando o dall'API REST, la seconda chiamata potrebbe essere eseguita per prima. Se le azioni hanno effetti secondari, questi potrebbero essere osservati in qualsiasi ordine.

Inoltre, non vi è alcuna garanzia che le azioni verranno eseguite automaticamente. Due azioni possono essere eseguite contemporaneamente e avere effetti secondari interfoliati. OpenWhisk non garantisce uno specifico modello di coerenza simultanea per gli effetti secondari. Qualsiasi effetto secondario dipenderà dall'implementazione.

### Garanzie di esecuzione dell'azione
{: #openwhisk_atmostonce}

Alla ricezione di una richiesta di chiamata, il sistema registra la richiesta e invia un'attivazione.

Il sistema restituisce un ID di attivazione (in caso di chiamata non bloccante) per confermare la ricezione della chiamata.
Nota che se si verifica un problema di rete o un altro errore che avviene prima di ricevere una risposta HTTP, è possibile
che {{site.data.keyword.openwhisk_short}} abbia ricevuto ed elaborato la richiesta.

Il sistema tenta di richiamare l'azione una volta, ottenendo uno dei quattro seguenti risultati:
- *success*: la chiamata dell'azione è stata completata correttamente.
- *application error*: la chiamata dell'azione è stata eseguita correttamente, ma l'azione ha restituito un valore di errore sullo scopo, ad esempio perché non è stata soddisfatta una precondizione sugli argomenti.
- *action developer error*: l'azione è stata richiamata, ma è terminata in modo anomalo; ad esempio l'azione non ha rilevato un'eccezione o era presente un errore di sintassi.
- *whisk internal error*: il sistema non è stato in grado di richiamare l'azione.
Il risultato viene registrato nel campo `stato` del record di attivazione, come illustrato in una delle seguenti sezioni.

Per ogni chiamata ricevuta correttamente, e che potrebbe
essere addebitata all'utente, ci sarà infine un record di attivazione.

Nota che in caso di un *action developer error*, è possibile che l'azione sia stata eseguita in modo parziale e che abbia generato degli effetti secondari
visibili esternamente.   È responsabilità dell'utente verificare che tali effetti secondari siano realmente avvenuti e, se necessario, immettere la logica per la
ripetizione dei tentativi.   Nota anche che alcuni *whisk internal error* indicheranno che un'azione ha avviato l'esecuzione ma
il sistema ha riscontrato un errore prima che l'azione registrasse il completamento.

## Record di attivazione
{: #openwhisk_ref_activation}

Ogni chiamata di un'azione e ogni trigger che attiva risultati in un record di attivazione.

Un record di attivazione contiene i seguenti campi:

- *activationId*: l'ID dell'attivazione.
- *start* e *end*: data/ora di inizio e fine dell'attivazione. I valori sono espressi nel [formato temporale UNIX](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap04.html#tag_04_15).
- *namespace* e `nome`: lo spazio dei nomi e il nome dell'entità.
- *logs*: un array di stringhe con i log prodotti dall'azione durante la sua attivazione. Ogni elemento dell'array corrisponde a un riga di output emessa dall'azione in `stdout` o `stderr` e include il tempo e il flusso dell'output del log. La struttura è la seguente: `TIMESTAMP STREAM: LOG_OUTPUT`.
- *response*: un dizionario che definisce le chiavi `success`, `status` e `result`:
  - *status*: il risultato dell'attivazione, che può assumere uno dei seguenti valori: "success", "application error", "action developer error", "whisk internal error".
  - *success*: è `true` se, e solo se, lo stato è `"success"`
- *result*: un dizionario che contiene il risultato dell'attivazione. Se l'attivazione è stata eseguita correttamente, contiene il valore restituito dall'azione. Se l'attivazione non è stata eseguita correttamente, `result` contiene la chiave `error`, generalmente accompagnata da una spiegazione dell'errore.


## Azioni JavaScript
{: #openwhisk_ref_javascript}

### Prototipo della funzione
{: #openwhisk_ref_javascript_fnproto}

Azioni JavaScript {{site.data.keyword.openwhisk_short}} eseguite in un runtime Node.js.

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
{: #openwhisk_ref_javascript_synchasynch}

È comune che le funzioni JavaScript proseguano la loro esecuzione in una funzione di callback anche dopo una restituzione. Per conformità, un'attivazione di una azione JavaScript può essere *sincrona* o *asincrona*.

Un'attivazione dell'azione JavaScript è **sincrona** se la funzione principale termina in una delle seguenti condizioni:

- La funzione principale termina senza eseguire un'istruzione `return`.
- La funzione principale termina con l'esecuzione di un'istruzione `return` che restituisce qualsiasi valore *eccetto* una Promessa.

Di seguito è riportato un esempio di azione sincrona.

```
// un'azione in cui ciascun percorso comporta un'attivazione sincrona
function main(params) {
  if (params.payload == 0) {
     return;
  } else if (params.payload == 1) {
     return {payload: 'Hello, World!'};
  } else if (params.payload == 2) {
    return {error: 'payload must be 0 or 1'};
  }
}
```
{: codeblock}

L'attivazione di un'azione JavaScript è **asincrona** se la funzione principale termina restituendo una Promessa.  In questo caso, il sistema presuppone che l'azione sia ancora in esecuzione, finché la Promessa non verrà soddisfatta o respinta.
Inizia a creare l'istanza di un nuovo oggetto Promessa e a trasmettergli una funzione di callback. Il callback utilizza due argomenti, resolve e reject, che sono entrambe funzioni. Tutto il codice asincrono va all'interno di tale callback.


Di seguito è riportato un esempio di come soddisfare una Promessa richiamando la funzione resolve.

```
function main(args) {
     return new Promise(function(resolve, reject) {
       setTimeout(function() {
         resolve({ done: true });
       }, 100);
    })
 }
```
{: codeblock}

Di seguito è riportato un esempio di come rifiutare una Promessa richiamando la funzione reject.

```
function main(args) {
     return new Promise(function(resolve, reject) {
       setTimeout(function() {
         reject({ done: true });
       }, 100);
    })
 }
```
{: codeblock}

È possibile che un'azione sia sincrona su alcuni input e asincrona su altri. Di seguito viene riportato un esempio.

```
  function main(params) {
      if (params.payload) {
         // asynchronous activation
         return new Promise(function(resolve, reject) {
                setTimeout(function() {
                  resolve({ done: true });
                }, 100);
             })
      } else {
         // synchronous activation
         return {done: true};
      }
  }
```
{: codeblock}

Nota che, indipendentemente dal fatto che un attivazione sia sincrona o asincrona, il richiamo dell'azione può essere bloccante o non bloccante.

### Oggetto whisk globale JavaScript rimosso

L'oggetto globale `whisk` è stato rimosso; migra le tue azioni nodejs per utilizzare metodi alternativi.
Per le funzioni `whisk.invoke()` e `whisk.trigger()` utilizza la libreria client già installata [openwhisk](https://www.npmjs.com/package/openwhisk).
Per `whisk.getAuthKey()` puoi ottenere il valore della chiave API dalla variabile di ambiente `__OW_API_KEY`.
Per `whisk.error()` puoi restituire un rejected Promise (ad esempio Promise.reject).

### Ambienti di runtime JavaScript
{: #openwhisk_ref_javascript_environments}

Le azioni JavaScript vengono eseguite per impostazione predefinita in un ambiente Node.js versione 6.9.1.  L'ambiente 6.9.1 verrà inoltre utilizzato per un'azione se l'indicatore `--kind` viene specificato esplicitamente con il valore 'nodejs:6' quando si crea o si aggiorna l'azione.
I seguenti pacchetti sono utilizzabili nell'ambiente Node.js 6.9.1:

- apn v2.1.2
- async v2.1.4
- btoa v1.1.2
- cheerio v0.22.0
- cloudant v1.6.2
- commander v2.9.0
- consul v0.27.0
- cookie-parser v1.4.3
- cradle v0.7.1
- errorhandler v1.5.0
- glob v7.1.1
- gm v1.23.0
- lodash v4.17.2
- log4js v0.6.38
- iconv-lite v0.4.15
- marked v0.3.6
- merge v1.2.0
- moment v2.17.0
- mongodb v2.2.11
- mustache v2.3.0
- nano v6.2.0
- node-uuid v1.4.7
- nodemailer v2.6.4
- oauth2-server v2.4.1
- openwhisk v3.3.2
- pkgcloud v1.4.0
- process v0.11.9
- pug v2.0.0-beta6
- redis v2.6.3
- request v2.79.0
- request-promise v4.1.1
- rimraf v2.5.4
- semver v5.3.0
- sendgrid v4.7.1
- serve-favicon v2.3.2
- socket.io v1.6.0
- socket.io-client v1.6.0
- superagent v3.0.0
- swagger-tools v0.10.1
- tmp v0.0.31
- twilio v2.11.1
- underscore v1.8.3
- uuid v3.0.0
- validator v6.1.0
- watson-developer-cloud v2.29.0
- when v3.7.7
- winston v2.3.0
- ws v1.1.1
- xml2js v0.4.17
- xmlhttprequest v1.8.0
- yauzl v2.7.0


## Ambienti di runtime Python
{: #openwhisk_ref_python_environments}

OpenWhisk supporta l'esecuzione di azioni Python utilizzando due versioni di runtime differenti.

### Azioni Python 3

Le azioni Python 3 sono eseguite utilizzando Python 3.6.1. Per utilzizare questo runtime, specifica il parametro CLI `wsk` `--kind python:3` durante la creazione o l'aggiornamento di un'azione.
Le azioni Python possono anche utilizzare i seguenti pacchetti, in aggiunta alle librerie standard Python 3.6.

- aiohttp v1.3.3
- appdirs v1.4.3
- asn1crypto v0.21.1
- async-timeout v1.2.0
- attrs v16.3.0
- beautifulsoup4 v4.5.1
- cffi v1.9.1
- chardet v2.3.0
- click v6.7
- cryptography v1.8.1
- cssselect v1.0.1
- Flask v0.12
- gevent v1.2.1
- greenlet v0.4.12
- httplib2 v0.9.2
- idna v2.5
- itsdangerous v0.24
- Jinja2 v2.9.5
- kafka-python v1.3.1
- lxml v3.6.4
- MarkupSafe v1.0
- multidict v2.1.4
- packaging v16.8
- parsel v1.1.0
- pyasn1 v0.2.3
- pyasn1-modules v0.0.8
- pycparser v2.17
- PyDispatcher v2.0.5
- pyOpenSSL v16.2.0
- pyparsing v2.2.0
- python-dateutil v2.5.3
- queuelib v1.4.2
- requests v2.11.1
- Scrapy v1.1.2
- service-identity v16.0.0
- simplejson v3.8.2
- six v1.10.0
- Twisted v16.4.0
- w3lib v1.17.0
- Werkzeug v0.12
- yarl v0.9.8
- zope.interface v4.3.3

### Azioni Python 2

Le azioni Python 2 sono eseguite utilizzando Python 2.7.12. Questo è il runtime predefinito per le azioni Python, a meno che non specifichi l'indicatore `--kind` durante la creazione o l'aggiornamento di un'azione. Per selezionare esplicitamente questo runtime, utilizza `--kind python:2`. Le azioni Python 2 possono anche utilizzare i seguenti pacchetti, in aggiunta alla libreria standard Python 2.7.

- appdirs v1.4.3
- asn1crypto v0.21.1
- attrs v16.3.0
- beautifulsoup4 v4.5.1
- cffi v1.9.1
- click v6.7
- cryptography v1.8.1
- cssselect v1.0.1
- enum34 v1.1.6
- Flask v0.11.1
- gevent v1.1.2
- greenlet v0.4.12
- httplib2 v0.9.2
- idna v2.5
- ipaddress v1.0.18
- itsdangerous v0.24
- Jinja2 v2.9.5
- kafka-python v1.3.1
- lxml v3.6.4
- MarkupSafe v1.0
- packaging v16.8
- parsel v1.1.0
- pyasn1 v0.2.3
- pyasn1-modules v0.0.8
- pycparser v2.17
- PyDispatcher v2.0.5
- pyOpenSSL v16.2.0
- pyparsing v2.2.0
- python-dateutil v2.5.3
- queuelib v1.4.2
- requests v2.11.1
- Scrapy v1.1.2
- service-identity v16.0.0
- simplejson v3.8.2
- six v1.10.0
- Twisted v16.4.0
- virtualenv v15.1.0
- w3lib v1.17.0
- Werkzeug v0.12
- zope.interface v4.3.3

## Azioni Docker
{: #openwhisk_ref_docker}

Le azioni Docker eseguono un file binario fornito dall'utente in un contenitore Docker. Il file binario viene eseguito in un'immagine Docker basata su [python:2.7.12-alpine](https://hub.docker.com/r/library/python), perciò il file binario deve essere compatibile con questa distribuzione.

La struttura di base Docker può essere opportunamente utilizzata per la creazione di immagini Docker compatibili con OpenWhisk. Puoi installare la struttura di base con il comando CLI `wsk sdk install docker`.

Il programma binario principale deve trovarsi in `/action/exec` all'interno del contenitore. L'eseguibile riceve gli argomenti di input tramite una singola stringa di argomenti della riga di comando che può essere deserializzata come oggetto `JSON`. Deve restituire un risultato tramite `stdout` come stringa a singola riga del `JSON` serializzato.

Puoi includere qualsiasi procedura di compilazione o dipendenza modificando il `Dockerfile` incluso in `dockerSkeleton`.

## API REST
{: #openwhisk_ref_restapi}

Tutte le capacità nel sistema sono disponibili mediante un'API REST. Sono presenti endpoint di raccolta e di entità per le azioni, i trigger, le regole, i pacchetti, le attivazioni e gli spazi dei nomi.

Gli endpoint di raccolta sono:

- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/actions`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/triggers`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/rules`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/packages`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/activations`

`openwhisk.`<span class="keyword" data-hd-keyref="DomainName">DomainName</span>` è il nome host dell'API OpenWhisk (ad esempio, openwhisk.ng.bluemix.net, 172.17.0.1 e così via).

Per `{namespace}`, il carattere `_` può essere utilizzato per specificare lo *spazio dei nomi
predefinito* dell'utente (ovvero, l'indirizzo di posta elettronica).

Puoi effettuare una richiesta GET sugli endpoint di raccolta per richiamare un elenco di entità della raccolta.

Sono presenti endpoint per ciascun tipo di entità:

- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/actions/[{packageName}/]{actionName}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/triggers/{triggerName}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/rules/{ruleName}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/packages/{packageName}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/activations/{activationName}`


Gli endpoint di spazio dei nomi e attivazione supportano solo le richieste GET. Gli endpoint di azioni, trigger, regole e pacchetti supportano le richieste GET, PUT e DELETE. Gli endpoint di azioni, trigger e regole supportano inoltre le richieste POST, che vengono utilizzate per richiamare azioni e trigger e per abilitare o disabilitare le regole. Per informazioni dettagliate, consulta la [Guida di riferimento API](https://console.{DomainName}/apidocs/98).

Tutte le API sono protette tramite autenticazione base HTTP. Le credenziali per l'autenticazione di base si trovano nella proprietà `AUTH` all'interno del file `~/.wskprops`, delimitate da due punti. Puoi richiamarle anche nella [procedura di configurazione della CLI](./index.html#openwhisk_start_configure_cli).

Di seguito viene riportato un esempio che utilizza il comando cURL per richiamare l'elenco di tutti i pacchetti nello spazio dei nomi `whisk.system`:

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
        "value": "Package that contains actions to interact with the Slack messaging service"
      }
    ],
    "version": "0.0.9",
    "namespace": "whisk.system"
  },
  ...
]
```
{: screen}

L'API OpenWhisk supporta chiamate di richiesta-risposta dai client web. OpenWhisk risponde alle richieste `OPTIONS` con le intestazione Cross-Origin Resource Sharing. Al momento, sono consentite tutte le origini (ad esempio, Access-Control-Allow-Origin è "`*`") e Access-Control-Allow-Headers produce Authorization e Content-Type.

**Attenzione:** poiché OpenWhisk supporta al momento una sola chiave per account, non si consiglia di utilizzare CORS al di là di semplici esperimenti. La tua chiave dovrebbe essere incorporata nel codice lato client, il che la rende visibile al pubblico. Utilizzare con cautela.

## Limiti di sistema
{: #openwhisk_syslimits}

### Azioni
{{site.data.keyword.openwhisk_short}} ha dei limiti di sistema, tra cui la quantità di memoria che un'azione può utilizzare e il numero di chiamate di azioni consentite per ciascun minuto.

La seguente tabella elenca i limiti predefiniti per le azioni.

| limite | descrizione | configurabile | unità | valore predefinito |
| ----- | ----------- | ------------ | -----| ------- |
| timeout | un contenitore non può essere eseguito per più di N millisecondi | per azione |  millisecondi | 60000 |
| memory | a un contenitore non possono essere assegnati più di N MB di memoria | per azione | MB | 256 |
| logs | un contenitore non può scrivere più di N MB in stdout | per azione | MB | 10 |
| concurrent | non possono essere inviate più di N attivazioni per ogni spazio dei nomi in esecuzione o in coda per l'esecuziome | per spazio dei nomi | numero | 1000 |
| minuteRate | non possono essere inviate più di N attivazioni per ogni spazio dei nomi al minuto | per utente | numero | 5000 |
| codeSize | la dimensiona massima del codice azione | non configurabile, limite per azione | MB | 48 |
| parameters | la dimensione massima dei parametri che possono essere collegati | non configurabile, limite per azione/pacchetto/trigger | MB | 1 |

### Timeout per azione (ms) (valore predefinito: 60 secondi)
{: #openwhisk_syslimits_timeout}
* Il limite di timeout N è compreso nell'intervallo [100 ms - 300000 ms] ed è impostato per azione in millisecondi.
* L'utente può modificare il limite durante la creazione dell'azione.
* Un contenitore in esecuzione per più di N millisecondi viene terminato.

### Memoria per azione (MB) (valore predefinito: 256 MB)
{: #openwhisk_syslimits_memory}
* Il limite di memoria M è compreso nell'intervallo [128 MB - 512 MB] ed è impostato per ciascuna azione in MB.
* L'utente può modificare il limite durante la creazione dell'azione.
* A un contenitore non può essere assegnata una quantità di memoria superiore al limite.

### Log per azione (MB) (valore predefinito: 10 MB)
{: #openwhisk_syslimits_logs}
* Il limite di log N è compreso nell'intervallo [0 MB..10 MB] ed è impostato per azione.
* Un utente può modificare il limite durante la creazione o l'aggiornamento dell'azione.
* I log che superano il limite impostato vengono troncati e viene aggiunta un'avvertenza come ultimo output dell'attivazione per indicare che l'attivazione ha superato il limite di log impostato.

### Risorsa per azione (MB) (valore fisso: 48 MB)
{: #openwhisk_syslimits_artifact}
* La dimensiona massima del codice per l'azione è 48 MB.
* Per un'azione Java ti raccomandiamo di utilizzare uno strumento per concatenare tutto il codice di origine incluse le dipendenze in un singolo file di bundle.

### Dimensione payload per attivazione (MB) (valore fisso: 1MB)
{: #openwhisk_syslimits_activationsize}
* La dimensione massima del contenuto POST più qualsiasi parametro sottoposto a currying per una chiamata dell'azione o attivazione del trigger è di 1 MB.

### Chiamata simultanea per lo spazio dei nomi (valore predefinito: 1000)
{: #openwhisk_syslimits_concur}
* Il numero di attivazioni che sono in esecuzione o in coda per l'esecuzione per uno spazio dei nomi non può essere maggiore di 1000.
* Il limite predefinito può essere configurato statisticamente da Whisk in consul kvstore.
* L'utente non può attualmente modificare questi limiti.

### Chiamate al minuto (valore fisso: 5000)
{: #openwhisk_syslimits_invocations}
* Il limite di frequenza N è impostato su 5000 e limita il numero di chiamate di azioni possibili in finestre temporali di un minuto.
* L'utente non può modificare questo limite durante la creazione dell'azione.
* Una chiamata CLI o API che superi questo limite riceverà un codice di errore corrispondente al codice di stato HTTP `429: TOO MANY REQUESTS`.

### Dimensione dei parametri (valore fisso: 1 MB)
{: #openwhisk_syslimits_parameters}
* Il limite di dimensione per i parametri durante la creazione o l'aggiornamento di un'azione/pacchetto/trigger è 1 MB.
* Il limite non può essere modificato dall'utente.
* Il tentativo di creazione o aggiornamento di un'entità con dei parametri troppo grandi verrà rifiutato.

### Numero limite dei file aperti dall'azione Docker (valore fisso: 64:64)
{: #openwhisk_syslimits_openulimit}
* Il numero massimo di file aperti è 64 (per i limiti hard e soft).
* Il comando docker run utilizza l'argomento `--ulimit nofile=64:64`.
* Per ulteriori informazioni sul numero limite di file aperti, consulta la documentazione [docker run](https://docs.docker.com/engine/reference/commandline/run).

### Limite dei processi per azione Docker (valore fisso: 512:512)
{: #openwhisk_syslimits_proculimit}
* Il numero massimo di processi disponibili per un utente è 512 (per i limiti hard e soft).
* Il comando docker run utilizza l'argomento `--ulimit nproc=512:512`.
* Per ulteriori informazioni sul limite del numero massimo di processi, consulta la documentazione [docker run](https://docs.docker.com/engine/reference/commandline/run).

### Trigger

I trigger sono soggetti a una frequenza di attivazione al minuto come indicato nella seguente tabella.

| limite | descrizione | configurabile | unità | valore predefinito |
| ----- | ----------- | ------------ | -----| ------- |
| minuteRate | non possono essere attivati più di N trigger per ogni spazio dei nomi al minuto | per utente | numero | 5000 |

### Trigger al minuto (valore fisso: 5000)
* Il limite di frequenza N è impostato su 5000 e limita il numero di trigger che possono essere attivati in finestre temporali di un minuto.
* L'utente non può modificare questo limite durante la creazione del trigger.
* Una chiamata CLI o API che superi questo limite riceverà un codice di errore corrispondente al codice di stato HTTP `429: TOO MANY REQUESTS`.
