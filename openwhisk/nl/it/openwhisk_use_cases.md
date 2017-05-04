---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

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

Un altro argomento importante a favore di {{site.data.keyword.openwhisk_short}} è il costo di un sistema in una configurazione del ripristino di emergenza. Mettiamo a confronto i microservizi con PaaS o CaaS rispetto all'utilizzo di {{site.data.keyword.openwhisk_short}}. Supponiamo di avere 10 microservizi che utilizzano contenitori o runtime CloudFoundry, vale a dire 10 processi in continua esecuzione e fatturabili in una singola zona di disponibilità, 20 quando eseguiti in 2 zone di disponibilità e 40 quando eseguiti in 2 regioni con due zone ciascuna. Nel fare la stessa cosa eseguendo i microservizi in {{site.data.keyword.openwhisk_short}}, puoi eseguire i microservizi in tutte le zone di disponibilità e regioni che desideri senza spendere un centesimo in più.

[Logistics Wizard](https://www.ibm.com/blogs/bluemix/2017/02/microservices-multi-compute-approach-using-cloud-foundry-openwhisk/) è un'applicazione di esempio a livello aziendale che utilizza {{site.data.keyword.openwhisk_short}} e CloudFoundry per creare applicazioni in stile 12-factor. Si tratta di una soluzione di gestione della catena di fornitura intelligente che ha lo scopo di simulare un ambiente che esegue un sistema ERP. Permette di ampliare questo sistema ERP con le applicazioni per migliorare la visibilità e l'agilità dei gestori della catena di fornitura.

## Applicazioni web
{: #openwhisk_common_use_cases_webapps}

Data la natura guidata dagli eventi di {{site.data.keyword.openwhisk_short}}, esso offre numerosi vantaggi per le applicazioni rivolte agli utenti, poiché le richieste HTTP provenienti dal browser dell'utente fungono da eventi. Le applicazioni {{site.data.keyword.openwhisk_short}} utilizzano la capacità di elaborazione e vengono fatturate solo quando completano le richieste dell'utente. Non esistono modalità di inattività o di attesa. Ciò rende {{site.data.keyword.openwhisk_short}} molto meno costoso rispetto ai contenitori o alle applicazioni CloudFoundry tradizionali che potrebbero restare la maggior parte del tempo semplicemente in attesa della richieste dell'utente in entrata ed essere fatturate per tutto questo tempo di “sospensione”. 

È possibile creare ed eseguire un'applicazione web completa con {{site.data.keyword.openwhisk_short}}. La combinazione di API serverless con il file hosting statico per le risorse del sito, ad esempio HTML, JavaScript e CSS, ci permette di creare intere applicazioni serverless. La semplicità di gestione di un ambiente {{site.data.keyword.openwhisk_short}} su host (o meglio, non avendo nulla da gestire dal momento che è ospitato su Bluemix) è un grande vantaggio rispetto al supporto e alla gestione di un runtime Node.js Express o altri runtime di server tradizionali.

Ecco alcuni esempi su come utilizzare {{site.data.keyword.openwhisk_short}} per creare un'applicazione web:
- [Web Actions: Serverless Web Apps with {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/web-actions-serverless-web-apps-with-openwhisk-f21db459f9ba).
- [Build a user-facing {{site.data.keyword.openwhisk_short}} application with Bluemix and Node.js](https://www.ibm.com/developerworks/cloud/library/cl-openwhisk-node-bluemix-user-facing-app/index.html)
- [Serverless HTTP handlers with {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/serverless-http-handlers-with-openwhisk-90a986cc7cdd)

## IoT
{: #openwhisk_common_use_cases_iot}

Gli scenari dell'Internet delle cose sono spesso intrinsecamente guidati dai sensori. Ad esempio, un'azione potrebbe essere attivata in {{site.data.keyword.openwhisk_short}} se vi è la necessità di reagire di fronte a un sensore che supera una determinata temperatura. Le interazioni IoT sono generalmente senza stato con un rischio di livello di carico molto alto in caso di eventi importanti (catastrofi naturali, fenomeni meteorologici significativi, ingorghi ecc.). Questo crea la necessità di un sistema elastico dove il normale carico di lavoro potrebbe essere basso, ma che deve ridimensionarsi molto rapidamente con tempi di risposta prevedibili ed essere in grado di gestire un numero estremamente elevato di eventi senza preavviso al sistema. È molto difficile creare un sistema che soddisfi questi requisiti utilizzando le architetture server tradizionali in quanto tendono ad essere poco potenti e incapaci di gestire picchi di traffico o potrebbero essere sottoposte a un provisioning eccessivo ed essere quindi estremamente costose.

È certamente possibile implementare applicazioni IoT utilizzando architetture server tradizionali, tuttavia, in molti casi la combinazione di diversi servizi e bridge di dati richiede pipeline flessibili e dalle elevate prestazioni, che vanno dai dispositivi IoT all'archiviazione cloud e di una piattaforma di analisi. Spesso i bridge pre-configurati non hanno la programmabilità necessaria per implementare e ottimizzare l'architettura di una determinata soluzione. Data la grande varietà di possibili pipeline e la mancanza di standardizzazione attorno alla fusione di dati, in generale, e in IoT, in particolare, esistono molti casi in cui la pipeline richiede la trasformazione di dati personalizzata (per la conversione di formato, il filtraggio, l'ampliamento ecc.). {{site.data.keyword.openwhisk_short}} è uno strumento eccellente per implementare tale trasformazione in una modalità 'serverless', in cu la logica personalizzata è ospitata su una piattaforma cloud flessibile e interamente gestita.

Ecco un'applicazione IoT di esempio che utilizza {{site.data.keyword.openwhisk_short}}, NodeRed, Cognitive e altri servizi: [Serverless transformation of IoT data-in-motion with {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/serverless-transformation-of-iot-data-in-motion-with-openwhisk-272e36117d6c#.akt3ocjdt).

![Esempio di architettura della soluzione IoT](images/IoT_solution_architecture_example.png)

## Backend API
{: #openwhisk_common_use_cases_iot}

Le piattaforme di elaborazione serverless offrono agli sviluppatori un modo rapido per creare API senza server. {{site.data.keyword.openwhisk_short}} supporta la generazione automatica dell'API REST per le azioni. La [funzione sperimentale](./apigateway.md) di {{site.data.keyword.openwhisk_short}} ti consente di richiamare un'azione con metodi HTTP diversi da POST e senza la chiave API di autorizzazione dell'azione attraverso {{site.data.keyword.openwhisk_short}} API Gateway. Questa funzione è utile non solo per esporre le API ai clienti esterni, ma anche per creare applicazioni di microservizi.

Inoltre, le azioni {{site.data.keyword.openwhisk_short}} possono essere connesse a uno strumento di gestione API a scelta (come [IBM API Connect](https://www-03.ibm.com/software/products/en/api-connect) o altri). Analogamente agli altri casi d'uso, si applicano tutte le considerazioni per la scalabilità e altri servizi QoS (Qualities of Services). 

[Emoting](https://github.com/l2fprod/openwhisk-emoting) è un'applicazione di esempio che utilizza le azioni {{site.data.keyword.openwhisk_short}} tramite l'API REST.

Ecco un esempio e una discussione di [utilizzo di Serverless come backend API](https://martinfowler.com/articles/serverless.html#ACoupleOfExamples).

## Back-end mobile
{: #openwhisk_common_use_cases_mobile}

Numerose applicazioni mobile richiedono una logica lato server. Dal momento che solitamente gli sviluppatori di applicazioni mobili non hanno esperienza nella gestione della logica lato server e si concentrerebbero invece sull'applicazione in esecuzione sul dispositivo, l'utilizzo di {{site.data.keyword.openwhisk_short}} come back-end lato server rappresenta una buona soluzione. Inoltre, il supporto integrato per Swift lato server consente agli sviluppatori di riutilizzare le proprie competenze di programmazione iOS. Le applicazioni mobili hanno spesso modelli di carico imprevedibili e la soluzione {{site.data.keyword.openwhisk_short}} ospitata, come IBM Bluemix, può ridimensionarsi per soddisfare praticamente qualsiasi esigenza del carico di lavoro, senza la necessità di fornire risorse prima del tempo.

[Skylink](https://github.com/IBM-Bluemix/skylink) è un'applicazione di esempio che ti consente di collegare un drone tramite iPad a IBM Cloud con l'analisi delle immagini quasi in tempo reale utilizzando {{site.data.keyword.openwhisk_short}}, IBM Cloudant, IBM Watson e Alchemy Vision.

[BluePic](https://github.com/IBM-Swift/BluePic) è un'applicazione per la condivisione di foto e immagini che ti consente di scattare foto e di condividerle con gli altri utenti di BluePic. Questa applicazione mostra come sfruttare, in un'applicazione mobile iOS 10, un'applicazione server basata su Kitura scritta in Swift; l'applicazione utilizza {{site.data.keyword.openwhisk_short}}, Cloudant, Object Storage per i dati di immagine. AlchemyAPI è utilizzato anche nella sequenza {{site.data.keyword.openwhisk_short}} per analizzare l'immagine ed estrarre i tag di testo in base al contenuto dell'immagine e quindi inviare una notifica di push all'utente.

## Elaborazione dati
{: #openwhisk_common_use_cases_data}

Data la quantità di dati attualmente disponibile, lo sviluppo di applicazioni richiede la capacità di elaborare nuovi dati e, potenzialmente, rispondere agli stessi. Questa necessità include il bisogno di elaborare record di database strutturati e documenti non strutturati, immagini o video. {{site.data.keyword.openwhisk_short}} può essere configurato tramite i feed forniti dal sistema o personalizzati per reagire di fronte alle modifiche nei dati ed eseguire automaticamente le azioni sui feed di dati in entrata. Le azioni possono essere programmate per elaborare le modifiche, trasformare i formati dei dati, inviare e ricevere messaggi, richiamare altre azioni e aggiornare i diversi archivi di dati tra cui database relazionali basati su SQL, griglie di dati in memoria, database NoSQL, file, broker di messaggistica e numerosi altri sistemi. Le regole e le sequenze di {{site.data.keyword.openwhisk_short}} forniscono la flessibilità di apportare modifiche nell'elaborazione della pipeline senza programmazione, semplicemente tramite delle modifiche di configurazione. Ciò rende il sistema basato su {{site.data.keyword.openwhisk_short}} estremamente agile e facilmente adattabile ai requisiti di modifica.

Il progetto [OpenChecks](https://github.com/krook/openchecks) è un modello di verifica che mostra come utilizzare {{site.data.keyword.openwhisk_short}} per l'elaborazione del deposito di assegni su un conto bancario utilizzando il riconoscimento ottico dei caratteri. Attualmente è costruito sul servizio pubblico Bluemix {{site.data.keyword.openwhisk_short}} e si basa su Cloudant e SoftLayer Object Storage. In loco, potrebbe utilizzare CouchDB e OpenStack Swift. Altri servizi di archiviazione potrebbero includere FileNet o Cleversafe. Tesseract fornisce la libreria OCR.
## Cognitive
{: #openwhisk_common_use_cases_cognitive}

Le tecnologie Cognitive possono essere combinate efficacemente con {{site.data.keyword.openwhisk_short}} per creare potenti applicazioni. Ad esempio, IBM Alchemy API e Watson Visual Recognition possono essere utilizzati con {{site.data.keyword.openwhisk_short}} per estrarre automaticamente informazioni utili dai video senza doverli guardare. Può essere semplicemente un'estensione “cognitiva” del caso d'uso [Elaborazione dati](#data-processing) descritto in precedenza. Un altro buon uso di {{site.data.keyword.openwhisk_short}} è quello di implementare la funzione Bot combinata con i servizi cognitivi. 

Ecco un'applicazione di esempio [Dark vision](https://github.com/IBM-Bluemix/openwhisk-darkvisionapp) che fa proprio questo. In questa applicazione l'utente carica un video o immagine utilizzando l'applicazione web Dark Vision, che lo memorizza in un database Cloudant. Una volta caricato il video, {{site.data.keyword.openwhisk_short}} rileva il nuovo video ascoltando le modifiche Cloudant (trigger). {{site.data.keyword.openwhisk_short}} attiva quindi l'azione dell'estrattore di video. Durante la sua esecuzione, l'estrattore produce dei frame (immagini) e li memorizza in Cloudant. I frame vengono quindi elaborati mediante Watson Visual Recognition e i risultati vengono memorizzati nello stesso DB Cloudant. È possibile visualizzare i risultati utilizzando l'applicazione web Dark Vision OPPURE un'applicazione iOS. È possibile utilizzare Object Storage in aggiunta a Cloudant. Così facendo, i metadati di video e immagini vengono memorizzati in Cloudant e i file multimediali vengono memorizzati in Object Storage.

Ecco un'[applicazione di esempio iOS Swift](https://github.com/gconan/BluemixMobileServicesDemoApp) che mostra {{site.data.keyword.openwhisk_short}}, IBM Mobile Analytics, Watson per l'analisi dei toni e la pubblicazione in un canale Slack.

## Elaborazione eventi con Kafka o Message Hub 

{{site.data.keyword.openwhisk_short}} è particolarmente adatto ad essere usato insieme a Kafka, al servizio IBM Message Hub (basato su Kafka) e ad altri sistemi di messaggistica. La natura guidata dagli eventi di questi sistemi richiede il runtime basato su eventi per elaborare i messaggi e applicare la logica di business a questi messaggi, che è esattamente ciò che {{site.data.keyword.openwhisk_short}} fornisce con i suoi feed, trigger, azioni ecc. Kafka e Message Hub sono spesso utilizzati per volumi molto elevati e imprevedibili di carico di lavoro e richiedono che il consumo di quei messaggi sia scalabile da un momento all'altro, che è di nuovo un punto chiave di {{site.data.keyword.openwhisk_short}}. {{site.data.keyword.openwhisk_short}} ha la capacità integrata di consumare i messaggi così come di pubblicare i messaggi forniti nel pacchetto [openwhisk-package-kafka](https://github.com/openwhisk/openwhisk-package-kafka).

Ecco un'[applicazione di esempio che implementa uno scenario di elaborazione eventi](https://github.com/IBM/openwhisk-data-processing-message-hub) con {{site.data.keyword.openwhisk_short}}, Message Hub e Kafka.
