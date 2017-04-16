
---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Tipi di modello
{: #patterns}

I modelli nativi cloud sono progetti verificati che ti supportano nel garantire una topologia affidabile, scalabile e coerente per le tue applicazioni. Quando crei un progetto, ti vengono offerti diversi tipi di modello tra cui puoi scegliere. Semplicemente seleziona il tipo di modello e le funzionalità che desideri incorporare nel tuo progetto. Dopo aver definito le tue preferenze del progetto, ti viene generato un progetto starter per la modifica, l'esecuzione o il debug e la distribuzione locale o in {{site.data.keyword.Bluemix}}.

## Applicazione web
{: #web}

I progetti web aggiungono la capacità di servire il contenuto web come HTML, JavaScript e i fogli di calcolo al server web.

Sono disponibili i seguenti starter web:

* Web di base: serve un file `index.html` statico, un foglio di calcolo vuoto e predefinito e un file JavaScript.
* WebPack: crea un progetto in cui i file di origine ECMAScript 6 (ES6) si trovano in `src/client` e vengono compilati con WebPack per renderli più piccoli e convertiti per l'utilizzo nel browser.
* Webpack + React: un framework avanzato per creare le interfacce utente. I file di origine sono in `src/client/app` e saranno compilati con WebPack e serviti nella directory pubblica.


## Applicazione mobile
{: #mobile}

I modelli dell'applicazione mobile ti supportano nella creazione delle applicazioni mobili che si collegano direttamente ai servizi di backend, come ad esempio {{site.data.keyword.mobilepushshort}}, {{site.data.keyword.mobileanalytics_short}},
{{site.data.keyword.appid_short}} e altri ancora. I progetti possono venire aggiunti tramite sdkGen, come i BFF e i microservizi.

Puoi scegliere da un elenco di starter, come ad esempio {{site.data.keyword.watson}} Conversation, {{site.data.keyword.visualrecognitionshort}},
{{site.data.keyword.openwhisk_short}} e altri ancora.

Puoi generare le tue applicazioni mobili in Swift, Android o Cordova.


## Backend for Frontend (BFF)
{: #bff}

I modelli Backend for Frontend, comunemente noti come BFF, ti aiutano a concentrarti sull'esposizione dei dati e dei servizi di business in modo da soddisfare i requisiti di interazione con gli utenti. Per ottimizzare l'esperienza dell'utente nella tua soluzione cloud, potrebbe essere necessaria un'esperienza utente distinta per l'applicazione mobile e un'esperienza più ricca e dettagliata per l'applicazione Web. Con l'introduzione dei dispositivi a controllo vocale come il servizio [{{site.data.keyword.conversationfull}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/developercloud/conversation.html), l'interazione con un utente potrebbe essere controllata tramite voce. Questo canale digitale richiederà un BFF molto diverso per gestire tali interazioni basate sulla voce.

Con {{site.data.keyword.Bluemix_notm}}, puoi creare un BFF utilizzando l'approccio di programmazione poliglotta per definire il BFF. IBM consiglia di utilizzare Node.js, Swift o Java e di eseguirli in un modello nativo del cloud con Cloud Foundry, servizi Container o senza il server. 

Il BFF gestirà l'integrazione con i servizi per la persistenza, la memorizzazione nella cache e l'integrazione dei dati con servizi di alto valore come {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}} e analisi dei dati come {{site.data.keyword.sparks}}.

Il BFF esporrà un'API utilizzando soprattutto un modello REST, ma puoi progettare il tuo BFF per lavorare da un'architettura di messaggistica mediante {{site.data.keyword.messagehub}}.

È disponibile uno starter di base BFF utilizzando Node.js o Swift.


## Microservizio
{: #microservice}

I progetti del microservizio forniscono le fondamenta per la creazione dei microservizi di backend, incluso un endpoint di integrità di base, un'API REST. I progetti generati conterranno tutte le dipendenze necessarie per lo stesso microservizio, così come per ogni servizio cloud collegato.

È disponibile uno starter di base del microservizio utilizzando Java.

<!--
## Other
{: #other}

The Other pattern represents a project that consists of only the language-specific server-side web framework. It has all the other file assets to work with the project, such as needed libraries and config files.

Content to be provided by Karl Bishop.
-->


## Linguaggi
{: #languages notoc}

I linguaggi supportati sono:

   * [Java ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](../runtimes/liberty/getting-started.html){: new_window}
   * [Node.js ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](../runtimes/nodejs/getting-started.html){: new_window}
   * [Swift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](../runtimes/swift/getting-started.html){: new_window}


### Java
{: #java notoc}

Java dispone di funzionalità comprovate per la creazione delle applicazioni enterprise-grade. Ma le nuove funzionalità in Java 8, combinate con runtime più leggeri come Liberty e framework come Spring Boot, rendono anche Java perfettamente adatto alla creazione dei microservizi.


### Node.js
{: #node notoc}

Node.js è un runtime JavaScript che utilizza event-driven, un modello non bloccante, rendendolo più leggero ed efficiente, eccellendo per velocità effettiva e scalabilità per le applicazioni web, i modelli di backend-for-front-end e i microservizi. L'ecosistema di pacchetti Node.js, npm, fornisce l'accesso a una grande raccolta di moduli open source, fornendo un'ampia gamma di funzionalità per velocizzare lo sviluppo della tua applicazione.


### Swift
{: #swift notoc}

Swift è un linguaggio di programmazione moderno creato da Apple nel 2014 progettato per sostituire l'utilizzo di Objective C ed è open source da dicembre 2015. Oggi, viene utilizzato per creare software iOS, macOS, servizi web e sistemi su sistemi operativi Linux e macOS utilizzando l'architettura x86, ARM o Z. Scrive come un linguaggio di script ma è compilato per ottenere elevate prestazioni come C- con minore sovraccarico rendendolo ideale per i runtime cloud. Utilizza un sistema del tipo statico e sicuro che visualizzi in Java ma lo stile funzionale e le routine asincrone in JavaScript. È molto performante e l'origine compila il codice nativo utilizzando la toolchain del compilatore LLVM e può facilmente utilizzare le librerie di sistema esterne scritte in C.
