---

 

copyright:

  years: 2016
lastupdated: "2016-09-09"
 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Implementazione di feed
{: #openwhisk_feeds}

OpenWhisk supporta un'API aperta, in cui ogni utente può esporre un servizio di produzione eventi in forma di **feed** in un **pacchetto**.   Questa sezione descrive le opzioni di architettura e implementazione per fornire i propri feed.

Questo materiale è destinato agli utenti esperti di OpenWhisk che intendono pubblicare i propri feed.  La maggior parte degli utenti OpenWhisk può tranquillamente saltare questa sezione.

## Architettura dei feed

Esistono almeno 3 modelli architetturali per la creazione di un feed: **Hook**, **Polling** e **Connessioni**.

### Hook
Nel modello *Hook*, impostiamo un feed utilizzando una funzione [webhook](https://en.wikipedia.org/wiki/Webhook) esposta da un altro servizio.   In questa strategia, configuriamo un webhook su un servizio esterno per consentire di pubblicare direttamente in un URL per attivare un trigger.  Questa è di gran lunga l'opzione più semplice e interessante per implementare feed a bassa frequenza.

### Polling
Nel modello "Polling", disponiamo di un'*azione* OpenWhisk per eseguire periodicamente il polling di un endpoint per il recupero di nuovi dati.
Questo modello è relativamente semplice da costruire, ma la frequenza degli eventi sarà ovviamente
limitata dall'intervallo di polling.

### Connessioni
Nel modello "Connessioni", impostiamo in un qualsiasi punto un servizio separato che mantiene una connessione permanente a un'origine di feed.    L'implementazione basata sulla connessione può interagire con un endpoint del servizio mediante il polling lungo o per impostare una notifica di push.


## Differenza tra feed e trigger

I feed e i trigger sono strettamente correlati,
ma restano due concetti tecnicamente distinti.   

- OpenWhisk elabora gli **eventi** che fluiscono nel sistema.

- Un **trigger** è tecnicamente un nome per una classe di eventi.   Ogni evento appartiene esattamente a un solo trigger; per analogia, un trigger assomiglia a un *argomento* nei sistemi di pubblicazione/sottoscrizione
basati sugli argomenti.    Una **regola** *T -> A* significa che "ogni volta che un evento arriva da un trigger *T*, si richiama l'azione *A* con il payload del trigger.

- Un **feed** è un flusso di eventi che appartengono tutti a un trigger *T*.    Un feed è controllato da un'**azione di feed** che gestisce la creazione, eliminazione, sospensione e ripristino del flusso di eventi che comprendono un feed.    In genere, l'azione di feed interagisce con i servizi esterni che producono gli eventi, tramite un'API REST che gestisce le notifiche.

##  Implementazione delle azioni di feed

L'*azione di feed* è una normale *azione* OpenWhisk, ma deve accettare i seguenti parametri:
* **lifecycleEvent**: un valore tra 'CREATE', 'DELETE', 'PAUSE' o 'UNPAUSE'
* **triggerName**: il nome completo del trigger che contiene gli eventi prodotti da questo feed.
* **authKey**: le credenziali di autenticazione di base dell'utente OpenWhisk che possiede il trigger appena citato

L'azione di feed può anche accettare qualsiasi altro parametro necessario per gestire il feed.  Ad esempio, l'azione di feed relativa alle modifiche cloudant prevede di ricevere parametri che includono *'dbname'*, *'username'* ecc.

Quando l'utente crea un trigger dalla CLI con il parametro **--feed**, il sistema richiama automaticamente l'azione di feed con i parametri appropriati.

Ad esempio, supponiamo che l'utente abbia creato un bind `mycloudant` per il pacchetto `cloudant`
con il proprio nome utente e password come parametri associati.  Quando l'utente immette il seguente comando dalla CLI,

`wsk trigger create T --feed mycloudant/changes -p dbName myTable`

il sistema effettuerà un'azione simile alla seguente:

`wsk action invoke mycloudant/changes -p lifecycleEvent CREATE -p triggerName T -p authKey <userAuthKey> -p password <password value from mycloudant binding> -p username <username value from mycloudant binding> -p dbName mytype`

L'azione di feed denominata *changes* acquisisce questi parametri e viene intrapresa ogni azione necessaria per impostare un flusso di eventi da Cloudant, con la configurazione appropriata, indirizzato al trigger *T*.    

Per il feed *changes* di Cloudant, l'azione avviene per comunicare direttamente con un servizio *trigger cloudant* che abbiamo implementato con un'architettura basata sulla connessione.   Le altre architetture verranno illustrate di seguito.

Un protocollo di azione di feed simile si verifica per `wsk trigger delete`.    

## Implementazione di feed con gli hook

È facile configurare un feed mediante un hook se il produttore eventi supporta una funzione webhook/callback.

Con questo metodo, *non è necessario* impostare un servizio permanente al di fuori di OpenWhisk.  Tutta la gestione dei feed avviene naturalmente tramite le *azioni di feed* OpenWhisk senza stato, che interagiscono
direttamente con un'API webhook di terze parti.

Quando richiamata con `CREATE`, l'azione di feed installa semplicemente un webhook per qualche altro servizio, chiedendo al servizio remoto di pubblicare le notifiche all'ULR `fireTrigger` appropriato in OpenWhisk.

Il webhook deve essere indirizzato per l'invio di notifiche a un URL come nel seguente esempio:

`POST /namespaces/{namespace}/triggers/{triggerName}`

Il modulo con la richiesta POST verrà interpretato come documento JSON che definisce i parametri per l'evento trigger.
Le regole OpenWhisk passano questi parametri trigger a qualsiasi azione da attivare come risultato dell'evento.

## Implementazione di feed con il polling

È possibile configurare un'*azione* OpenWhisk per eseguire il polling di un'origine di feed interamente all'interno di OpenWhisk, senza la necessità di impostare connessioni permanenti o servizi esterni.

Per i feed in cui non è disponibile un webhook, ma non sono necessari tempi di risposta a bassa latenza o di grandi volumi, il polling risulta essere un'opzione interessante.

Per impostare un feed basato sul polling, l'azione di feed utilizza i seguenti passi quando viene chiamata per eseguire `CREATE`:

1.   L'azione di feed imposta un trigger periodico (*T*) con la frequenza desiderata, utilizzando il feed `whisk.system/alarms`.
2.   Lo sviluppatore del feed crea un'azione `pollMyService` che esegue semplicemente il polling del servizio remoto e restituisce tutti i nuovi eventi.
3.  L'azione di feed imposta una *regola* *T -> pollMyService*.

Questa procedura implementa un trigger basato sul polling utilizzando esclusivamente azioni OpenWhisk, senza bisogno di un servizio separato.

## Implementazione di feed tramite le connessioni

Le due precedenti scelte architetturali sono semplici e facili da implementare. Tuttavia, se vuoi ottenere un feed ad alte prestazioni, non esiste alternativa alle connessioni permanenti e polling lungo o tecniche simili.

Poiché le azioni OpenWhisk devono essere di breve esecuzione, un'azione non può mantenere una connessione permanente a una terza parte. Dobbiamo invece
impostare un servizio separato (esterno a OpenWhisk) che sia sempre in esecuzione.   Questi sono chiamati *servizi provider*.  Un servizio provider può mantenere connessioni a origini eventi di terze parti che supportano il polling lungo o altre notifiche basate sulla connessione.   
Il servizio provider deve fornire un'API REST che consenta all'*azione di feed* di controllare il feed.   Il servizio provider funge da proxy tra il provider di eventi e OpenWhisk:  quando riceve gli eventi dalla terza parte, li invia a OpenWhisk attivando un trigger.

Il feed Cloudant *changes* rappresenta un esempio canonico; esso imposta un servizio `cloudanttrigger` che funge da mediatore tra le notifiche Cloudant su una connessione permanente e i trigger OpenWhisk.

Il feed *alarm* viene implementato con un modello simile.

L'architettura basata sulla connessione è l'opzione con le prestazioni più elevate,
ma impone un maggior sovraccarico sulle operazioni rispetto alle architetture di polling e hook.   
