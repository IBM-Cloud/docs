---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Azioni web
{: #openwhisk_webactions}

Le azioni web sono azioni OpenWhisk annotate che ti permettono di creare rapidamente delle applicazioni basate su web. In questo modo, puoi programmare la logica di backend a cui la tua applicazione web può accedere in forma anonima senza la necessità di una chiave di autenticazione OpenWhisk. Spetta allo sviluppatore dell'azione implementare la propria autenticazione e autorizzazione desiderata (ad esempio, il flusso OAuth).
{: shortdesc}

Le attivazioni dell'azione web saranno associate all'utente che ha creato l'azione. Questa azione rimanda il costo dell'attivazione dal chiamante al proprietario dell'azione.

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

Puoi creare un'*azione web* `hello` nel pacchetto `demo` per lo spazio dei nomi `guest` utilizzando l'indicatore `--web` della CLI con un valore di `true` o `yes`:
```
wsk package create demo
```
{: pre}
```
wsk action create /guest/demo/hello hello.js --web true
```
{: pre}

Utilizzando l'indicatore `--web` con un valore di `true` o `yes` si consente che un'azione sia accessibile tramite l'interfaccia REST senza
bisogno delle credenziali. Un'azione web può essere richiamata utilizzando un URL strutturato nel seguente modo:
`https://{APIHOST}/api/v1/web/{QUALIFIED ACTION NAME}.{EXT}`. Il nome completo di un'azione è composto da tre parti: lo spazio dei nomi, il nome pacchetto e il nome azione.

*Il nome completo dell'azione deve includere il suo nome pacchetto, che sarà 'predefinito' se l'azione non si trova in un pacchetto denominato.*

Un esempio è `guest/demo/hello`. Il percorso dell'API dell'azione web può essere utilizzato con `curl` o `wget` senza una chiave API. Può anche essere immesso direttamente nel tuo browser.

Prova ad aprire [https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello?name=Jane](https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello?name=Jane) nel tuo browser Web o prova a richiamare l'azione tramite `curl`:
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello?name=Jane
```
{: pre}

Di seguito è riportato un esempio di azione web che esegue un reindirizzamento HTTP:
```javascript
function main() {
  return { 
    headers: { location: 'http://openwhisk.org' },
    statusCode: 302
  }
}
```
{: codeblock}    

O imposta un cookie:
```javascript
function main() {
  return { 
    headers: { 
      'Set-Cookie': 'UserID=Jane; Max-Age=3600; Version=',
      'Content-Type': 'text/html'
    }, 
    statusCode: 200,
    body: '<html><body><h3>hello</h3></body></html>' }
}
```
{: codeblock}  

O restituisce un `image/png`:
```javascript
function main() {
    let png = <base 64 encoded string>
    return { headers: { 'Content-Type': 'image/png' },
             statusCode: 200,
             body: png };
}
```
{: codeblock}  

Or returns `application/json`:
```javascript
function main(params) { 
    return {
        statusCode: 200,
        headers: { 'Content-Type': 'application/json' },
        body: new Buffer(JSON.stringify(params)).toString('base64'),
    };
}
```
{: codeblock}  

It is important to be aware of the [limite della dimensione della risposta](./openwhisk_reference.html) per le azioni, in quanto una risposta che supera i limiti di sistema predefiniti avrà esito negativo. Gli oggetti di grandi dimensioni non devono essere inviati in linea attraverso OpenWhisk, ma differite ad esempio a un archivio oggetti.

## Gestione delle richieste HTTP con le azioni
{: #openwhisk_webactions_http}

Un'azione OpenWhisk che non sia un'azione web richiede l'autenticazione e deve rispondere con un oggetto JSON. Al contrario, le azioni web possono essere richiamate senza autenticazione e possono essere utilizzate per implementare gestori HTTP che rispondono con i contenuti di *headers*, *statusCode* e *body* di tipi diversi. L'azione web deve comunque restituire un oggetto JSON, ma il sistema OpenWhisk (ossia il `controller`) considererà diversamente un'azione web se il suo risultato include uno o più dei seguenti elementi come proprietà JSON di livello superiore:

- `headers`: un oggetto JSON in cui le chiavi sono nomi intestazione e i valori sono valori di stringa per tali intestazioni (l'impostazione predefinita è nessuna intestazione).
- `statusCode`: un codice di stato HTTP valido (il valore predefinito è 200 OK).
- `body`: una stringa che può essere un testo semplice o una stringa con codifica base64 (per i dati binari).

Il controller passerà insieme le intestazioni specificate dall'azione, se presenti, al client HTTP al termine della richiesta/risposta. Allo stesso modo, il controller risponderà con il codice di stato fornito, se presente. Infine, il corpo viene passato come corpo della risposta. A meno che non ci sia una `content-type header` dichiarata nelle `headers` dei risultati dell'azione, il corpo viene passato come fosse una stringa (altrimenti genera un errore). Quando si definisce il `content-type`, il controller determinerà se la risposta è composta da dati binari o testo semplice e decodificherà la stringa utilizzando un decoder base64 come necessario. Se il corpo non viene decodificato correttamente, viene restituito un errore al chiamante.

*Nota*: un oggetto o array JSON viene considerato come dati binari e deve essere codificato in base64 come mostrato nell'esempio precedente.

## Contesto HTTP

Tutte le azioni web, quando richiamate, ricevono ulteriori dettagli della richiesta HTTP come parametri per l'argomento di input dell'azione. Questi sono:

- `__ow_method` (tipo: stringa): il metodo HTTP della richiesta.
- `__ow_headers` (tipo: associazione da stringa a stringa): le intestazioni della richiesta.
- `__ow_path` (tipo: stringa): il percorso senza corrispondenza della richiesta (la corrispondenza si arresta dopo il consumo dell'estensione dell'azione).
- `__ow_user` (tipo: stringa): lo spazio dei nomi che identifica l'oggetto autenticato OpenWhisk
- `__ow_body` (tipo: stringa): l'entità del corpo della richiesta, in forma di stringa con codifica base64 se il contenuto è binario, altrimenti una stringa in testo semplice
- `__ow_query` (tipo: stringa): i parametri di query dalla richiesta in forma di stringa non analizzata

Una richiesta non può sovrascrivere alcuno dei suddetti parametri `__ow_`, altrimenti la richiesta avrà esito negativo con un codice di stato uguale a 400 Bad Request.

`__ow_user` è presente solo quando l'azione web è [annotata per richiedere l'autenticazione](./openwhisk_annotations.html#openwhisk_annotations_webactions) e consente a un'azione web di implementare la propria politica di autorizzazione. `__ow_query` è disponibile solo quando un'azione web sceglie di gestire la [richiesta HTTP "raw"](#raw-http-handling). Si tratta di una stringa che contiene i parametri di query analizzati dall'URI (separati da `&`). La proprietà `__ow_body` è presente quando si gestiscono le richieste HTTP "raw" oppure quando l'entità della richiesta HTTP non è un oggetto JSON o dati di modulo. Le azioni web ricevono comunque i parametri di query e corpo come proprietà di prima classe negli argomenti dell'azione, dove i parametri di corpo hanno la precedenza sui parametri di query che, a loro volta, hanno la precedenza sui parametri di azione e pacchetto.

## Funzioni aggiuntive

Le azioni web forniscono alcune funzioni aggiuntive che includono:

- `Estensioni di contenuto`: la richiesta deve specificare il tipo di contenuto desiderato come uno tra `.json`, `.html`, `.http`, `.svg` o `.text`. Questo viene fatto aggiungendo un'estensione al nome dell'azione nell'URI, in modo che un'azione  `/guest/demo/hello` sia indicata come `/guest/demo/hello.http` per ricevere indietro, ad esempio, una risposta HTTP. Per praticità, viene utilizzata l'estensione `.http` se non viene rilevata alcuna estensione.
- `Proiezione dei campi dal risultato`: il percorso che segue il nome dell'azione viene utilizzato per proiettare uno o più livelli di risposta. Ad esempio,
`/guest/demo/hello.html/body`. Ciò consente a un'azione che restituisce un dizionario `{body: "..." }` di proiettare la proprietà `body` e di restituire direttamente il suo valore stringa. Il percorso proiettato segue un modello di percorso assoluto (come in XPath).
- `Parametri di query e corpo come input`: l'azione riceve i parametri di query così come i parametri nel corpo della richiesta. L'ordine di precedenza per l'unione dei parametri è: parametri pacchetto, parametri azione, parametri query, parametri corpo dove ognuno di questi sovrascrive eventuali valori precedenti in caso di sovrapposizione. Ad esempio, `/guest/demo/hello.http?name=Jane` passerà l'argomento `{name: "Jane"}` all'azione.
- `Dati modulo`: oltre allo standard `application/json`, le azioni web possono ricevere come input l'URL codificato dai dati `application/x-www-form-urlencoded data`.
- `Attivazione tramite più verbi HTTP`: un'azione web può essere richiamata tramite uno di questi metodi HTTP: `GET`, `POST`, `PUT`, `PATCH` e `DELETE`, oltre a `HEAD` e `OPTIONS`.
- `Gestione di entità HTTP raw e corpo diverso da JSON`: un'azione web può accettare un corpo della richiesta HTTP diverso da un oggetto JSON e può scegliere di ricevere questi valori sempre come dei valori opachi (testo semplice quando non binario o stringa con codifica base64).

L'esempio riportato di seguito delinea brevemente come utilizzare queste funzioni in un'azione web. Considera un'azione `/guest/demo/hello` con il seguente corpo:
```javascript
function main(params) { 
    return { response: params };
}
```

Quando questa azione viene richiamata come azione web, puoi modificare la risposta dell'azione web proiettando percorsi differenti dal risultato.
Ad esempio, per restituire l'intero oggetto e vedere quali argomenti riceve l'azione:

```
 curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json
 ```
{: pre}
```json
{
  "response": {
    "__ow_method": "get",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

e con un parametro di query:
```
 curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json?name=Jane
 ```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "get",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

o dati di modulo:
```
 curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -d "name":"Jane"
 ```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "10",      
      "content-type": "application/x-www-form-urlencoded",      
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

o l'oggetto JSON:
```
 curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -H 'Content-Type: application/json' -d '{"name":"Jane"}'
```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "15",      
      "content-type": "application/json",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

e per proiettare solo il nome (come testo):
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.text/response/name?name=Jane
```
{: pre}
```
Jane
```

Puoi notare che, per praticità, le entità del corpo dell'oggetto JSON, i dati di modulo e i parametri di query sono trattati tutti come dei dizionari, in cui i rispettivi valori sono direttamente accessibili come proprietà di input dell'azione. Questo non avviene per le azioni web che scelgono di gestire invece le entità della richiesta HTTP in maniera più diretta o quando l'azione web riceve un'entità che non è un oggetto JSON.

Ecco un esempio di utilizzo di un content-type "testo" con lo stesso esempio mostrato sopra:
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -H 'Content-Type: text/plain' -d "Jane"
```
{: pre}
```json
{
  "response": {
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "4",      
      "content-type": "text/plain",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": "",
    "__ow_body": "Jane"
  }
}
```


## Estensioni di contenuto
{: #openwhisk_webactions_extensions}

Un'estensione di contenuto è generalmente richiesta quando si richiama un'azione web; in assenza di un'estensione, viene utilizzato `.http` come estensione predefinita. Le estensioni `.json` e `.http` non richiedono un percorso di proiezione, mentre le estensioni `.html`, `.svg` e `.text` lo richiedono; tuttavia per comodità si utilizza il percorso predefinito per la corrispondenza con il nome estensione. Quindi, per richiamare un'azione web e ricevere una risposta `.html`, l'azione deve rispondere con un oggetto JSON contenente una proprietà di livello superiore denominata `html` (o la risposta deve essere nel percorso indicato esplicitamente). In altre parole, `/guest/demo/hello.html` equivale a proiettare esplicitamente la proprietà `html`, come in `/guest/demo/hello.html/html`. Il nome completo dell'azione deve includere il suo nome pacchetto, che sarà `default` se l'azione non si trova in un pacchetto denominato.


## Parametri protetti
{: #openwhisk_webactions_protected}

Un'estensione di contenuto è generalmente richiesta quando si richiama un'azione web; in assenza di un'estensione, viene utilizzato `.http` come estensione predefinita. Le estensioni `.json` e `.http` non richiedono un percorso di proiezione, mentre le estensioni `.html`, `.svg` e `.text` lo richiedono; tuttavia per comodità si utilizza il percorso predefinito per la corrispondenza con il nome estensione. Quindi, per richiamare un'azione web e ricevere una risposta `.html`, l'azione deve rispondere con un oggetto JSON contenente una proprietà di livello superiore denominata `html` (o la risposta deve essere nel percorso indicato esplicitamente). In altre parole, `/guest/demo/hello.html` equivale a proiettare esplicitamente la proprietà `html`, come in `/guest/demo/hello.html/html`. Il nome completo dell'azione deve includere il suo nome pacchetto, che sarà `default` se l'azione non si trova in un pacchetto denominato.


## Parametri protetti

I parametri di azione sono protetti e trattati come immutabili. I parametri vengono automaticamente finalizzati durante l'abilitazione della azioni web.

```
 wsk action create /guest/demo/hello hello.js \
      --parameter name Jane \
      --web true
```

Come risultato di queste modifiche, `name` viene collegato a `Jane` e non può essere sovrascritto dai parametri di query o corpo per via dell'annotazione finale. Ciò protegge l'azione dai parametri di query o corpo che tentano di modificare questo valore in modo intenzionale o accidentale. 

## Disabilitazione delle azioni web

Per disabilitare il richiamo di un'azione web tramite l'API web (`https://openwhisk.ng.bluemix.net/api/v1/web/`), trasmetti un valore di `false` o `no` all'indicatore `--web` durante l'aggiornamento di un'azione con la CLI.

```
 wsk action update /guest/demo/hello hello.js --web false
```
{: pre}

## Gestione HTTP raw

Un'azione web può scegliere di interpretare ed elaborare direttamente un corpo HTTP in entrata, senza la promozione di un oggetto JSON a proprietà di prima classe disponibili per l'input dell'azione (ad esempio, `args.name` rispetto all'analisi di `args.__ow_query`). Ciò viene fatto tramite un'[annotazione](annotations.md) `raw-http`. Utilizziamo lo stesso esempio mostrato in precedenza, ma abbiamo adesso un'azione web HTTP "raw" che riceve `name` sia come parametri di query sia come valore JSON nel corpo della richiesta HTTP:
```
 curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json?name=Jane -X POST -H "Content-Type: application/json" -d '{"name":"Jane"}' 
```
{: pre}
```json
{
  "response": {
    "__ow_method": "post",
    "__ow_query": "name=Jane",
    "__ow_body": "eyJuYW1lIjoiSmFuZSJ9",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "15",
      "content-type": "application/json",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"      
    },
    "__ow_path": ""
  }
}
```

In questo caso, possiamo notare che il contenuto JSON è codificato in base64 perché è trattato come un valore binario. Per questo valore, l'azione deve utilizzare la decodifica base64 e l'analisi JSON per ripristinare l'oggetto JSON. OpenWhisk utilizza il framework [Spray](https://github.com/spray/spray) per [determinare](https://github.com/spray/spray/blob/master/spray-http/src/main/scala/spray/http/MediaType.scala#L282) quali tipi di contenuto sono binari e quali sono in testo semplice.


### Abilitazione della gestione HTTP raw

Le azioni web HTTP raw sono abilitate tramite l'indicatore `--web` utilizzando un valore di `raw`.

```
 wsk action create /guest/demo/hello hello.js --web raw
```

### Disabilitazione della gestione HTTP raw

La disabilitazione di HTTP raw può essere realizzata trasmettendo un valore di `false` o `no` all'indicatore `--web`.

```
 wsk update create /guest/demo/hello hello.js --web false
```

### Decodifica del contenuto del corpo binario da Base64

Quando si utilizza la gestione HTTP raw, il contenuto `__ow_body` sarà codificato in Base64 quando il tipo di contenuto della richiesta è binario.
Le seguenti sono funzioni che dimostrano come decodificare il contenuto del corpo in Node, Python e Swift. Salva semplicemente un metodo illustrato
di seguito nel file, crea un'azione web HTTP raw utilizzando la risorsa salvata e richiama l'azione web.

#### Node

```javascript
  function main(args) {
    decoded = new Buffer(args.__ow_body, 'base64').toString('utf-8')
    return {body: decoded}
}
```
{: codeblock}

#### Python

```python
def main(args):
    try:
        decoded = args['__ow_body'].decode('base64').strip()
        return {"body": decoded}
    except:
        return {"body": "Could not decode body from Base64."}
```
{: codeblock}

#### Swift

```swift
extension String {
    func base64Decode() -> String? {
        guard let data = Data(base64Encoded: self) else {
            return nil
        }

        return String(data: data, encoding: .utf8)
    }
}

func main(args: [String:Any]) -> [String:Any] {
    if let body = args["__ow_body"] as? String {
        if let decoded = body.base64Decode() {
            return [ "body" : decoded ]
        }
    }

    return ["body": "Could not decode body from Base64."]
}
```
{: codeblock}

Come esempio, slava la funzione Node come `decode.js` ed esegui i seguenti comandi:
```
 wsk action create decode decode.js --web raw
```
{: pre}
```
ok: created action decode
```
```
curl -k -H "content-type: application" -X POST -d "Decoded body" https:// openwhisk.ng.bluemix.net/api/v1/web/guest/default/decodeNode.json
```
{: pre}
```json
{
  "body": "Decoded body"
}
```

## Gestione degli errori
{: #openwhisk_webactions_errors}

Quando un'azione OpenWhisk non riesce, esistono due diverse modalità di errore. La prima è nota come *errore applicazione* ed è analoga a un'eccezione rilevata: l'azione restituisce un oggetto JSON contenente una proprietà `error` di livello superiore. La seconda è un *errore sviluppatore* che si verifica quando l'azione non riesce in modo irreversibile e non produce una risposta (questo è simile a un'eccezione non rilevata). Per le azioni web, il controller gestisce gli errori dell'applicazione come segue:

- Ogni proiezione di percorso specificata viene ignorata e il controller proietta invece la proprietà `error`.
- Il controller applica la gestione dei contenuti prevista dall'estensione dell'azione al valore della proprietà `error`.

Gli sviluppatori devono essere consapevoli di come possono essere utilizzate le azioni web e generare di conseguenza le risposte di errore. Ad esempio, un'azione web utilizzata con l'estensione `.http`
dovrebbe restituire una risposta HTTP come: `{error: { statusCode: 400 }`. In caso contrario, si avrà una mancata corrispondenza tra il tipo di contenuto implicito dall'estensione e il content-type dell'azione nella risposta di errore. Una considerazione speciale va fatta per le azioni web che sono delle sequenze, affinché i componenti che costituiscono una sequenza possano generare, quando necessario, gli errori adeguati.

