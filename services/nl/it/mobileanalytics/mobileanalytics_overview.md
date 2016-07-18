---

copyright:
  years: 2015, 2016

---
{:shortdesc: .shortdesc}

# Informazioni su {{site.data.keyword.mobileanalytics_short}}  
{: aboutmobileanalytics}
*Ultimo aggiornamento: 21 aprile 2016*
{: .last-updated}

{: shortdesc}
Il servizio {{site.data.keyword.mobileanalytics_full}} fornisce un'analisi approfondita dell'utilizzo e delle prestazioni delle applicazioni chiave per gli sviluppatori di applicazioni mobili e i proprietari di applicazioni.  Utilizzando {{site.data.keyword.mobileanalytics_short}}, i proprietari e gli sviluppatori di applicazioni possono comprendere cosa sta
succedendo sul "lato utente" e possono utilizzare questa analisi approfondita per sviluppare meglio delle applicazioni di vero interesse per gli utenti e
che si distinguono nella ricchissima offerta di applicazioni mobili. 

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
		<dd>Crea un'istanza del servizio in {{site.data.keyword.Bluemix}}, aggiungi l'SDK al tuo progetto, incolla due righe di codice nella tua applicazione e sei pronto a raccogliere dozzine di metriche predefinite.</dd>
	<dt>Raccogli i dati che vuoi</dt>
		<dd>Strumenta le applicazioni di eventi personalizzati, scopri in che modo gli utenti stanno interagendo con la tua applicazione, tieni traccia degli acquisiti e monitora l'attività delle applicazioni.  
</dd>
<dt>Consulta le metriche per tutte le tue applicazioni con un colpo d'occhio</dt>
	<dd>La console {{site.data.keyword.mobileanalytics_short}} offre sia grafici già pronti che grafici personalizzati, senza che occorra scrivere delle query.</dd>
<dt>Concentrati su quello che è importante per te</dt>
	<dd>Filtra le metriche in base a data/ora, adattatore, applicazione, versione applicazione, sistema operativo, versione del sistema operativo e modello di dispositivo.</dd>
<dt>Scopri rapidamente i problemi</dt>
	<dd>Monitora lo stato di arresto anomalo. Imposta dei trigger di avviso sulle metriche critiche e instrada gli avvisi a qualsiasi endpoint REST. </dd>
<dt>Risolvi la causa di fondo</dt>
	<dd>Utilizza la registrazione client personalizzata nella tua applicazione, carica automaticamente i log ed esegui ricerche al loro interno dalla console. Esegui il drill-down sugli eventi di arresto anomalo per visualizzare le tracce di stack. </dd>
</dl>
 

## Utilizzo di metriche ed eventi
{: #usingmetrics}

Con le **metriche predefinite**, puoi rispondere a domande come:

*Quanti nuovi utenti ho?*  
*Quante persone stanno attivamente utilizzando la mia applicazione?*  
*Con che frequenza le persone stanno utilizzando la mia applicazione?*  
*A che ora del giorno le persone stanno utilizzando la mia applicazione?*  
*Quali modelli di dispositivo preferiscono i miei utenti?*  
*Quando devo abbandonare il supporto per i sistemi operativi legacy?*  
*Per quale applicazioni si stanno riscontrando dei problemi delle prestazioni?*  

Aggiungendo dei tuoi **eventi personalizzati**, puoi rispondere a domande come:  

*Quali funzioni sono utilizzate di più e quali di meno?*  
*Dove si trovano gli utenti che accedono ed escono dalla mia applicazione?*  
*Quali attività gli utenti stanno visualizzando maggiormente?*  
*Gli utenti stanno completando i flussi di lavoro nell'applicazione? (ad esempio, i funnel di conversione)*  

<!--Client-side logs and usage data are gathered automatically and sent to the Mobile Analytics -->
<!-- service on demand. Developers and -->
<!-- administrators can use the {{site.data.keyword.mobileanalytics_short}} service dashboard to view data that -->
<!-- is gathered by the client SDK. -->

<!--## Data visualization
{: data-visualization}

All data that is collected by the analytics service can be visualized through the {{site.data.keyword.mobileanalytics_short}} dashboard which is accessible from your {{site.data.keyword.Bluemix_notm}} dashboard by clicking your IBM {{site.data.keyword.mobileanalytics_short}} service tile instance. You can also create custom charts, based on data that is collected by the analytics service in the dashboard. In addition to an at-a-glance view of your mobile analytics, the analytics feature includes the capability to perform a raw search against client logs, captured client crash data, and any extra data that you explicitly provide through client API function calls that feed into the {{site.data.keyword.mobileanalytics_short}} service. -->

># Link correlati {:class="linklist"}
<!-->## Esercitazioni ed esempi {:id="samples"}-->
<!-->* [Link1](https://github.com/)-->
>
># Link correlati {:class="linklist"}
>## Link correlati {:id="general"}
## SDK
<!-- Links to SDK download and SDK Developer Guide -->
* [SDK Android](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core )  
* [SDK iOS](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)  
>
>{:elementKind="article" id="rellinks"}
