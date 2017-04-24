---

copyright:
  years: 2016, 2017
  lastupdated: "2017-04-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Creazione e chiamata di azioni {{site.data.keyword.openwhisk_short}}
{: #openwhisk_actions}


Le azioni sono frammenti di codice senza stato eseguiti sulla piattaforma {{site.data.keyword.openwhisk}}. Un'azione può essere scritta in forma di funzione JavaScript, Swift o Python, di metodo Java o di programma eseguibile personalizzato incluso in un contenitore Docker. Ad esempio, un'azione può essere utilizzata per rilevare i volti in un'immagine, rispondere a una modifica del database, aggregare una serie di chiamate API o pubblicare un Tweet.
{:shortdesc}
Le azioni possono essere richiamate esplicitamente o eseguite in risposta a un evento. In entrambi i casi, ogni esecuzione di un'azione produce un record di attivazione che viene identificato da un ID di attivazione univoco. L'input in un'azione e i risultati di un'azione fungono da dizionario di coppie chiave-valore, in cui la chiave è una stringa e il valore è un valore JSON valido. Le azioni possono anche essere formate da chiamate ad altre azioni o a una sequenza definita di azioni.

Impara a creare, richiamare ed eseguire il debug di azioni nel tuo ambiente di sviluppo preferito:
* [JavaScript](#openwhisk_create_action_js)
* [Swift](#openwhisk_actions_swift)
* [Python](#openwhisk_actions_python)
* [Java](#openwhisk_actions_java)
* [Docker](#openwhisk_actions_docker)

Altre informazioni su:

* [Visualizzazione dell'output di un'azione](#openwhisk_actions_polling)
* [Elenco azioni](#openwhisk_listing_actions)
* [Eliminazione di azioni](#openwhisk_delete_action)
* [Accesso ai metadati dell'azione nel corpo dell'azione](#openwhisk_action_metadata)


## Creazione e chiamata di azioni JavaScript
{: #openwhisk_create_action_js}

Le seguenti sezioni ti guidano nell'utilizzo di azioni in JavaScript. Inizierai con la creazione e la chiamata di un'azione semplice. Procederai quindi all'aggiunta di parametri a un'azione e al richiamo di tale azione con i parametri. La fase successiva, prevede l'impostazione e il richiamo dei parametri predefiniti. Potrai quindi creare azioni asincrone e, infine, lavorare con le sequenze di azioni.


### Creazione e chiamata di un'azione JavaScript semplice
{: #openwhisk_single_action_js}

Consulta la procedura e gli esempi di seguito riportati per creare la tua prima azione JavaScript.

1. Crea un file JavaScript con il seguente contenuto. In questo esempio, il nome file è "hello.js".

  ```javascript
  function main() {
      return {payload: 'Hello world'};
  }
  ```
    {: codeblock}

  Il file JavaScript potrebbe contenere ulteriori funzioni. Tuttavia, per convenzione, è necessaria una funzione denominata `main` che fornisca il punto di ingresso all'azione.

2. Crea un'azione partendo dalla seguente funzione JavaScript. In questo esempio, l'azione è denominata "hello".

  ```
  wsk action create hello hello.js
  ```
      {: pre}
  ```
  ok: created action hello
  ```

3. Elenca le azioni che hai creato:

  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  hello       private
  ```

  Puoi vedere l'azione `hello` che hai appena creato.

4. Una volta creata la tua azione, puoi eseguirla nel cloud in OpenWhisk con il comando 'invoke'. Puoi chiamare le azioni con una chiamata *bloccante* (ad esempio, stile richiesta/risposta) o *non bloccante*, specificando un indicatore nel comando. Una richiesta di chiamata bloccante *attenderà* che il risultato di attivazione sia disponibile. Il periodo di attesa è inferiore a 60 secondi o al [limite di tempo](./openwhisk_reference.html#openwhisk_syslimits) configurato dall'azione. Il risultato dell'attivazione viene restituito se è disponibile entro il periodo di attesa. In caso contrario, l'attivazione continua l'elaborazione nel sistema e viene restituito un ID di attivazione in modo che si possa controllare il risultato in un secondo momento, come avviene con le richieste non bloccanti (vedi [qui](#openwhisk_actions_polling) per suggerimenti sul monitoraggio della attivazioni).

  Questo esempio utilizza il parametro di blocco `--blocking`:

  ```
  wsk action invoke --blocking hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 44794bd6aab74415b4e42a308d880e5b
  ```
  ```json
  {
      "result": {
          "payload": "Hello world"
      },
      "status": "success",
      "success": true
  }
  ```

  Il comando restituisce due informazioni importanti:
  * L'ID di attivazione (`44794bd6aab74415b4e42a308d880e5b`)
  * Il risultato della chiamata se è disponibile entro il periodo di attesa previsto

  Il risultato, in questo caso, è la stringa `Hello world` restituita dalla funzione JavaScript. L'ID di attivazione può essere utilizzato per richiamare i log o il risultato della chiamata in un momento successivo.  

5. Se non ti serve subito il risultato dell'azione, puoi omettere l'indicatore `--blocking` ed effettuare una chiamata non bloccante. Puoi ottenere il risultato successivamente attraverso l'ID di attivazione. Vedi il seguente esempio:

  ```
  wsk action invoke hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 6bf1f670ee614a7eb5af3c9fde813043
  ```

  ```
  wsk activation result 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: pre}
  ```json
  {
      "payload": "Hello world"
  }
  ```

6. Se dimentichi di registrare l'ID di attivazione, puoi ottenere un elenco delle attivazioni ordinate dalla più recente alla più obsoleta. Esegui il seguente comando per ottenere un elenco delle tue attivazioni:

  ```
  wsk activation list
  ```
  {: pre}
  ```
  activations
  44794bd6aab74415b4e42a308d880e5b         hello
  6bf1f670ee614a7eb5af3c9fde813043         hello
  ```

### Trasmissione di parametri a un'azione

È possibile trasmettere dei parametri all'azione quando viene richiamata.

1. Utilizza i parametri nell'azione. Ad esempio, aggiorna il file "hello.js" con il seguente contenuto:

  ```javascript
  function main(params) {
      return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

  I parametri di input vengono trasmessi alla funzione `main` come parametro dell'oggetto JSON. Osserva in che modo i parametri `name` e `place` vengono richiamati dall'oggetto `params` in questo esempio.

2. Aggiorna l'azione `hello` e chiamala, mentre le trasmetti i valori dei parametri `name` e `place`. Vedi il seguente esempio:

  ```
  wsk action update hello hello.js
  ```
  {: pre}

3.  I parametri possono essere forniti esplicitamente nella riga di comando o fornendo un file contenente i parametri desiderati.

  Per passare i parametri direttamente tramite la riga di comando, fornisci una coppia chiave/valore all'indicatore `--param`:
  ```
  wsk action invoke --blocking --result hello --param name Bernie --param place Vermont
  ```
  {: pre}

  Per poter utilizzare un file contenente il contenuto del parametro, crea il file che contiene i parametri nel formato JSON. Il nome file
  deve essere passato all'indicatore `param-file`:

  File del parametro di esempio denominato parameters.json:
  ```json
  {
      "name": "Bernie",
      "place": "Vermont"
  }
  ```
  {: codeblock}

  ```
  wsk action invoke --blocking --result hello --param-file parameters.json
  ```
  {: pre}

  ```json
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```

  Osserva l'uso dell'opzione `--result` per visualizzare solo il risultato della chiamata.

### Impostazione dei parametri predefiniti
{: #openwhisk_binding_actions}

Le azioni possono essere richiamate con più parametri. Ricorda che l'azione `hello` dell'esempio precedente prevede due parametri: il *nome* di una persona e il *luogo* di provenienza.

Anziché trasmettere ogni volta tutti i parametri a un'azione, puoi eseguire il bind di determinati parametri. Il seguente esempio esegue il bind del parametro *place*, cosicché l'azione assuma come valore predefinito il luogo "Vermont":

1. Aggiorna l'azione utilizzando l'opzione `--param` per eseguire il bind dei valori di parametro o passando un file che contiene i parametri a `--param-file`

  Per specificare i parametri predefiniti esplicitamente nella riga di comando, fornisci una coppia chiave/valore all'indicatore `param`:

  ```
  wsk action update hello --param place Vermont
  ```
  {: pre}

  La trasmissione dei parametri a un file richiede la creazione di un file con il contenuto desiderato nel formato JSON.
  Il nome file deve essere passato all'indicatore `-param-file`:

  File del parametro di esempio denominato parameters.json:
  ```json
  {
      "place": "Vermont"
  }
  ```
  {: codeblock}

  ```
  wsk action update hello --param-file parameters.json
  ```
  {: pre}

2. Richiama l'azione, trasmettendo questa volta solo il parametro `name`.

  ```
  wsk action invoke --blocking --result hello --param name Bernie
  ```
  {: pre}
  ```json
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```

  Nota che non hai dovuto specificare il parametro del luogo quando hai richiamato l'azione. I parametri associati mediante bind possono sempre essere sovrascritti specificando il valore del parametro al momento della chiamata.

3. Richiama l'azione, trasmettendo il valore sia di `name` che di `place`. Quest'ultimo sovrascrive il valore associato mediante bind all'azione.

  Utilizzo dell'indicatore `--param`:

  ```
  wsk action invoke --blocking --result hello --param name Bernie --param place "Washington, DC"
  ```
  {: pre}

  Utilizzo dell'indicatore `--param-file`:

  File parameters.json:
  ```json
  {
    "name": "Bernie",
    "place": "Vermont"
  }
  ```
  {: codeblock}
  ```
  wsk action invoke --blocking --result hello --param-file parameters.json
  ```
  {: pre}
  
  ```json
  {  
      "payload": "Hello, Bernie from Washington, DC"
  }
  ```

### Creazione di azioni asincrone
{: #openwhisk_asynchrony_js}

Le funzioni JavaScript eseguite in modo asincrono potrebbero dover restituire il risultato dell'attivazione dopo la restituzione della funzione `main`. Puoi ottenere questo risultato restituendo una Promessa nella tua azione.

1. Salva il seguente contenuto in un file denominato `asyncAction.js`.

  ```javascript
  function main(args) {
       return new Promise(function(resolve, reject) {
         setTimeout(function() {
           resolve({ done: true });
         }, 2000);
      })
   }
  ```
  {: codeblock}

  Nota che la funzione `main` restituisce una Promessa, che indica che l'attivazione non è stata ancora completata, ma il suo completamento è previsto in futuro.

  In questo caso, la funzione JavaScript `setTimeout()` attende due secondi prima di richiamare la funzione di callback.  Questo rappresenta il codice asincrono e va all'interno della funzione di callback della Promessa.

  Il callback della Promessa utilizza due argomenti, resolve e reject, che sono entrambe funzioni.  La chiamata a `resolve()` soddisfa la Promessa e indica che l'attivazione è stata completata normalmente.

  Una chiamata a `reject()` può essere utilizzata per rifiutare la Promessa e segnalare che l'attivazione è stata completata in modo anomalo.

2. Esegui i seguenti comandi per creare l'azione e richiamarla:

  ```
  wsk action create asyncAction asyncAction.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result asyncAction
  ```
  {: pre}
  ```json
  {
      "done": true
  }
  ```

  Nota che hai eseguito una chiamata bloccante di un'azione asincrona.

3. Richiama il log di attivazione per vedere quanto tempo è stato impiegato per il completamento dell'attivazione:

  ```
  wsk activation list --limit 1 asyncAction
  ```
  {: pre}
  ```
  activations
  b066ca51e68c4d3382df2d8033265db0             asyncAction
  ```


  ```
  wsk activation get b066ca51e68c4d3382df2d8033265db0
  ```
  {: pre}
 ```json
  {
      "start": 1455881628103,
      "end":   1455881648126
  }
  ```

  Confrontando gli indicatori di data/ora `start` e `end` nel record di attivazione, puoi notare che per il completamento di questa attivazione sono stati impiegati poco più due secondi.

### Utilizzo di azioni per la chiamata di un'API esterna
{: #openwhisk_apicall_action}

Gli esempi forniti finora hanno rappresentato funzioni JavaScript autonome. Puoi creare anche un'azione che richiama un'API esterna.

Questo esempio richiama un servizio Yahoo Meteo per ottenere le condizioni attuali in un'ubicazione specifica.

1. Salva il seguente contenuto in un file denominato `weather.js`.

  ```javascript
  var request = require('request');

  function main(params) {
      var location = params.location || 'Vermont';
        var url = 'https://query.yahooapis.com/v1/public/yql?q=select item.condition from weather.forecast where woeid in (select woeid from geo.places(1) where text="' + location + '")&format=json';

      return new Promise(function(resolve, reject) {
          request.get(url, function(error, response, body) {
              if (error) {
                  reject(error);    
                }
                else {
                  var condition = JSON.parse(body).query.results.channel.item.condition;
                    var text = condition.text;
                    var temperature = condition.temp;
                    var output = 'It is ' + temperature + ' degrees in ' + location + ' and ' + text;
                    resolve({msg: output});
                }
          });
      });
  }
  ```
  {: codeblock}

  Nota che l'azione dell'esempio utilizza la libreria JavaScript `request` per effettuare una richiesta HTTP all'API Yahoo Meteo ed estrae campi dal risultato JSON. I [riferimenti](./openwhisk_reference.html#openwhisk_ref_javascript_environments) indicano nel dettaglio i pacchetti Node.js che puoi utilizzare nelle tue azioni.

  Questo esempio mostra anche la necessità di eseguire azioni asincrone. L'azione restituisce una Promessa per indicare che il risultato di questa azione non è ancora disponibile nel momento in cui viene restituita la funzione. Il risultato è invece disponibile nel callback `request` al completamento della chiamata HTTP e viene trasmesso come argomento alla funzione `resolve()`.

2. Esegui i seguenti comandi per creare l'azione e richiamarla:

  ```
  wsk action create weather weather.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result weather --param location "Brooklyn, NY"
  ```
  {: pre}
  ```json
  {
      "msg": "It is 28 degrees in Brooklyn, NY and Cloudy"
  }
  ```

### Creazione pacchetto di un'azione come modulo Node.js
{: #openwhisk_js_packaged_action}

Come alternativa alla scrittura di tutto il tuo codice di azione in un unico file di origine JavaScript, puoi scrivere un'azione come pacchetto `npm`. Considera come esempio una directory con i seguenti file:

Prima, `package.json`:

```json
{
  "name": "my-action",
  "main": "index.js",
  "dependencies" : {
    "left-pad" : "1.1.3"
  }
}
```
{: codeblock}

Quindi, `index.js`:

```javascript
function myAction(args) {
    const leftPad = require("left-pad")
    const lines = args.lines || [];
    return { padded: lines.map(l => leftPad(l, 30, ".")) }
}

exports.main = myAction;
```
{: codeblock}

Nota che l'azione viene esposta tramite `exports.main`; il gestore azione può avere qualsiasi nome purché sia conforme alla solita indicazione di accettare un oggetto e restituire un oggetto ( o una `Promessa` di un oggetto). Per convenzione Node.js, devi denominare questo file `index.js` o specificare il nome file che preferisci come proprietà `main` in package.json.

Per creare un'azione OpenWhisk da questo pacchetto:

1. Installa prima tutte le dipendenze localmente

  ```
  npm install
  ```
  {: pre}

2. Crea un archivio `.zip` contenente tutti i file (incluse tutte le dipendenze):

  ```
  zip -r action.zip *
  ```
  {: pre}

    > Nota: l'utilizzo dell'azione di Windows Explorer per la creazione del file zip creerà una struttura non corretta. Le azioni zip OpenWhisk devono avere `package.json` al livello root dello zip, mentre Windows Explorer lo inserirà in una cartella nidificata. L'opzione più sicura è quella di utilizzare il comando `zip` nella riga comandi come mostrato sopra.


3. Crea l'azione:

  ```
  wsk action create packageAction --kind nodejs:6 action.zip
  ```
  {: pre}

  Nota che durante la creazione di un'azione da un archivio `.zip` mediante lo strumento CLI, devi fornire esplicitamente un valore per l'indicatore `--kind`.

4. Puoi richiamare l'azione come qualsiasi altra:

  ```
  wsk action invoke --blocking --result packageAction --param lines "[\"and now\", \"for something completely\", \"different\" ]"
  ```
  {: pre}
  ```json
  {
      "padded": [
          ".......................and now",
          "......for something completely",
          ".....................different"
      ]
  }
  ```


Infine, nota che mentre la maggior parte dei pacchetti `npm` installa le origini JavaScript su `npm install`, altri installano e compilano anche delle risorse binarie. Il caricamento dei file di archivio attualmente non supporta le dipendenze binarie, ma solo le dipendenze JavaScript. Le chiamate di azioni potrebbero non riuscire se l'archivio include dipendenze binarie.

## Creazione di sequenze di azioni
{: #openwhisk_create_action_sequence}

Puoi creare un'azione che concatena una sequenza di azioni.

In un pacchetto denominato `/whisk.system/utils` vengono fornite varie azioni di utilità che puoi utilizzare per creare la tua prima sequenza. Per ulteriori informazioni sui pacchetti, vedi la sezione [Pacchetti](./openwhisk_packages.html).

1. Visualizza le azioni del pacchetto `/whisk.system/utils`.

  ```
  wsk package get --summary /whisk.system/utils
  ```
  {: pre}
  ```
  package /whisk.system/utils: Mattoni che formattano e assemblano i dati
   action /whisk.system/utils/head: Estrae il prefisso di un array
   action /whisk.system/utils/split: Suddivide una stringa in un array
   action /whisk.system/utils/sort: Ordina un array
   action /whisk.system/utils/echo: Restituisce l'input
   action /whisk.system/utils/date: Data e ora corrente
   action /whisk.system/utils/cat: Concatena l'input in una stringa
  ```


  In questo esempio utilizzerai le azioni `split` e `sort`.

2. Crea una sequenza di azioni in modo che il risultato di un'azione venga trasmesso come argomento all'azione successiva.

  ```
  wsk action create sequenceAction --sequence /whisk.system/utils/split,/whisk.system/utils/sort
  ```
  {: pre}

  Questa sequenza di azioni converte alcune righe di testo in array e ordina le righe.

3. Richiama l'azione:

  ```
  wsk action invoke --blocking --result sequenceAction --param payload "Over-ripe sushi,\nThe Master\nIs full of regret."
  ```
  {: pre}
  ```json
  {
      "length": 3,
      "lines": [
          "Is full of regret.",
          "Over-ripe sushi,",
          "The Master"
      ]
  }
  ```


  Nel risultato, noterai che le righe sono ordinate.

**Nota**: i parametri passati tra le azioni nella sequenza sono espliciti, ad eccezione dei parametri predefiniti.
Pertanto, i parametri che vengono passati alla sequenza di azioni sono disponibili solo per la prima azione nella sequenza.
Il risultato della prima azione della sequenza diventa l'oggetto JSON di input per la seconda azione della sequenza (e così via).
Questo oggetto non include nessuno dei parametri originariamente passati alla sequenza, a meno che la prima azione non li includa esplicitamente nel suo risultato.
I parametri passati a un'azione vengono uniti ai parametri predefiniti dell'azione. I parametri passati hanno la precedenza e sostituiscono tutti i parametri predefiniti corrispondenti.
Per ulteriori informazioni sul richiamo delle sequenze di azioni con più parametri denominati, vedi [Impostazione dei parametri predefiniti](./openwhisk_actions.html#openwhisk_binding_actions).

## Creazione di azioni Python
{: #openwhisk_actions_python}

Il processo di creazione delle azioni Python è simile a quello delle azioni JavaScript. Le seguenti sezioni ti guidano lungo la creazione e la chiamata di una singola azione Python e l'aggiunta di parametri a tale azione.

### Creazione e chiamata di un'azione
{: #openwhisk_actions_python_invoke}

Un'azione è semplicemente una funzione Python di livello superiore. Ad esempio, crea un file denominato `hello.py` con il seguente codice di origine: 

```python
def main(args):
    name = args.get("name", "stranger")
    greeting = "Hello " + name + "!"
    print(greeting)
        return {"greeting": greeting}
```
{: codeblock}

Le azioni Python utilizzano sempre un dizionario e ne producono un altro. Il metodo immesso per l'azione è `main` per impostazione predefinita ma può essere specificato espressamente durante la creazione dell'azione con la CLI `wsk` utilizzando `--main`, come per qualsiasi altro tipo di azione.

Puoi creare un'azione OpenWhisk denominata `helloPython` da questa funzione
nel seguente modo:

```
wsk action create helloPython hello.py
```
{: pre}
La CLI deduce automaticamente il tipo di azione dall'estensione del file di origine. Per i file di origine `.py`, l'azione viene eseguita utilizzando un runtime Python 2.7. Puoi anche creare un'azione eseguita con Python 3.6 specificando esplicitamente il parametro `--kind python:3`. Consulta la [guida di riferimento](./openwhisk_reference.html#openwhisk_ref_python_environments) Phyton per ulteriori informazioni su Python 2.7 vs. 3.6.

Le azioni Python vengono richiamate come le azioni JavaScript:

```
wsk action invoke --blocking --result helloPython --param name World
```
{: pre}

```json
  {
      "greeting": "Hello World!"
  }
```


## Creazione di azioni Swift

Il processo di creazione di azioni Swift è analogo a quello delle azioni JavaScript. Le seguenti sezioni ti guidano lungo la creazione e la chiamata di una singola azione swift e l'aggiunta di parametri a tale azione.

Puoi inoltre utilizzare il [Swift Sandbox](https://swiftlang.ng.bluemix.net) online per testare il tuo codice Swift senza dover installare Xcode sulla tua macchina.

### Creazione e chiamata di un'azione

Un'azione è semplicemente una funzione Swift di livello superiore. Ad esempio, crea un file denominato
`hello.swift` con il seguente contenuto:

```swift
func main(args: [String:Any]) -> [String:Any] {
    if let name = args["name"] as? String {
        return [ "greeting" : "Hello \(name)!" ]
    } else {
        return [ "greeting" : "Hello stranger!" ]
    }
}
```
{: codeblock}

Le azioni Swift utilizzano sempre un dizionario e ne producono un altro.

Puoi creare un'azione {{site.data.keyword.openwhisk_short}} denominata `helloSwift` partendo
da questa funzione:

```
wsk action create helloSwift hello.swift
```
{: pre}

Quando utilizzi la riga di comando e un file di origine `.swift`, non devi necessariamente
specificare che stai creando un'azione Swift (e non un'azione JavaScript),
poiché lo strumento lo desume dall'estensione del file.

Le azioni Swift vengono richiamate come le azioni JavaScript:

```
wsk action invoke --blocking --result helloSwift --param name World
```
{: pre}

```json
  {
      "greeting": "Hello World!"
  }
```

**Attenzione:** le azioni Swift vengono eseguite in un ambiente Linux. L'uso su Linux è ancora in fase di
sviluppo e {{site.data.keyword.openwhisk_short}} di solito utilizza la release più recente disponibile, che non è necessariamente stabile. Inoltre, la versione di Swift utilizzata con {{site.data.keyword.openwhisk_short}} potrebbe essere incoerente con le versioni di Swift delle release stabili di XCode su MacOS.

### Creazione pacchetto di un'azione come eseguibile Swift
{: #openwhisk_actions_swift_zip}

Quando crei un'azione OpenWhisk Swift con un file di origine Swift, questo deve essere compilato in un file binario prima che l'azione venga eseguita. Una volta fatto, le successive chiamate all'azione saranno molto più veloci fino a quando il contenitore della tua azione non viene eliminato. Questo ritardo è noto come ritardo di avvio a freddo. 

Per evitare il ritardo di avvio a freddo, puoi compilare il file Swift in un file binario e quindi caricarlo in OpenWhisk in un file zip. Poiché hai bisogno della struttura OpenWhisk, il modo più semplice per creare il file binario è quello di costruirlo all'interno dello stesso ambiente in cui verrà eseguito. La procedura è la seguente:

- Esegui un contenitore di azioni Swift interattivo.
```
docker run --rm -it -v "$(pwd):/owexec" openwhisk/swift3action bash
```
{: pre}

    Ti troverai in una shell bash all'interno del contenitore Docker. Esegui i seguenti comandi al suo interno:

- Per praticità, installa lo zip per creare un pacchetto del file binario
  ```
  apt-get install -y zip
  ```
  {: pre}
- Copia il codice sorgente e preparati a costruirlo
  ```
  cp /owexec/hello.swift /swift3Action/spm-build/main.swift 
  ```
  {: pre}
  ```
  cat /swift3Action/epilogue.swift >> /swift3Action/spm-build/main.swift
  ```
  {: pre}
  ```
  echo '_run_main(mainFunction:main)' >> /swift3Action/spm-build/main.swift
  ```
  {: pre}
- zBuild e link
  ```
  /swift3Action/spm-build/swiftbuildandlink.sh
  ```
  {: pre}
- Crea l'archivio zip
  ```
  cd /swift3Action/spm-build
  ```
  {: pre}
  ```
  zip /owexec/hello.zip .build/release/Action
  ```
- Esci dal contenitore Docker
  ```
  exit
  ```
  {: pre}
È stato creato hello.zip nella stessa directory di hello.swift. 
-Caricalo in OpenWhisk con il nome azione helloSwifty:
  ```
  wsk action update helloSwiftly hello.zip --kind swift:3
  ```
  {: pre}
- Per verificare la sua velocità, esegui 
  ```
  wsk action invoke helloSwiftly --blocking
  ``` 
  {: pre}

Il tempo impiegato dall'azione per l'esecuzione è la proprietà "duration" e viene confrontato con il tempo per l'esecuzione con una procedura di compilazione nell'azione hello.

## Creazione di azioni Java
{: #openwhisk_actions_java}

Il processo di creazione di azioni Java è analogo a quello delle azioni JavaScript e Swift. Le seguenti sezioni ti guidano lungo la creazione e la chiamata di una singola azione Java e l'aggiunta di parametri a tale azione.

Per compilare, verificare e archiviare i file Java, devi disporre di [JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) installato localmente.

### Creazione e chiamata di un'azione
{: #openwhisk_actions_java_invoke}

Un'azione Java è un programma Java con un metodo denominato `main` con la firma esatta come nel seguente esempio:
```java
public static com.google.gson.JsonObject main(com.google.gson.JsonObject);
```
{: codeblock}

Ad esempio, crea un file Java denominato `Hello.java` con il seguente contenuto:

```java
import com.google.gson.JsonObject;
public class Hello {
    public static JsonObject main(JsonObject args) {
        String name = "stranger";
        if (args.has("name"))
            name = args.getAsJsonPrimitive("name").getAsString();
        JsonObject response = new JsonObject();
        response.addProperty("greeting", "Hello " + name + "!");
        return response;
    }
}
```
{: codeblock}

Quindi, compila `Hello.java` in un file JAR `hello.jar` nel seguente modo:
```
javac Hello.java
```
{: pre}
```
jar cvf hello.jar Hello.class
```
{: pre}

**Nota:** [google-gson](https://github.com/google/gson) deve essere presente nel tuo CLASSPATH Java durante la compilazione del file Java.

Puoi creare un'azione OpenWhisk denominata `helloJava` da questo file JAR nel seguente modo:

```
wsk action create helloJava hello.jar --main Hello
```

Quando utilizzi la riga di comando e un file di origine `.jar`, non devi necessariamente
specificare che stai creando un'azione Java;
lo strumento lo desume dall'estensione del file.

Devi specificare il nome della classe principale utilizzando `--main`. Una classe principale eleggibile
è una classe che implementa un metodo `main` statico come descritto qui di seguito. Se la classe
non è il pacchetto predefinito, utilizza il nome della classe completo,
ad esempio, `--main com.example.MyMain`.

Le azioni Java vengono richiamate come le azioni JavaScript e Swift:

```
wsk action invoke --blocking --result helloJava --param name World
```
{: pre}

```json
  {
      "greeting": "Hello World!"
  }
```

## Creazione di azioni Docker

Le azioni {{site.data.keyword.openwhisk_short}} Docker ti permettono di scrivere le tue azioni in qualsiasi linguaggio.

Il tuo codice viene compilato in un file binario eseguibile e incorporato in un'immagine Docker. Il programma binario interagisce con il sistema, prendendo l'input proveniente da `stdin` e rispondendo tramite `stdout`.

È necessario, come requisito, disporre di un account Docker Hub.  Per impostare un account e un ID Docker gratuiti, passa a [Docker Hub](https://hub.docker.com){: new_window}.

Per le seguenti istruzioni, supponiamo che l'ID utente Docker sia `janesmith` e che la password sia `janes_password`.  Supponendo che la CLI sia già configurata, sono richiesti tre passaggi per impostare un file binario personalizzato che venga utilizzato da {{site.data.keyword.openwhisk_short}}. Al termine di questa procedura, l'immagine Docker caricata può essere utilizzata come azione.

1. Scarica la struttura di base Docker. Puoi effettuare questa operazione utilizzando la CLI come segue:

  ```
  wsk sdk install docker
  ```
  ```
  {: pre}
  ```
  La struttura di base Docker è ora installata nella directory corrente.
  ```

  ```
  ls dockerSkeleton/
  ```
  {: pre}
  ```
  Dockerfile      README.md       buildAndPush.sh example.c
  ```

  La struttura di base è un template contenitore Docker in cui puoi inserire il tuo codice sotto forma di file binari personalizzati.

2. Configura il tuo file binario personalizzato nella struttura di base black box. La struttura di base include già un programma C che puoi utilizzare.

  ```
  cat dockerSkeleton/example.c
  ```
  {: pre}
  ```c
  #include <stdio.h>
  int main(int argc, char *argv[]) {
      printf("This is an example log message from an arbitrary C program!\n");
      printf("{ \"msg\": \"Hello from arbitrary C program!\", \"args\": %s }",
             (argc == 1) ? "undefined" : argv[1]);
  }
  ```
  {: codeblock}

  Puoi modificare il file come desideri o puoi aggiungere ulteriore codice e dipendenze all'immagine Docker.
  In quest'ultimo caso, potresti dover modificare il `Dockerfile` come necessario per creare il tuo eseguibile.
  Il binario deve trovarsi all'interno del contenitore in `/action/exec`.

  L'eseguibile riceve un singolo argomento dalla riga comandi. Si tratta di una serializzazione della stringa dell'oggetto JSON
  che rappresenta gli argomenti per l'azione. Il programma può accedere a `stdout` o `stderr`.
  Per convenzione, l'ultima riga dell'output _deve_ essere un oggetto JSON in stringhe che rappresenta il risultato dell'azione.

3. Crea l'immagine Docker e caricala attraverso lo script fornito. Devi prima eseguire `docker login` per autenticarti, quindi eseguire lo script con un nome immagine a scelta.

  ```
  docker login -u janesmith -p janes_password
  ```
  {: pre}
  ```
  cd dockerSkeleton
  ```
  {: pre}
  ```
  ./buildAndPush.sh janesmith/blackboxdemo
  ```
  {: pre}

  Nota che una parte del file example.c viene compilata nell'ambito del processo di creazione dell'immagine Docker, quindi non hai bisogno di avere C compilato sulla tua macchina.
  In effetti, a meno che tu non stia compilando il binario su una macchina host compatibile, non può essere eseguito all'interno del contenitore in quanto i formati non corrisponderanno.

  Il tuo contenitore Docker può ora essere utilizzato come azione {{site.data.keyword.openwhisk_short}}.

  ```
  wsk action create --docker example janesmith/blackboxdemo
  ```
  {: pre}

  Nota l'utilizzo di `--docker` durante la creazione di un'azione. Attualmente, si presume che tutte le immagini Docker siano ospitate su Docker Hub.
  L'azione può essere richiamata come qualsiasi altra azione {{site.data.keyword.openwhisk_short}}.

  ```
  wsk action invoke --blocking --result example --param payload Rey
  ```
  {: pre}
  ```json
  {
      "args": {
          "payload": "Rey"
      },
      "msg": "Hello from arbitrary C program!"
  }
  ```

  Per aggiornare l'azione Docker, esegui buildAndPush.sh per caricare l'immagine più recente in Docker Hub. Ciò consentirà al sistema di estrarre la tua nuova immagine Docker la prossima volta che eseguirà il codice per l'azione.
  Se non ci sono contenitori caldi, tutte le nuove chiamate utilizzeranno la nuova immagine Docker.
  Tuttavia, se c'è un contenitore caldo che utilizza una versione precedente della tua immagine Docker, eventuali nuove chiamate continueranno a utilizzare tale immagine a meno che tu non esegua il comando `wsk action update`. Questo indicherà al sistema che per le nuove chiamate deve eseguire un docker pull per ottenere la tua nuova immagine Docker.

  ```
  ./buildAndPush.sh janesmith/blackboxdemo
  ```
  {: pre}

  ```
  wsk action update --docker example janesmith/blackboxdemo
  ```
  {: pre}

  Per ulteriori informazioni sulla creazione di azioni Docker, vedi la sezione [Riferimenti](./openwhisk_reference.html#openwhisk_ref_docker).

## Visualizzazione dell'output di un'azione
{: #openwhisk_actions_polling}

Le azioni {{site.data.keyword.openwhisk_short}} possono essere richiamate da altri utenti, in risposta a vari eventi o nell'ambito di una sequenza di azioni. In questi casi, può essere utile monitorare le chiamate.

Puoi utilizzare la CLI {{site.data.keyword.openwhisk_short}} per visualizzare l'output delle azioni non appena vengono richiamate.

1. Immetti il seguente comando da una shell:
  ```
  wsk activation poll
  ```
  {: pre}

  Questo comando avvia un ciclo di polling che cerca continuamente attivazioni nei log.

2. Passa a un'altra finestra e richiama un'azione:

  ```
  wsk action invoke /whisk.system/samples/helloWorld --param payload Bob
  ```
  {: pre}
  ```
  ok: invoked /whisk.system/samples/helloWorld with id 7331f9b9e2044d85afd219b12c0f1491
  ```

3. Osserva il log delle attivazioni nella finestra di polling:

  ```
  Activation: helloWorld (7331f9b9e2044d85afd219b12c0f1491)
    2016-02-11T16:46:56.842065025Z stdout: hello bob!
  ```

  Allo stesso modo, quando esegui il programma di utilità di polling, puoi vedere i log in tempo reale per individuare eventuali azioni in esecuzione per tuo conto in OpenWhisk.


## Elenco azioni
{: #openwhisk_listing_actions}

Puoi elencare tutte le azioni che hai creato utilizzando:

```
wsk action list
```
{: pre}

Man mano che scrivi più azioni, l'elenco diventa più lungo e può essere utile raggruppare le azioni correlate in dei [pacchetti](./openwhisk_packages.html). Per filtrare l'elenco di azioni per ottenere solo quelle all'interno di uno specifico pacchetto, puoi utilizzare: 

```
wsk action list [PACKAGE NAME]
```
{: pre}


## Eliminazione di azioni
{: #openwhisk_delete_action}

Puoi effettuare una pulizia eliminando le azioni che non desideri utilizzare.

1. Esegui il seguente comando per eliminare un'azione:
  ```
  wsk action delete hello
  ```
  {: pre}
  ```
  ok: deleted hello
  ```

2. Verifica che l'azione non venga più mostrata nell'elenco delle azioni.
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  ```
  {: pre}

## Accesso ai metadati dell'azione nel corpo dell'azione
{: #openwhisk_action_metadata}

L'ambiente dell'azione contiene diverse proprietà specifiche per l'azione in esecuzione.
Questo permette all'azione di funzionare programmaticamente con gli asset OpenWhisk tramite l'API REST
o di impostare un avviso quando l'azione sta per terminare il suo budget di tempo assegnato.
Le proprietà sono accessibili tramite l'ambiente del sistema per tutti i runtime supportati:
le azioni Node.js, Python, Swift, Java e Docker quando si utilizza la struttura di base Docker OpenWhisk.

* `__OW_API_HOST` l'host dell'API per la distribuzione OpenWhisk che sta eseguendo questa azione
* `__OW_API_KEY` la chiave API per l'oggetto che sta richiamando l'azione, questa chiave potrebbe essere una chiave API limitata
* `__OW_NAMESPACE` lo spazio dei nomi per l'_attivazione_ (potrebbe non essere lo stesso dell'azione)
* `__OW_ACTION_NAME` il nome completo dell'azione in esecuzione
* `__OW_ACTIVATION_ID` l'ID di attivazione per l'istanza dell'azione in esecuzione
* `__OW_DEADLINE` il tempo approssimativo in cui questa azione avrà consumato la propria intera quota di durata (misurato in millisecondi)
