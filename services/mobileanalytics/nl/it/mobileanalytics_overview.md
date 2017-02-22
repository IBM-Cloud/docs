---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Informazioni su {{site.data.keyword.mobileanalytics_short}}  
{: aboutmobileanalytics}

{: shortdesc}
Il servizio {{site.data.keyword.mobileanalytics_full}} fornisce un'analisi approfondita dell'utilizzo e delle prestazioni delle applicazioni chiave per gli sviluppatori di applicazioni mobili e i proprietari di applicazioni. Utilizzando {{site.data.keyword.mobileanalytics_short}}, i proprietari e gli sviluppatori di applicazioni possono comprendere cosa sta succedendo sul lato utente e possono utilizzare questa analisi approfondita per sviluppare meglio delle applicazioni di vero interesse per gli utenti e che si distinguono nella ricchissima offerta di applicazioni mobili.  

{: #overview}  
Il servizio include la console {{site.data.keyword.mobileanalytics_short}}, dove gli sviluppatori e i proprietari di applicazioni possono monitorare le prestazioni delle applicazioni mobili, visualizzare le statistiche di utilizzo e cercare nei log dispositivo.  {{site.data.keyword.mobileanalytics_short}} fornisce degli SDK client per iOS 8+ (solo Swift) e Android 4+.

<!-- Mobile Analytics Server SDKs - set of server SDKs to protect resources that are-->
<!--hosted on {{site.data.keyword.Bluemix_notm}}. Currently supported runtimes are-->
<!--Node.js and Java for Liberty.-->

Con il servizio {{site.data.keyword.mobileanalytics_short}} puoi:
<!-- and includes the following capabilities: -->
<!-- * Near real-time analytics for client activity. Exp -->
<!--* Network latency analytics. GA only -->
<!-- * Client log search and download. Exp -->
<!--* Server log search and download. GA only -->
<!-- Crash and stack trace search. Exp -->

<dl>
	<dt>Ottenere delle immediate informazioni approfondite</dt>
		<dd>Visualizzare le metriche di prestazioni e utilizzo in tempo reale.</dd>
	<dt>Eseguire l'implementazione in pochi minuti</dt>
		<dd>Crea un'istanza del servizio in {{site.data.keyword.Bluemix}}, aggiungi l'SDK al tuo progetto, incolla due righe di codice nella tua applicazione e sei pronto a raccogliere dozzine di metriche predefinite. </dd>
	<dt>Raccogli i dati che vuoi</dt>
		<dd>Strumenta le applicazioni di eventi personalizzati, scopri in che modo gli utenti stanno interagendo con la tua applicazione, tieni traccia degli acquisiti e monitora l'attività delle applicazioni.  
</dd>
<dt>Consulta le metriche per tutte le tue applicazioni con un colpo d'occhio </dt>
	<dd>La console {{site.data.keyword.mobileanalytics_short}} offre <!-- both --> grafici già pronti <!--and custom-->, senza che occorra scrivere delle query.</dd>
<dt>Concentrati su quello che è importante per te</dt>
	<dd>Filtra le metriche in base a data/ora, adattatore, applicazione, versione applicazione, sistema operativo, versione del sistema operativo e modello di dispositivo. </dd>
<dt>Scopri rapidamente i problemi</dt>
	<dd>Monitora lo stato di arresto anomalo. Imposta dei trigger di avviso sulle metriche critiche e instrada gli avvisi a qualsiasi endpoint REST. </dd>
<dt>Risolvi la causa di fondo</dt>
	<dd>Utilizza la registrazione personalizzata nella tua applicazione, carica automaticamente i log ed esegui ricerche al loro interno dalla console. Esegui il drill-down sugli eventi di arresto anomalo per visualizzare le tracce di stack.</dd>
</dl>
 

## Utilizzo di metriche ed eventi
{: #usingmetrics}

Con le **metriche predefinite**, puoi rispondere a domande come:

* Quanti nuovi utenti ho?   
* Quante persone stanno attivamente utilizzando la mia applicazione?   
* Con che frequenza le persone stanno utilizzando la mia applicazione?  
* A che ora del giorno le persone stanno utilizzando la mia applicazione?    
* Quali modelli di dispositivo preferiscono i miei utenti?  
* Quando devo abbandonare il supporto per i sistemi operativi legacy?  
* Per quali applicazioni si stanno riscontrando dei problemi delle prestazioni?   

Aggiungendo dei tuoi **eventi personalizzati**, puoi rispondere a domande come: 

* Quali funzioni sono utilizzate di più e quali di meno?   
* Dove si trovano gli utenti che accedono ed escono dalla mia applicazione?   
* Quali attività gli utenti stanno visualizzando maggiormente?   
* Gli utenti stanno completando i flussi di lavoro nell'applicazione (ad esempio, i funnel di conversione)?    

I dati di utilizzo e i log lato client vengono raccolti automaticamente ed inviati al servizio Mobile Analytics su richiesta. Gli sviluppatori e gli amministratori possono utilizzare il dashboard del servizio {{site.data.keyword.mobileanalytics_short}} per visualizzare i dati raccolti dall'SDK client.

## Visualizzazione dati
{: data-visualization}

Tutti i dati raccolti dal servizio Analytics possono essere visualizzati tramite il dashboard {{site.data.keyword.mobileanalytics_short}} che è accessibile dal tuo dashboard {{site.data.keyword.Bluemix_notm}} facendo clic sull'istanza del tile del servizio IBM {{site.data.keyword.mobileanalytics_short}}. <!--You can also create custom charts, based on data that is collected by the analytics service in the dashboard.--> In aggiunta, per una visualizzazione immediata delle tue analisi mobili, la funzione di analisi include la funzionalità di eseguire una ricerca non elaborata nei tuoi log client, dati di arresti anomali del client acquisiti e qualsiasi ulteriore dato che fornisci esplicitamente tramite le chiamate della funzione API client che fornisce il servizio {{site.data.keyword.mobileanalytics_short}}. 

## Domande frequenti {{site.data.keyword.mobileanalytics_short}}  
{: #faq}

<dl>
	<dt>Che cos'è {{site.data.keyword.mobileanalytics_full}}?</dt>
		<dd>{{site.data.keyword.mobileanalytics_full}} è un servizio che fornisce informazioni approfondite cronologiche e in tempo reale su come stanno venendo eseguite ed utilizzate le tue applicazioni. Utilizzando {{site.data.keyword.mobileanalytics_short}}, i proprietari e gli sviluppatori dell'applicazione possono prendere decisioni di indirizzamento dati monitorando gli andamenti degli utenti attivi, delle sessioni, delle piattaforme mobili e degli arresti anomali dell'applicazione. Puoi anche impostare gli avvisi su metriche selezionate che, una volta attivati, inviano messaggi a tutti gli endpoint REST, inclusi il servizio di push o i tuoi servizi di messaggistica interni.</dd>
	<dt>Come posso utilizzare {{site.data.keyword.mobileanalytics_short}} per {{site.data.keyword.Bluemix_notm}}?</dt>
		<dd>Come responsabile del prodotto dell'applicazione mobile, puoi visualizzare quante persone utilizzano la tua applicazione (metriche utente) e quando la stanno utilizzando (metriche sessione). Queste informazioni sono presentate come serie temporali e sono aggiornate in tempo reale in modo che puoi notare l'effetto delle modifiche che effettui per la tua applicazione. Puoi impostare un filtro per visualizzare versioni o sistemi operativi dell'applicazione specifici e prendere decisioni di assegnazione della priorità o di deprecazione. </dd>
		<dd>Come venditore dell'applicazione mobile, puoi utilizzare le metriche sessione e utente per monitorare il coinvolgimento, gestire la variazione e valutare l'efficacia dell'impatto di marketing dell'applicazione mobile osservando le modifiche nel tempo e correlandole ai tuoi dati evento. </dd>
		<dd>Come sviluppatore dell'applicazione mobile, puoi utilizzare le metriche degli arresti anomali per rilevare e risolvere problemi nelle prestazioni dell'applicazione mobile prima che frustino l'utente e danneggino la reputazione dell'applicazione. Puoi monitorare il numero e la frequenza degli arresti anomali dalla console di analisi e puoi dare priorità agli arresti anomali che coinvolgono molti utenti. Puoi impostare gli avvisi per inviare notifiche o per effettuare azioni automatizzate quando gli arresti anomali superano una soglia fornita e puoi risolvere i problemi eseguendo il drilldown delle istanze con arresti anomali per visualizzare i log del dispositivo e le tracce di stack dell'applicazione. </dd>
	<dt>Ho bisogno di una analista dei dati per utilizzare Mobile Analytics?</dt>
		<dd>No, {{site.data.keyword.mobileanalytics_short}} offre una console di analisi pronta per l'utilizzo per le parti interessate di business e per gli sviluppatori dell'applicazione. Non è richiesta alcuna competenza di query.</dd>
	<dt>Posso eseguire query personalizzate sui miei dati di analisi?</dt>
		<dd>{{site.data.keyword.mobileanalytics_short}} non consente query personalizzate ma sarà preso in considerazione per il futuro.</dd>
	<dt>Come posso collegare la mia applicazione a {{site.data.keyword.mobileanalytics_short}}? </dt>
		<dd>[Scarica la nostra SDK open source per iOS o Android](install-client-sdk.html), o utilizza la {{site.data.keyword.mobileanalytics_short}} [API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/) per altre piattaforme. </dd>
	<dt>In quali regioni Bluemix è disponibile {{site.data.keyword.mobileanalytics_short}}?</dt>
		<dd>Al momento, Mobile Analytics è disponibile negli Stati Uniti - Sud e nel Regno Unito. La disponibilità in altre regioni è stata pianificata ma il periodo non è ancora stato determinato. </dd>
	<dt>Quanto costa questo servizio?</dt>
		<dd>I primi 100 milioni di eventi raccolti ogni mese sono gratuiti e quindi, il costo degli eventi è $1 per milioni di eventi.</dd>
	<dt>Cosa è un evento?</dt>
		<dd>Al momento gli eventi riportati includono l'avvio e la fine della sessione dell'applicazione (incluso l'arresto anomalo dell'applicazione), le notifiche di avviso e le voci di log.</dd>
	<dt>Come posso stimare quanto il servizio costerà al mese?</dt>
		<dd>Poiché il prezzo dipende dal numero di eventi inviati al servizio per account del client, la stima del prezzo equivale alla stima degli eventi.  
<p>
Il prezzo che viene addebitato è la somma degli eventi da tutte le applicazioni che hai collegato a {{site.data.keyword.mobileanalytics_short}}. Per un'applicazione specificata, il numero di eventi dipende dal grado di strumentazione che hai implementato nell'applicazione, dal numero di utenti e da quanto sono attivi gli utenti.   
</p>
<p>
Utilizza questa formula per stimare l'utilizzo:
eventi per mese per applicazione = (utenti al giorno)(sessioni per utente al giorno)(giorni del mese)(eventi per sessione)
</p>
<p>
Gli eventi per sessione possono variare ampiamente da 2 a diverse centinaia, a seconda di quante chiamate di rete, analisi personalizzate, acquisizioni log e definizioni dell'avviso lo sviluppatore ha configurato nell'applicazione.
</p>
	<dt>Per quanto tempo sono conservati i miei dati?</dt>
		<dd>I dati sono conservati almeno per 30 giorni. </dd>
	<dt>Quanto ci impiegano i dati ad essere visualizzati nella console {{site.data.keyword.mobileanalytics_short}}?</dt>
		<dd>I dati nella console {{site.data.keyword.mobileanalytics_short}} sono quasi in tempo reale, il che significa che i dati vengono visualizzati pochi secondi dopo gli eventi effettivi.</dd>
	<dt>Quale è la differenza tra {{site.data.keyword.mobileanalytics_full}} e le analisi mobili di MobileFirst Platform Foundation?</dt>
		<dd>Le metriche sessione e utente sono molto simili in queste due console, ma le analisi che provengono da MobileFirst Platform Foundation contengono ulteriori metriche e impostazioni che consentono ai client di gestire il proprio cluster di analisi in locale. Inoltre, la console di analisi MobileFirst Platform Foundation interrompe le metriche per gli adattatori e le procedure dell'adattatore, mentre nel servizio {{site.data.keyword.mobileanalytics_short}}, queste metriche sono integrate nelle tabelle e nei grafici della richiesta di rete.</dd>
	<dt>Sto utilizzando MobileFirst Platform Foundation in locale per sviluppare le mie applicazioni ma non voglio ospitare il mio proprio cluster di analisi. Posso invece utilizzare {{site.data.keyword.mobileanalytics_full}}?</dt>
		<dd>Sì. Disponi di un paio di opzioni: Se stai utilizzando MobileFirst Platform Foundation 7.x o 8.0 e le tue applicazioni sono instrumentate con le SDK MobileFirst Platform, puoi configurare il tuo server MobileFirst per notificare i dati di analisi a {{site.data.keyword.mobileanalytics_short}} per {{site.data.keyword.Bluemix_notm}}. Leggi il post del blog [Configuring Mobile Analytics and Mobile Foundation Bluemix services ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://mobilefirstplatform.ibmcloud.com/blog/2016/07/11/analytics-bm-service/ "icona link esterno"){: new_window} per i dettagli. In alternativa, puoi instrumentare le tue applicazioni ad utilizzare la SDK {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} ed inviare notifiche direttamente al servizio {{site.data.keyword.mobileanalytics_short}}.</dd>
	<!-- <dt>My instance of  {{site.data.keyword.mobileanalytics_short}} does not look like the screen shots in the catalog. What's going on?</dt> -->
		<!-- <dd>Most likely you are using the Classic view interface for {{site.data.keyword.Bluemix_notm}}. Classic view is deprecated, so {{site.data.keyword.mobileanalytics_short}} runs best in the new {{site.data.keyword.Bluemix_notm}} interface. If you are in Classic view, you will see a link in the {{site.data.keyword.Bluemix_notm}} header that says <strong>Try the new {{site.data.keyword.Bluemix_notm}}</strong>. Click that link to use the new interface.</dd> -->
</dl>


# rellinks
 {:class="linklist"}

## SDK
{: rellink-sdk}
<!-- Links to SDK download and SDK Developer Guide -->
* [Android SDK ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core "icona link esterno"){: new_window} 
* [iOS SDK ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core "icona link esterno"){: new_window}

<!-- {:elementKind="article" id="rellinks"} -->
