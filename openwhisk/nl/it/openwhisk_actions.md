---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Creazione e chiamata di azioni {{site.data.keyword.openwhisk_short}}
{: #openwhisk_actions}

*Ultimo aggiornamento: 22 marzo 2016*

Le azioni sono frammenti di codice senza stato eseguiti sulla piattaforma {{site.data.keyword.openwhisk}}. Un'azione può essere una funzione JavaScript, una funzione Swift o un programma eseguibile personalizzato contenuto in un contenitore Docker. Ad esempio, un'azione può essere utilizzata per rilevare i volti in un'immagine, aggregare una serie di chiamate API o pubblicare un Tweet.
{:shortdesc}

Le azioni possono essere richiamate esplicitamente o eseguite in risposta a un evento. In entrambi i casi, l'esecuzione di un'azione dei risultati sfocia in un record di attivazione identificato da un ID di attivazione univoco. L'input in un'azione e i risultati di un'azione fungono da dizionario di coppie chiave-valore, in cui la chiave è una stringa e il valore è un valore JSON valido.

Le azioni possono essere formate da chiamate ad altre azioni o da una sequenza definita di azioni.

## Creazione e chiamata di azioni JavaScript
{: #openwhisk_create_action_js}

Le seguenti sezioni ti guidano nell'utilizzo di azioni in JavaScript. Partendo dalla creazione e dalla chiamata di un'azione semplice, aggiungerai parametri a un'azione e la richiamerai con dei parametri, imposterai parametri predefiniti e li richiamerai, creerai azioni asincrone e, infine, utilizzerai le sequenze di azioni.


### Creazione e chiamata di un'azione JavaScript semplice
{: #openwhisk_single_action_js}

Consulta la procedura e gli esempi di seguito riportati per creare la tua prima azione JavaScript.

1. Crea un file JavaScript con il seguente contenuto. In questo esempio, il nome file è "hello.js".
  
```
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
  {: screen}

3. Elenca le azioni che hai creato:
  
  ```
  wsk action list
```
  {: pre}
```
  actions
  hello       private
```
  {: screen}

  Puoi vedere l'azione `hello` che hai appena creato.

4. Una volta creata la tua azione, puoi eseguirla nel cloud in {{site.data.keyword.openwhisk_short}} con il comando "invoke". Puoi chiamare le azioni con una chiamata *bloccante* o *non bloccante*, specificando un indicatore nel comando. Una chiamata bloccante attende il completamento dell'azione e restituisce un risultato. Questo esempio utilizza il parametro bloccante `-blocking`:

```
  wsk action invoke --blocking hello
```
  {: pre}
```
  ok: invoked hello with id 44794bd6aab74415b4e42a308d880e5b
  response:
  {
      "result": {
          "payload": "Hello world"
      },
      "status": "success",
      "success": true
  }
```
  {: screen}

  Il comando restituisce due informazioni importanti:
  * L'ID di attivazione (`44794bd6aab74415b4e42a308d880e5b`)
  * Il risultato della chiamata

  Il risultato, in questo caso, è la stringa `Hello world` restituita dalla funzione JavaScript. L'ID di attivazione può essere utilizzato per richiamare i log o il risultato della chiamata in un momento successivo.  

5. Se non ti serve subito il risultato dell'azione, puoi omettere l'indicatore `--blocking` ed effettuare una chiamata non bloccante. Puoi ottenere il risultato successivamente attraverso l'ID di attivazione. Vedi il seguente esempio:

```
  wsk action invoke hello
```
  {: pre}
```
  ok: invoked hello with id 6bf1f670ee614a7eb5af3c9fde813043
```
  {: screen}

```
  wsk activation result 6bf1f670ee614a7eb5af3c9fde813043
```
  {: pre}
```
  {
      "payload": "Hello world"
  }
```
  {: screen}

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
  {: screen}

### Trasmissione di parametri a un'azione
{: #openwhisk_adding_parameters_js}

È possibile trasmettere dei parametri all'azione quando viene richiamata.

1. Utilizza i parametri nell'azione. Ad esempio, aggiorna il file "hello.js" con il seguente contenuto:
  
  ```
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
```
  wsk action invoke --blocking --result hello --param name 'Bernie' --param place 'Vermont'
```
  {: pre}
```
  {
      "payload": "Hello, Bernie from Vermont"
  }
```
  {: screen}

  Osserva l'uso dell'opzione `--param` per specificare il nome e il valore del parametro e dell'opzione `--result` per visualizzare solo il risultato della chiamata.

### Impostazione dei parametri predefiniti
{: #openwhisk_binding_actions}

Le azioni possono essere richiamate con più parametri. Ricorda che l'azione `hello` dell'esempio precedente prevede due parametri: il *nome* di una persona e il *luogo* di provenienza.

Anziché trasmettere ogni volta tutti i parametri a un'azione, puoi eseguire il bind di determinati parametri. Il seguente esempio esegue il bind del parametro *place*, cosicché l'azione assuma come valore predefinito il luogo "Vermont":
 
1. Aggiorna l'azione utilizzando l'opzione `--param` per eseguire il bind dei valori parametro.

```
  wsk action update hello --param place 'Vermont'
```
  {: pre}

2. Richiama l'azione, trasmettendo stavolta solo il parametro `name`.

```
  wsk action invoke --blocking --result hello --param name 'Bernie'
```
  {: pre}
```
  {
      "payload": "Hello, Bernie from Vermont"
  }
```
  {: screen}

  Nota che non hai dovuto specificare il parametro del luogo quando hai richiamato l'azione. I parametri associati mediante bind possono sempre essere sovrascritti specificando il valore del parametro al momento della chiamata.

3. Richiama l'azione, trasmettendo il valore sia di `name` che di `place`. Quest'ultimo sovrascrive il valore associato mediante bind all'azione.

```
  wsk action invoke --blocking --result hello --param name 'Bernie' --param place 'Washington, DC'
```
  {: pre}
```
  {  
      "payload": "Hello, Bernie from Washington, DC"
  }
```
  {: screen}

### Creazione di azioni asincrone
{: #openwhisk_asynchrony_js}

Le funzioni JavaScript che proseguono l'esecuzione in una funzione di callback potrebbero dover restituire il risultato dell'attivazione dopo la restituzione della funzione `main`. Puoi effettuare questa operazione utilizzando nella tua azione le funzioni `whisk.async()` e `whisk.done()`.

1. Salva il seguente contenuto in un file denominato `asyncAction.js`.

```
  function main() {
      setTimeout(function() {
          return whisk.done({done: true});
      }, 20000);
      return whisk.async();
  }
```
  {: codeblock}

  Nota che la funzione `main` viene restituita immediatamente e che il valore restituito da `whisk.async()` indica che questa attivazione deve rimanere in esecuzione.

  In questo caso, la funzione JavaScript `setTimeout()` attende venti secondi prima di richiamare la funzione di callback, in cui la chiamata a `whisk.done()` indica che l'attivazione è completa.

2. Esegui i seguenti comandi per creare l'azione e richiamarla:

```
  wsk action create asyncAction asyncAction.js
```
  {: pre}
```
  wsk action invoke --blocking --result asyncAction
```
 {: pre}
```
   {
      "done": true
  }
```
  {: screen}

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
  {: screen}


```
  wsk activation get b066ca51e68c4d3382df2d8033265db0
```
  {: pre}
```
  {
      "start": 1455881628103,
      "end":   1455881648126,
      ...
  }
```
  {: screen}

  Confrontando la data/ora `start` con la data/ora `end` nel record di attivazione, puoi osservare che il completamento di questa attivazione ha richiesto poco più di venti secondi.


### Utilizzo di azioni per la chiamata di un'API esterna
{: #openwhisk_apicall_action}

Gli esempi forniti finora hanno rappresentato funzioni JavaScript autonome. Puoi creare anche un'azione che richiama un'API esterna.

Questo esempio richiama un servizio Yahoo Meteo per ottenere le condizioni attuali in un'ubicazione specifica. 

1. Salva il seguente contenuto in un file denominato `weather.js`.
```
    var request = require('request');
    
    function main(msg) {
        var location = msg.location || 'Vermont';
        var url = 'https://query.yahooapis.com/v1/public/yql?q=select item.condition from weather.forecast where woeid in (select woeid from geo.places(1) where text="' + location + '")&format=json';
    
        request.get(url, function(error, response, body) {
            var condition = JSON.parse(body).query.results.channel.item.condition;
            var text = condition.text;
            var temperature = condition.temp;
            var output = 'It is ' + temperature + ' degrees in ' + location + ' and ' + text;
            whisk.done({msg: output});
        });
    
        return whisk.async();
    }
```
  {: codeblock}

  Nota che l'azione dell'esempio utilizza la libreria JavaScript `request` per effettuare una richiesta HTTP all'API Yahoo Meteo ed estrae campi dal risultato JSON. I [riferimenti](./openwhisk_reference.html#runtime_ref_runtime_environment) indicano nel dettaglio i pacchetti Node.js che puoi utilizzare nelle tue azioni.
  
  Questo esempio mostra anche la necessità di eseguire azioni asincrone. L'azione restituisce `whisk.async()` per indicare che il risultato di questa azione non è ancora disponibile nel momento in cui viene restituita la funzione. Il risultato sarà invece disponibile nel callback `request` al completamento della chiamata HTTP e verrà trasmesso come argomento alla funzione `whisk.done()`.

2. Esegui i seguenti comandi per creare l'azione e richiamarla:
  ```
  wsk action create weather weather.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result weather --param location 'Brooklyn, NY'
  ```
  {: pre}
  ```
  {
      "msg": "It is 28 degrees in Brooklyn, NY and Cloudy"
  }
  ```
  {: screen}

### Creazione di sequenze di azioni
{: #openwhisk_create_action_sequence}

Puoi creare un'azione che concatena una sequenza di azioni.

In un pacchetto denominato `/whisk.system/util` vengono fornite varie azioni di utilità che puoi utilizzare per creare la tua prima sequenza. Per ulteriori informazioni sui pacchetti, vedi la sezione [Pacchetti](./openwhisk_packages.html).

1. Visualizza le azioni del pacchetto `/whisk.system/util`.
  
```
  wsk package get --summary /whisk.system/util
```
  {: pre}
```
  package /whisk.system/util
   action /whisk.system/util/cat: Concatenate array of strings, and split lines into an array
   action /whisk.system/util/head: Filter first K array elements and discard rest
   action /whisk.system/util/date: Get current date and time
   action /whisk.system/util/sort: Sort array
```
  {: screen}

  In questo esempio utilizzerai le azioni `cat` e `sort`.

2. Crea una sequenza di azioni in modo che il risultato di un'azione venga trasmesso come argomento all'azione successiva.
  
```
  wsk action create myAction --sequence /whisk.system/util/cat,/whisk.system/util/sort
```
  {: pre}

  Questa sequenza di azioni converte alcune righe di testo in array e ordina le righe.

3. Prima di richiamare la sequenza di azioni, crea un file di testo denominato "haiku.txt" inserendo alcune righe di testo:

```
  Over-ripe sushi,
  The Master
  Is full of regret.
```
  {: codeblock}

4. Richiama l'azione:
  
```
  wsk action invoke --blocking --result myAction --param payload "$(cat haiku.txt)"
```
  {: pre}
```
  {
      "length": 3,
      "lines": [
          "Is full of regret.",
          "Over-ripe sushi,",
          "The Master"
      ]
  }
```
  {: screen}

  Nel risultato, noterai che le righe sono ordinate.

**Nota**: per ulteriori informazioni sulla chiamata delle sequenze di azioni con l'indicazione di più parametri, vedi [Impostazione dei parametri predefiniti](./openwhisk_actions.html##openwhisk_binding_actions)

## Creazione di azioni Swift
{: #openwhisk_actions_swift}

Il processo di creazione di azioni Swift è analogo a quello delle azioni JavaScript. Le seguenti sezioni ti guidano lungo la creazione e la chiamata di una singola azione swift e l'aggiunta di parametri a tale azione.

Puoi inoltre utilizzare il [Swift Sandbox](https://swiftlang.ng.bluemix.net) online per testare il tuo codice Swift senza dover installare Xcode sulla tua macchina.

### Creazione e chiamata di un'azione
{: #openwhisk_actions_invoke_swift}

Un'azione è semplicemente una funzione Swift di livello superiore. Ad esempio, crea un file denominato
`hello.swift` con il seguente contenuto:

```
  func main(args: [String:Any]) -> [String:Any] {
      if let name = args["name"] as? String {
          return [ "greeting" : "Hello \(name)!" ]
      } else {
          return [ "greeting" : "Hello stranger!" ]
      }
  }
```
{: codeblock}

Nota che esattamente come le azioni JavaScript, le azioni Swift utilizzano sempre un
dizionario e ne producono un altro.

Puoi creare un'azione {{site.data.keyword.openwhisk_short}} denominata `helloSwift` partendo
da questa funzione:

```
wsk action create helloSwift hello.swift
```
{: pre}

Quando utilizzi la riga di comando e un file di origine `.swift`, non devi necessariamente
specificare che stai creando un'azione Swift (e non un'azione JavaScript), poiché
lo strumento lo desume dall'estensione del file.

Le azioni Swift vengono richiamate come le azioni JavaScript:

```
wsk action invoke --blocking --result helloSwift --param name World
```
{: pre}

```
  {
      "greeting": "Hello World!"
  }
```
{: screen}

**Attenzione:** le azioni Swift vengono eseguite in un ambiente Linux. L'uso su Linux è ancora in fase di
sviluppo e {{site.data.keyword.openwhisk_short}} di solito utilizza la release più recente disponibile, che non è necessariamente stabile. Inoltre, la versione di Swift utilizzata con {{site.data.keyword.openwhisk_short}} potrebbe essere incoerente con le versioni di Swift delle release stabili di XCode su MacOS.

## Creazione di azioni Docker
{: #openwhisk_actions_docker}

Le azioni {{site.data.keyword.openwhisk_short}} Docker ti permettono di scrivere le tue azioni in qualsiasi linguaggio.

Il tuo codice viene compilato in un file binario eseguibile e incorporato in un'immagine Docker. Il programma binario interagisce con il sistema, prendendo l'input proveniente da `stdin` e rispondendo tramite `stdout`.

È necessario, come requisito, disporre di un account Docker Hub.  Per impostare un account e un ID Docker gratuiti, passa a [Docker Hub](https://hub.docker.com){: new_window}.

Per le seguenti istruzioni, poniamo che l'ID utente sia "janesmith" e che la password sia "janes_password".  Supponendo che la CLI sia già stata configurata, l'impostazione di un file binario personalizzato che venga utilizzato da {{site.data.keyword.openwhisk_short}} richiede tre passaggi.  Al termine di questa procedura, l'immagine Docker caricata può essere utilizzata come azione.

1. Scarica la struttura di base Docker. Puoi effettuare questa operazione utilizzando la CLI come segue:

```
  wsk sdk install docker
```
  {: pre}
```
  La struttura di base Docker è ora installata nella directory corrente.
```
  {: screen}

```
  ls dockerSkeleton/
```
  {: pre}
```
  Dockerfile      README.md       buildAndPush.sh client          server
```
  {: screen}

  La struttura di base è un template contenitore Docker in cui puoi inserire il tuo codice sotto forma di file binari personalizzati.

2. Configura il tuo file binario personalizzato nella struttura di base black box. La struttura di base include già un programma C che puoi utilizzare.

```
  cat ./dockerSkeleton/client/example.c
```
  {: pre}
  {: pre}
```
  #include <stdio.h>
  
  int main(int argc, char *argv[]) {
      printf("Hello %s from arbitrary C program!\n",
             (argc == 1) ? "anonymous" : argv[1]);
  }
```
  {: screen}

  Puoi modificare il file come desideri.

3. Crea l'immagine Docker e caricala attraverso lo script fornito. Devi prima eseguire `login docker` per autenticarti, quindi eseguire lo script con un nome immagine a scelta.

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

4. Per creare un'azione a partire da un'immagine Docker invece che da un file JavaScript fornito, aggiungi `--docker` e sostituire il nome del file JavaScript con il nome dell'immagine Docker.

```
  wsk action create --docker example janesmith/blackboxdemo
```
  {: pre}
```
  wsk action invoke --blocking --result example --param payload Rey
```
  {: pre}
```
  {
      "msg": "Hello Rey from arbitrary C program!\n"
  }
```
  {: screen}


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
  {: screen}

3. Osserva il log delle attivazioni nella finestra di polling:

```
  Activation: helloWorld (7331f9b9e2044d85afd219b12c0f1491)
    2016-02-11T16:46:56.842065025Z stdout: hello bob!
```
  {: screen}

  Allo stesso modo, quando esegui il programma di utilità di polling, puoi vedere i log in tempo reale per individuare eventuali azioni in esecuzione per tuo conto in {{site.data.keyword.openwhisk_short}}.

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
  {: screen}

2. Verifica che l'azione non venga più mostrata nell'elenco delle azioni.
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  ```
  {: screen}
