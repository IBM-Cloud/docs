---

copyright:
  years: 2016, 2017
lastupdated: "2016-04-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Creazione dei progetti nativi cloud
{: #web-mobile}

Puoi gestire le applicazioni native cloud tramite il concetto di {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} [Progetti](projects.html). Puoi creare un progetto utilizzando la [{{site.data.keyword.dev_console}}](devex.html) o la [{{site.data.keyword.dev_cli_notm}}](dev_cli.html) per la CLI {{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}}. La {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} offre le funzionalità del servizio più comuni necessarie allo sviluppatore dell'applicazione cloud in una sola esperienza collegata che è stata ottimizzata per lo sviluppatore.

La {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} abilita uno sviluppatore dell'applicazione nativa cloud a creare un progetto da molti [tipi di modello](patterns.html) e [starter](starters.html), a creare e collegare i servizi ottimizzati {{site.data.keyword.Bluemix_notm}} chiave al tuo progetto e a scaricare velocemente il codice di lavoro con le SDK. Le SDK sono completamente integrate con le credenziali o le dipendenze della funzionalità, questo ti abilita ad averle in esecuzione in pochi minuti. Quando la tua applicazione è in esecuzione e hai configurato le funzionalità configurate, puoi tornare al tuo progetto per monitorare e gestire il coinvolgimento dei tuoi utenti dell'applicazione. Puoi anche configurare e gestire i tuoi servizi tramite la {{site.data.keyword.dev_console}}.

<!--
While the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} provides an integrated development experience, some developers might still want to have finer-grained control and wire services together manually. If this is your preferred approach, you might want to consider using the [{{site.data.keyword.mobilefirstbp}} Starter boilerplate](try_mobile.html).
-->

<!--With {{site.data.keyword.Bluemix}} Mobile services, you can incorporate pre-built, managed, and scalable cloud services into your mobile applications. You can focus on building your mobile apps, instead of the complexities of managing the back-end infrastructure.

The Mobile dashboard provides an integrated experience on {{site.data.keyword.Bluemix_notm}} where you can create mobile projects easily from within the dashboard.
-->


