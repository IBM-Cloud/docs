---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Casi d'uso comuni di {{site.data.keyword.openwhisk_short}}
{: #openwhisk_common_use_cases}

Il modello di esecuzione offerto da {{site.data.keyword.openwhisk_short}} supporta un'ampia gamma di casi d'uso. Le seguenti sezioni includono alcuni esempi tipici. Per una discussione più dettagliata sull'architettura Serverless, i casi d'uso di esempio, i pro e i contro e le procedure consigliate per l'implementazione, leggi l'eccellente [articolo di Mike Roberts sul blog di Martin Fowler](https://martinfowler.com/articles/serverless.html).
{: shortdesc}

## Microservizi
{: #openwhisk_common_use_cases_microservices}

Nonostante la loro utilità, le soluzioni basate sui microservizi rimangono difficili da creare con le tradizionali tecnologie cloud, che spesso richiedono il controllo di una toolchain complessa e la separazione delle pipeline operative e di creazione. I piccoli e dinamici team, che impiegano troppo tempo ad affrontare le complessità infrastrutturali e operative (tolleranza agli errori, bilanciamento del carico, auto-scaling e registrazione), vogliono soprattutto un modo per sviluppare un codice di valore aggiunto e semplificato con i linguaggi di programmazione che già conoscono e prediligono e che siano più adatti a risolvere problemi particolari. 

La natura modulare e intrinsecamente scalabile di {{site.data.keyword.openwhisk_short}} lo rende ideale per l'implementazione di parti granulari di logica nelle azioni. Le azioni {{site.data.keyword.openwhisk_short}} sono indipendenti tra loro e possono essere implementate utilizzando una varietà di linguaggi supportati da {{site.data.keyword.openwhisk_short}} e accedere ai diversi sistemi di backend. Ogni azione può essere implementata e gestita autonomamente e viene ridimensionata indipendentemente dalle altre azioni. L'interconnettività tra le azioni è fornita da {{site.data.keyword.openwhisk_short}} sotto forma di regole, sequenze e convenzioni di denominazione. Tutto ciò è di buon auspicio per le applicazioni basate sui microservizi.

## Applicazioni web
{: #openwhisk_common_use_cases_webapps}

Anche se {{site.data.keyword.openwhisk_short}} era stato originariamente concepito per la programmazione basata su eventi, offre numerosi vantaggi per le applicazioni rivolte agli utenti. Ad esempio, se lo combini con un piccolo stub Node.js, puoi utilizzarlo per servire le applicazioni in cui è semplice eseguire il debug. Inoltre, poiché le applicazioni {{site.data.keyword.openwhisk_short}} richiedono un'intensità di calcolo molto inferiore rispetto all'esecuzione di un processo server su una piattaforma PaaS, sono anche notevolmente più economiche.  

È possibile creare ed eseguire un'applicazione web completa con OpenWhisk. La combinazione di API serverless con il file hosting statico per le risorse del sito, ad esempio HTML, JavaScript e CSS, ci permette di creare intere applicazioni serverless. La semplicità di gestione di un ambiente {{site.data.keyword.openwhisk_short}} su host (o meglio, non avendo nulla da gestire dal momento che è ospitato su Bluemix) è un grande vantaggio rispetto al supporto e alla gestione di un runtime Node.js Express o altri runtime di server tradizionali.

Una delle cose che aiuta, è l'opzione dello strumento *wsk* della CLI {{site.data.keyword.openwhisk_short}} denominata "--annotation web-export true", che rende il codice accessibile da un browser web.

Ecco alcuni esempi su come utilizzare {{site.data.keyword.openwhisk_short}} per creare un'applicazione web:
- [Web Actions: Serverless Web Apps with OpenWhisk](https://medium.com/openwhisk/web-actions-serverless-web-apps-with-openwhisk-f21db459f9ba).
- [Build a user-facing {{site.data.keyword.openwhisk_short}} application with Bluemix and Node.js](https://www.ibm.com/developerworks/cloud/library/cl-openwhisk-node-bluemix-user-facing-app/index.html)
- [Serverless HTTP handlers with OpenWhisk](https://medium.com/openwhisk/serverless-http-handlers-with-openwhisk-90a986cc7cdd)

## IoT
{: #openwhisk_common_use_cases_iot}

È certamente possibile implementare applicazioni IoT utilizzando architetture server tradizionali, tuttavia, in molti casi la combinazione di diversi servizi e bridge di dati richiede pipeline flessibili e dalle elevate prestazioni, che vanno dai dispositivi IoT all'archiviazione cloud e di una piattaforma di analisi. Spesso i bridge pre-configurati non hanno la programmabilità necessaria per implementare e ottimizzare l'architettura di una determinata soluzione. Data la grande varietà di possibili pipeline e la mancanza di standardizzazione attorno alla fusione di dati, in generale, e in IoT, in particolare, esistono molti casi in cui la pipeline richiede la trasformazione di dati personalizzata (per la conversione di formato, il filtraggio, l'ampliamento ecc.). {{site.data.keyword.openwhisk_short}} è uno strumento eccellente per implementare tale trasformazione in una modalità 'serverless', in cu la logica personalizzata è ospitata su una piattaforma cloud flessibile e interamente gestita.

Gli scenari dell'Internet delle cose sono spesso intrinsecamente guidati dai sensori. Ad esempio, un'azione potrebbe essere attivata in {{site.data.keyword.openwhisk_short}} se vi è la necessità di reagire di fronte a un sensore che supera una determinata temperatura. Le interazioni IoT sono generalmente senza stato con un rischio di livello di carico molto alto in caso di eventi importanti (catastrofi naturali, fenomeni meteorologici significativi, ingorghi ecc.). Questo crea la necessità di un sistema elastico dove il normale carico di lavoro potrebbe essere basso, ma che deve ridimensionarsi molto rapidamente con tempi di risposta prevedibili ed essere in grado di gestire un numero estremamente elevato di eventi senza preavviso al sistema. È molto difficile creare un sistema che soddisfi questi requisiti utilizzando le architetture server tradizionali in quanto tendono ad essere poco potenti e incapaci di gestire picchi di traffico o potrebbero essere sottoposte a un provisioning eccessivo ed estremamente costose. 

Ecco un'applicazione IoT di esempio che utilizza OpenWhisk, NodeRed, Cognitive e altri servizi: [Serverless transformation of IoT data-in-motion with OpenWhisk](https://medium.com/openwhisk/serverless-transformation-of-iot-data-in-motion-with-openwhisk-272e36117d6c#.akt3ocjdt).

![Esempio di architettura della soluzione IoT](images/IoT_solution_architecture_example.png)

## Backend API
{: #openwhisk_common_use_cases_iot}

Le piattaforme di elaborazione serverless offrono agli sviluppatori un modo rapido per creare API senza server. {{site.data.keyword.openwhisk_short}} supporta la generazione automatica di API REST per le azioni ed è molto semplice collegare il tuo strumento di gestione API preferito (come [IBM API Connect](https://www-03.ibm.com/software/products/en/api-connect) o altri) a queste API REST fornite da OpenWhisk. Analogamente agli altri casi d'uso, si applicano tutte le considerazioni per la scalabilità e altri servizi QoS (Qualities of Services). 

Ecco un esempio e una discussione di [utilizzo di Serverless come backend API](https://martinfowler.com/articles/serverless.html#ACoupleOfExamples).

## Back-end mobile
{: #openwhisk_common_use_cases_mobile}

Numerose applicazioni mobile richiedono una logica lato server. Per gli sviluppatori di applicazioni mobili che non vogliono gestire la logica lato server e preferiscono concentrarsi sull'applicazione in esecuzione sul dispositivo o browser, l'utilizzo di {{site.data.keyword.openwhisk_short}} come backend lato server rappresenta una buona soluzione. Inoltre, il supporto integrato per Swift consente agli sviluppatori di riutilizzare le proprie competenze di programmazione iOS. Le applicazioni mobili hanno spesso modelli di carico imprevedibili e la soluzione {{site.data.keyword.openwhisk_short}} ospitata, come IBM Bluemix, può ridimensionarsi per soddisfare praticamente qualsiasi esigenza del carico di lavoro, senza la necessità di fornire risorse prima del tempo. 

## Elaborazione dati
{: #openwhisk_common_use_cases_data}

Data la quantità di dati attualmente disponibile, lo sviluppo di applicazioni richiede la capacità di elaborare nuovi dati e, potenzialmente, rispondere agli stessi. Questa necessità include il bisogno di elaborare record di database strutturati e documenti non strutturati, immagini o video. {{site.data.keyword.openwhisk_short}} può essere configurato tramite i feed forniti dal sistema o personalizzati per reagire di fronte alle modifiche nei dati ed eseguire automaticamente le azioni sui feed di dati in entrata. Le azioni possono essere programmate per elaborare le modifiche, trasformare i formati dei dati, inviare e ricevere messaggi, richiamare altre azioni e aggiornare i diversi archivi di dati tra cui database relazionali basati su SQL, griglie di dati in memoria, database NoSQL, file, broker di messaggistica e numerosi altri sistemi. Le regole e le sequenze di {{site.data.keyword.openwhisk_short}} forniscono la flessibilità di apportare modifiche nell'elaborazione della pipeline senza programmazione, semplicemente tramite delle modifiche di configurazione. Ciò rende il sistema basato su {{site.data.keyword.openwhisk_short}} estremamente agile e facilmente adattabile ai requisiti di modifica. 

## Cognitive
{: #openwhisk_common_use_cases_cognitive}

Le tecnologie Cognitive possono essere combinate efficacemente con {{site.data.keyword.openwhisk_short}} per creare potenti applicazioni. Ad esempio, IBM Alchemy API e Watson Visual Recognition possono essere utilizzati con {{site.data.keyword.openwhisk_short}} per estrarre automaticamente informazioni utili dai video senza doverli guardare. 

Ecco un'applicazione di esempio [Dark vision](https://github.com/IBM-Bluemix/openwhisk-darkvisionapp) che fa proprio questo. In questa applicazione l'utente carica un video o immagine utilizzando l'applicazione web Dark Vision, che lo memorizza in un database Cloudant. Una volta caricato il video, {{site.data.keyword.openwhisk_short}} rileva il nuovo video ascoltando le modifiche Cloudant (trigger). {{site.data.keyword.openwhisk_short}} attiva quindi l'azione dell'estrattore di video. Durante la sua esecuzione, l'estrattore produce dei frame (immagini) e li memorizza in Cloudant. I frame vengono quindi elaborati mediante Watson Visual Recognition e i risultati vengono memorizzati nello stesso DB Cloudant. È possibile visualizzare i risultati utilizzando l'applicazione web Dark Vision OPPURE un'applicazione iOS. È possibile utilizzare Object Storage in aggiunta a Cloudant. Così facendo, i metadati di video e immagini vengono memorizzati in Cloudant e i file multimediali vengono memorizzati in Object Storage.
