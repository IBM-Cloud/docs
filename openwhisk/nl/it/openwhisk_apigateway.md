---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# API Gateway (sperimentale)
{: #openwhisk_apigateway}

Le [azioni web](openwhisk_webactions.html) vengono rilasciate per la disponibilità generale.

Le azioni web ti consentono di richiamare un'azione con metodi HTTP diversi da POST e senza la chiave API di autorizzazione dell'azione.

In seguito al feedback degli utenti, le azioni Web rappresentano il modello di programmazione scelto per costruire le azioni OpenWhisk in grado di gestire gli eventi HTTP.

La maggior parte delle funzionalità di API Gateway è stata unita nelle azioni web: le azioni web ti consentono di gestire ogni richiesta HTTP e di restituire risposte HTTP con il pieno controllo dalla tua azione web. 

Un'integrazione rivisitata di OpenWhisk API Gateway sarà disponibile a breve. Sarà configurato come proxy per le tue azioni web, fornendo loro le funzioni di API Gateway come ad esempio il limite di frequenza, la convalida del token oauth, le chiavi API e altro.

**Nota:** le API che crei utilizzando `wsk api-experimental` continueranno a funzionare, tuttavia dovresti iniziare a migrare le API alle azioni web.

## Configurazione della CLI OpenWhisk
{: #openwhisk_apigateway_cli}
Questa funzione sperimentale funziona solo con il nuovo modello di autenticazione OpenWhisk in cui ogni spazio dei nomi ha una chiave di autenticazione univoca associata ad esso.
Segui le istruzioni in [Configure CLI](https://console.ng.bluemix.net/openwhisk/cli) su come configurare la chiave di autenticazione per il tuo spazio dei nomi specifico.

## Esponi un'azione OpenWhisk
{: #openwhisk_apigateway_hello}

Andiamo ad esporre un'azione semplice che è già stata preinstallata con OpenWhisk

```
wsk api-experimental create /hello /echo get /whisk.system/utils/echo
```
{: pre}
```
ok: created api /echo GET for action /whisk.system/utils/echo
https://21ef035.api-gw.mybluemix.net/hello/echo
```
{: screen}
Viene generato un nuovo URL che espone l'azione `echo` tramite un metodo HTTP **GET**.

Facciamo una prova inviando una richiesta HTTP all'URL.
```
curl https://21ef035.api-gw.mybluemix.net/hello/echo?marco=polo
```
{: pre}
Questo richiamerà l'azione `echo`, restituendo una stringa JSON con i parametri inviati.
```
{
  "marco":"polo"
}
```
{: screen}

Puoi trasmettere i parametri all'azione tramite parametri query semplici o tramite un corpo della richiesta.

### Esposizione di più azioni
{: #openwhisk_apigateway_actions}

Diciamo che vuoi esporre una serie di azioni di un club letterario per i tuoi amici.
Disponi di una serie di azioni per implementare il tuo backend per il club letterario:

| azione | metodo http | descrizione |
| ----------- | ----------- | ------------ |
| getBooks    | GET | ottieni dettagli libro  |
| postBooks   | POST | aggiungi un libro |
| putBooks    | PUT | aggiorna dettagli libro |
| deleteBooks | DELETE | elimina un libro |

Creiamo un'API per il club letterario, denominata `Book Club`, con `/club` come proprio percorso di base dell'URL HTTP e `books` come risorsa.
```
wsk api-experimental create -n "Book Club" /club /books get getBooks
wsk api-experimental create /club /books post postBooks
wsk api-experimental create /club /books put putBooks
wsk api-experimental create /club /books delete deleteBooks
```
{: pre}

Nota che la prima azione esposta con il percorso di base `/club` prende l'etichetta dell'API con il nome `Book Club` e tutte le altre azioni esposte in `/club` saranno associate a `Book Club`

Elenchiamo tutte le azioni che abbiamo appena esposto.

```
wsk api-experimental list
```
{: pre}
```
ok: apis
Action                   Verb          API Name        URL
getBooks                   get         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
postBooks                 post         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
putBooks                   put         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
deleteBooks             delete         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

Ora, solo per divertimento, aggiungiamo un nuovo libro `JavaScript: The Good Parts` con un HTTP **POST**
```
curl -X POST -d '{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}' https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: pre}
```
{
  "result": "success"
}
```
{: screen}

Andiamo all'elenco dei libri utilizzando la nostra azione `getBooks` tramite HTTP **GET**
```
curl -X GET https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: pre}
```
{
  "result": [{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}]
}
```

### Esportazione della configurazione
Esportiamo l'API denominata `Book Club` in un file che possiamo utilizzare come base per ricreare le API utilizzando un file come input. 
```
wsk api-experimental get "Book Club" > club-swagger.json
```
{: pre}

Come prima cosa testiamo il file swagger eliminando tutti gli URL esposti in un percorso di base comune.
Puoi eliminare tutti gli URL esposti utilizzando il percorso di base `/club` o l'etichetta del nome dell'API `"Book Club"`:
```
wsk api-experimental delete /club
```
{: pre}
```
ok: deleted API /club
```
{: screen}

Ora ripristiniamo l'API denominata `Book Club` utilizzando il file `club-swagger.json`
```
wsk api-experimental create --config-file club-swagger.json
```
{: pre}
```
ok: created api /books delete for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books get for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books post for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books put for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

Possiamo verificare che l'API è stata ricreata
```
wsk api-experimental list /club
```
{: pre}
```
ok: apis
Action                    Verb         API Name        URL
getBooks                   get         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
postBooks                 post         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
putBooks                   put         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
deleteBooks             delete         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

- **Nota**: questa funzione è al momento un'offerta sperimentale che consente agli utenti una prima occasione per provarla e fornire dei feedback. Il seguente feedback è già stato ricevuto:
  - Nessuna capacità di personalizzare il controllo dell'accesso HTTP per CORS (Cross-Origin Resource Sharing); al momento, le intestazioni della risposta API generata sono configurate per gestire tutti i verbi o origini HTTP (ad esempio *). Le seguenti intestazioni vengono sempre restituite:
    - Access-Control-Allow-Origin: *
    - Access-Control-Allow-Headers: Autorizzazione, Tipo di contenuto
    - Access-Control-Allow-Methods: GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS
  - È supportato solo il tipo di contenuto `application/json` per la richiesta e la risposta.
  - Nessun modo programmatico per controllare la risposta dall'azione OpenWhisk.
  - Tutte le azioni OpenWhisk sono esposte tramite l'accesso pubblico, nessuna capacità di configurare una chiave API personalizzata.
  - I parametri del percorso non sono supportati, solo i parametri query e corpo della richiesta.
  - Se l'API viene creata senza un nome API, il nome sarà il percorso di base e non può essere modificato.
  - Quando si ricreano le API tramite un file di input, l'API deve prima essere eliminata.
  - Le API esportate contengono la tua chiave API OpenWhisk, queste informazioni sono sensibili, nessun modello disponibile.