## Progetti
{: #projects}

La {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} combina l'interfaccia utente dell'applicazione, i dati e i servizi in un *progetto* completo. Creando un progetto, tutte le parti necessarie della tua applicazione e le funzionalità aggiunte sono conservate nel server {{site.data.keyword.Bluemix_notm}}. Puoi scaricare il tuo codice dell'applicazione e le credenziali e i programmi di inizializzazione necessari se i servizi sono configurati nel tuo progetto. Puoi visualizzare tutti i tuoi progetti selezionando **Progetti**.  

Puoi visualizzare le informazioni aggiuntive su un solo progetto selezionandolo nella pagina **Progetti**. Questa visualizza la pagina **Panoramica del progetto**, che include i servizi che sono configurati e disponibili per il progetto. I servizi sono funzionalità separate che estendono la tua applicazione aggiungendo una funzione. Poiché vengono aggiunte individualmente, puoi aggiungere i servizi di cui hai bisogno, come i servizi push, di autenticazione, dei dati e  di archiviazione o altri servizi. Quando aggiungi un servizio al tuo progetto nella pagina **Panoramica progetto** e segui le istruzioni per configurarlo, viene automaticamente associato alla tua applicazione. Per ulteriori informazioni sulla Pagina progetto, vedi [Pagina Panoramica progetto](project_overview_page.html).

Per creare il tuo progetto, devi selezionare un [modello](patterns.html), seguito da uno [starter](starters.html).


### Pagina Panoramica progetto
{: #project_overview}

Puoi visualizzare e lavorare con un unico progetto {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} selezionandolo dalla pagina **Progetti**, che aprirà la pagina Panoramica progetto. 
{: shortdesc}

La pagina **Panoramica progetto** visualizza un tile per ogni funzionalità configurata o disponibile per la configurazione con il progetto selezionato. Il tile visualizza il tipo di funzionalità e un pulsante *azioni* con tre punti allineati verticalmente. Le funzionalità che potrebbero essere disponibili o configurate includono, ad esempio, {{site.data.keyword.mobilepushshort}}, Analytics o Data e Storage. Le funzionalità compatibili dipendono dal tipo di progetto e dalle funzionalità che sono disponibili in quella regione, pertanto non tutte le funzionalità potranno essere associate a ogni progetto. 

Quando un tipo di funzionalità non è ancora associata al progetto, sul tile viene visualizzato un pulsante **Crea**. Le opzioni del pulsante delle azioni comprendono la creazione di un'istanza del servizio o di aggiungerne una esistente quando la funzionalità non è ancora associata. La selezione di **Aggiungi esistente** fornisce un elenco di istanze del servizio di quel tipo nel tuo spazio.

Se la funzionalità è già associata a questo progetto, il nome dell'istanza del servizio associato viene visualizzato sul tile dopo il tipo di funzionalità. Questo rende più facile individuare l'istanza del servizio correlata a questo progetto sulla tua {{site.data.keyword.dev_console}}. Se la funzionalità è già associata al progetto, le azioni disponibili sul relativo pulsante sono **Visualizza** e **Rimuovi**. La rimozione di un'istanza del servizio rimuove solo l'associazione a tale progetto e non elimina l'istanza del servizio dalla tua {{site.data.keyword.dev_console}}. Per eliminare un'istanza del servizio, fai clic sulla pagina **Web e mobile > Servizi** per visualizzare ed eliminare le tue istanze del servizio.

Seleziona **Richiama codice** sul tile **Codice** per scaricare il codice per il tuo progetto. Per ulteriori informazioni sul download del codice, vedi [Richiama codice](get_code.html).


### Aggiornamento del tuo progetto per utilizzare un nuovo starter
{: #update-starter}

1. Dalla pagina **Progetti** o **Panoramica progetto**, fai clic sull'icona **Menu overflow** e seleziona **Aggiorna starter**.

2. Scegli un nuovo starter e fai clic su **Aggiorna**.

3. Fai clic su **Richiama codice** nella pagina **Panoramica progetto** per selezionare il tuo linguaggio.

   In alternativa puoi fare clic sulla pagina **Codice**.


### Aggiornamento del tuo progetto per generare un nuovo linguaggio
{: #update-language}

1. Dalle pagine **Progetti** o **Panoramica progetto**, fai clic sull'icona **Menu overflow** e seleziona **Aggiorna starter**.

2. Seleziona un nuovo linguaggio e fai clic su **Aggiorna**.

3. Fai clic su **Richiama codice** nella pagina **Panoramica progetto** per selezionare il tuo linguaggio.


## Tipi di modello
{: #patterns}

I modelli nativi cloud sono progetti verificati che ti supportano nel garantire una topologia affidabile, scalabile e coerente per le tue applicazioni. Quando crei un progetto, ti vengono offerti diversi tipi di modello tra cui puoi scegliere. Semplicemente seleziona il tipo di modello e le funzionalità che desideri incorporare nel tuo progetto. Dopo aver definito le tue preferenze del progetto, ti viene generato un progetto starter per la modifica, l'esecuzione o il debug e la distribuzione locale o in {{site.data.keyword.Bluemix}}.


### Applicazione web
{: #web}

I progetti web aggiungono la capacità di servire il contenuto web come HTML, JavaScript e i fogli di calcolo al server web.

Sono disponibili i seguenti starter web:

* Web di base: serve un file `index.html` statico, un foglio di calcolo vuoto e predefinito e un file JavaScript.
* WebPack: crea un progetto in cui i file di origine ECMAScript 6 (ES6) si trovano in `src/client` e vengono compilati con WebPack per renderli più piccoli e convertiti per l'utilizzo nel browser.
* Webpack + React: un framework avanzato per creare le interfacce utente. I file di origine sono in `src/client/app` e saranno compilati con WebPack e serviti nella directory pubblica.


### Applicazione mobile
{: #mobile}

I modelli dell'applicazione mobile ti supportano nella creazione delle applicazioni mobili che si collegano direttamente ai servizi di backend, come ad esempio {{site.data.keyword.mobilepushshort}}, {{site.data.keyword.mobileanalytics_short}},
{{site.data.keyword.appid_short}} e altri ancora. I progetti possono venire aggiunti tramite sdkGen, come i BFF e i microservizi.

Puoi scegliere da un elenco di starter, come ad esempio {{site.data.keyword.watson}} Conversation, {{site.data.keyword.visualrecognitionshort}},
{{site.data.keyword.openwhisk_short}} e altri ancora.

Puoi generare le tue applicazioni mobili in Swift, Android o Cordova.


### Backend for Frontend (BFF)
{: #bff}

I modelli Backend for Frontend, comunemente noti come BFF, ti aiutano a concentrarti sull'esposizione dei dati e dei servizi di business in modo da soddisfare i requisiti di interazione con gli utenti. Per ottimizzare l'esperienza dell'utente nella tua soluzione cloud, potrebbe essere necessaria un'esperienza utente distinta per l'applicazione mobile e un'esperienza più ricca e dettagliata per l'applicazione Web. Con l'introduzione dei dispositivi a controllo vocale come il servizio [{{site.data.keyword.conversationfull}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/developercloud/conversation.html), l'interazione con un utente potrebbe essere controllata tramite voce. Questo canale digitale richiederà un BFF molto diverso per gestire tali interazioni basate sulla voce.

Con {{site.data.keyword.Bluemix_notm}}, puoi creare un BFF utilizzando l'approccio di programmazione poliglotta per definire il BFF. IBM consiglia di utilizzare Node.js, Swift o Java e di eseguirli in un modello nativo del cloud con Cloud Foundry, servizi Container o senza il server.

Il BFF gestirà l'integrazione con i servizi per la persistenza, la memorizzazione nella cache e l'integrazione dei dati con servizi di alto valore come {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}} e analisi dei dati come {{site.data.keyword.sparks}}.

Il BFF esporrà un'API utilizzando soprattutto un modello REST, ma puoi progettare il tuo BFF per lavorare da un'architettura di messaggistica mediante {{site.data.keyword.messagehub}}.

È disponibile uno starter di base BFF utilizzando Node.js o Swift.


### Microservizio
{: #microservice}

I progetti del microservizio forniscono le fondamenta per la creazione dei microservizi di backend, incluso un endpoint di integrità di base, un'API REST. I progetti generati conterranno tutte le dipendenze necessarie per lo stesso microservizio, così come per ogni servizio cloud collegato.

È disponibile uno starter di base del microservizio utilizzando Java.

<!--
## Other
{: #other}

The Other pattern represents a project that consists of only the language-specific server-side web framework. It has all the other file assets to work with the project, such as needed libraries and config files.

Content to be provided by Karl Bishop.
-->


### Linguaggi
{: #languages notoc}

I linguaggi supportati sono:

   * [Java ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](../runtimes/liberty/getting-started.html){: new_window}
   * [Node.js ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](../runtimes/nodejs/getting-started.html){: new_window}
   * [Swift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](../runtimes/swift/getting-started.html){: new_window}


#### Java
{: #java notoc}

Java dispone di funzionalità comprovate per la creazione delle applicazioni enterprise-grade. Ma le nuove funzionalità in Java 8, combinate con runtime più leggeri come Liberty e framework come Spring Boot, rendono anche Java perfettamente adatto alla creazione dei microservizi.


#### Node.js
{: #node notoc}

Node.js è un runtime JavaScript che utilizza event-driven, un modello non bloccante, rendendolo più leggero ed efficiente, eccellendo per velocità effettiva e scalabilità per le applicazioni web, i modelli di backend-for-front-end e i microservizi. L'ecosistema di pacchetti Node.js, npm, fornisce l'accesso a una grande raccolta di moduli open source, fornendo un'ampia gamma di funzionalità per velocizzare lo sviluppo della tua applicazione.


#### Swift
{: #swift notoc}

Swift è un linguaggio di programmazione moderno creato da Apple nel 2014 progettato per sostituire l'utilizzo di Objective C ed è open source da dicembre 2015. Oggi, viene utilizzato per creare software iOS, macOS, servizi web e sistemi su sistemi operativi Linux e macOS utilizzando l'architettura x86, ARM o Z. Scrive come un linguaggio di script ma è compilato per ottenere elevate prestazioni come C- con minore sovraccarico rendendolo ideale per i runtime cloud. Utilizza un sistema del tipo statico e sicuro che visualizzi in Java ma lo stile funzionale e le routine asincrone in JavaScript. È molto performante e l'origine compila il codice nativo utilizzando la toolchain del compilatore LLVM e può facilmente utilizzare le librerie di sistema esterne scritte in C.


## Starter
{: #starters}

Con la {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}, puoi scegliere tra diversi starter per ogni tipo di modello.

Gli starter sono ottimizzati per essere codice di partenza pronto per la produzione che si focalizzano sulla dimostrazione di un'integrazione {{site.data.keyword.Bluemix_notm}} chiave con un servizio di elevato valore. Ogni starter si focalizza su un servizio e mostra l'integrazione delle SDK del servizio nel codice. In alcuni casi, gli starter offrono un'esperienza utente semplice per sottolineare l'integrazione dei dati del servizio o le interazioni con l'utente. Ogni starter codice è configurato per essere abilitato con le funzionalità Authentication, Data e possibilmente altre funzionalità, se decidi di configurarle per il tuo progetto.
