---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Aggiornamenti più recenti al pacchetto di build di SDK for Nodejs
{: #latest_updates}

Un elenco degli aggiornamenti più recenti nel pacchetto di build sdk-for-nodejs.

## 10 marzo, 2017: pacchetto di build Node.js aggiornato v3.11
Questa release del pacchetto di build supporta le versioni di runtime di IBM SDK for Node.js: 0.10.47, 0.10.48, 0.12.17, 0.12.18, 4.7.3, 4.8.0, 6.9.5 e 6.10.0. La versione predefinita è ora la 4.8.0.

In aggiunta ai nuovi runtime, questa release contiene una correzione a un bug riscontrato durante l'abilitazione dell'handler di gestione dell'applicazione shell utilizzando la IU devconsole. Questo pacchetto di build modifica il modo in cui la configurazione automatica utilizza il servizio Monitoring and Analytics. Le applicazioni che utilizzano il piano gratuito non avranno più la funzionalità di registrazione aggiunta alle loro applicazioni, sta venendo sostituita da logmet.

## 20 gennaio, 2017: pacchetto di build Node.js aggiornato v3.10
Questa release del pacchetto di build supporta le versioni di runtime di IBM SDK for Node.js: 0.10.47, 0.10.48, 0.12.17, 0.12.18, 4.7.0, 4.7.2, 6.9.2 e 6.9.4. La versione predefinita è ora la 4.7.2.

Contiene una correzione a un bug per cui "npm start" non veniva sempre richiamato per avviare l'applicazione.

## 17 novembre, 2016: pacchetto di build Node.js aggiornato v3.9
Questa release del pacchetto di build supporta le versioni di runtime di IBM SDK for Node.js: 0.10.47, 0.10.48, 0.12.16, 0.12.17, 4.6.1, 4.6.2, 6.7.0 e 6.9.1. La versione predefinita è ora la 4.6.2.

Tieni presente che Node.js v6 è stato promosso allo stato di LTS il 18 ottobre 2016 e presto diventerà il runtime predefinito del pacchetto di build. Node.js v0.10 ha terminato il suo ciclo di vita il 31 ottobre 2016 e a breve non sarà più incluso nel pacchetto di build. Consulta [Node.js version long-term support and the SDK for Node.js buildpack](https://www.ibm.com/blogs/bluemix/2016/11/node-version-support-and-sdk-buildpack/) per ulteriori dettagli.

I bug che influenzano gli handler di traccia e di inspector della gestione dell'applicaizone, quando utilizzati insieme a Node.js v6, sono stati risolti in questa release. Consulta [Managing Liberty and Node.js apps](/docs/manageapps/app_mng.html#inspector) per ulteriori informazioni su come l'handler inspector sta venendo modificato ora che Node.js v6 ha integrato la funzionalità inspector.

## 7 ottobre 2016: pacchetto di build Node.js aggiornato v3.8-20161006-1211
Questa release del pacchetto di build supporta le versioni di runtime di IBM SDK for Node.js: 0.10.46, 0.10.47, 0.12.15, 0.12.16, 4.5.0, 4.6.0, 6.6.0 e 6.7.0. La versione predefinita è ora la 4.6.0.

In aggiunta ai nuovi runtime, questa release contiene correzioni di bug del pacchetto di build. Inclusa una correzione a un problema noto quando utilizzi Node.js 6.x e la modalità di sviluppo che era stata menzionata negli aggiornamenti della release v3.7-20160826-1101. È inoltre sincronizzata con il [pacchetto di build Node.js Cloud Foundry v1.5.20](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.20).

## 26 agosto, 2016: pacchetto di build Node.js aggiornato v3.7-20160826-1101
Questa release del pacchetto di build supporta le versioni di runtime di IBM SDK for Node.js: 0.10.45, 0.10.46, 0.12.14, 0.12.15, 4.4.7, 4.5.0, 6.2.2 e 6.4.0. La versione predefinita è ora la 4.5.0.

Questa release supporta le correzioni ai bug, inclusi quelli dal [Cloud Foundry’s Node.js buildpack 1.5.18](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.18).

La release rimuove il supporto per il gestore Gestione applicazioni strongpm come annunciato in [Bluemix Node.js Buildpack v3.3 – FIPS mode and more](https://developer.ibm.com/bluemix/2016/05/05/node-buildpack-update-fips-mode/).

Nota che è presente un problema noto quando utilizzi Node.js 6.x e la [Modalità di sviluppo](/docs/manageapps/app_mng.html#devmode). Per aggirare questo problema dovrai ripreparare la tua applicazione dopo l'abilitazione della modalità di sviluppo prima di poter iniziare ad utilizzarla.

## 22 luglio 2016: pacchetto di build Node.js aggiornato v3.6-20160715-0749
Questa release del pacchetto di build supporta le versioni di runtime di IBM SDK for Node.js: 0.10.45, 0.10.46, 0.12.14, 0.12.15, 4.4.6, 4.4.7, 6.2.1 e 6.2.2. La versione predefinita è ora la 4.4.7.

Questa release include un proxy di gestione dell'applicazione aggiornato che supporta gli accessi federati.

Sono incluse le correzioni per le seguenti vulnerabilità di sicurezza:
* [CVE-2016-1669](http://www-01.ibm.com/support/docview.wss?uid=swg21986383)

## 22 giugno 2016: pacchetto di build Node.js aggiornato v3.5-20160609-1608

Questa release del pacchetto di build aggiunge le versioni di runtime di IBM SDK for Node.js 4.4.5 e 6.2.0. La versione predefinita è ora la 4.4.5.

La release rimuove il supporto per le versioni di runtime vecchie come annunciato in [Bluemix Node.js Buildpack v3.3 – FIPS mode and more](https://developer.ibm.com/bluemix/2016/05/05/node-buildpack-update-fips-mode/). Il pacchetto di build ora supporta 0.10.44, 0.10.45, 0.12.13, 0.12.14, 4.4.4, 4.4.5, 6.1.0 e 6.2.0.

Questa release supporta le correzioni ai problemi dal [pacchetto di build Node.js di Cloud Foundry 1.5.14](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.14).

## 20 maggio 2016: pacchetto di build Node.js aggiornato v3.4-20160518-1653

Questa release del pacchetto di build aggiunge le versioni di runtime di IBM SDK for Node.js 0.10.45, 0.12.14, 4.4.4, 6.0.0 e 6.1.0. La versione predefinita è ora la 4.4.4.

Sono incluse le correzioni per le seguenti vulnerabilità di sicurezza:
* [CVE-2015-8855](http://www-01.ibm.com/support/docview.wss?uid=swg21982852)
* [CVE-2016-2108 CVE-2016-2107 CVE-2016-2105 CVE-2016-2106 CVE-2016-2109 CVE-2016-2176 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.openssl.org/news/secadv/20160503.txt)

Nota che è presente un problema noto con npm v3 e il programma di utilità dell'inspector Gestione applicazioni. npm 3.8.6 è il valore predefinito con i runtime 6.0.0 e 6.1.0. Se desideri utilizzare i runtime 6.x e il programma di utilità dell'inspector, dovrai specificare una versione npm 2.X nel tuo package.json come soluzione alternativa temporanea.

## 29 aprile 2016: pacchetto di build Node.js aggiornato v3.3-20160428-1409

Questa release del pacchetto di build aggiunge le versioni di runtime di IBM SDK for Node.js 0.10.44, 0.12.13, 4.4.0, 4.4.1, 4.4.2 e 4.4.3. La versione predefinita è ora la 4.4.3.
i
Per 4.3.1 e successive, è ora possibile utilizzare una versione abilitata FIPS del runtime utilizzando la variabile di ambiente `FIPS_MODE=true` per la tua applicazione.

Il pacchetto di build aggiornato e le nuove versioni di runtime contengono inoltre le correzioni per le vulnerabilità della sicurezza:
* [CVE-2016-2515](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-2537](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-3956](http://www-01.ibm.com/support/docview.wss?uid=swg21980827)

Il pacchetto di build aggiornato contiene inoltre le correzioni a diversi bug:
* Ora le build di IBM SDK for Node.js saranno sempre utilizzate se ne è disponibile una che corrisponde all'intervallo richiesto. Precedentemente questo era vero solo per le versioni di runtime 4.x.
* Ora il programma di utilità inspector Gestione applicazioni utilizzerà le versioni di runtime 4.x.
* Risolta una regressione nel programma di utilità Gestione applicazioni strongpm.

## 18 marzo 2016: pacchetto di build Node.js aggiornato v3.2-20160315-1257

Questa release del pacchetto di build sposta il runtime IBM SDK for Node.js predefinito dalla versione 4.3.0 alla 4.3.2. Essa inoltre include IBM SDK for Node.js versioni 0.10.43, 0.12.12, e 4.3.1. Utilizza queste ultime versioni di Node.js per apportare le correzioni a diverse vulnerabilità di sicurezza.

## 4 marzo 2016: pacchetto di build Node.js aggiornato v3.1-20160222-1123

Questa release del pacchetto di build sposta il runtime IBM SDK for Node.js predefinito dalla versione 4.2.4 alla 4.3.0. Essa inoltre include IBM SDK for Node.js versioni 0.10.42, 0.12.10 e 4.2.6. Utilizza queste ultime versioni di Node.js per apportare le correzioni a diverse vulnerabilità di sicurezza.

## 4 febbraio 2016: pacchetto di build Node.js aggiornato v3.0-20160125-1224

Questa release è completamente sincronizzata con il pacchetto di build [Cloud Foundry community Node.js](https://github.com/cloudfoundry/nodejs-buildpack). In aggiunta alle modifiche della community, sono state apportate delle modifiche ad alcuni valori predefiniti, insieme a ottimizzazioni per ridurre il periodo di preparazione della funzione Gestione applicazioni.

* Aggiornamenti del pacchetto di build:

  * Node.js v4.2.4 (IBM SDK for Node.js Versione 4) è ora il runtime predefinito su Bluemix, sostituisce v0.12.9. Questa modifica potrebbe portare la tua applicazione a comportarsi diversamente se non hai specificato una versione particolare per la tua applicazione. Per informazioni su come specificare una versione di Node.js per la tua applicazione Bluemix, consulta la documentazione [Runtime Node.js](index.html).

  * NODE_ENV è ora configurato su *production* per impostazione predefinita. Questa modifica comporterà che alcune dipendenze del nodo si comporteranno diversamente. Ad esempio, il framework Express non restituirà più le stacktrace nel browser web per gli endpoint in errore, ma invece visualizza *Errore interno del server*. Quando NPM_CONFIG_PRODUCTION è impostato su *true*, NPM imposterà NODE_ENV su *production* per gli script subshell solo nella fase npm install. Questa funzione consente agli utenti di impostare NODE_ENV su un altro valore come *development* per il runtime dell'applicazione. Per chiarezza, gli script npm visualizzeranno il messaggio **NODE_ENV=production**.

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

Una correzione di bug per il servizio Monitoring and Analytics
L'inclusione di un runtime memorizzato in cache per IBM SDK for Node.js v4.2.3.0, v4.2.2.0, v1.2.0.8 e v1.2.0.7, basati sulle versioni della community Node.js v4.2.3, v4.2.2, v0.12.9 e v0.12.8.
In aggiunta, nella v3.0beta il runtime Node.js predefinito viene modificato con v4.2.3.

Il pacchetto di build v3.0beta di IBM Node.js è stato ora rilasciato come un pacchetto di build non predefinito su Bluemix con Node.js v4.2.3 come runtime predefinito. Per garantire che le tue applicazioni e i tuoi servizi continuino a funzionare su Bluemix, esegui il push della tua applicazione con la versione beta del pacchetto di build. Dopo 30 giorni o più, la v3 diventerà il pacchetto di build predefinito.

Per eseguire il push della tua applicazione con v3.0beta:
* Utilizza l'opzione "-b" nel tuo comando 'cf push':

```
        cf push -b sdk-for-nodejs-v3beta
```
{: codeblock}

* In alternativa utilizza l'opzione "buildpack" nel tuo file manifest.yml:

```
        buildpack: sdk-for-nodejs-v3beta
```
{: codeblock}

Questa modifica al runtime predefinito non influenzerà la tua applicazione se hai configurato una specifica versione di Node.js nel package.json della tua applicazione.

**Nota:** puoi sempre specificare la versione di Node.js per eseguire la tua applicazione utilizzando la voce engines.node nel tuo package.json come spiegato in [Versioni disponibili](index.html#available_versions).

## 23 novembre 2015: pacchetto di build Node.js aggiornato v2.7-20151118-1003

Con 2.7, abbiamo incluso la versione 4.2.1.0 di IBM SDK for Node.js (basato su Node v4.2.1 (LTS)). Non è ancora il valore predefinito, ma può essere specificato per l'utilizzo. **Nota:** questa versione sostituisce la build open source che era precedentemente disponibile. Abbiamo anche apportato delle correzioni per dei piccoli bug al nostro framework di estensione del servizio.

## 19 ottobre 2015: pacchetto di build Node.js aggiornato v2.6.1-20151015-1326

Node.js v2.6.1 introduce una correzione di bug al [gestore di gestione delle applicazioni StrongPM](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/) e una versione NPM più congruente.

## 15 ottobre 2015: pacchetto di build Node.js aggiornato v2.6-20151006-1309

Questa release del pacchetto di build Node.js offre l'integrazione di [StrongLoop Process Manager ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://strong-pm.io) alla funzione Gestione applicazioni. Per ulteriori informazioni, consulta il post del blog [StrongLoop DevOps for Node.js Applications on Bluemix](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/).

## 15 giugno 2015: pacchetto di build Node.js aggiornato v2.0-20150608-1503

In questa release, è stata eseguita la sincronizzazione tra il pacchetto di build Node.js e [il pacchetto di build Node.js della community CF](https://github.com/cloudfoundry/nodejs-buildpack) più recente, fornito dalla community con numerose nuove funzioni.
Inoltre, è stata rinnovata la funzione Gestione applicazioni nel pacchetto di build Node.js, che abilita programmi di utilità quali shell, node-inspector, Bluemix Live Sync e altro ancora. Per i dettagli vedi [Gestione applicazioni](/docs/manageapps/app_mng.html).

## 5 maggio 2015: pacchetto di build Node.js aggiornato v1.17-20150429-1033

* Il pacchetto di build Node.js viene ora fornito con [IBM SDK for Node.js v0.12.1](https://developer.ibm.com/node/sdk/).
* Se la tua applicazione non specifica un runtime nel file package.json, inizierà a utilizzare v0.12.1, anziché v0.10.x. Se devi utilizzare la versione precedente, specifica v0.10.x nel file package.json come mostrato di seguito.

```
        "engines": {
            "node": "0.10.x"
        }
```
{: codeblock}

* Problemi noti con v0.12.1:
   * Quando si utilizza la funzione Strumenti di debug fornita da Bluemix Live Sync, la funzione “Sospendi” non è disponibile.
   * Il modulo mqlight utilizzato per il servizio MQ Light non è supportato sulla v0.12.x

* Sono state risolte diverse vulnerabilità della sicurezza:
  * Correzione delle vulnerabilità in OpenSSL che influiscono su IBM SDK for Node.js. Ulteriori dettagli sono disponibili nel [bollettino di sicurezza](http://www-01.ibm.com/support/docview.wss?uid=swg21701494).
  * Correzione delle vulnerabilità in RC4 Stream Cipher che influiscono su IBM SDK for Node.js. Ulteriori dettagli sono disponibili nel [bollettino di sicurezza](http://www-01.ibm.com/support/docview.wss?uid=swg21882778).

##  2 aprile 2015: pacchetto di build Node.js aggiornato v1.15-20150331-2231

* Il pacchetto di build Node.js include adesso tre nuove funzioni che ti consentono di sviluppare rapidamente su Bluemix come faresti sul desktop, senza eseguire nuovamente la distribuzione
  * Desktop Sync: sincronizza qualsiasi struttura desktop (Windows) con lo spazio di lavoro del progetto basato su cloud
  * Live Edit: ti consente di apportare modifiche a un'applicazione Node.js in esecuzione in Bluemix e verificarla nel tuo browser immediatamente.
  * Debug: accedi tramite shell nel tuo ambiente ed esegui il debug! Puoi modificare il codice in modo dinamico, inserire dei punti di interruzione, analizzare in dettaglio il codice, riavviare il runtime e altro ancora, utilizzando il programma di debug Node Inspector
  * Per ulteriori informazioni vedi [Gestione applicazioni](/docs/manageapps/app_mng.html#Utilities).
* Abbiamo estratto le ultime modifiche dal [pacchetto di build Node.js di Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack). Questa modifica viene fornita con diverse correzioni di bug e miglioramenti apportati dalla community.
* Il pacchetto di build Node.js viene ora fornito con [IBM SDK for Node.js v1.1.0.13](https://developer.ibm.com/node/sdk/).

## 5 gennaio 2015: pacchetto di build Node.js aggiornato v1.9.1-20141208-1221

* Il pacchetto di build Node.js include ora il supporto per l'impostazione dei log dinamici. Con tale supporto, gli sviluppatori possono modificare il livello di log della propria applicazione dinamicamente se, per la registrazione l'applicazione utilizza i moduli log4js, bunyan o ibmbluemix.
* Il pacchetto di build Node.js viene ora fornito con [IBM SDK for Node.js v0.10.33](https://developer.ibm.com/node/sdk/). Questo aggiornamento include delle correzioni per il problema POODLE.

## 23 ottobre 2014: pacchetto di build Node.js aggiornato v1.6-20141013-1736

* Il pacchetto di build Node.js viene ora fornito con [IBM SDK for Node.js v1.1.0.8](https://developer.ibm.com/node/sdk/). Questo aggiornamento indica che ottieni un runtime IBM Node.js pienamente supportato quando specifichi il runtime Node.js stabile più recente per la tua applicazione, v0.10.32. Questo SDK più recente viene fornito con una correzione per
un problema con il modulo qs integrato che determinava una condizione di DoS (denial-of-service). Contiene anche una versione aggiornata del modulo npm e altri miglioramenti nei moduli
http e url. Per ulteriori dettagli, consulta [v0.10.32 Change Log](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog).
* Il pacchetto di build contiene anche una correzione per un bug che stava aggiungendo un file
index.html non corretto nell'applicazione del cliente durante la distribuzione.

## 30 settembre 2014: pacchetto di build Node.js aggiornato v1.4-20140908-1746

* Il pacchetto di build Node.js viene ora fornito con [IBM SDK for Node.js v1.1.0.7](https://developer.ibm.com/node/sdk/). Questo aggiornamento indica che ottieni un runtime IBM Node.js pienamente supportato quando specifichi il runtime Node.js stabile più recente per la tua applicazione, v0.10.31. Con un runtime Node.js completamente supportato, i clienti ricevono un'esperienza di supporto importante.
* Il pacchetto di build contiene un framework di servizi migliorato. In modo specifico, funziona meglio quando si esegue il bind del servizio Monitoring and Analytics e fornisce delle informazioni di diagnostica aggiuntive se il servizio ha un malfunzionamento.

## 28 agosto 2014: pacchetto di build Node.js aggiornato v1.3-20140821-1143

* Il pacchetto di build Node.js più recente è ora fornito con IBM SDK for Node.js v1.1.0.6. Questo aggiornamento indica che otterrai un runtime IBM Node.js pienamente supportato quando specifichi il runtime Node.js stabile più recente, v0.10.30, per la tua applicazione. Questo runtime corregge [V8 Memory Corruption vulnerability ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow).
* Il pacchetto di build include anche dei miglioramenti e delle correzioni di bug all'estensione del servizio Monitoring and Analytics, consentendoti di diagnosticare le prestazioni e le condizioni di errore tramite il servizio.

## 29 luglio 2014: pacchetto di build Node.js aggiornato v1.1-20140717-1447

Il pacchetto di build Node.js è ora fornito con IBM SDK for Node.js v1.1.0.5. Questo aggiornamento indica che otterrai un runtime IBM Node.js pienamente supportato quando specifichi il runtime Node.js stabile più recente per la tua applicazione, v0.10.29. Per ulteriori informazioni sulle [IBM Node.js SDKs](https://developer.ibm.com/node/sdk/).

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [runtime node.js](index.html)
