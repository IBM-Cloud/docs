---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Aggiornamenti più recenti al pacchetto di build sdk-for-nodejs
{: #latest_updates}

*Ultimo aggiornamento: 22 marzo 2016*

Un elenco degli aggiornamenti più recenti nel pacchetto di build sdk-for-nodejs.
## 29 aprile 2016: pacchetto di build Node.js aggiornato v3.3-20160418-1749

Questa release del pacchetto di build aggiunge le versioni di runtime di IBM SDK for Node.js 0.10.44, 0.12.13, 4.4.1 e 4.4.2. La versione predefinita è ora la 4.4.2. Molte vecchie versioni di runtime di IBM SDK for Node.js sono state rimosse. Il pacchetto di build include ora solo le ultime due versioni di 0.10.x, 0.12.x e 4.x le quali al momento sono 0.10.43, 0.10.44, 0.12.12, 0.12.13, 4.4.1 e 4.4.2.

Per 4.4.1 e 4.4.2, è ora possibile utilizzare una versione compatibile FIPS del runtime utilizzando la variabile di ambiente `FIPS_MODE=true` per la tua applicazione. Quindi cerca `FIPS_MODE` nell'output della fase di preparazione per confermare che è stata riconosciuta dal pacchetto di build.

Il pacchetto di build aggiornato e le nuove versioni di runtime contengono inoltre le correzioni per le vulnerabilità della sicurezza:
* [CVE-2016-2515](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-2537](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-3956](http://www-01.ibm.com/support/docview.wss?uid=swg21980827)

Il pacchetto di build aggiornato contiene inoltre le correzioni a due bug:
* Ora le build di IBM SDK for Node.js saranno sempre utilizzate se ne è disponibile una che corrisponde all'intervallo richiesto. Precedentemente era vero solo per le versioni di runtime 4.x.
* Ora il programma di utilità inspector Gestione applicazioni utilizzerà le versioni di runtime 4.x.

## 18 marzo 2016: pacchetto di build Node.js aggiornato v3.2-20160315-1257

Questa release del pacchetto di build sposta il runtime IBM SDK for Node.js predefinito dalla versione 4.3.0 alla 4.3.2. Essa inoltre include IBM SDK for Node.js versioni 0.10.43, 0.12.12, e 4.3.1. Gli utenti devono utilizzare queste ultime versioni di Node.js per apportare le correzioni a diverse vulnerabilità di sicurezza.

## 4 marzo 2016: pacchetto di build Node.js aggiornato v3.1-20160222-1123

Questa release del pacchetto di build sposta il runtime IBM SDK for Node.js predefinito dalla versione 4.2.4 alla 4.3.0. Essa inoltre include IBM SDK for Node.js versioni 0.10.42, 0.12.10 e 4.2.6. Gli utenti devono utilizzare queste ultime versioni di Node.js per apportare le correzioni a diverse vulnerabilità di sicurezza.

## 4 febbraio 2016: pacchetto di build Node.js aggiornato v3.0-20160125-1224

Questa release è completamente sincronizzata con il pacchetto di build [Cloud Foundry community Node.js](https://github.com/cloudfoundry/nodejs-buildpack). In aggiunta alle modifiche della community, sono state apportate delle modifiche ad alcuni valori predefiniti, ottimizzazioni per ridurre il periodo di preparazione della funzione Gestione applicazioni.

* Aggiornamenti del pacchetto di build:

  * Node.js v4.2.4 (IBM SDK for Node.js Versione 4) è ora il runtime predefinito su Bluemix, sostituisce v0.12.9. Ciò potrebbe portare la tua applicazione a comportarsi diversamente se non hai specificato una versione particolare per la tua applicazione. Per informazioni su come specificare una versione di Node.js per la tua applicazione Bluemix, consulta la documentazione [Runtime Node.js](index.html).

  * NODE_ENV è ora configurato su *production* per impostazione predefinita. Ciò comporterà che alcune dipendenze del nodo si comporteranno diversamente. Ad esempio, il framework Express non restituirà più le stacktrace nel browser web per gli endpoint in errore, ma invece visualizzerà solo *Errore interno del server*. Quando NPM_CONFIG_PRODUCTION è impostato su *true*, NPM imposterà NODE_ENV su *production* per gli script subshell solo nella fase npm install. Ciò consente agli utenti di impostare NODE_ENV su un altro valore come *development* per il runtime dell'applicazione. Per chiarezza, gli script npm visualizzeranno il messaggio **NODE_ENV=production**.

  * È inclusa una correzione di bug per il servizio Monitoring and Analytics.

* Aggiornamenti per la memorizzazione in cache:

  * Se la cache è disabilitata (NODE_MODULES_CACHE=false) il pacchetto di build non tenterà di memorizzare nella cache i moduli/componenti. Precedentemente questa impostazione faceva in modo che la cache non venisse visualizzata ma che ancora memorizzasse nella cache i moduli installati per distribuzioni future. Ora non sarà visualizzata e non tenterà di archiviare alcuna cache.

  * I Bower_components vengono memorizzati nella cache per impostazione predefinita in aggiunta ai node_modules.

* Altri aggiornamenti:

  * Sono state aggiunte delle avvertenze utili per le dipendenze mancanti come gulp, bower e angular.

  * Lo script delete è stato aggiornato come le informazioni della versione del pacchetto di build.

  * La raccomandazione clustering (WEB_CONCURRENCY) inizialmente introdotta dalla community è stata rimossa perché la determinazione di memoria non era accurata su Bluemix.


## 16 dicembre 2015: pacchetto di build Node.js aggiornato v2.8-20151209-1403 e v3.0beta-20151211-2041

Questa release del pacchetto di build Node.js viene fornita con due versioni, v2.8 e v3.0beta. Entrambe le versioni includono le seguenti modifiche:

Una correzione di bug per il servizio Monitoring and Analytics L'inclusione di un runtime
memorizzato in cache per IBM SDK for Node.js v4.2.3.0, v4.2.2.0, v1.2.0.8 e v1.2.0.7 (basati
rispettivamente su Node.js v4.2.3, v4.2.2, v0.12.9 e v0.12.8 di community) Inoltre, in v3.0beta, il runtime Node.js predefinito è modificato in v4.2.3.

Il pacchetto di build v3.0beta di IBM Node.js è stato rilasciato come un pacchetto di build non predefinito su Bluemix con Node.js v4.2.3 come runtime predefinito. Per garantire che le tue applicazioni e i tuoi servizi continuino a funzionare su Bluemix, esegui il push della tua applicazione con la versione beta del pacchetto di build. Dopo 30 giorni o più, la v3 diventerà il pacchetto di build predefinito.

Per eseguire il push della tua applicazione con v3.0beta:
* Utilizza l'opzione "-b" nel tuo comando 'cf push':

```
        cf push -b sdk-for-nodejs-v3beta
```
{: codeblock}

* In alternativa, utilizza l'opzione "buildpack" nel tuo file manifest.yml:

```
        buildpack: sdk-for-nodejs-v3beta
```
{: codeblock}

Questa modifica al runtime predefinito non influenzerà la tua applicazione se hai configurato una specifica versione di Node.js nel package.json della tua applicazione. Nota che puoi sempre specificare la versione di Node.js per eseguire la tua applicazione utilizzando la voce engines.node nel tuo package.json come spiegato in [Versioni disponibili](index.html#available_versions).

## 23 novembre 2015: pacchetto di build Node.js aggiornato v2.7-20151118-1003

Con 2.7, abbiamo incluso la versione 4.2.1.0 di IBM SDK for Node.js (basato su Node v4.2.1 (LTS)). Non è ancora il valore predefinito, ma può essere specificato per l'utilizzo. Nota: sostituisce la build open-source che era disponibile precedentemente. Abbiamo anche apportato delle correzioni per dei piccoli bug al nostro framework di estensione del servizio.

## 19 ottobre 2015: pacchetto di build Node.js aggiornato v2.6.1-20151015-1326

Node.js v2.6.1 introduce una correzione di bug al [gestore di gestione delle applicazioni StrongPM](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/) e una versione NPM più congruente.

## 15 ottobre 2015: pacchetto di build Node.js aggiornato v2.6-20151006-1309

Questa release del pacchetto di build Node.js offre l'integrazione di [StrongLoop Process Manager](https://strong-pm.io) alla funzione Gestione applicazioni. Per ulteriori informazioni, consulta il post del blog [StrongLoop DevOps for Node.js Applications on Bluemix](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/).

## 15 giugno 2015: pacchetto di build Node.js aggiornato v2.0-20150608-1503

In questa release, è stata eseguita la sincronizzazione tra il pacchetto di build Node.js e [il pacchetto di build Node.js della community CF](https://github.com/cloudfoundry/nodejs-buildpack) più recente, fornito dalla community con numerose nuove funzioni.
Inoltre, è stata rinnovata la funzione Gestione applicazioni nel pacchetto di build Node.js, che abilita programmi di utilità quali shell, node-inspector, Bluemix Live Sync e altro ancora. Per i dettagli vedi [Gestione applicazioni](../../manageapps/app_mng.html).

## 5 maggio 2015: pacchetto di build Node.js aggiornato v1.17-20150429-1033

* Il pacchetto di build Node.js viene ora fornito con [IBM SDK for Node.js v0.12.1](https://developer.ibm.com/node/sdk/).
* Se la tua applicazione non specifica un runtime nel file package.json, inizierà a utilizzare v0.12.1, anziché v0.10.x. Se devi utilizzare la versione precedente, specifica v0.10.x nel file package.json come mostrato di seguito

```
        "engines": {
            "node": "0.10.x"
        }
```
{: codeblock}

* Esistono dei problemi noti con v0.12.1:
   * Quando si utilizza la funzione Strumenti di debug fornita da Bluemix Live Sync, la funzione “Sospendi” non è disponibile.
   * Il modulo mqlight utilizzato per il servizio MQ Light non è supportato sulla v0.12.x

* Sono state risolte diverse vulnerabilità della sicurezza:
  * Correzione delle vulnerabilità in OpenSSL che influiscono su IBM SDK for Node.js. Ulteriori dettagli sono disponibili nel [bollettino di sicurezza](http://www-01.ibm.com/support/docview.wss?uid=swg21701494).
  * Correzione delle vulnerabilità in RC4 Stream Cipher che influiscono su IBM SDK for Node.js. Ulteriori dettagli sono disponibili nel [bollettino di sicurezza](http://www-01.ibm.com/support/docview.wss?uid=swg21882778).

##  2 aprile 2015: pacchetto di build Node.js aggiornato v1.15-20150331-2231

* Il pacchetto di build Node.js include adesso tre nuove funzioni che ti consentono di sviluppare rapidamente su Bluemix come faresti sul desktop, senza eseguire nuovamente la distribuzione
  * Desktop Sync: sincronizza qualsiasi struttura desktop (Windows) con lo spazio di lavoro del progetto basato su cloud
  * Live Edit: puoi apportare modifiche a un'applicazione Node.js in esecuzione in Bluemix e verificarla nel tuo browser immediatamente.
  * Debug: accedi tramite shell nel tuo ambiente ed esegui il debug! Puoi modificare il codice in modo dinamico, inserire dei punti di interruzione, analizzare in dettaglio il codice, riavviare il runtime e altro ancora, utilizzando il programma di debug Node Inspector
  * Per ulteriori informazioni vedi [Gestione applicazioni](../../manageapps/app_mng.html#Utilities).
* Abbiamo estratto le ultime modifiche dal [pacchetto di build Node.js di Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack). Questo viene fornito con diverse correzioni di bug e miglioramenti apportati dalla community.
* Il pacchetto di build Node.js viene ora fornito con [IBM SDK for Node.js v1.1.0.13](https://developer.ibm.com/node/sdk/).

## 5 gennaio 2015: pacchetto di build Node.js aggiornato v1.9.1-20141208-1221

* Il pacchetto di build Node.js include ora il supporto per l'impostazione dei log dinamici. Con tale supporto, gli sviluppatori possono modificare il livello di log della propria applicazione in fase di elaborazione se, per la registrazione, l'applicazione utilizza i moduli log4js, bunyan o ibmbluemix.
* Il pacchetto di build Node.js viene ora fornito con [IBM SDK for Node.js v0.10.33](https://developer.ibm.com/node/sdk/). Include delle correzioni per il problema POODLE.

## 23 ottobre 2014: pacchetto di build Node.js aggiornato v1.6-20141013-1736

* Il pacchetto di build Node.js viene ora fornito con [IBM SDK for Node.js v1.1.0.8](https://developer.ibm.com/node/sdk/). Ciò significa che ottieni un runtime IBM Node.js pienamente supportato quando specifichi il runtime Node.js stabile più recente per la tua applicazione, v0.10.32. Questo SDK più recente viene fornito con una correzione per
un problema con il modulo qs integrato che determinava una condizione di DoS (denial-of-service). Contiene anche una versione aggiornata del modulo npm e altri miglioramenti nei moduli
http e url. Per ulteriori dettagli, consulta [v0.10.32 Change Log](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog).
* Il pacchetto di build contiene anche una correzione per un bug che stava aggiungendo un file
index.html non corretto nell'applicazione del cliente durante la distribuzione.

## 30 settembre 2014: pacchetto di build Node.js aggiornato v1.4-20140908-1746

* Il pacchetto di build Node.js viene ora fornito con [IBM SDK for Node.js v1.1.0.7](https://developer.ibm.com/node/sdk/). Ciò significa che otterrai un runtime IBM Node.js pienamente supportato quando specifichi il runtime Node.js stabile più recente per la tua applicazione, v0.10.31. Con il runtime Node.js pienamente supportato, i clienti possono procedere alle loro attività di sviluppo utilizzandolo come base sapendo di poter contare sullo stesso approfondito supporto che hanno sempre avuto per i prodotti IBM.
* Il pacchetto di build contiene un framework di servizi migliorato. In modo specifico, funziona meglio quando si esegue il bind del servizio Monitoring and Analytics e fornisce delle informazioni di diagnostica aggiuntive in caso di errori.

## 28 agosto 2014: pacchetto di build Node.js aggiornato v1.3-20140821-1143

* Il pacchetto di build Node.js più recente è ora fornito con IBM SDK for Node.js v1.1.0.6. Ciò significa che otterrai un runtime IBM Node.js pienamente supportato quando specifichi il runtime Node.js stabile più recente, v0.10.30, per la tua applicazione. Questo runtime corregge la [vulnerabilità di danneggiamento della memoria V8](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow).
* Il pacchetto di build include anche dei miglioramenti e delle correzioni di bug all'estensione del servizio Monitoring and Analytics, consentendoti di diagnosticare le prestazioni e le condizioni di errore tramite il servizio.

## 29 luglio 2014: pacchetto di build Node.js aggiornato v1.1-20140717-1447

Il pacchetto di build Node.js è ora fornito con IBM SDK for Node.js v1.1.0.5. Ciò significa che otterrai un runtime IBM Node.js pienamente supportato quando specifichi il runtime Node.js stabile più recente per la tua applicazione, v0.10.29. Per ulteriori informazioni sugli SDK IBM Node.js, fai clic [qui](https://developer.ibm.com/node/sdk/).

# rellinks
## general
* [runtime node.js](index.html)
