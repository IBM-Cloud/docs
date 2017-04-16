---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Informazioni su {{site.data.keyword.openwhisk_short}}

{{site.data.keyword.openwhisk}} è una piattaforma di elaborazione guidata dagli eventi, indicata anche come Serverless computing o FaaS (Function as a Service), che esegue il codice in risposta a eventi o chiamate dirette. La seguente figura mostra l'architettura di alto livello di {{site.data.keyword.openwhisk}}.
{: shortdesc}

![Architettura di {{site.data.keyword.openwhisk_short}}](./images/OpenWhisk.png)

Esempi di eventi includono le modifiche ai record di database, letture del sensore IoT che superano una determinata temperatura, nuovi commit di codice a un repository GitHub o semplici richieste HTTP provenienti da applicazioni Web o mobili. Gli eventi provenienti da origini eventi interne ed esterne vengono incanalati attraverso un trigger e le regole consentono alle azioni di reazione a tali eventi.

Le azioni possono essere piccoli frammenti di codice Javascript o Swift oppure codice binario personalizzato integrato in un contenitore Docker. Le azioni di {{site.data.keyword.openwhisk_short}} vengono distribuite istantaneamente ed eseguite ogni volta che un trigger viene attivato. Più trigger vengono attivati, più azioni vengono richiamate. Se non viene attivato alcun trigger, non ci sono codici azione in esecuzione e, dunque, nessun consumo.

Oltre che con l'associazione delle azioni ai trigger, è possibile richiamare direttamente un'azione utilizzando l'API, la CLI o l'SDK iOS {{site.data.keyword.openwhisk_short}}. È possibile concatenare una serie di azioni anche senza dover scrivere alcun codice. Ciascuna azione della catena viene richiamata in sequenza con l'output di un'azione che viene trasmessa come input alla successiva azione della sequenza.

Con contenitori o macchine virtuali tradizionali a esecuzione prolungata, è prassi comune distribuire più macchine virtuali o contenitori in modo da difendersi dalle interruzioni di una singola istanza. Tuttavia, {{site.data.keyword.openwhisk_short}} offre un modello alternativo privo di costi correlati alla resilienza. L'esecuzione di azioni su richiesta fornisce una scalabilità intrinseca e un utilizzo ottimale, poiché il numero di azioni in esecuzione corrisponde sempre al tasso di trigger. Inoltre, lo sviluppatore ora si concentra solo sul codice, senza preoccuparsi di monitorare, applicare patch e proteggere l'infrastruttura di sistema, la rete, l'archiviazione e il server sottostanti.

Le integrazioni con servizi aggiuntivi e provider di eventi possono essere aggiunte con i pacchetti. Un pacchetto è una raccolta di feed e azioni. Un feed è un pezzo di codice che configura un'origine eventi esterna per l'attivazione di eventi trigger. Ad esempio, un trigger creato con un feed di modifica Cloudant configurerà un servizio per l'attivazione del trigger ad ogni aggiunta o modifica di un documento in un database Cloudant. Le azioni dei pacchetti rappresentano una logica riutilizzabile, che può essere resa disponibile da un fornitore di servizi cosicché gli sviluppatori non debbano limitarsi a utilizzare il servizio come un'origine eventi, ma possano anche richiamare le API di tale servizio.

Un catalogo di pacchetti esistente consente di ampliare le applicazioni con funzioni utili e accedere a servizi esterni appartenenti all'ecosistema con rapidità. Sono esempi di servizi esterni con attivazione {{site.data.keyword.openwhisk_short}}: Cloudant, The Weather Company, Slack e GitHub.


