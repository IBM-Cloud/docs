---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-26"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Gateway API
{: #openwhisk_apigateway}

Le azioni OpenWhisk possono beneficiare della Gestione API.

Il Gateway API funge da proxy per le [Azioni web](webactions.md) e fornisce loro ulteriori funzioni che includono l'instradamento del metodo HTTP, i segreti/ID client, il limite di frequenza, CORS, la visualizzazione dei log di risposta e di utilizzo delle API e la definizione delle politiche di condivisione API.
Per ulteriori informazioni sulla funzione Gateway API, puoi consultare la [documentazione sulla gestione delle API](/docs/apis/management/manage_openwhisk_apis.html#manage_openwhisk_apis)

## Crea API dalle azioni web OpenWhisk utilizzando il tuo browser.

Con Gateway API, puoi esporre un'azione OpenWhisk in forma di API. Dopo aver definito l'API, puoi applicare le politiche di sicurezza e di limite di frequenza, visualizzare i log di risposta e di utilizzo delle API e definire le politiche di condivisione API.
Nel dashboard OpenWhisk, fai clic sulla [scheda API](https://console.ng.bluemix.net/openwhisk/apimanagement).


## Crea API dalle azioni web OpenWhisk utilizzando la CLI

### Configurazione della CLI OpenWhisk

Configura la CLI OpenWhisk CLI con l'apihost `wsk property set --apihost openwhisk.ng.bluemix.net`
Per poter utilizzare `wsk api`, il file di configurazione della CLI `~/.wskprops` deve contenere il token di accesso Bluemix.
Per ottenere il token di accesso, utilizza il comando CLI `wsk bluemix login`, per ulteriori informazioni sul comando esegui `wsk bluemix login -h`

**Nota:** se si verifica un errore di comando che richiede il sso (single sign on), questo non è attualmente supportato. Come soluzione temporanea, accedi con la CLI CloudFoundry utilizzando `cf login`, quindi copia il token di accesso dal file di configurazione della directory HOME `~/.cf/config.json` nel file `~/.wskprops` come proprietà `APIGW_ACCESS_TOKEN="value of AccessToken`. Rimuovi il prefisso `Bearer ` quando copi la stringa del token di accesso.

**Nota:** le API che crei utilizzando `wsk api-experimental` continueranno a funzionare per un breve periodo, tuttavia dovresti iniziare a migrare le API alle azioni web e riconfigurare le tue API esistenti utilizzando il nuovo comando CLI `wsk api`.

### Crea la tua prima API utilizzando la CLI

1. Crea un file JavaScript con il seguente contenuto. In questo esempio, il nome file è "hello.js".
  ```javascript
  function main({name:name='Serverless API'}) {
      return {payload: `Hello world ${name}`};
  }
  ```
  {: codeblock}
  
2. Crea un'azione web partendo dalla seguente funzione JavaScript. In questo esempio, l'azione è denominata "hello". Assicurati di aggiungere l'indicatore `--web true`
  
  ```
  wsk action create hello hello.js --web true
  ```
  {: pre}
  ```
  ok: created action hello
  ```
  
3. Crea un'API con il percorso di base `/hello`, il percorso `/world` e il metodo `get` con il tipo di risposta `json`
  
  ```
  wsk api create /hello /world get hello --response-type json
  ```
  ```
  ok: created API /hello/world GET for action /_/hello
  https://${APIHOST}:9001/api/21ef035/hello/world
  ```
  Viene generato un nuovo URL che espone l'azione `hello` tramite un metodo HTTP **GET**.
  
4. Facciamo una prova inviando una richiesta HTTP all'URL.
  
  ```
  $ curl https://${APIHOST}:9001/api/21ef035/hello/world?name=OpenWhisk
  ```
  ```json
  {
  "payload": "Hello world OpenWhisk"
  }
  ```
  È stata richiamata l'azione web `hello`, che restituisce un oggetto JSON che include il parametro `name` inviato tramite parametro di query. Puoi trasmettere i parametri all'azione tramite semplici parametri query o tramite il corpo della richiesta. Le azioni web ti consentono di richiamare un'azione in modo pubblico senza la chiave API di autorizzazione OpenWhisk.
  
### Controllo completo sulla risposta HTTP
  
  L'indicatore `--response-type` controlla l'URL di destinazione dell'azione web da trasmettere tramite proxy dal Gateway API. L'utilizzo di `--response-type json` come nell'esempio precedente, restituisce il risultato completo dell'azione in formato JSON e imposta automaticamente l'intestazione Content-Type su `application/json` che ti permette di iniziare facilmente. 
  
  Una volta iniziato, vuoi avere il controllo completo sulle proprietà di risposta HTTP come `statusCode`, `headers` e restituire diversi tipi di contenuto nel `body`. Puoi farlo utilizzando `--response-type http`, che ti permette di configurare l'URL di destinazione dell'azione web con l'estensione `http`.

  Puoi scegliere di modificare il codice dell'azione per rispettare la restituzione delle azioni web con estensione `http` o includere l'azione in una sequenza che passa il suo risultato a una nuova azione che trasforma il risultato in modo da essere formattato correttamente per una risposta HTTP. Per ulteriori informazioni sui tipi di risposta e sulle estensioni delle azioni web, consulta la documentazione [Azioni web](webactions.md).

  Modifica il codice per `hello.js` che restituisce le proprietà JSON `body`, `statusCode` e `headers`
  ```javascript
  function main({name:name='Serverless API'}) {
      return {
        body: new Buffer(JSON.stringify({payload:`Hello world ${name}`})).toString('base64'), 
        statusCode:200, 
        headers:{ 'Content-Type': 'application/json'}
      };
  }
  ```
  {: codeblock}
  Nota che il corpo deve essere restituito con codifica `base64` e non come stringa.
  
  Aggiorna l'azione con il risultato modificato
  ```
  wsk action update hello hello.js --web true
  ```
  {: pre}
  Aggiorna l'API con `--response-type http`
  ```
  wsk api create /hello /world get hello --response-type http
  ```
  {: pre}
  Chiama l'API aggiornata
  ```
  curl https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/hello/world
  ```
  {: pre}
  ```json
  {
  "payload": "Hello world Serverless API"
  }
  ```
  Hai ora il pieno controllo delle tue API, puoi controllare i contenuti come l'URL di restituzione o impostare il codice di stato per errori come Non trovato (404), Non autorizzato (401) o anche Errore interno (500).

### Esposizione di più azioni web

Diciamo che vuoi esporre una serie di azioni di un club letterario per i tuoi amici.
Disponi di una serie di azioni per implementare il tuo backend per il club letterario:

| azione | metodo HTTP | descrizione |
| ----------- | ----------- | ------------ |
| getBooks    | GET | ottieni dettagli libro  |
| postBooks   | POST | aggiungi un libro |
| putBooks    | PUT | aggiorna dettagli libro |
| deleteBooks | DELETE | elimina un libro |

Creiamo un'API per il club letterario, denominata `Book Club`, con `/club` come proprio percorso di base dell'URL HTTP e `books` come risorsa.
```
wsk api create -n "Book Club" /club /books get getBooks --response-type http
wsk api create /club /books post postBooks              --response-type http
wsk api create /club /books put putBooks                --response-type http
wsk api create /club /books delete deleteBooks          --response-type http
```

Nota che la prima azione esposta con il percorso di base `/club` prende l'etichetta dell'API con il nome `Book Club` e tutte le altre azioni esposte in `/club` saranno associate a `Book Club`

Elenchiamo tutte le azioni che abbiamo appena esposto.

```
wsk api list -f
```
```
ok: APIs
Action: getBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: get
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: postBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: post
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: putBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: put
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: deleteBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: delete
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```

Ora, solo per divertimento, aggiungiamo un nuovo libro `JavaScript: The Good Parts` con un HTTP **POST**
```
curl -X POST -d '{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}' https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
```
{
  "result": "success"
}
```

Andiamo all'elenco dei libri utilizzando la nostra azione `getBooks` tramite HTTP **GET**
```
curl -X GET https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
```
{
  "result": [{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}]
}
```

### Esportazione della configurazione
Esportiamo l'API denominata `Book Club` in un file che possiamo utilizzare come base per ricreare le API utilizzando un file come input. 
```
wsk api get "Book Club" > club-swagger.json
```

Come prima cosa testiamo il file swagger eliminando tutti gli URL esposti in un percorso di base comune.
Puoi eliminare tutti gli URL esposti utilizzando il percorso di base `/club` o l'etichetta del nome dell'API `"Book Club"`:
```
wsk api delete /club
```
```
ok: deleted API /club
```
### Modifica della configurazione

Puoi modificare la configurazione nel dashboard OpenWhisk: fai clic sulla [scheda API](https://console.ng.bluemix.net/openwhisk/apimanagement) per configurare la sicurezza, il limite di frequenza e altre funzioni.

### Importazione della configurazione

Ora ripristiniamo l'API denominata `Book Club` utilizzando il file `club-swagger.json`
```
wsk api create --config-file club-swagger.json
```
```
ok: created api /books delete for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books get for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books post for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books put for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```

Possiamo verificare che l'API è stata ricreata
```
wsk api list /club
```
```
ok: apis
Action                    Verb         API Name        URL
getBooks                   get         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
postBooks                 post         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
putBooks                   put         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
deleteBooks             delete         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
