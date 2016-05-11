---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Informazioni su {{site.data.keyword.openwhisk}}

*Ultimo aggiornamento: 22 febbraio 2016*

Le seguenti sezioni forniscono informazioni dettagliate su {{site.data.keyword.openwhisk}}.
{: shortdesc}

## Modalità di funzionamento di {{site.data.keyword.openwhisk_short}}
{: #openwhisk_how}

{{site.data.keyword.openwhisk_short}} è una piattaforma di elaborazione guidata dagli eventi che esegue il codice in risposta a eventi o richiami diretti.

La seguente figura mostra l'architettura di alto livello di {{site.data.keyword.openwhisk_short}}.

![Architettura di {{site.data.keyword.openwhisk_short}}](OpenWhisk.png)

Esempi di eventi includono le modifiche ai record di database, letture del sensore IoT che superano una determinata temperatura, nuovi commit di codice a un repository GitHub o semplici richieste HTTP provenienti da applicazioni Web o mobili. Gli eventi provenienti da origini eventi interne ed esterne vengono incanalati attraverso un trigger e le regole consentono alle azioni di reazione a tali eventi.

Le azioni possono essere piccoli frammenti di codice Javascript o Swift oppure binari personalizzati integrati in un contenitore Docker. Le azioni di {{site.data.keyword.openwhisk_short}} vengono distribuite istantaneamente ed eseguite ogni volta che un trigger viene attivato. Più trigger vengono attivati, più azioni vengono richiamate. Se non viene attivato alcun trigger, non ci sono codici azione in esecuzione e, dunque, nessun consumo.

Oltre che con l'associazione delle azioni ai trigger, è possibile richiamare direttamente un'azione utilizzando l'API, la CLI o l'SDK iOS {{site.data.keyword.openwhisk_short}}. È possibile concatenare una serie di azioni anche senza dover scrivere alcun codice. Ciascuna azione della catena viene richiamata in sequenza con l'output di un'azione che viene trasmessa come input alla successiva azione della sequenza.

Con contenitori o macchine virtuali tradizionali a esecuzione prolungata, è prassi comune distribuire più macchine virtuali o contenitori in modo da difendersi dalle interruzioni di una singola istanza. Tuttavia, {{site.data.keyword.openwhisk_short}} offre un modello alternativo privo di costi correlati alla resilienza. L'esecuzione di azioni su richiesta fornisce una scalabilità intrinseca e un utilizzo ottimale, poiché il numero di azioni in esecuzione corrisponde sempre al tasso di trigger. Inoltre, lo sviluppatore ora si concentra solo sul suo codice, senza preoccuparsi di monitorare, applicare patch e proteggere l'infrastruttura di sistema, la rete, l'archiviazione e il server sottostanti.

Le integrazioni con servizi aggiuntivi e provider di eventi possono essere aggiunte con i pacchetti. Un pacchetto è una raccolta di feed e azioni. Un feed è un pezzo di codice che configura un'origine eventi esterna per l'attivazione di eventi trigger. Ad esempio, un trigger creato con un feed di modifica Cloudant configurerà un servizio per l'attivazione del trigger ad ogni aggiunta o modifica di un documento in un database Cloudant. Le azioni dei pacchetti rappresentano una logica riutilizzabile, che può essere resa disponibile da un fornitore di servizi cosicché gli sviluppatori non debbano limitarsi a utilizzare il servizio come un'origine eventi, ma possano anche richiamare le API di tale servizio.

Un catalogo di pacchetti esistente consente di ampliare le applicazioni con funzioni utili e accedere a servizi esterni appartenenti all'ecosistema con rapidità. Sono esempi di servizi esterni con attivazione {{site.data.keyword.openwhisk_short}}: Cloudant, The Weather Company, Slack e GitHub.


## Casi d'uso comuni
{: #openwhisk_use_cases}

Il modello di esecuzione offerto da {{site.data.keyword.openwhisk_short}} supporta un'ampia gamma di casi d'uso. Le seguenti sezioni includono alcuni esempi tipici.

### Scomposizione di applicazioni in microservizi
La natura modulare e intrinsecamente scalabile di {{site.data.keyword.openwhisk_short}} lo rende adatto all'implementazione di parti granulari di logica all'interno delle azioni. Ad esempio, {{site.data.keyword.openwhisk_short}} può essere utile per rimuovere attività (in background) ad alto carico potenzialmente spinose dal codice front-end e implementarle come azioni.

### Back-end mobile
Numerose applicazioni mobile richiedono una logica lato server. Posto che solitamente gli sviluppatori mobile non hanno esperienza nella gestione della logica lato server e si concentrerebbero invece sull'applicazione in esecuzione sul dispositivo, l'utilizzo di {{site.data.keyword.openwhisk_short}} come back-end lato server rappresenta una buona soluzione. Inoltre, il supporto integrato per Swift consente agli sviluppatori di riutilizzare le proprie competenze di programmazione iOS.

### Elaborazione dati
Data la quantità di dati attualmente disponibile, lo sviluppo di applicazioni richiede la capacità di elaborare nuovi dati e, potenzialmente, rispondere agli stessi. Questa necessità include il bisogno di elaborare record di database strutturati e documenti non strutturati, immagini o video.

### IoT
Gli scenari dell'Internet delle cose sono spesso intrinsecamente guidati dai sensori. Ad esempio, un'azione potrebbe essere avviata in {{site.data.keyword.openwhisk_short}} se occorre rispondere al superamento di una determinata temperatura da parte di un sensore.