## Modalità di funzionamento di {{site.data.keyword.openwhisk_short}}
{: #openwhisk_how}

Trattandosi di un progetto open-source, OpenWhisk ha alle spalle giganti come Nginx, Kafka, Consul, Docker, CouchDB. Tutti questi componenti si uniscono per formare un “servizio di programmazione basato su eventi serverless”. Per spiegare tutti i componenti in modo più dettagliato, tracciamo come si svolge una chiamata di un'azione nel sistema. Una chiamata in OpenWhisk è la principale operazione di un motore serverless: eseguire il codice che l'utente ha immesso nel sistema e restituire i risultati di tale esecuzione.

### Creazione dell'azione

Per dare alla spiegazione un po' più di contesto, creiamo prima una azione nel sistema. Utilizzeremo questa azione per spiegare i concetti in seguito durante la traccia nel sistema. I seguenti comandi presuppongono che la [CLI OpenWhisk sia configurata correttamente](https://github.com/openwhisk/openwhisk/tree/master/docs#setting-up-the-openwhisk-cli).

Innanzitutto, creeremo un file *action.js* contenente il seguente codice che stamperà “Hello World” in stdout e restituirà un oggetto JSON contenente “world” sotto la chiave “hello”.
```javascript
function main() {
    console.log('Hello World');
    return { hello: 'world' };
}
```
{: codeblock}

Creiamo l'azione utilizzando:
```
wsk action create myAction action.js
```
{: pre}

Fatto. Ora vogliamo davvero richiamare l'azione:
```
wsk action invoke myAction
```
{: pre}

## Il flusso interno di elaborazione
Che cosa succede realmente dietro le quinte di OpenWhisk?

![Flusso di elaborazione OpenWhisk](images/OpenWhisk_flow_of_processing.png)

### Accesso al sistema: nginx

Primo: l'API rivolta agli utenti OpenWhisk è completamente basata su HTTP e segue una progettazione RESTful. Di conseguenza, il comando inviato tramite wsk-CLI è essenzialmente una richiesta HTTP nel sistema OpenWhisk. Il comando sopra specificato si traduce all'incirca come:
```
POST /api/v1/namespaces/$userNamespace/actions/myAction
Host: $openwhiskEndpoint
```
{: screen}

Nota la variabile *$userNamespace*. Un utente ha accesso ad almeno uno spazio dei nomi. Per semplicità, supponiamo che l'utente possieda lo spazio dei nomi in cui è inserito *myAction*.

Il primo punto di ingresso nel sistema avviene attraverso **nginx**, “un server proxy inverso e HTTP”. È utilizzato principalmente per la terminazione SSL e per l'inoltro di chiamate HTTP appropriate al componente successivo.

### Accesso al sistema: Controller

Non avendo contribuito molto alla nostra richiesta HTTP, nginx la inoltra al **Controller**, il componente successivo del nostro viaggio attraverso OpenWhisk. Si tratta di un'implementazione basata su Scala della reale API REST (basata su **Akka** e **Spray**) e funge quindi da interfaccia per tutte le operazioni che un utente può eseguire, incluse le richieste [CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete) per le tue entità in OpenWhisk e la chiamata di azioni (che è quello che stiamo facendo in questo momento).

Per prima cosa il Controller disambigua ciò che l'utente sta tentando di fare e lo fa in base al metodo HTTP che utilizzi nella tua richiesta HTTP. Come da traduzione precedente, l'utente emette una richiesta POST a un'azione esistente, che il Controller traduce in una **chiamata di un'azione**.

Dato il ruolo centrale del Controller (da cui il nome), sarà coinvolto in una certa misura in tutte le seguenti operazioni.

### Autenticazione e autorizzazione: CouchDB

Adesso il Controller verifica chi sei (*Autenticazione*) e se disponi del privilegio di fare ciò che vuoi con quella entità (*Autorizzazione*). Le credenziali incluse nella richiesta vengono verificate nel cosiddetto database **soggetti** in un'istanza **CouchDB**.

In questo caso, viene verificato che l'utente esista nel database OpenWhisk e che disponga del privilegio per richiamare l'azione myAction, che si suppone sia l'azione in uno spazio dei nomi proprio dell'utente. Questo dà effettivamente all'utente il privilegio di richiamare l'azione, che è ciò che vuole fare.

A questo punto, tutto è pronto per la prossima fase di elaborazione.

### Richiamo dell'azione: di nuovo CouchDB…

Poiché adesso il Controller è sicuro che l'utente è autorizzato e che dispone dei privilegi per richiamare l'azione, carica questa azione (in questo caso *myAction*) dal database **whisks** in CouchDB.

Il record dell'azione contiene principalmente il codice da eseguire (mostrato sopra) e i parametri predefiniti che vuoi passare alla tua azione, uniti ai parametri che hai incluso nell'effettiva richiesta di chiamata. Contiene inoltre le restrizioni della risorsa imposte per l'esecuzione, come ad esempio la quantità di memoria che può consumare.

In questo caso particolare, la nostra azione non prende alcun parametro (la definizione dei parametri della funzione è un elenco vuoto), quindi supponiamo di non aver impostato alcun parametro predefinito e di non aver inviato specifici parametri all'azione, rendendolo così il caso più semplice.

### Chi richiama l'azione: Consul

Il Controller (o più specificamente la sua di parte bilanciamento del carico) ha ora tutto pronto per l'esecuzione del tuo codice. Deve però sapere chi è disponibile a farlo. Viene utilizzato **Consul**, un rilevatore di servizi, per tenere traccia degli esecutori disponibili nel sistema controllando continuamente il loro stato di integrità. Questi esecutori sono chiamati **Invoker**.

Il Controller, che ora sa quali Invoker sono disponibili, ne sceglie uno per richiamare l'azione richiesta.

Per questo caso, supponiamo che il sistema abbia 3 Invoker disponibili, da 0 a 2, e che il Controller scelga *Invoker 2* per richiamare l'azione in questione.

### Forma una fila: Kafka

D'ora in poi, alla richiesta di chiamata inviata possono accadere principalmente due cose negative:

1. Il sistema può arrestarsi in modo anomalo, perdendo così la tua chiamata
2. Il carico di lavoro del sistema potrebbe essere eccessivo e la chiamata deve prima attendere il completamento di altre chiamate.

La risposta a entrambi i problemi è **Kafka**, “un sistema di messaggistica di pubblicazione-sottoscrizione distribuito ad alta velocità”. Il Controller e l'Invoker comunicano esclusivamente attraverso i messaggi inviati in buffer e resi persistenti da Kafka. Ciò alleggerisce il carico di buffer in memoria, che può provocare una *OutOfMemoryException*, per il Controller e l'Invoker garantendo anche che i messaggi non vadano persi in caso di arresto anomalo del sistema.

Per far richiamare l'azione, il Controller pubblica dunque un messaggio in Kafka, che include l'azione da richiamare e i parametri da passare all'azione (in questo caso, nessuno). Questo messaggio viene indirizzato all'Invoker che il Controller ha scelto dall'elenco ottenuto da Consul.

Una volta che Kafka ha confermato la ricezione del messaggio, la richiesta HTTP per l'utente riceve come risposta un **ActivationId**. L'utente lo utilizzerà successivamente per accedere ai risultati di questa chiamata specifica. Questo è un modello di chiamata asincrono, in cui la richiesta HTTP termina dopo che il sistema ha accettato la richiesta di richiamare un'azione. È disponibile anche un modello sincrono (detto chiamata bloccante), che però non è trattato in questo articolo.

### Chiamata del codice: Invoker

L'**Invoker** è il cuore di OpenWhisk. Il compito dell'Invoker è quello di richiamare un'azione, è implementato anche in Scala, ma non è tutto. Per eseguire azioni in modo isolato e sicuro, utilizza  **Docker**.

Docker è utilizzato per configurare un nuovo ambiente automaticamente incapsulato (chiamato *contenitore*) per ogni azione che richiamiamo in modo rapido, isolato e controllato. Il processo è semplice: per ogni chiamata di azione viene generato un contenitore Docker, viene inserito il codice dell'azione, si passa alla sua esecuzione utilizzando i parametri trasmessi, si ottiene il risultato e infine il contenitore viene distrutto. Qui è anche dove viene eseguita al massimo l'ottimizzazione delle prestazioni per ridurre il sovraccarico e limitare il più possibile i tempi di risposta. 

Nel nostro caso specifico, poiché abbiamo un'azione basata su *Node.js*, l'Invoker avvierà un contenitore Node.js, inserirà il codice da *myAction*, lo eseguirà senza parametri, estrarrà il risultato, salverà i log e distruggerà il contenitore Node.js.

### Memorizzazione dei risultati: di nuovo CouchDB

Quando l'Invoker riceve il risultato, questo viene memorizzato nel database **whisks** in forma di attivazione sotto l'ActivationId menzionato sopra. Il database **whisks** risiede in **CouchDB**.

Nel nostro caso specifico, l'Invoker recupera l'oggetto JSON risultante dall'azione, prende il log scritto da Docker, li inserisce nel codice di attivazione e memorizza il tutto nel database. Il risultato è simile al seguente:

```json
{
   "activationId": "31809ddca6f64cfc9de2937ebd44fbb9",
   "response": {
       "statusCode": 0,
       "result": {
           "hello": "world"
       }
   },
   "end": 1474459415621,
   "logs": [
       "2016-09-21T12:03:35.619234386Z stdout: Hello World"
   ],
   "start": 1474459415595,
}
```
{: codeblock}

Nota che il record contiene sia il risultato restituito sia i log scritti. Contiene anche l'ora di inizio e di fine della chiamata dell'azione. In un record di attivazione sono presenti più campi; per semplicità viene qui visualizzata una versione ridotta.

Adesso puoi utilizzare di nuovo l'API REST (iniziando dal passo 1) per ottenere la tua attivazione e il risultato della tua azione. Per farlo, devi utilizzare:

```bash
wsk activation get 31809ddca6f64cfc9de2937ebd44fbb9
```
{: pre} 

### Riepilogo

Abbiamo visto come un semplice **wsk action invoke myAction** passa attraverso diverse fasi del sistema {{site.data.keyword.openwhisk_short}}. Il sistema si compone principalmente di due soli componenti personalizzati, il **Controller** e l'**Invoker**. Tutto il resto è già lì, sviluppato da tantissime persone nella community open-source.

Puoi trovare ulteriori informazioni su {{site.data.keyword.openwhisk_short}} nei seguenti argomenti:

* [Nomi entità](./openwhisk_reference.html#openwhisk_entities)
* [Semantica delle azioni](./openwhisk_reference.html#openwhisk_semantics)
* [Limiti](./openwhisk_reference.md#openwhisk_syslimits)
* [API REST](./openwhisk_reference.md#openwhisk_ref_restapi)
