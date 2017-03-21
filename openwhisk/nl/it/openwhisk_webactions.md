---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Azioni web (sperimentale)
{: #openwhisk_webactions}

Le azioni web sono azioni OpenWhisk annotate che ti permettono di creare rapidamente delle applicazioni basate su web. In questo modo, puoi programmare la logica di backend a cui la tua applicazione web può accedere in forma anonima senza la necessità di una chiave di autenticazione OpenWhisk. Spetta allo sviluppatore dell'azione implementare la propria autenticazione e autorizzazione desiderata (ad esempio, il flusso OAuth).
{: shortdesc}

Le attivazioni dell'azione web saranno associate all'utente che ha creato l'azione. Questa azione rimanda il costo dell'attivazione dal chiamante al proprietario dell'azione. 

**Nota**: questa funzione è al momento un'offerta sperimentale che consente agli utenti una prima occasione per provarla e fornire dei feedback.

Prendiamo la seguente azione JavaScript `hello.js`,
```javascript
function main({name}) {
  var msg = 'you did not tell me who you are.';
  if (name) {
    msg = `hello ${name}!`
  }
  return {body: `<html><body><h3>${msg}</h3></body></html>`}
}
```
{: codeblock}

Puoi creare un'*azione web* `hello` nel pacchetto `demo` per lo spazio dei nomi `guest` utilizzando l'annotazione `web-export`:
```
wsk package create demo
```
{: pre}
```
wsk action create /guest/demo/hello hello.js -a web-export true
```
{: pre}

L'annotazione `web-export` permette all'azione di essere accessibile come azione web tramite una nuova interfaccia REST. L'URL è strutturato nel seguente modo: `https://{APIHOST}/api/v1/experimental/web/{QUALIFIED ACTION NAME}.{EXT}`. Il nome completo di un'azione è composto da tre parti: lo spazio dei nomi, il nome pacchetto e il nome azione. Un esempio è `guest/demo/hello`. L'ultima parte dell'URI richiama l'`extension` che in genere è `.http`, sebbene siano permessi anche altri valori come descritto più avanti. Il percorso dell'API dell'azione web può essere utilizzato con `curl` o `wget` senza una chiave API. Può anche essere immesso direttamente nel tuo browser. 

Prova ad aprire [https://${APIHOST}/api/v1/experimental/web/guest/demo/hello.http?name=Jane](https://${APIHOST}/api/v1/experimental/web/guest/demo/hello.http?name=Jane) nel tuo browser Web o prova a richiamare l'azione tramite `curl`:
```
curl https://openwhisk.{DomainName}/api/v1/experimental/web/guest/demo/hello.http?name=Jane
```
{: pre}
Di seguito è riportato un esempio di azione web che esegue un reindirizzamento HTTP:
```javascript
function main() {
  return { 
    headers: { "location": "http://openwhisk.org" }, 
    code: 302 
  }
}
```
{: codeblock}

O imposta un cookie:
```javascript
function main() {
  return { 
    headers: { 
      "Set-Cookie": "UserID=Jane; Max-Age=3600; Version=",
      "Content-Type": "text/html"  
    }, 
    code: 200, 
    body: "<html><body><h3>hello</h3></body></html" }
}
```
{: codeblock}

O restituisce un `image/png`:
```javascript
function main() {
    let png = <base 64 encoded string>
    return { headers: { 'Content-Type': 'image/png' },
             code: 200,
             body: png };
}
```
{: codeblock}

Or returns `application/json`:
```javascript
function main(params) { 
    return {
        'code': 200,
        'headers':{'Content-Type':'application/json'},
        'body' : new Buffer(JSON.stringify(params)).toString('base64'),
    };
}
```
{: codeblock}

It is important to be aware of the [limite della dimensione della risposta](./openwhisk_reference.html) per le azioni, in quanto una risposta che supera i limiti di sistema predefiniti avrà esito negativo. Gli oggetti di grandi dimensioni non devono essere inviati in linea attraverso OpenWhisk, ma differite ad esempio a un archivio oggetti.

## Gestione delle richieste HTTP con le azioni
{: #openwhisk_webactions_http}

Un'azione OpenWhisk che non sia un'azione web richiede l'autenticazione e deve rispondere con un oggetto JSON. Al contrario, le azioni web possono essere richiamate senza autenticazione e possono essere utilizzate per implementare gestori HTTP che rispondono con i contenuti *intestazioni*, *codice stato* e *corpo* di tipi diversi. L'azione web deve comunque restituire un oggetto JSON, ma il sistema OpenWhisk (ossia il `controller`) considererà diversamente un'azione web se il suo risultato include uno o più dei seguenti elementi come proprietà JSON di livello superiore:

- `headers`: un oggetto JSON in cui le chiavi sono nomi intestazione e i valori sono valori di stringa per tali intestazioni (l'impostazione predefinita è nessuna intestazione).
- `code`: un codice di stato HTTP valido (il valore predefinito è 200 OK).
- `body`: una stringa che può essere un testo semplice o una stringa con codifica base64 (per i dati binari).

Il controller passerà insieme le intestazioni specificate dall'azione, se presenti, al client HTTP al termine della richiesta/risposta. Allo stesso modo, il controller risponderà con il codice di stato fornito, se presente. Infine, il corpo viene passato come corpo della risposta. A meno che non ci sia una `content-type header` dichiarata nelle `headers` dei risultati dell'azione, il corpo viene passato come fosse una stringa (altrimenti genera un errore). Quando si definisce il `content-type`, il controller determinerà se la risposta è composta da dati binari o testo semplice e decodificherà la stringa utilizzando un decoder base64 come necessario. Se il corpo non viene decodificato correttamente, viene restituito un errore al chiamante.

*Nota*: un oggetto o array JSON viene considerato come dati binari e deve essere codificato in base64 come mostrato nell'esempio precedente.

## Contesto HTTP

Un'azione web, quando richiamata, riceve tutte le informazioni disponibili della richiesta HTTP come parametri aggiuntivi nell'argomento di input dell'azione. Questi sono:

- `__ow_meta_verb`: il metodo HTTP della richiesta.
- `__ow_meta_headers`: le intestazioni della richiesta.
- `__ow_meta_path`: il percorso senza corrispondenza della richiesta (la corrispondenza si arresta dopo il consumo dell'estensione dell'azione).

La richiesta non può sovrascrivere alcuno dei suddetti parametri `__ow_`, altrimenti la richiesta avrà esito negativo con un codice di stato uguale a 400 Bad Request.

## Funzioni aggiuntive
{: #openwhisk_webactions_extra}

Le azioni web forniscono alcune funzioni aggiuntive che includono:

- `Estensioni di contenuto`: la richiesta deve specificare il tipo di contenuto desiderato come uno di  `.json`, `.html`, `.text` o `.http`. Questo viene fatto aggiungendo un'estensione al nome dell'azione nell'URI, in modo che un'azione  `/guest/demo/hello` sia indicata come `/guest/demo/hello.http` per ricevere indietro, ad esempio, una risposta HTTP.
- `Proiezione dei campi dal risultato`: il percorso che segue il nome dell'azione viene utilizzato per proiettare uno o più livelli di risposta. Ad esempio,
`/guest/demo/hello.html/body`. Ciò consente a un'azione che restituisce un dizionario `{body: "..." }` di proiettare la proprietà `body` e di restituire direttamente il suo valore stringa. Il percorso proiettato segue un modello di percorso assoluto (come in XPath).
- `Parametri di query e corpo come input`: l'azione riceve i parametri di query così come i parametri nel corpo della richiesta. L'ordine di precedenza per l'unione dei parametri è: parametri pacchetto, parametri azione, parametri query, parametri corpo dove ognuno di questi sovrascrive eventuali valori precedenti in caso di sovrapposizione. Ad esempio, `/guest/demo/hello.http?name=Jane` passerà l'argomento `{name: "Jane"}` all'azione.
- `Dati modulo`: oltre allo standard `application/json`, le azioni web possono ricevere come input l'URL codificato dai dati `application/x-www-form-urlencoded data`. 
- `Attivazione tramite più verbi HTTP`: un'azione web può essere richiamata attraverso uno di quattro metodi HTTP: `GET`, `POST`, `PUT` o `DELETE`.


L'esempio riportato di seguito delinea brevemente come utilizzare queste funzioni in un'azione web. Data un'azione `/guest/demo/hello` con il seguente corpo:
```javascript
function main(params) { 
    return { 'response': params};
}
```
{: codeblock}

e richiamando l'azione con un parametro di query `name`, utilizzando l'estensione `.json` per indicare una risposta JSON e proiettando il campo `/response` si produrrà la seguente risposta HTTP:
```
curl https://openwhisk.{DomainName}/api/v1/experimental/web/guest/demo/hello.json/response?name=Jane
```
{: pre}
```json
{
    "name": "Jane",
    "__ow_meta_verb": "get",
    "__ow_meta_headers": {
        "accept": "*/*",
        "user-agent": "curl/7.51.0"
    },
    "__ow_meta_path": "/response"
}
```

## Estensioni di contenuto
{: #openwhisk_webactions_extensions}

Un'estensione di contenuto è richiesta quando si richiama un'azione web. Le estensioni `.json` e `.http` non richiedono un percorso di proiezione, mentre le estensioni `.text` e `.html` lo richiedono; tuttavia per comodità si utilizza il percorso predefinito per la corrispondenza con il nome estensione. Quindi, per richiamare un'azione web e ricevere una risposta `.html`, l'azione deve rispondere con un oggetto JSON contenente una proprietà di livello superiore denominata `html` (o la risposta deve essere nel percorso indicato esplicitamente). In altre parole, `/guest/demo/hello.html` equivale a proiettare esplicitamente la proprietà `html`, come in `/guest/demo/hello.html/html`. Il nome completo dell'azione deve includere il suo nome pacchetto, che sarà `default` se l'azione non si trova in un pacchetto denominato.


## Parametri protetti
{: #openwhisk_webactions_protected}

I parametri di azione possono essere anche protetti e trattati come immutabili. Per finalizzare i parametri e per rendere accessibile un'azione web, è necessario collegare due [annotazioni](/openwhisk_annotations.html) all'azione: `final` e `web-export`, una delle quali deve essere impostata su `true` per avere effetto. Riprendendo la distribuzione dell'azione precedente, aggiungiamo le annotazioni nel seguente modo:

```
wsk action create /guest/demo/hello hello.js \
      --parameter name Jane \
      --annotation final true \
      --annotation web-export true
```
{: pre}

Come risultato di queste modifiche, `name` viene collegato a `Jane` e non può essere sovrascritto dai parametri di query o corpo per via dell'annotazione finale. Ciò protegge l'azione dai parametri di query o corpo che tentano di modificare questo valore in modo intenzionale o accidentale. 

## Disabilitazione delle azioni web
{: #openwhisk_webactions_disable}

Per disabilitare il richiamo di un'azione web tramite la nuova API (`https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/experimental/web/`), basta rimuovere l'annotazione o impostarla su `false`.

```
wsk action update /guest/demo/hello hello.js \
      --annotation web-export false
```
{: pre}     

## Gestione degli errori
{: #openwhisk_webactions_errors}

Quando un'azione OpenWhisk non riesce, esistono due diverse modalità di errore. La prima è nota come *errore applicazione* ed è analoga a un'eccezione rilevata: l'azione restituisce un oggetto JSON contenente una proprietà `error` di livello superiore. La seconda è un *errore sviluppatore* che si verifica quando l'azione non riesce in modo irreversibile e non produce una risposta (questo è simile a un'eccezione non rilevata). Per le azioni web, il controller gestisce gli errori dell'applicazione come segue:

- Ogni proiezione di percorso specificata viene ignorata e il controller proietta invece la proprietà `error`.
- Il controller applica la gestione dei contenuti prevista dall'estensione dell'azione al valore della proprietà `error`.

Gli sviluppatori devono essere consapevoli di come possono essere utilizzate le azioni web e generare di conseguenza le risposte di errore. Ad esempio, un'azione web utilizzata con l'estensione `.http`
dovrebbe restituire una risposta HTTP come: `{error: { code: 400 }`. In caso contrario, si avrà una mancata corrispondenza tra il content-type implicito dall'estensione e il content-type dell'azione nella risposta di errore. Una considerazione speciale va fatta per le azioni web che sono delle sequenze, affinché i componenti che costituiscono una sequenza possano generare, quando necessario, gli errori adeguati.
