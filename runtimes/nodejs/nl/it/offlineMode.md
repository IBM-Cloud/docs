---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Modalità offline per node.js
{: #offline_mode}

Quando un'applicazione node.js viene trasmessa a {{site.data.keyword.Bluemix}} il pacchetto di build SDK for Node.js
normalmente scarica le risorse utente dalle risorse esterne come i moduli del nodo da NPM.  In alcune situazioni
come con [Bluemix Dedicato](/docs/dedicated/index.html#dedicated) e
[Bluemix Locale](/docs/local/index.html#local),  puoi desiderare di non affidarti ai siti esterni a Bluemix oppure
di disporre di un controllo più esplicito su essi.  
{: shortdesc}

I seguenti sono dei siti esterni a cui può accedere il pacchetto di build node.js. Negli ambienti Bluemix [Bluemix dedicato](/docs/dedicated/index.html#dedicated) e
[Bluemix locale](/docs/local/index.html#local) è necessario che questi siti siano *consentiti*.

* http://nodejs.org/ può essere utilizzato per verificare le versioni del motore del nodo disponibili.
* https://s3pository.heroku.com è utilizzato per richiamare le versioni del motore del nodo non incluse nel pacchetto di build.
*  https://www.npmjs.com/package/npm e https://semver.herokuapp.com sono utilizzati per richiamare le versioni di npm non incluse nel pacchetto di build.
* https://iojs.org è utilizzato per richiamare la vecchia versione del nodo che non era contenuta nel pacchetto di build o non era disponibile all'indirizzo  https://semver.herokuapp.com.
* https://registry.npmjs.org è utilizzato per richiamare i moduli del nodo come express.

Per ridurre la serie di siti consentiti, configura le tue applicazioni del nodo in modo da utilizzare la versione del motore inclusa nel pacchetto di build SDK for Node.js.  Consulta gli [ultimi aggiornamenti](./updates.html) per la serie delle versioni del motore del nodo incluse nel pacchetto di build.  Se ciò viene fatto, l'unico sito richiesto per lo scaricamento dei moduli del nodo è https://registry.npmjs.org.

Fai attenzione che quando vengono installate le nuove versioni del pacchetto di build SDK for Node.js la serie di versioni del motore del nodo
viene spesso spostata alle nuove versioni.  Questo può richiedere la riconfigurazione della tua applicazione del nodo per specificare una nuova versione del motore del nodo.


## Applicazioni offline
{: #offline_applications}

Per eliminare la necessità di accedere a https://registry.npmjs.org puoi includere tutti i moduli del nodo richiesti dalla tua applicazione all'interno dell'applicazione.  Per fare ciò esegui **npm install** per tutti i moduli richiesti dalla tua applicazione e includi la risultante directory *node_modules* con la tua applicazione trasmessa.

Tieni presente che le tue dipendenze possono avere delle dipendenze e così via, ma il package.json
contiene solo le dipendenze di livello superiore. Se una delle dipendenze utilizza un intervallo nel package.json e ne viene rilasciata una nuova versione, i moduli nella tua directory node_modules possono diventare obsoleti. *Shrinkwrap* ti aiuta a bloccare tutte le versioni delle dipendenze in modo che questo non succeda.  Per utilizzare shrinkwrap avvia una directory node_modules vuota o pulita, quindi nella directory root del tuo progetto esegui:
0. npm install
1. npm dedupe
2. npm shrinkwrap

Questo può modificare il tuo *package.json* e aggiungere *npm-shrinkwrap.json* nella tua directory root.
Ogni volta che effettui una modifica alle dipendenze nel file *package.json*, ripeti le fasi *dedupe* e *shringwrap*.

## Gestione di un proxy
{: #working_with_proxy}

In alcuni ambienti come [Bluemix dedicato](/docs/dedicated/index.html#dedicated) e
[Bluemix locale](/docs/local/index.html#local) può essere configurato un proxy. Consulta
[Gestione di un proxy](/docs/manageapps/workingWithProxy.html) per ulteriori dettagli.
