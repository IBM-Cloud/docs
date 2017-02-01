---



copyright:

  years: 2015, 2017

lastupdated: "2017-01-12"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.Bluemix_local_notm}}
{: #local}


{{site.data.keyword.Bluemix_local}} porta la potenza e l'agilità della piattaforma {{site.data.keyword.Bluemix_notm}} basata sul cloud al tuo data center. Con {{site.data.keyword.Bluemix_local_notm}}, puoi proteggere i tuoi carichi di lavoro più sensibili dietro il tuo firewall aziendale, continuando al tempo stesso a essere connesso in modo protetto e sincronizzato con {{site.data.keyword.Bluemix_notm}} pubblico.
{:shortdesc}

IBM® utilizza le operazioni cloud come un servizio per monitorare e gestire il tuo ambiente, consentendoti così di concentrarti sulla creazione di applicazioni e servizi che vengono eseguiti sull'ambiente. {{site.data.keyword.IBM_notm}} gestisce anche gli aggiornamenti della piattaforma, consentendo così di concentrarti sull'attività di business.

Gli ambienti {{site.data.keyword.Bluemix_local_notm}} hanno gli stessi standard di sicurezza di {{site.data.keyword.Bluemix_notm}} pubblico in termini di sicurezza operativa. Fornisci l'hardware e l'infrastruttura, che ti offre il controllo su infrastruttura e [sicurezza](/docs/security/index.html#localplatformsecurity) fisica. L'accesso degli sviluppatori all'ambiente {{site.data.keyword.Bluemix_notm}} locale è controllato dalle tue politiche LDAP, che possono essere configurate dal team {{site.data.keyword.Bluemix_notm}} quando configura il tuo ambiente. All'interno dell'ambiente locale, utilizzando la pagina Amministrazione, puoi [gestire utenti e autorizzazioni](/docs/admin/index.html#oc_useradmin).

{{site.data.keyword.Bluemix_local_notm}} viene fornito con tutti i runtime {{site.data.keyword.Bluemix_notm}} inclusi e 64 GB di memoria di elaborazione.

Inoltre, è presente una serie di servizi disponibili come servizi {{site.data.keyword.Bluemix_local_notm}}. Consulta la seguente tabella per vedere cosa è incluso e cosa è disponibile per l'acquisto.

| **Tipo** | **Nome** | **Descrizione** |
|----------|----------|-----------------|
|Incluso | [Runtime {{site.data.keyword.Bluemix_notm}}](/docs/cfapps/runtimes.html) | Utilizza i runtime per avere un'applicazione subito operativa, senza dover impostare e gestire macchine e sistemi operativi. Tutti i runtime {{site.data.keyword.Bluemix_notm}} sono a tua disposizione per utilizzarli nella tua istanza di {{site.data.keyword.Bluemix_notm}} locale.|
|Incluso | [{{site.data.keyword.autoscaling}}](/docs/services/Auto-Scaling/index.html)| Ti permette di aumentare o ridurre dinamicamente la capacità
di elaborazione della tua applicazione in base alle politiche. Con questo servizio, hai un uso illimitato nel tuo ambiente {{site.data.keyword.Bluemix}} locale.|
|Facoltativo | [{{site.data.keyword.apiconnect_short}}](/docs/services/apiconnect/index.html) | {{site.data.keyword.apiconnect_long}} integra {{site.data.keyword.APIM}} e IBM StrongLoop in una singola offerta che fornisce una soluzione completa per creare, eseguire, gestire e implementare API e microservizi. |
|Facoltativo | [{{site.data.keyword.cloudant}}](/docs/services/Cloudant/index.html#Cloudant) | {{site.data.keyword.cloudant}} fornisce l'accesso a un livello di dati JSON NoSQL interamente gestito sempre attivo. Questo servizio è compatibile con CouchDB e accessibile mediante un'interfaccia HTTP di facile utilizzo per i modelli di applicazione web e mobile. Per ulteriori informazioni, consulta l'intera [ documentazione ![icona link esterno](../icons/launch-glyph.svg)](http://docs.cloudant.com/BluemixLocal.html){: new_window} e i [requisiti hardware ![icona link esterno](../icons/launch-glyph.svg)](http://docs.cloudant.com/BluemixLocalHardware.html){: new_window} per un ambiente locale. |
|Facoltativo | [{{site.data.keyword.containershort}}](/docs/containers/container_index.html) | Esegui i contenitori Docker su {{site.data.keyword.Bluemix_notm}} locale. I contenitori sono oggetti software virtuali che includono tutti gli elementi che un'applicazione deve eseguire. Un contenitore presenta i vantaggi dell'isolamento e dell'assegnazione delle risorse, ma offre una maggiore portabilità ed efficienza rispetto, ad esempio, a una macchina virtuale. Per informazioni sui requisiti hardware, vedi [IBM {{site.data.keyword.containershort}} in {{site.data.keyword.Bluemix_notm}} dedicato e Bluemix locale](/docs/containers/container_dl.html). |
|Facoltativo | [{{site.data.keyword.datacshort}}](/docs/services/DataCache/index.html#data_cache) | Questo servizio fornisce una griglia di dati in memoria
che supporta scenari di cache distribuita per le tue applicazioni. Include 50 GB di cache in memoria. |
| Facoltativo (beta) | [Registrazione](/docs/monitoringandlogging/cfapps_ml_logs_dedicated_ov.html#container_ml_logs_dedicated_ov) | Fornisce log per le tue applicazioni Cloud Foundry nella tua interfaccia utente {{site.data.keyword.Bluemix_notm}} e nei tuoi dashboard e log con funzione di ricerca in Kibana. |
|Facoltativo | [{{site.data.keyword.mobilepush}}](/docs/services/mobilepush/index.html) | {{site.data.keyword.mobilepush}} è un servizio che puoi utilizzare per inviare notifiche a dispositivi iOS e Android. Le notifiche possono essere destinate a tutti gli utenti dell'applicazione oppure a uno specifico insieme di utenti e dispositivi facendo uso delle tag. Puoi amministrare i dispositivi, le tag e le sottoscrizioni. Puoi anche utilizzare API (application program interface) REST (Representational State Transfer) e SDK (software development kit) per sviluppare ulteriormente le tue applicazioni client. |
|Facoltativo | [{{site.data.keyword.sescashort}}](/docs/services/SessionCache/index.html#session_cache) | Per aumentare la ridondanza, {{site.data.keyword.sescashort}} fornisce una replica di una sessione memorizzata nella cache. Pertanto, nel caso di un'interruzione o di un calo di tensione, la tua applicazione client mantiene l'accesso alla sessione nella cache. Il servizio supporta scenari di memorizzazione di sessioni nella cache per applicazioni Web e mobili. |
|Facoltativo | [{{site.data.keyword.iot_short}}](/docs/services/IoT/index.html) | Questo servizio consente alle tue applicazioni di comunicare tra loro e utilizzare i dati raccolti dai tuoi dispositivi, sensori e gateway connessi. L'offerta di base locale consente l'esecuzione di una versione privata di IBM {{site.data.keyword.iot_short}} nell'ambiente locale con una capacità di 100,000 applicazioni o dispositivi connessi contemporaneamente e 1.6 TB di scambio dati. |
{: caption="Table 1. Local services and runtimes" caption-side="top"}
{: #table01}


Sono presenti dei componenti facoltativi disponibili per te da acquistare per ridimensionare e estendere la capacità dei tuoi servizi o risorse. Puoi acquistare tutti questi componenti contattando il team di vendite; vai all'indirizzo [Contattaci](https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs) per informazioni su come contattare un rappresentante delle vendite. Per incrementare il tuo piano per un servizio, puoi selezionare il piano dal tile del servizio nel tuo catalogo.

| **Nome** | **Descrizione** |
|----------|-----------------|
|5 milioni di chiamate API {{site.data.keyword.apiconnect_short}} Professional per {{site.data.keyword.Bluemix_notm}} locale | Un ambiente che consente l'esecuzione di una versione privata di {{site.data.keyword.apiconnect_short}} con una capacità di 5 milioni di chiamate API al mese, destinate a progetti API del reparto. |
|Incremento di 100.000 chiamate API dedicate {{site.data.keyword.apiconnect_short}} Professional per {{site.data.keyword.Bluemix_notm}} locale| Un'estensione dell'ambiente {{site.data.keyword.apiconnect_short}} Professional che fornisce una capacità supplementare di 100.000 chiamate API al mese. |
|25 milioni di chiamate API dedicate {{site.data.keyword.apiconnect_short}} Enterprise per {{site.data.keyword.Bluemix_notm}} locale | Un ambiente che consente l'esecuzione di una versione privata di {{site.data.keyword.apiconnect_short}} con una capacità di 25 milioni di chiamate API al mese, destinate a progetti API di tutta l'azienda. |
|Incremento di 100.000 chiamate API dedicate {{site.data.keyword.apiconnect_short}} Enterprise per {{site.data.keyword.Bluemix_notm}} locale | Un'estensione dell'ambiente {{site.data.keyword.apiconnect_short}} Enterprise che fornisce una capacità supplementare di 100.000 chiamate API al mese. |
|{{site.data.keyword.Bluemix_notm}} Local {{site.data.keyword.cloudant}} Cluster | Un ambiente che consente la distribuzione di un cluster di 3 nodi del servizio {{site.data.keyword.cloudant}}. La capacità dei dati dei nodi è determinata dall'infrastruttura che ti è stata fornita per l'ambiente locale. |
|Incremento della capacità di 50 GB di {{site.data.keyword.Bluemix_notm}} Data & Session Cache | Un ambiente che consente la distribuzione e l'esecuzione di istanze Data Cache e Session Cache fino alla capacità cumulativa di 50 GB. |
|Aumento incrementale locale per {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.iot_short}} | Un ambiente aggiuntivo all'offerta del servizio di base locale {{site.data.keyword.iot_short}} che consente l'esecuzione di una versione privata di {{site.data.keyword.iot_short}} nell'ambiente locale con una capacità di 100,000 applicazioni o dispositivi connessi contemporaneamente e 0.5 TB di scambio dati. |
|Istanza del componente aggiuntivo {{site.data.keyword.IBM_notm}} {{site.data.keyword.mobilepush}} Local | Un ambiente che consente la distribuzione e l'esecuzione dell'istanza {{site.data.keyword.mobilepush}} con la capacità di accettare 300 richieste aggiuntive al secondo. |
{: caption="Table 2. Optional services components for purchase" caption-side="top"}
{: #table02}

| **Nome** | **Descrizione** |
|----------|-----------------|
|Capacità di 64 GB per i runtime Cloud Foundry locali  | Ambiente dei runtime Cloud Foundry con capacità di runtime di 64 GB. |
|Incremento della capacità di 16 GB per i runtime Cloud Foundry locali  | Un'estensione dell'ambiente dei runtime Cloud Foundry che fornisce una capacità di runtime extra di 16 GB. |
|Incremento della capacità di 16 GB per {{site.data.keyword.containerlong}} locale  | Un'estensione dell'ambiente {{site.data.keyword.containerlong}} che fornisce una capacità extra di 16 GB. |
|Capacità di 64 GB per {{site.data.keyword.containerlong}} locale  | Ambiente {{site.data.keyword.containerlong}} con 64 GB di capacità. |
{: caption="Table 3. Optional platform add-on components for purchase" caption-side="top"}
{: #table03}

**Nota**: i componenti locali {{site.data.keyword.Bluemix_notm}} possono indicare una capacità configurata specifica, come ad esempio gigabyte o transazioni al secondo. Poiché la capacità attuale messa in pratica per ogni configurazione del servizio cloud varia in base a molti fattori, la capacità attuale messa in pratica può essere maggiore o inferiore alla capacità configurata.

### Catalogo diffuso
{: #cataloglocal}

{{site.data.keyword.Bluemix_local_notm}} include un catalogo privato che riunisce i servizi approvati tra le tue distribuzioni pubbliche e locali. Puoi anche pubblicare e gestire l'accesso ai tuoi servizi tramite il catalogo {{site.data.keyword.Bluemix_notm}}. Hai la possibilità di decidere quali servizi pubblici rispondono ai tuoi requisiti aziendali, sulla base di criteri di sicurezza e privacy dei dati.

Se disponi di un'istanza privata di un servizio {{site.data.keyword.Bluemix_notm}} per il tuo ambiente locale, vedi una tag "Locale" con i nomi del servizio nella vista di amministrazione del catalogo. Allo stesso modo, se si tratta di un servizio personalizzato, il che significa che hai utilizzato un broker dei servizi per crearlo, vedi "Personalizzato" elencato insieme al nome del servizio. Tutti gli altri servizi elencati che non presentano una tag "locale" o "personalizzato" sono disponibili tramite la diffusione da {{site.data.keyword.Bluemix_notm}} pubblico. I servizi diffusi forniscono la funzione per creare applicazioni ibride composte da servizi pubblici e privati.

|Servizio	|Disponibile nella regione Stati Uniti Sud	|Disponibile nella regione Europa Regno Unito |Disponibile nella regione di Sydney in Australia|
|:----------|:------------------------------|:------------------|:------------------|
|{{site.data.keyword.alchemyapishort}} 		|Sì	   	|Sì  		|Sì|
|{{site.data.keyword.alertnotificationshort}}	|Sì		|Sì		|Sì	|
|{{site.data.keyword.apiconnect_short}}         |Sì            |Sì            |Sì  |
|{{site.data.keyword.appseccloudshort}}		|Sì		|Sì		|Sì |
|{{site.data.keyword.apiconnect_short}} 	|Sì   	 	|Sì  	 	|Sì   |
|Automated Accessibility Checker |Sì       |Sì    |Sì   |
|{{site.data.keyword.rules_short}}		|Sì		|Sì		|Sì |
|{{site.data.keyword.cloudant}}			|Sì		|Sì		|Sì |
|{{site.data.keyword.iotmapinsights_short}}    |Sì  |Sì  |Sì  |
|{{site.data.keyword.conversationshort}}  |Sì  |Sì  |Sì  |
|{{site.data.keyword.dashdbshort}}		|Sì		|Sì		|Sì |
|{{site.data.keyword.dataworks_short}}		|Sì		|Sì		|No|
|{{site.data.keyword.DB2OnCloud_short}}		|Sì		|Sì		|Sì |
|Digital Content Checker |Sì  |Sì  |Sì  |
|{{site.data.keyword.documentconversionshort}}	|Sì		|Sì		|Sì|
|{{site.data.keyword.iotdriverinsights_short}}  |Sì |Sì  |Sì  |
|{{site.data.keyword.geospatialshort_Geospatial}}	|Sì	|Sì		|Sì |
|{{site.data.keyword.GlobalizationPipeline_short}}	|Sì		| Sì		| Sì |
|{{site.data.keyword.identitymixershort}}		|Sì		|Sì		|Sì|
|{{site.data.keyword.iot4auto_short}} |Sì   |Sì  |Sì  |
|{{site.data.keyword.iotelectronics}}  |Sì  |Sì  |No |
|{{site.data.keyword.iotinsurance_short}} |No   |No   |Sì  |
|{{site.data.keyword.twittershort}}		|Sì		|Sì		|Sì|
|{{site.data.keyword.languagetranslationshort}}	|Sì		|Sì		|Sì |
|{{site.data.keyword.languagetranslatorshort}} |Sì  |Sì  |Sì  |
|{{site.data.keyword.dwl_short}}  |Sì  |Sì  |No  |
|{{site.data.keyword.eventhubshort}}		|Sì		|No		|No|
|{{site.data.keyword.messagehub}}		|Sì		|Sì		|No|
|{{site.data.keyword.manda}}			|Sì		|Sì		|Sì |
|{{site.data.keyword.amashort}}			|Sì		|Sì		|Sì |
|{{site.data.keyword.mqa}}			|Sì		|Sì		|Sì |
|{{site.data.keyword.mql}}			|No		|No		|Sì |
|{{site.data.keyword.nlclassifierlshort}} 	|Sì 		|Sì 		|Sì|
|{{site.data.keyword.personalityinsightsshort}}	|Sì		|Sì		|Sì|
|{{site.data.keyword.pm_short}}			|Sì		|Sì		|No |
|{{site.data.keyword.mobilepush}}		|Sì		|Sì		|Sì |
|{{site.data.keyword.retrieveandrankshort}}	|Sì 		|Sì 		|Sì|
|{{site.data.keyword.runbook_short}}		|Sì		|Sì		|Sì|
|{{site.data.keyword.SecureGateway}}		|Sì		|Sì		|Sì |
|{{site.data.keyword.ssofull}}			|Sì		|No		|No|
|{{site.data.keyword.speechtotextshort}}	|Sì 		|Sì	 	|Sì|
|{{site.data.keyword.streaminganalyticsshort}}	|Sì		|Sì		|Sì |
|{{site.data.keyword.texttospeechshort}} 	|Sì 		|Sì	 	|Sì|
|{{site.data.keyword.toneanalyzershort}} 	|Sì 		|Sì 		|Sì|
|{{site.data.keyword.tradeoffanalyticsshort}}	|Sì		|Sì		|Sì|
|{{site.data.keyword.visualrecognitionshort}}	|Sì 		|Sì	 	|Sì|
|{{site.data.keyword.iot_short}}		|Sì		|Sì		|No|
|{{site.data.keyword.weather_short}}		|Sì		|Sì		|Sì|
|{{site.data.keyword.workloadscheduler}}	|Sì		|Sì		|Sì |
{: caption="Table 4. Services available for syndication from {{site.data.keyword.Bluemix_notm}} Public by region" caption-side="top"}
{: #table04}

**Nota**: i servizi di terze parti non sono inclusi nella tabella. Controlla il tuo catalogo per le opzioni dei servizi di terze parti.


## Architettura di {{site.data.keyword.Bluemix_local_notm}}
{: #localarch}

{{site.data.keyword.Bluemix_local_notm}} si trova su una struttura virtuale protetta dal tuo firewall aziendale, mettendo così a tua disposizione l'infrastruttura cloud con le prestazioni più elevate e la massima protezione possibili. {{site.data.keyword.IBM_notm}} installa, esegue il monitoraggio in remoto e gestisce {{site.data.keyword.Bluemix_local_notm}} nel tuo data center attraverso la tecnologia [Relay](#localrelay) di {{site.data.keyword.IBM_notm}}. L'architettura logica in [Figure 1](#figure01) descrive come {{site.data.keyword.Bluemix_notm}} nel tuo ambiente locale e sulle modalità di gestione della tua istanza locale da parte di {{site.data.keyword.IBM_notm}}:

![Architettura {{site.data.keyword.Bluemix_local_notm}}.](images/bmlocal_arch.png "Diagramma dell'architettura di Bluemix locale") 

Figura 1. Architettura {{site.data.keyword.Bluemix_local_notm}}
{: #figure01}

La macchina virtuale di inizio (VM di inizio) viene seguita nella tua infrastruttura virtuale aziendale dietro il tuo firewall aziendale. La VM di inizio crea una connessione di rete in uscita al centro operativo {{site.data.keyword.IBM_notm}} tramite la tecnologia relay di {{site.data.keyword.IBM_notm}}. Il relay esegue molte funzioni ed è descritto nella seguente sezione [Relay](#localrelay).

I componenti della piattaforma {{site.data.keyword.Bluemix_notm}} e le funzionalità principali che supportano i componenti della piattaforma vengono eseguiti in una VLAN (virtual local area network) privata e isolata. {{site.data.keyword.Bluemix_local_notm}} utilizza una VLAN per la sottorete privata. L'utilizzo di una sottorete privata anziché di una VLAN pubblica è più sicuro e può contribuire a evitare problemi di instradamento. L'insieme delle funzioni principali che compongono e supportano la piattaforma include quanto segue:

<dl>
<dt>Piattaforma</dt>
<dd>Come minimo, la piattaforma è formata da componenti di Cloud Foundry e da alcuni servizi dell'applicazione locali. {{site.data.keyword.Bluemix_notm}} fornisce gli ambienti di calcolo Cloud Foundry e basati su {{site.data.keyword.containerlong}}. Un'azienda può disporre di uno o di entrambi questi ambienti di calcolo configurati.<br>
Un'azienda può inoltre aggiungere servizi dell'applicazione locali addizionali.<br>
<p>Fai riferimento a [Componenti facoltativi per l'acquisto: componenti aggiuntivi dei servizi](#table02) e [Componenti facoltativi per l'acquisto: componenti aggiuntivi della piattaforma](#table03) per i servizi aggiuntivi e le funzionalità di calcolo che possono essere aggiunte.</p>
</dd>
<dt>{{site.data.keyword.Bluemix_notm}} pubblico</dt>
<dd>
Un ambiente {{site.data.keyword.Bluemix_local_notm}} può disporre di una connessione in uscita a una regione {{site.data.keyword.Bluemix_notm}} pubblico. Una connessione al pubblico abilita la diffusione dei servizi pubblici nel catalogo locale. La diffusione del servizio {{site.data.keyword.Bluemix_notm}} pubblico fornisce una metodo conveniente per gli sviluppatori di creare le applicazioni ospitate nell'ambiente {{site.data.keyword.Bluemix_local_notm}} dell'azienda così come l'accesso ai servizi in esecuzione in {{site.data.keyword.Bluemix_notm}} pubblico. Consulta l'elenco di servizi {{site.data.keyword.IBM_notm}} che possono essere diffusi da {{site.data.keyword.Bluemix_notm}} pubblico nella sezione [Catalogo diffuso](#cataloglocal).
</dd>
<dt>Operazioni {{site.data.keyword.IBM_notm}}</dt>
<dd>
{{site.data.keyword.IBM_notm}} gestisce, monitora e mantiene i servizi e la piattaforma locali, in modo che puoi concentrati sulla creazione di applicazioni innovative. Il team OSS (Operations Support Services) di {{site.data.keyword.IBM_notm}} esegue le operazioni utilizzando una connessione tunnel VPN dalla VM di inizio alla rete delle operazioni di {{site.data.keyword.IBM_notm}}.
</dd>
<dt>Azienda</dt>
<dd>
L'ambiente della rete aziendale dispone di un link di rete bidirezionale a {{site.data.keyword.Bluemix_local_notm}}. Questo consente alle applicazioni ospitate in {{site.data.keyword.Bluemix_local_notm}} di accedere ai servizi e alle risorse nell'azienda, inclusi i servizi aziendali e le origini dati. Il link di rete consente a {{site.data.keyword.Bluemix_local_notm}} di utilizzare la tua LDAP per l'autenticazione dei tuoi amministratori e sviluppatori.
</dd>
<dt>Servizi locali</dt>
<dd>È disponibile una serie di servizi utilizzabili privatamente nel tuo ambiente {{site.data.keyword.Bluemix_local_notm}}. Generalmente, decidi quale servizio desideri per il tuo ambiente prima della distribuzione dal team {{site.data.keyword.IBM_notm}}. Per un elenco di servizi disponibili, vai a [Servizi locali e runtime](#table01).
</dd>
<dt>Gateway DataPower</dt>
<dd>
Le applicazioni gateway DataPower di {{site.data.keyword.IBM_notm}} forniscono accesso ai domini dell'applicazione {{site.data.keyword.Bluemix_notm}}. Queste applicazioni ti collegano alla tua rete intranet e alla rete privata {{site.data.keyword.Bluemix_notm}}, fornendo un gateway sicuro per la distribuzione {{site.data.keyword.Bluemix_notm}}. I tuoi sviluppatori che distribuiscono applicazioni e servizi, ottengono l'accesso dalla tua intranet tramite questo gateway. Gli utenti delle applicazioni otterranno l'accesso tramite le applicazioni DataPower così come i tuoi amministratori.
</dd>
<dt>Intelligence di sicurezza</dt>
<dd><p>{{site.data.keyword.IBM_notm}} utilizza QRadar Security Intelligence Platform per fornire un'architettura unificata per l'integrazione di diversi componenti chiave. Tali componenti includono informazioni sulla sicurezza e gestione eventi, gestione di log, rilevamento anomalie, indagini forensi sugli incidenti e gestione delle vulnerabilità e della configurazione. {{site.data.keyword.Bluemix_notm}} utilizza inoltre {{site.data.keyword.IBM_notm}} QRadar SIEM (security information and event management) per monitorare le azioni utente privilegiate e i tentativi di accesso riusciti e non riusciti degli sviluppatori di applicazioni. I report QRadar forniscono al cliente la visibilità su queste azioni o utilizzando la sezione Report e log della pagina Amministrazione. Per informazioni sui report di sicurezza, consultare [Visualizzazione dei report](/docs/admin/index.html#oc_report).</p>
<p>{{site.data.keyword.IBM_notm}} BigFix garantisce che le correzioni per i sistemi operativi vengano applicate con frequenza adeguata. Il processo di applicazione di patch è automatizzato e la pianificazione viene concordata tra te e IBM. Per informazioni su manutenzione e aggiornamenti, vedi [Gestione della tua istanza locale](index.html#maintainlocal).</p>
</dd>
</dl>

Le tue applicazioni vengono distribuite all'interno di contenitori virtuali eseguiti su macchine virtuali Cloud Foundry. Tutti i componenti Cloud Foundry, quali i controller cloud, i gestori di integrità, i router e i DEA (Droplet Execution Agent), vengono distribuiti durante la configurazione di {{site.data.keyword.Bluemix_notm}}. La distribuzione {{site.data.keyword.Bluemix_notm}} include inoltre i vari componenti gestionali {{site.data.keyword.Bluemix_notm}}.

Per informazioni sulle specifiche di rete e i requisiti dell'infrastruttura, vai a [Requisiti dell'infrastruttura {{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#localinfra).

### Relay
{: #localrelay}

Relay è il collegamento sicuro tra la tua rete aziendale e le operazioni cloud di {{site.data.keyword.IBM_notm}}. Il traffico sulla connessione relay è l'attività automatica utilizzata per servire e gestire la piattaforma {{site.data.keyword.Bluemix_local_notm}} le risorse di calcolo e i servizi per le tue istanze. Il traffico sulla connessione relay può essere categorizzato nel seguente modo:

* monitoraggio degli eventi
* intelligence di sicurezza
* distribuzioni e aggiornamenti
* determinazione del problema e correzioni
* manutenzione di emergenza

<dl>
<dt>
Monitoraggio e eventi
</dt>
<dd>
Le funzioni di monitoraggio e evento vengono distribuite nel tuo data center. I dati dell'applicazione rimangono nel tuo data center.<br>
Il traffico sulla connessione relay include la funzionalità di monitoraggio utilizzata dalle operazioni {{site.data.keyword.IBM_notm}} per eseguire il monitoraggio dell'integrità e per completare la determinazione del problema quando necessario.<br>
<p>Nessun dato sensibile viene incluso nelle informazioni di monitoraggio, il che significa niente password, nessun dato o log dell'applicazione e nessuna chiave. Il traffico sul relay include i flussi dalla VM di inizio al centro operativo {{site.data.keyword.Bluemix_notm}}.</p>
</dd>
<dt>
Intelligence di sicurezza
</dt>
<dd>
{{site.data.keyword.IBM_notm}} utilizza QRadar Security Intelligence Platform per fornire un'architettura unificata per l'integrazione di diversi componenti chiave. Tali componenti includono informazioni sulla sicurezza e gestione eventi, gestione di log, rilevamento anomalie, indagini forensi sugli incidenti e gestione delle vulnerabilità e della configurazione.<br>
<p>{{site.data.keyword.Bluemix_notm}} utilizza inoltre {{site.data.keyword.IBM_notm}} QRadar SIEM (security information and event management) per monitorare le azioni utente privilegiate e i tentativi di accesso riusciti e non riusciti.</p>
<p>I report QRadar forniscono all'amministratore {{site.data.keyword.Bluemix_notm}} la visibilità sugli eventi e i dati evento utilizzando la sezione Report e log della pagina Amministrazione. I report QRadar vengono generati su base regolare, giornaliera e mensile a seconda del tipo di report. Tutti i report vengono conservati per 90 giorni nella console di gestione. Al termine dei 90 giorni, i report sono disponibili offline su richiesta a {{site.data.keyword.IBM_notm}} per 9 mesi. In totale, i report sono disponibili per il recupero per un massimo di 1 anno.</p>
<p>Non viene incluso alcun dato dell'applicazione nel traffico utilizzato da QRadar. Gli unici dati che possono potenzialmente essere considerati come sensibili sono gli ID utente per i report dei tentativi di accesso e gli indirizzi IP di alcuni componenti {{site.data.keyword.Bluemix_notm}}.
Il traffico sul relay include i flussi tra il processore evento QRadar in {{site.data.keyword.Bluemix_local_notm}} e una console QRadar nel centro operativo {{site.data.keyword.IBM_notm}}.</p>
</dd>
<dt>
Distribuzione e aggiornamenti di manutenzione
</dt>
<dd>
Tranne che per l'installazione iniziale della VM di inizio installata nelle prime fasi del processo di distribuzione, la distribuzione della maggior parte degli altri componenti viene automatizzata utilizzando UrbanCode Deploy.<br>
<p>Per l'attività di distribuzione, UrbanCode Deploy si basa su [BOSH ![icona link esterno](../icons/launch-glyph.svg)](https://bosh.cloudfoundry.org/){:new_window}, con i componenti BOSH tra i primi ad essere distribuiti dalla VM di inizio. La funzionalità di fornitura continua di UrbanCode Deploy viene utilizzata per fornire gli aggiornamenti di piattaforma attraverso un coerente processo di test e convalida.</p>
<p>Gli script e i pacchetti vengono trasferiti dal centro operativo {{site.data.keyword.IBM_notm}} alla tua piattaforma {{site.data.keyword.Bluemix_notm}} locale tramite il relay.</p>
</dd>
<dt>
Correzioni
</dt>
<dd>
{{site.data.keyword.IBM_notm}} BigFix garantisce che gli aggiornamenti di sicurezza per i sistemi operativi vengano applicati con frequenza adeguata. Il processo di applicazione di patch è automatizzato e la pianificazione viene concordata tra te e IBM.
</dd>
<dt>
Determinazione del problema e manutenzione di emergenza
</dt>
<dd>
{{site.data.keyword.IBM_notm}} fornisce un elenco degli utenti e degli ID autorizzati dalle operazioni {{site.data.keyword.IBM_notm}} che possono accedere al tuo ambiente. Puoi controllare ogni accesso al tuo ambiente tramite la pagina Amministrazione del tuo ambiente {{site.data.keyword.Bluemix_local_notm}}.<br>
<p>Gli utenti delle operazioni {{site.data.keyword.IBM_notm}} avranno accesso soltanto all'ambiente {{site.data.keyword.Bluemix_local_notm}} per informazioni più approfondite sulla stato della piattaforma. Il team delle operazioni non concede mai l'accesso ai tuoi dati o codice dell'applicazione, ed esegue solo i comandi necessari per la determinazione del problema per controllare le configurazioni o i parametri nei casi di emergenza per eseguire le operazioni che non sono automatizzate. Nessuno di questi comandi trasferisce alcun dato sensibile sul relay.</p>
<p>L'accesso al tuo ambiente locale è protetto tramite autenticazione a due fattori durante varie fasi del processo di connessione. Attraverso la creazione di un report di sicurezza, puoi scoprire chi ha effettuato l'accesso al tuo ambiente inclusi quando e perché.</p>
<p>Il traffico sul relay per la determinazione del problema e la manutenzione di emergenza è traffico SSH, così come il traffico LDAP e Kerberos che viene utilizzato per l'autenticazione degli utenti {{site.data.keyword.IBM_notm}}.<br>
In qualità di amministratore, puoi visualizzare l'intero ambiente ai fini della gestione di incidenti, problemi, modifiche, funzionalità e sicurezza. Puoi accedere alle informazioni sul tuo ambiente, attraverso la pagina Amministrazione. La tecnologia Relay mantiene questa pagina aggiornata con i dati evento della piattaforma più recenti da QRadar. </p>
</dd>
</dl>

### Ispezione SSL
{: #sslinspection}

Le applicazioni Cloud Foundry e {{site.data.keyword.Bluemix_notm}} possono utilizzare i certificati di ispezione SSL quando accedono a risorse all'esterno dell'ambiente locale. L'ispezione del contenuto SSL è disponibile per il tuo ambiente, se fornisci un certificato root che viene utilizzato per accedere ai flussi SSL ispezionati. 

Il team di distribuzione {{site.data.keyword.Bluemix_notm}} carica il certificato root per abilitare l'ispezione SSL nell'ambiente durante il processo di distribuzione del tuo ambiente locale. L'abilitazione dell'ispezione SSL durante il processo di configurazione dell'ambiente non aumenta il tempo di distribuzione. Se questa funzionalità non viene abilitata durante la distribuzione iniziale, puoi richiedere che venga abilitata; tuttavia, potrebbero essere associati ulteriori costi e potrebbero volerci da due a quattro giorni per il completamento a seconda delle tue finestre di manutenzione disponibili.


## Configurazione della tua istanza {{site.data.keyword.Bluemix_local_notm}}
{: #setuplocal}

{{site.data.keyword.Bluemix_local_notm}} è progettato per fornire una versione privata dell'offerta {{site.data.keyword.Bluemix_notm}} pubblico che è ospitata nell'hardware di tua scelta. Le due opzioni più comuni sono di fornire l'hardware nel formato VMware oppure puoi scegliere di ordinare il sistema {{site.data.keyword.Bluemix_notm}} locale, che è integrato nell'applicazione PureApplication preconfigurata che puoi ordinare tramite {{site.data.keyword.IBM_notm}}. Per ulteriori informazioni sulle opzioni dell'applicazione PureApplication, vedi [IBM {{site.data.keyword.Bluemix_notm}} Local System W3500 and W3550 models run cloud native services, enabled middleware, and open pattern workloads concurrently ![icona link esterno](../icons/launch-glyph.svg)](https://www-01.ibm.com/common/ssi/rep_ca/5/897/ENUS216-325/){: new_window}.

Per {{site.data.keyword.Bluemix_local_notm}}, puoi utilizzare i servizi e i runtime {{site.data.keyword.Bluemix_notm}} per supportare le tue esigenze di elaborazione in un ambiente cloud protetto, ospitato e gestito dal cliente. {{site.data.keyword.IBM_notm}} ti fornisce l'accesso a {{site.data.keyword.Bluemix_local_notm}} utilizzando un accesso protetto da password. Puoi accedere a servizi, runtime
e risorse associate nonché distribuire e rimuovere applicazioni {{site.data.keyword.Bluemix_notm}}. Riesamina i seguenti passi per lavorare con il tuo rappresentante {{site.data.keyword.IBM_notm}} per configurare la tua istanza locale di {{site.data.keyword.Bluemix_notm}}.

**Nota**: se scegli di ospitare {{site.data.keyword.Bluemix_local_notm}} sull'opzione hardware di sistema {{site.data.keyword.Bluemix_notm}} locale, il processo di configurazione potrebbe essere diverso, non hai bisogno di fornire così tante informazioni al rappresentante IBM. Inoltre, i tuoi ruoli e responsabilità attraverso le fasi di inizio, avanzamento e completamento potrebbero essere ridotti per via del modello di manutenzione dell'applicazione PureApplication invece che mediante il modello di gestione necessario per l'utilizzo della VMware di proprietà del cliente.

Per configurare la tua versione privata di {{site.data.keyword.Bluemix_notm}}:

<ol>
<li>Riesamina i <a href="index.html#localinfra" title="Si apre in nuova pagina">Requisiti dell'infrastruttura {{site.data.keyword.Bluemix_local_notm}}</a> per configurare la tua istanza locale.</li>
<li>Per iniziare, contatta il tuo rappresentante dell'account designato {{site.data.keyword.IBM_notm}} oppure
<a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">contatta
{{site.data.keyword.Bluemix_notm}} <img src="../icons/launch-glyph.svg" alt="icona link esterno">
</a>.</li>
<li>Stabilisci un accordo per {{site.data.keyword.Bluemix_local_notm}} con {{site.data.keyword.IBM_notm}} che includa le date cardine per la distribuzione.
	<ol type="a">
	<li>Determina insieme a IBM le quote mensili ricorrenti e la configurazione monouso per la tua istanza {{site.data.keyword.Bluemix_notm}} locale. La quota mensile ricorrente si basa sui servizi locali
che desideri utilizzare, oltre a una sottoscrizione a tutti i servizi pubblici {{site.data.keyword.Bluemix_notm}}. Riceverai quindi una fattura per tutto ciò che scegli di utilizzare
al di fuori di tale accordo di sottoscrizione.</li>
	<li>Identifica le scadenze per ogni fase di configurazione della tua istanza di {{site.data.keyword.Bluemix_local_notm}}.</li>
	</ol>
	</li>
<li>Dopo la creazione della tua piattaforma e del tuo account, identifichi le persone all'interno della tua organizzazione per i ruoli necessari per rendere operativa la tua istanza locale. Per ulteriori informazioni sui ruoli che puoi assegnare, vedi <a href="/docs/local/index.html#rolesresponsibilities">Ruoli e responsabilità {{site.data.keyword.Bluemix_notm}} locale</a>.
</li>
<li>Tu fornisci l'hardware e {{site.data.keyword.IBM_notm}} ti aiuta a definire e stabilire la connettività di rete tra la tua rete aziendale e la tua istanza di {{site.data.keyword.Bluemix_local_notm}}. Per ulteriori informazioni sui requisiti dell'infrastruttura, vedi <a href="index.html#localinfra">Requisiti dell'infrastruttura {{site.data.keyword.Bluemix_local_notm}}</a>.
	<ol type="a">
	<li>{{site.data.keyword.IBM_notm}} configura l'accesso alla rete e il LDAP in base alle informazioni che hai fornito. L'accesso amministrativo
viene fornito ai contatti da te designati. Devi designare un
contatto anche per il supporto e la fatturazione.</li>
	<li>{{site.data.keyword.IBM_notm}} configura un catalogo diffuso su diversi canali nell'ambiente locale per visualizzare i tuoi servizi locali e molti dei servizi {{site.data.keyword.Bluemix_notm}} pubblici.</li>
	<li>Convalidi la configurazione di rete e del firewall e l'accesso e l'endpoint LDAP.</li>
	</ol>
</li>
</ol>

Per la distribuzione e configurazione iniziale del tuo ambiente puoi prevedere un processo simile a quello elencato di seguito. Per i dettagli sui responsabili di ciascuna attività, vedi [Ruoli e responsabilità](/docs/local/index.html#rolesresponsibilities).

**Nota**: se scegli di ospitare la tua istanza locale nell'opzione hardware di sistema {{site.data.keyword.Bluemix_notm}} locale, puoi saltare le fasi da 1 a 3 del seguente elenco.

<ol>
<li>Fornisci la configurazione VMware conforme alle specifiche per le risorse di calcolo, la rete e l'archiviazione. Per ulteriori informazioni sui requisiti dell'infrastruttura, vedi <a href="/docs/local/index.html#localinfra">{{site.data.keyword.Bluemix_notm}} Local infrastructure requirements</a>.</li>
<li>Fornisci le credenziali del cluster vCenter che verranno utilizzate dalla macchina virtuale di inizio. Devi fornire le seguenti informazioni:
<ul>
<li>Nome del cluster VMware</li>
<li>Credenziali del cluster vCenter che includono ID utente e password</li>
<li>Nome o nomi dell'archivio dati (nome LUN archiviazione)</li>
<li>ID VLAN/Gruppo di porte VMware</li>
<li>Nome del pool di risorse</li>
</ul>
</li>
<li>Lavora insieme a {{site.data.keyword.IBM_notm}} per convalidare le credenziali fornite nell'attività precedente.</li>
<li>Fornisci 7 indirizzi IP sulla tua rete. Se disponi di un proxy Web protetto per consentire l'accesso in uscita a Internet per i componenti {{site.data.keyword.Bluemix_notm}} interni, devi fornire le credenziali per poter stabilire la connessione.
<p>**Nota**: se il tuo proxy Web non è protetto, non sarà necessario fornire le credenziali. Inoltre, nota che tutti i clienti {{site.data.keyword.Bluemix_local_notm}} utilizzano un proxy Web.</p></li>
<li>{{site.data.keyword.IBM_notm}} fornisce un elenco di URL che è necessario consentire tramite il proxy Web prima di avviare la distribuzione.<br />
<p>**Nota**: per garantire che le tue applicazioni nuove o esistenti possano accedere alle risorse necessarie, potresti dover effettuare ulteriori passaggi per raggruppare le risorse con il pacchetto di build o lavorare con il team di sicurezza per aggiungere in un elenco gli URL necessari per eseguire le tue applicazioni. Per ulteriori informazioni sull'utilizzo dei pacchetti di build Node.js e Liberty for Java, vedi <a href="../runtimes/nodejs/offlineMode.html">Offline mode for node.js</a> e <a href="../runtimes/liberty/offlineMode.html">Offline mode for Liberty for Java</a>.</p>
</li>
<li>Specifica i nomi di dominio per la distribuzione e gli ID che desideri utilizzare. Quando configuri la tua istanza locale, ottieni due domini definiti in modo parziale e puoi scegliere il prefisso per i due domini. Ad esempio, puoi scegliere il prefisso per <code>*mycompany*.bluemix.net</code> e <code>*mycompany*.mybluemix.net</code>.<br />
<br />
Puoi anche definire un dominio personalizzato completo, come mycustombmx.mycompany.com e application.mycompany.com. È necessario fornire il certificato SSL, la chiave del certificato e il certificato root prima che l'ambiente venga distribuito. Il certificato root fornito può anche essere utilizzato per configurare l'<a href="index.html#sslinspection">Ispezione SSL</a> per il tuo ambiente su richiesta. <br />
<br />
Puoi scegliere il numero di domini personalizzati desiderato per le tue applicazioni, finché fornisci i certificati per i domini personalizzati. Per ulteriori informazioni sulla creazione del dominio personalizzato, consulta <a href="../manageapps/updapps.html#domain">Creazione e utilizzo di un dominio personalizzato</a>.</li>
<li>Scegli quale tecnologia utilizzare (il tunnel IPSec o OpenVPN) per configurare Relay per la riconnessione al centro operativo {{site.data.keyword.IBM_notm}}.</li>
<li>{{site.data.keyword.IBM_notm}} installa e avvia la macchina virtuale di inizio all'interno del cluster {{site.data.keyword.Bluemix_notm}}. Se fornisci il tuo proprio VMware, il rappresentante {{site.data.keyword.IBM_notm}} aiuterà il tuo rappresentante clienti a completare questa attività. Se hai ordinato l'opzione hardware del sistema {{site.data.keyword.Bluemix_notm}} locale, un rappresentante IBM completa questa attività.</li>
<li>{{site.data.keyword.IBM_notm}} configura Relay per comunicare con il centro operativo {{site.data.keyword.IBM_notm}}.</li>
<li>Il repository della macchina virtuale di inizio inserisce le risorse di build aggiornate.</li>
<li>Fornisci le credenziali in modo che {{site.data.keyword.IBM_notm}} possa connettersi all'istanza della directory LDAP aziendale.</li>
<li>{{site.data.keyword.IBM_notm}} utilizza l'automazione per distribuire la piattaforma {{site.data.keyword.Bluemix_notm}} di base.</li>
<li>{{site.data.keyword.IBM_notm}} distribuisce la piattaforma di base che include i runtime elastici, la console, la funzione di amministrazione e il monitoraggio.</li>
<li>{{site.data.keyword.IBM_notm}} collega il tuo catalogo diffuso dalla distribuzione locale a un'istanza di {{site.data.keyword.Bluemix_notm}} pubblico per l'utilizzo di servizi pubblici. Per impostazione predefinita, nella tua istanza locale è disponibile una serie di servizi pubblici. Puoi utilizzare la pagina Amministrazione della gestione del catalogo per attivare o disattivare i servizi per la tua istanza locale.</li>
<li>{{site.data.keyword.IBM_notm}} configura il tuo accesso amministrativo all'ambiente.</li>
<li>Puoi iniziare a utilizzare la tua istanza locale, monitorata dal team operativo {{site.data.keyword.IBM_notm}}, al fine di rispondere agli avvisi.</li>
</ol>

Una volta configurata la tua istanza {{site.data.keyword.Bluemix_notm}}, puoi monitorare e gestire l'istanza {{site.data.keyword.Bluemix_notm}} utilizzando la pagina Amministrazione. Per ulteriori informazioni, vedi [Managing {{site.data.keyword.Bluemix_local_notm}} e dedicato](../admin/index.html#mng). Per informazioni su aggiornamenti e manutenzione, vedi [Manutenzione dell'istanza locale](index.html#maintainlocal).

##Ruoli e responsabilità
{: #rolesresponsibilities}

Se hai configurato un account {{site.data.keyword.Bluemix_local_notm}}, devi identificare le persone all'interno della tua organizzazione a cui assegnare i ruoli necessari per rendere operativa la tua istanza.

###Ruoli

Il seguente elenco mostra i ruoli e le responsabilità dei clienti che puoi assegnare:

<dl>
<dt>**Procurement focal**</dt>
<dd>Lavora con il rappresentante {{site.data.keyword.IBM_notm}} per organizzare il tuo ambiente {{site.data.keyword.Bluemix_local_notm}}, occupandosi inoltre dell'identificazione delle persone adeguate a gestire ogni aspetto del progetto all'interno della tua organizzazione. La persona assegnata a questo ruolo controlla la selezione del modello, gli accordi commerciali e la disposizione dell'accesso alle risorse dei clienti. Il Procurement focal è il contatto generale per la configurazione dell'istanza locale.</dd>
<dt>**Responsabile della conformità**</dt>
<dd>Lavora con il rappresentante {{site.data.keyword.IBM_notm}} per selezionare un'opzione di topologia e distribuzione che risponda ai tuoi requisiti di sicurezza. La persona assegnata a questo ruolo collabora con i consulenti di conformità {{site.data.keyword.IBM_notm}} per determinare quali modelli di distribuzione raggiungono gli obiettivi di conformità.</dd>
<dt>**Network specialist**</dt>
<dd>Lavora con il rappresentante {{site.data.keyword.IBM_notm}} per identificare i piani di rete per la distribuzione di {{site.data.keyword.Bluemix_notm}}. La persona assegnata a questo ruolo riesamina le specifiche di rete richieste da {{site.data.keyword.IBM_notm}} e lavora con {{site.data.keyword.IBM_notm}} su un piano di implementazione. Al termine della fase di installazione e verifica, la persona assegnata a questo ruolo conferma che la configurazione di rete è in conformità con gli standard aziendali.</dd>
<dt>**DevOps focal**</dt>
<dd>Lavora con il rappresentante {{site.data.keyword.IBM_notm}} per pianificare e applicare gli aggiornamenti di manutenzione necessari per la piattaforma, i servizi e i runtime {{site.data.keyword.Bluemix_notm}}. La persona assegnata a questo ruolo lavora anche con il rappresentante {{site.data.keyword.IBM_notm}} sulla configurazione della tua istanza di {{site.data.keyword.Bluemix_local_notm}}.</dd>
<dt>**Specialista IaaS**</dt>
<dd>Lavora con i rappresentanti {{site.data.keyword.IBM_notm}} sul piano di distribuzione per VMware. In genere, si tratta di un amministratore VMware nel data center. La persona assegnata a questo ruolo riesamina i  <a href="../local/index.html#localinfra">requisiti dell'infrastruttura {{site.data.keyword.Bluemix_local_notm}}</a> e lavora con {{site.data.keyword.IBM_notm}} su un piano di implementazione. Al termine della distribuzione, la persona assegnata a questo ruolo conferma che la distribuzione è in conformità con gli standard aziendali a livello IaaS.</dd>
<dt>**Operations focal**</dt>
<dd>Lavora con il team di supporto {{site.data.keyword.IBM_notm}} come necessario quando l'ambiente è attivo e in esecuzione. In genere si tratta di qualcuno con l'accesso **Superuser** alla console di gestione che può approvare gli aggiornamenti di manutenzione pianificati per l'ambiente {{site.data.keyword.Bluemix_notm}} ed essere disponibile tutte le volte che si verifica un incidente critico. La persona assegnata a questo ruolo deve avere una conoscenza tecnica dell'ambiente {{site.data.keyword.Bluemix_notm}} ed essere nella posizione di raggiungere le altre persone nell'azienda con competenze avanzate in un'area che potrebbe essere influenzata inclusi ad esempio la rete e la sicurezza.
</dd>
</dl>

I tuoi rappresentanti dei clienti collaborano con gli specialisti {{site.data.keyword.IBM_notm}} che lavorano insieme per garantirti tutto il supporto di cui hai bisogno. Puoi eseguire l'upgrade al livello di supporto Premium per lavorare con un CSM (Client Success Manager) dedicato per il tuo account. Per ulteriori informazioni sui diversi livelli di supporto, vedi [Come contattare il supporto](../support/index.html#contacting-support). Il CSM completa i seguenti tipi di attività:

<ul>
<li>Fornisce coordinamento tecnico tra te e IBM.</li>
<li>Coordina gli aggiornamenti, l'aiuto di esperti di IBM e l'abilitazione iniziale da un supporto tecnico {{site.data.keyword.Bluemix_notm}}.</li>
<li>Fornisce informazioni sui tipi di supporto disponibili.</li>
<li>Funge, se necessario, da punto di escalation iniziale.</li>
</ul>

Il team operativo e di supporto {{site.data.keyword.Bluemix_notm}} che insieme a te gestisce l'istanza {{site.data.keyword.Bluemix_notm}} potrebbe accedere al tuo ambiente locale, ma lo fa solo per i seguenti motivi.

<ul>
<li>Per rispondere agli avvisi ed eseguire la manutenzione operativa</li>
<li>Per tentare di riprodurre un problema riportato su un ticket di supporto</li>
</ul>

###Responsabilità

Dalla configurazione del tuo ambiente alla manutenzione continua, tu e IBM dovrete completare una serie di attività. Le seguenti tabelle illustrano le attività richieste e i proprietari per lo svolgimento delle attività attraverso le fasi di inizio, avanzamento e completamento.

La fase di inizio è utilizzata per organizzare l'ambiente {{site.data.keyword.Bluemix_local_notm}}. In questa fase, hai già riesaminato i requisiti dell'infrastruttura [locale](../local/index.html#localinfra). Gli obiettivi principali di questa fase sono i seguenti:

- Esaminare l'accordo finanziario e stabilire le date cardine per la distribuzione.
- Creare la piattaforma {{site.data.keyword.Bluemix_notm}} e fornire accesso a runtime e servizi.
- Definire e stabilire la connettività di rete tra la tua rete aziendale e le operazioni {{site.data.keyword.Bluemix_notm}}.
- Identificare e assegnare i ruoli per il team amministrativo.

| **Attività** | **Dettagli attività** | **Parte responsabile** |
|----------|------------------|-----------------------|
|Impostare gli standard di conformità | Identificare gli standard governativi, di settore e aziendali richiesti per l'ambiente. | Cliente |
|Creare un piano di integrazione di sicurezza e conformità | Creare un piano di sicurezza e di integrazione che includa i costi, la pianificazione e le risorse necessarie per garantire la conformità di sicurezza. | {{site.data.keyword.IBM_notm}} |
|Approvazione del piano di conformità | Approvare il piano di conformità. | Cliente |
|Creare il dimensionamento per l'ambiente |  	Creare il dimensionamento dell'ambiente sulla base di scelte predefinite che tengono in considerazione gli obiettivi di alta disponibilità e ripristino di emergenza, così come il provisioning iniziale di DEA e servizi necessario per supportare le applicazioni create con la piattaforma. Lavora insieme a {{site.data.keyword.IBM_notm}} per definire, ad esempio, quali database sono necessari, quali servizi vengono offerti nel catalogo diffuso del cliente e altro ancora. | Responsabilità condivisa tra {{site.data.keyword.IBM_notm}} e il cliente |
|Selezionare l'architettura | Selezionare l'architettura sulla base di scelte predefinite che tengono in considerazione i requisiti di alta disponibilità e ripristino di emergenza. | {{site.data.keyword.IBM_notm}} |
|Definire gli obiettivi del ripristino di emergenza | Definire i requisiti di ripristino di emergenza per l'ambiente. | Cliente |
|Creare il piano di ripristino di emergenza | Consultare e definire il piano di ripristino di emergenza. {{site.data.keyword.IBM_notm}} crea un modello di ripristino di emergenza e con te stabilisce dove fornire il feedback e approvare il piano. | Responsabilità condivisa tra {{site.data.keyword.IBM_notm}} e il cliente |
|Creare il piano di backup e ripristino | Creare un piano di backup e ripristino che definisce la frequenza e i requisiti per la distribuzione interna ed esterna del backup. {{site.data.keyword.IBM_notm}} esegue il backup dei componenti della piattaforma, dei servizi {{site.data.keyword.IBM_notm}} e dei metadati dei servizi, inclusi i ruoli utente e altro ancora. Tu esegui il backup dei dati specifici dell'applicazione di cui sei responsabile. | Responsabilità condivisa tra {{site.data.keyword.IBM_notm}} e il cliente |
|Identificare gli strumenti per il rilevamento degli eventi e la determinazione dei problemi | Identificare gli strumenti {{site.data.keyword.IBM_notm}} e di terze parti utilizzati per il rilevamento degli eventi e la determinazione dei problemi a livello della piattaforma {{site.data.keyword.Bluemix_notm}}. | {{site.data.keyword.IBM_notm}} |
|Definire il piano di escalation | Definire il piano di escalation per valutare e risolvere gli eventi rilevati dai componenti di monitoraggio. | {{site.data.keyword.IBM_notm}} |
|Firmare gli accordi relativi a infrastruttura, piattaforma e supporto | Firmare l'accordo di sottoscrizione che include i termini e le condizioni finanziarie per l'ambiente. Firmare la sottoscrizione di supporto. | Cliente |
|Disporre l'ambiente | Disporre le risorse di calcolo, la rete e la memoria. Per ulteriori informazioni sui requisiti dell'infrastruttura per l'ambiente, vedi [Requisiti dell'infrastruttura locale](../local/index.html#localinfra). | Cliente |
|Installare la soluzione VPN | Installare la soluzione VPN bidirezionale. | {{site.data.keyword.IBM_notm}} |
|Installare i componenti della piattaforma, dell'applicazione e di monitoraggio e gestione | Installare, configurare e verificare i componenti della piattaforma, come ad esempio BOSH Director, Cloud Controller, Health Manager, messaggistica, router, DEA e provider di servizi e i componenti di monitoraggio definiti nel piano di escalation e rilevamento dei problemi. | {{site.data.keyword.IBM_notm}} |
|Installare e configurare i componenti di sicurezza | Installare e configurare i componenti di sicurezza vincolati nel piano di monitoraggio e di escalation, tra cui {{site.data.keyword.IBM_notm}} QRadar, archivio credenziali, sistema di prevenzione delle intrusioni, {{site.data.keyword.IBM_notm}} BigFix e {{site.data.keyword.IBM_notm}} Security Privileged Identity Management. | {{site.data.keyword.IBM_notm}} |
|Configurare il server di accesso | Configurare il server di accesso per l'utilizzo del LDAP aziendale. | {{site.data.keyword.IBM_notm}} |
|Installare e configurare i componenti personalizzati |  	Installare e configurare i componenti personalizzati che si trovano al di fuori del campo di applicazione del prodotto e dei servizi {{site.data.keyword.Bluemix_notm}}. | Cliente |
|Connettere la pipeline {{site.data.keyword.Bluemix_notm}} | Connettere la pipeline di fornitura e di integrazione continua {{site.data.keyword.Bluemix_notm}} ai repository {{site.data.keyword.IBM_notm}}. | {{site.data.keyword.IBM_notm}} |
|Personalizzare i componenti della soluzione esterni | Personalizzare i servizi di bilanciamento del carico per gli scenari di ripristino di emergenza. | Cliente |
|Tracciare lo stato per le verifiche di sicurezza, conformità e controllo  | Tracciare lo stato fino al punto in cui vengono osservati tutti gli strumenti e processi per raggiungere la conformità identificata. | Cliente |
|Controllare l'infrastruttura fisica | Controllare le sedi fisiche che ospitano i componenti della soluzione per individuare eventuali minacce e riesaminare i controlli di sicurezza per proteggere il data center. | Cliente |
|Ispezionare il software di monitoraggio | Ispezionare i componenti di monitoraggio e gestione, come definito nel piano di escalation e determinazione dei problemi. | Cliente |
|Ispezionare il sistema operativo | Verificare che l'immagine del sistema operativo rispetti gli standard di conformità. {{site.data.keyword.IBM_notm}} fornisce l'accesso all'immagine del sistema operativo. | Responsabilità condivisa tra {{site.data.keyword.IBM_notm}} e il cliente |
{: caption="Table 5. Inception phase tasks" caption-side="top"}

La fase successiva è quella di avanzamento. La fase di avanzamento descrive il rapporto di collaborazione in corso tra te e IBM. Gli obiettivi principali per questa fase sono i seguenti:

- Esaminare le capacità e coordinare le modifiche necessarie.
- Esaminare i miglioramenti di manutenzione e piattaforma.
- Coordinare le attività per la risoluzione dei problemi e l'analisi delle cause principali.

| **Attività** | **Dettagli attività** | **Parte responsabile** |
|----------|------------------|-----------------------|
|Esaminare i report sulle capacità settimanali | Esaminare i report sulle capacità settimanali e adottare misure correttive laddove necessario. | Cliente |
|Creare proiezioni mensili | Raccogliere informazioni e creare una proiezione mensile della capacità e del consumo. | Responsabilità condivisa tra {{site.data.keyword.IBM_notm}} e il cliente |
|Esaminare le proiezioni della capacità | Esaminare le proiezioni della capacità relative ad eventi esterni che potrebbero influire sulle capacità così come sulle nuove distribuzioni previste per le applicazioni. Lavorare con {{site.data.keyword.IBM_notm}} per esaminare le proiezioni e creare un piano adeguato. | Responsabilità condivisa tra {{site.data.keyword.IBM_notm}} e il cliente |
|Regolare la capacità |  Aggiungere o rimuovere capacità al mutare delle esigenze. | {{site.data.keyword.IBM_notm}} |
|Pubblicare gli aggiornamenti e la manutenzione previsti | Creare la documentazione per la manutenzione richiesta dei componenti {{site.data.keyword.IBM_notm}}. | {{site.data.keyword.IBM_notm}} |
|Effettuare la manutenzione | Lavorare con {{site.data.keyword.IBM_notm}} per pianificare la manutenzione richiesta all'interno di una finestra di 21 giorni. Puoi fornire le date che per te potrebbero non andare bene all'interno della finestra di 21 giorni; {{site.data.keyword.IBM_notm}} provvederà a pianificare la manutenzione di conseguenza. | Responsabilità condivisa tra {{site.data.keyword.IBM_notm}} e il cliente |
|Rilevamento di errori di provisioning | Correggere gli errori di provisioning, se presenti, per i servizi creati dal cliente che vengono distribuiti nel catalogo. | {{site.data.keyword.IBM_notm}} |
|Eseguire scansioni di rete e IP | Eseguire scansioni di rete e IP giornaliere e mensili. | Responsabilità condivisa tra {{site.data.keyword.IBM_notm}} e il cliente |
|Fornire accesso ai log di controllo | Fornire accesso a tutti i log di controllo amministrativo e della sicurezza.   | Responsabilità condivisa tra {{site.data.keyword.IBM_notm}} e il cliente |
|Effettuare dei test | Effettuare periodicamente il test dei controlli chiave sulle operazioni e il test di penetrazione di terze parti. | Responsabilità condivisa tra {{site.data.keyword.IBM_notm}} e il cliente |
|Segnalazione dello stato, coordinamento dei controlli e incontri di conformità  | Completare la segnalazione dello stato, il coordinamento del controllo esterno e la rappresentazione negli incontri sullo stato di revisione della conformità. | {{site.data.keyword.IBM_notm}} |
|Verifica dell'occupazione lavorativa e delle esigenze aziendali | Completare la verifica trimestrale dell'occupazione lavorativa e la verifica delle continue esigenze aziendali per i rappresentanti {{site.data.keyword.IBM_notm}} che hanno accesso all'ambiente del cliente. | {{site.data.keyword.IBM_notm}} |
|Risoluzione delle vulnerabilità di sicurezza | Risolvere le vulnerabilità di sicurezza segnalate nella piattaforma. | {{site.data.keyword.IBM_notm}} |
{: caption="Table 6. Progression phase tasks" caption-side="top"}

La fase finale di completamento rappresenta la fine del rapporto tra te e {{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}}. Le attività principali per questa fase sono le seguenti:

* Termine dell'accordo finanziario
* Rimozione di tutte le connessioni di rete
* Riciclaggio dell'infrastruttura

| **Attività** | **Dettagli attività** | **Parte responsabile** |
|----------|------------------|-----------------------|
|Terminare l'accordo finanziario | Discutere e concordare un termine per il contratto dell'accordo finanziario. | Responsabilità condivisa tra {{site.data.keyword.IBM_notm}} e il cliente |
|Rimuovere le autorizzazioni per l'ambiente | Disattivare l'accesso e le credenziali per l'ambiente. | Responsabilità condivisa tra {{site.data.keyword.IBM_notm}} e il cliente |
|Arrestare Relay | Interrompere la connessione Relay. | {{site.data.keyword.IBM_notm}} |
|Riciclare l'infrastruttura | Riciclare l'infrastruttura in base alle direttive aziendali. | Cliente |
{: caption="Table 7. Completion phase tasks" caption-side="top"}


## Requisiti infrastruttura {{site.data.keyword.Bluemix_local_notm}}
{: #localinfra}

Per {{site.data.keyword.Bluemix_local_notm}}, la sicurezza fisica e l'infrastruttura per ospitare l'istanza locale sono di tua competenza. I requisiti dell'infrastruttura sono gli stessi anche se scegli di utilizzare e gestire la tua propria VMware o acquistare il sistema {{site.data.keyword.Bluemix_local_notm}} che include l'applicazione PureApp ordinata da IBM. Tuttavia, esistono due opzioni per l'applicazione PureApp che hai scelto durante l'ordine e il processo di ridimensionamento fa differenza tra VMware e il sistema {{site.data.keyword.Bluemix_local_notm}}. Per ulteriori informazioni sulle opzioni dell'applicazione PureApp, vedi [IBM {{site.data.keyword.Bluemix_notm}} Local System W3500 and W3550 models run cloud native services, enabled middleware, and open pattern workloads concurrently ![icona link esterno](../icons/launch-glyph.svg)](https://www-01.ibm.com/common/ssi/rep_ca/5/897/ENUS216-325/){: new_window}.

{{site.data.keyword.IBM_notm}} imposta i seguenti requisiti minimi per la configurazione di {{site.data.keyword.Bluemix_local_notm}}.

### Hardware

Anche se ci sono dei requisiti per il tipo e la dimensione di hardware disponibile, puoi scegliere qualsiasi combinazione per soddisfare i requisiti totali di risorse.

<dl>
<dt>**Hardware VMware ESXi**</dt>
<dd>
ESXi è un livello di virtualizzazione che viene eseguito sui server fisici e che astrae processore, memoria, archiviazione e risorse in più macchine virtuali. Scegli qualsiasi combinazione che soddisfi i seguenti totali di risorse, a condizione che il conteggio di core fisici minimo per ESXi sia otto. Le seguenti specifiche sono relative solo al runtime core di {{site.data.keyword.Bluemix_notm}}.
<ul>
<li>32 core fisici a 2.0 o più GHz ciascuno</li>
<li>512 GB di RAM fisica</li>
<li>Dimensione archivio dati totale di 7,5 TB
<ul>
<li>Archivio dati di 7 TB per contenere {{site.data.keyword.Bluemix_notm}}</li>
<li>Archivio dati di 500 GB per contenere la macchina virtuale di inizio</li>
</ul>
</li>
</ul>
<p><strong>Nota:</strong> se utilizzi più archivi dati, utilizza lo stesso prefisso per ognuno.</p>
</dd>
<dt>**Alta disponibilità**</dt>
<dd>
Per supportare il malfunzionamento di un singolo nodo, devi disporre di n+1 ESXi. Ad esempio, se la condizione di 32 core e 512 GB di memoria viene soddisfatta utilizzando due server da 16x core con 256 GB ESXi, avrai bisogno di tre di questi server per supportare un errore completo di un singolo nodo.
<p><strong>Nota:</strong> l'amministratore VMware dei clienti può decidere di implementare un rigido failover dell'alta disponibilità nel cluster per garantire le risorse. Se scegli di procedere senza il failover dell'alta disponibilità, puoi soddisfare il requisito minimo di risorsa di 32 core e 512 GB.</p>
</dd>
<dt>**Rete**</dt>
<dd>
I requisiti consigliati includono un gruppo di porte accessibili ai clienti con sette indirizzi IP di rete cliente con accesso Internet in uscita nella stessa sottorete. Due porte sono utilizzate dalla macchina virtuale di inizio, tre porte sono degli indirizzi IP virtuali utilizzati per i domini e le ultime due sono indirizzi IP pubblici per i DataPower. Definisci quindi una seconda VLAN privata tra i soli ESXi utilizzati per {{site.data.keyword.Bluemix_local_notm}}. Questa VLAN viene visualizzata come un gruppo di porte in VMware. {{site.data.keyword.Bluemix_local_notm}} lo utilizza per la sottorete privata, che è più sicura e può contribuire a evitare problemi di instradamento.<br />
<p>Sono utilizzate le seguenti porte:</p>
<ul>
<li>Porta 443 per la connessione Relay
<p>**Nota**: se scegli di utilizzare un tunnel IPSec invece di OpenVPN, apri una porta cliente per questa connessione.</p></li>
<li>Porta 389 o SSL 636 per la connessione LDAP o Active Directory</li>
</ul>
<p>**Nota**: {{site.data.keyword.IBM_notm}} può rilevare interruzioni nelle connessioni di rete. Nel caso in cui la connessione di rete venga interrotta, {{site.data.keyword.IBM_notm}} ti contatterà e collaborerà con il tuo specialista di rete per risolvere il problema.</p>
</dd>
<dt>**Uplink della rete**</dt>
<dd>Utilizza due o più interfacce da 1 a 10 Gbps, a seconda del carico di lavoro previsto per il sistema.</dd>
</dl>

### Configurazione del server vCenter

Riesamina i seguenti requisiti di versione, datacenter, pool di risorse e archivio dati.

<dl>
<dt>**Versioni VMware supportate**</dt>
<dd>vCenter ed ESXi 5.1, 5.5 e 6.0</dd>
<dt>**Tipi VMware supportati**</dt>
<dd>vSphere Enterprise<br />
vSphere Enterprise Plus, se intendi utilizzare gli switch virtuali distribuiti</dd>
<dt>**Datacenter**</dt>
<dd>Crea un datacenter, se non ne esiste uno.</dd>
<dt>**Cartella Datacenter**</dt>
<dd>Crea una cartella di macchina virtuale con lo stesso nome del cluster, se non intendi concedere l'accesso come amministratore propagato dal datacenter.</dd>
<dt>**Cluster**</dt>
<dd>Crea un cluster specificamente per l'utilizzo da parte di {{site.data.keyword.Bluemix_local_notm}}. Un esempio per il nome cluster è `bluemix`.</dd>
<dt>**Pool di risorse**</dt>
<dd>Crea un pool di risorse nel cluster {{site.data.keyword.Bluemix_local_notm}}. Un esempio per il nome di pool di risorse è `local`.</dd>
</dt>**Archivi dati**</dt>
<dd>Richiede 7,5 TB per la distribuzione iniziale di {{site.data.keyword.Bluemix_notm}}.<br />
<br />
**Nota**: quando utilizzi più di un archivio dati, assicurarti che ciascuno inizi con lo stesso prefisso. Degli esempi di più nomi di archivio dati con lo stesso prefisso sono `bluemix_datastore_01` e `bluemix_datastore_02`.</dd>
<dt>**Rete**</dt>
<dd>Devi disporre di un'unica rete accessibile ai clienti con funzionalità Internet in uscita. La VLAN ospita la sottorete privata in cui vengono eseguiti i componenti Bluemix locale. Tutto il traffico viene instradato dalla sottorete privata alla sottorete del cliente. Un IP della sottorete del cliente viene utilizzato per tutti gli accessi a Bluemix locale. Quindi, è possibile definire una seconda VLAN privata tra i soli ESXi utilizzati per Bluemix locale. Questa VLAN viene visualizzata come un gruppo di porte in VMware. Bluemix locale la utilizza per la sottorete privata, che è maggiormente protetta e può aiutare a evitare problemi di instradamento.
<p>Se utilizzi dei vDS (vSphere Distributed Switch), crea una cartella contenitore per il vDS e inseriscilo al suo interno.</p>
</dl>

### Larghezza di banda della rete per Relay

La velocità effettiva consigliata è 5 Mbps in upload e 5 Mbps in download, e puoi prevedere un utilizzo di dati mensile di 10 GB. Quando vengono consegnate grandi raccolte di dati, che possono raggiungere i 4 GB, {{site.data.keyword.IBM_notm}} stabilisce delle finestre concordate.

### Autorizzazioni VMware

Imposta i ruoli e le autorizzazioni di seguito indicati. La propagazione è impostata per ciascuna autorizzazione. Se l'autorizzazione viene propagata, viene passata verso il basso nella gerarchia degli oggetti. Tuttavia, le autorizzazioni per un oggetto secondario sovrascrivono sempre le autorizzazioni propagate da un oggetto principale.

<dl>
<dt>**Server vCenter**</dt>
<dd>Imposta il ruolo come di sola lettura e non propagato.<br />
<br />
**Nota**: questo ruolo è necessario per richiamare lo stato attività per specifiche operazioni di disco.</dd>
<dt>**Datacenter**</dt>
<dd>Crea il ruolo "{{site.data.keyword.Bluemix_notm}}" e concedi le seguenti autorizzazioni:
<ul>
<li>Per l'**archivio dati**, imposta **Operazioni su file di basso livello** e **Aggiorna file macchina virtuale**.</li>
<li>Per **vApp**, imposta **Importa**.</li>
<li>Per il gruppo **dvPort**, imposta **Modifica**. Verrà utilizzato esclusivamente dai vDS.</li>
</ul>
**Nota**: questo ruolo è necessario per supportare gli inserimenti di file negli archivi dati.</dd>
<dt>**Cluster**</dt>
<dd>Imposta il ruolo come amministratore e propagato.</dd>
<dt>**Archivi dati**</dt>
<dd>Imposta il ruolo come amministratore e propagato per ciascun archivio dati {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>**Rete**</dt>
<dd><ul>
<li>Per vSwitch, imposta i gruppi di porte pubbliche e private, con il ruolo amministratore e non propagato.</li>
<li>Per la cartella principale vDS, imposta come in sola lettura e propagata.</li>
<li>Per vDS, imposta i gruppi di porte pubbliche e private con il ruolo amministratore e non propagato.</li>
</ul>
</dd>
</dl>

### Ridimensionamento del tuo ambiente

#### Opzione VMware

Se hai scelto di fornire la tua propria opzione hardware VMware basata su specifiche minime, hai configurato 64 GB di memoria disponibile. Se vuoi aggiungere 16 o 32 GB, devi lavorare con il tuo team hardware per fornire la memoria disponibile o aggiungere un server ESXi, se necessario come descritto nel seguente esempio. Quando la capacità hardware è disponibile, lavora con il tuo CSM (client success manager) che può lavorare con il team IBM per gestire l'incremento della memoria di calcolo.

Per incrementare il pool DEA, ogni DEA viene configurata con:

- 16 o 32 GB di RAM
- 2x o 4x vCPU
- 150 o 300 GB di archiviazione

Ad esempio, se la dimensione dell'host ESXi è 256 GB di memoria con 16x core, vengono aggiunti otto DEA. Se la dimensione dell'host ESXi è 64 GB di memoria con 8x core, è richiesta l'aggiunta di due ESXi e quattro DEA. Sono richiesti 1,5 TB di archiviazione aggiuntivi per ogni quattro DEA. Questo esempio è basato su un DEA configurato con 32 GB di RAM, 4x vCPU e 300 GB di archiviazione.


#### Opzione sistema Bluemix locale

Se hai scelto di ordinare l'hardware PureApplication tramite {{site.data.keyword.IBM_notm}} per ospitare la tua istanza {{site.data.keyword.Bluemix_notm}} locale, devi ordinare un altro nodo di calcolo nella dimensione di specifica che hai precedentemente acquistato. Puoi ordinare un altro nodo tramite il tuo CSM (client success manager) che lavora con il team IBM per ottenere che l'hardware aggiornato di venga direttamente spedito. Una volta che l'hardware è stato consegnato e installato, IBM viene notificata e il team di distribuzione aggiunge ulteriori 64 GB. A seconda della dimensione del nodo di calcolo che hai ordinato, potresti avere ulteriore capacità disponibile per aggiornamenti futuri. In questo caso, dovrai semplicemente contattare IBM e il team può aggiungere ulteriori incrementi di 64 GB di memoria di calcolo disponibile quando necessario.

## Gestione della tua istanza locale
{: #maintainlocal}

{{site.data.keyword.IBM_notm}} effettua la manutenzione e l'installazione di aggiornamenti e correzioni ai runtime e ai servizi di {{site.data.keyword.Bluemix_notm}} come {{site.data.keyword.IBM_notm}} ritiene appropriato. I servizi potrebbero non essere disponibili durante le finestre di manutenzione. Inoltre, {{site.data.keyword.IBM_notm}} collabora con te per pianificare gli aggiornamenti di manutenzione per la piattaforma {{site.data.keyword.Bluemix_notm}}.

### Manutenzione di {{site.data.keyword.Bluemix_notm}}

Per {{site.data.keyword.Bluemix_local_notm}} sono richiesti i seguenti tipi di manutenzione:

<dl>
<dt>**Manutenzione standard per i servizi**</dt>
<dd>I servizi utilizzano delle finestre di manutenzione standard predefinite, che potrebbero causare la non disponibilità del servizi. {{site.data.keyword.IBM_notm}} non richiede l'approvazione dei clienti per eseguire la manutenzione dei servizi, ma prova a ridurre al minimo l'impatto sui tuoi servizi.<br />
<br />
{{site.data.keyword.IBM_notm}} invia dei messaggi di broadcast che descrivono in modo dettagliato le modifiche pianificate per ciascuna finestra di manutenzione nella pagina Stato.<br />
<br />
**Importante**: alcuni servizi potrebbero non essere a tua disposizione durante il periodo di manutenzione.</dd>

<dt>**Manutenzione standard per la piattaforma {{site.data.keyword.Bluemix_notm}}**</dt>
<dd>Gli aggiornamenti di manutenzione vengono applicati in base al coordinamento tra te e {{site.data.keyword.IBM_notm}} entro una finestra di 21 giorni. Fornisci a {{site.data.keyword.IBM_notm}} le finestre di manutenzione preapprovate e le date o gli orari specifici che potrebbero non andare bene per te; {{site.data.keyword.IBM_notm}} cercherà di pianificare gli aggiornamenti durante o intorno alle date da te selezionate.<br />
<p>Vai a **AMMINISTRAZIONE > INFORMAZIONI DI SISTEMA** per visualizzare gli aggiornamenti di manutenzione pianificati e in sospeso. Per ulteriori informazioni sull'impostazione delle tue finestre preapprovate, e la visualizzazione o l'approvazione degli aggiornamenti di manutenzione pianificati, vai a <a href="../admin/index.html#oc_schedulemaintenance">Aggiornamenti di manutenzione</a>.</p></dd>
</dl>

**Importante**: {{site.data.keyword.IBM_notm}} si riserva il diritto di interrompere i servizi per applicare la manutenzione di emergenza a seconda delle necessità. {{site.data.keyword.IBM_notm}} potrebbe modificare le ore di manutenzione pianificate, ma verrai avvisato di tali modifiche nonché di tutte le informazioni relative alla manutenzione di emergenza.

Se viene segnalato un problema dopo l'aggiornamento di manutenzione, insieme al rappresentante del supporto {{site.data.keyword.Bluemix_notm}} puoi stabilire se sia utile consentire a {{site.data.keyword.IBM_notm}} di eseguire il rollback dell'aggiornamento. Previo accordo, {{site.data.keyword.IBM_notm}} esegue il rollback dell'aggiornamento per ripristinare l'ambiente allo stato precedente.

### Manutenzione dell'infrastruttura del cliente
{: #inframaintenance}

{{site.data.keyword.Bluemix_local_notm}} viene distribuito sull'hypervisor ESXi e l'applicazione vCenter viene utilizzata per gestire centralmente le macchine virtuali e gli host ESXi. {{site.data.keyword.Bluemix_notm}} supporta le ultime tre versioni di ESXi e vCenter, compresi tutti gli aggiornamenti e le patch intermedi. Per informazioni sulle ultime versioni supportate, consulta la documentazione [Requisiti dell'infrastruttura locale](../local/index.html#localinfra).

**Importante**: con la distribuzione di {{site.data.keyword.Bluemix_local_notm}} locale sull'hypervisor ESXi, aggiornamenti e patch per ESXi possono ostacolare la disponibilità dell'ambiente locale, incluse tutte le applicazioni e i servizi in esecuzione nell'ambiente. Invia una notifica a {{site.data.keyword.Bluemix_notm}} attraverso un ticket di supporto prima di completare un aggiornamento o una patch, per far sì che l'interruzione del servizio non allerti il team operativo interessato. Se ti è stato assegnato un client success manager (CSM), puoi comunicargli la pianificazione dell'aggiornamento.

Per accertarti che la tua istanza locale sia compatibile con le ultime versioni supportate, il team operativo {{site.data.keyword.Bluemix_notm}} monitora l'ambiente per accertarsi che non siano presenti versioni non supportate che potrebbero non corrispondere agli ultimi aggiornamenti dell'ambiente {{site.data.keyword.Bluemix_notm}} locale. Alcuni aggiornamenti di {{site.data.keyword.Bluemix_notm}}, quali gli aggiornamenti della versione di Cloud Foundry, richiedono l'aggiornamento del software ESXi o vCenter. Il supporto {{site.data.keyword.Bluemix_notm}} ti allerterà sugli aggiornamenti, comunicandoti quali eseguire ed entro che data. L'aggiornamento deve essere completato entro la finestra temporale indicata.

{{site.data.keyword.Bluemix_notm}} fa il possibile per preservare la compatibilità degli ambienti locali con le ultime versioni di ESXi e vCenter. Tuttavia, potrebbero presentarsi brevi periodi di tempo in cui le versioni più recenti di ESXi e vCenter non sono supportate. Fai riferimento alla documentazione [Requisiti dell'infrastruttura locale](/docs/local/index.html#localinfra) per individuare le ultime versioni compatibili prima di procedere a qualsiasi aggiornamento.


## Risposta e supporto agli incidenti per {{site.data.keyword.Bluemix_local_notm}}
{: #incidentresponse}

### Problemi rilevati dal cliente

Se identifichi un problema che richiede un intervento e attenzione da parte del supporto {{site.data.keyword.IBM_notm}}, puoi contattarlo in vari modi. Per informazioni su come contattare il supporto, vedi [Come contattare il supporto](../support/index.html#contacting-bluemix-support-local). A seconda del problema, dovrà essere risolto da te e/o da IBM.

### Incidenti critici rilevati da IBM

Gli incidenti critici sono interruzioni dei servizi impreviste con carattere d'urgenza e problemi di stabilità che colpiscono il tuo ambiente o i tuoi utenti. Se {{site.data.keyword.IBM_notm}} individua un incidente critico nel proprio ambiente, te lo comunica tramite notifica nella pagina **Stato**. Puoi consultare la pagina Stato anche per eventuali problemi noti relativi alla piattaforma o ai tuoi servizi. Per ulteriori informazioni sulla pagina Stato, consulta [Visualizzazione dello stato](../admin/index.html#oc_status).

Se desideri integrare le tue notifiche con un servizio Web che supporti gli hook Web, vedi [Notifiche e sottoscrizioni di eventi](/docs/admin/index.html#oc_eventsubscription) per informazioni su come estendere le funzioni di notifica.

![Processo di risposta agli eventi incidenti](images/incidentresponseprocess.png "Processo di risposta agli incidenti")

Figura 2. Processo di risposta agli incidenti

A seconda del problema, dovrà essere risolto da te e/o da IBM. Se hai domande sull'incidente o se hai bisogno che un rappresentante {{site.data.keyword.IBM_notm}} ti aiuti a risolvere il problema, puoi aprire un ticket di supporto. Per informazioni su come contattare il supporto, vedi [Come contattare il supporto](../support/index.html#contacting-bluemix-support-local).

**Nota**: i ticket di supporto con severità 1 vengono monitorati 24 ore al giorno, 7 giorni a settimana. Gli altri ticket vengono elaborati dalle 22:00 GMT di domenica alle 12:00 GMT di sabato. Per ulteriori informazioni sulla severità dei ticket di supporto e sull'utilizzo del supporto, vedi <a href="/docs/support/index.html#contacting-bluemix-support-local">Come contattare il supporto</a>.

## Ripristino di emergenza per {{site.data.keyword.Bluemix_local_notm}}
{: #dr}

Il ripristino di emergenza per {{site.data.keyword.Bluemix_short}} locale può essere configurato in modo analogo a quello valido quando si utilizza {{site.data.keyword.Bluemix_short}} pubblico. {{site.data.keyword.Bluemix_short}} pubblico fornisce una piattaforma costantemente disponibile per l'innovazione con più misure di sicurezza per garantire che le tue organizzazioni, i tuoi spazi e le tue applicazioni siano sempre disponibili. La distribuzione delle applicazioni in più regioni geografiche consente una disponibilità continua che protegge contro l'imprevista perdita simultanea di più componenti hardware o software o la perdita di un intero data center; in tal modo, anche in caso di catastrofe naturale in una posizione geografica, le istanze distribuite della tua applicazione {{site.data.keyword.Bluemix_notm}} pubblico saranno disponibili in posizioni geografiche alternative.
{: shortdesc}

Il ripristino di emergenza per {{site.data.keyword.Bluemix_short}} locale è reso possibile grazie alla disponibilità continua per le tue applicazioni, all'alta disponibilità intrinseca della piattaforma e alla possibilità di ripristinare l'istanza in caso di errore. Sei responsabile dell'abilitazione della disponibilità continua delle tue applicazioni mediante la distribuzione a più regioni. L'alta disponibilità viene integrata a livello della piattaforma tramite le tecnologie incluse in Cloud Foundry e altri componenti. Inoltre, puoi collaborare con {{site.data.keyword.IBM_notm}} per assicurarti che il backup dei tuoi dati venga eseguito correttamente nel caso in cui sia necessario ripristinare la tua istanza.

### Abilitazione della disponibilità continua per {{site.data.keyword.Bluemix_local_notm}}
{: #enabling}

Per impostazione predefinita, {{site.data.keyword.Bluemix_notm}} pubblico viene distribuito in più posizioni geografiche. Tuttavia, per abilitare le istanze {{site.data.keyword.Bluemix_local_notm}} distribuite a livello globale, devi effettuare le seguenti attività:

* Assicurati che gli sviluppatori stiano distribuendo le applicazioni in più di una regione, mediante un processo manuale o automatico. Le regioni selezionate dovrebbero trovarsi a più di 200 km di distanza l'una dall'altra per garantire che, in caso di catastrofe naturale, non vengano colpite entrambe le posizioni geografiche.
* Configurare un programma di bilanciamento del carico globale, come Akamai o Dyn, per puntare ad applicazioni in almeno due regioni diverse.

**Nota**: non tutti i servizi {{site.data.keyword.Bluemix_notm}} supportano la distribuzione regionale. Quando crei un'applicazione, se vuoi garantire una distribuzione geografica, devi fare in modo che i servizi utilizzati dall'applicazione abbiano come funzione fondamentale la sincronizzazione dei dati.

#### Distribuzione di applicazioni {{site.data.keyword.Bluemix_local_notm}} in più posizioni geografiche
{: #deploying}

Per eseguire la distribuzione in una seconda posizione o in più posizioni, devi seguire un processo simile a quello effettuato per abilitare la posizione geografica primaria:

1. Abilita un nuovo ambiente locale per ospitare istanze aggiuntive delle tue applicazioni. Per creare un nuovo ambiente, contatta il team del settore vendite {{site.data.keyword.IBM_notm}} per avviare il processo. Per ulteriori informazioni sulla configurazione di un'istanza locale, vedi [Configurazione di {{site.data.keyword.Bluemix_local_notm}}](../local/index.html#setuplocal). Devi effettuare un accesso distinto per ogni ambiente. Ciascuna posizione fisica degli ambienti host deve trovarsi ad almeno 200 km di distanza dalla posizione originale per garantire la disponibilità.
2. Ottieni il nome di dominio univoco in cui verrà ospitata la tua nuova applicazione distribuita. Ad esempio, se il dominio originale è *mycompany.caeast.bluemix.net*, puoi creare un nuovo ambiente locale con un nuovo dominio come, ad esempio, *mycompany.cawest.bluemix.net* e distribuire al nuovo dominio.
3. Esegui la distribuzione nella nuova posizione ogni volta che distribuisci l'applicazione originale. Per ulteriori informazioni sulla distribuzione, vedi [Caricamento della tua applicazione](/docs/starters/upload_app.html).


#### Abilitazione di un programma di bilanciamento del carico globale per {{site.data.keyword.Bluemix_local_notm}}
{: #glb}

Un programma di bilanciamento del carico globale non solo garantisce la disponibilità continua ed è richiesto per il ripristino di emergenza, ma presenta anche diversi vantaggi aggiuntivi:

* Indirizza gli utenti alla regione {{site.data.keyword.Bluemix_notm}} più vicina per impostazione predefinita
* Indirizza in base alle prestazioni
* Instrada selettivamente una percentuale di traffico a una nuova versione dell'applicazione
* Fornisce il failover del sito in base alla verifica dell'integrità della regione
* Fornisce il failover del sito in base alla verifica dell'integrità dell'applicazione
* Utilizza un instradamento ponderato tra gli endpoint

Puoi scegliere un programma di bilanciamento del carico globale come Akamai o Dyn. Per ulteriori informazioni sull'utilizzo di Akamai come programma di bilanciamento del carico globale, vedi [Global traffic management ![icona link esterno](../icons/launch-glyph.svg)](https://www.akamai.com/us/en/solutions/products/web-performance/global-traffic-management.jsp){: new_window}. Per ulteriori informazioni sull'utilizzo di Dyn come programma di bilanciamento del carico globale, vedi [4 Reasons Businesses Are Taking Global Load Balancing to the Cloud ![icona link esterno](../icons/launch-glyph.svg)](http://dyn.com/blog/4-reasons-businesses-are-taking-global-load-balancing-to-the-cloud/){: new_window}.

### Alta disponibilità
{: #ha}

Oltre a consentire la disponibilità continua, {{site.data.keyword.Bluemix_notm}} fornisce anche l'alta disponibilità in tutta la piattaforma utilizzando le tecnologie integrate in Cloud Foundry e altri componenti.

Queste tecnologie includono:

<dl>
<dt>Scalabilità in Cloud Foundry DEA</dt>
<dd>Un <a href="https://docs.cloudfoundry.org/concepts/architecture/execution-agent.html" target="_blank">DEA (Droplet Execution Agent) <img src="../icons/launch-glyph.svg" alt="icona link esterno">
</a> Cloud Foundry effettua verifiche dell'integrità nelle applicazioni eseguite al suo interno. Se si verifica un problema con l'applicazione o con lo stesso DEA, distribuisce ulteriori istanze dell'applicazione a un DEA alternativo per risolvere il problema. Per ulteriori informazioni, vedi <a href="https://docs.cloudfoundry.org/concepts/high-availability.html" target="_blank">Configuring CF for High Availability with Redundancy <img src="../icons/launch-glyph.svg" alt="icona link esterno">
</a>.
<p>Per garantire l'elevata disponibilità per le tue applicazioni, hai bisogno di abbastanza risorse di elaborazione per bilanciare il carico e puoi inoltre richiederne ulteriori per supportare un possibile malfunzionamento. Se hai bisogno di ridimensionare il tuo ambiente incrementando il tuo pool DEA in modo da essere preparato a un malfunzionamento o per affrontare un'anomalia durante il caricamento delle tue istanze dell'applicazione, puoi collaborare con il tuo rappresentante IBM per ordinare ulteriori DEA e per verificare di avere l'hardware appropriato per supportare le risorse aggiunte.
</p>
</dd>
<dt>Backup dei metadati</dt>
<dd>I metadati vengono sottoposti a backup in una posizione secondaria, in genere una macchina virtuale installata in loco. Se possibile, dovresti replicare il backup nel tuo ambiente ad almeno 200 km di distanza.</dd>
</dl>

## Ripristino della tua istanza locale
{: #restorelocal}

Il backup di impostazioni, metadati e configurazioni di {{site.data.keyword.Bluemix_local_notm}} viene eseguito periodicamente come tutela in caso di eventuali interruzioni non pianificate nell'ambiente. I dati per i quali sei responsabile del backup includono i dati dell'applicazione, i dati dei servizi del database cloud e gli archivi oggetti.

Come parte del backup dei dati, che include i metadati del sistema e le configurazioni, {{site.data.keyword.IBM_notm}} completa le seguenti attività:

<ul>
<li>Crittografa tutte le copie di backup e gestisce le chiavi di crittografia</li>
<li>Monitora e gestisce l'attività di backup</li>
<li>Fornisce i file di backup crittografati</li>
<li>Ripristina i dati richiesti</li>
<li>Gestisce i conflitti di pianificazione tra le operazioni di gestione dei backup e delle correzioni</li>
</ul>

Poiché la protezione dei dati privati è di importanza critica, {{site.data.keyword.IBM_notm}} ha bisogno della tua collaborazione quando si occupa della gestione dei file di backup in modo che i file non vengano spostati all'esterno dei tuoi data center. Nello specifico, {{site.data.keyword.IBM_notm}} richiede che tu completi le seguenti attività:

<ul>
<li>Spostare una copia dei tuoi dati di backup crittografati fuori sede, proprio come faresti per qualsiasi altro dato di backup da te gestito.</li>
<li>Fornire i file di backup per l'amministratore {{site.data.keyword.IBM_notm}} nel caso occorra eseguire un ripristino.</li>
</ul>

# rellinks
{: rellinks}
## general
{: general}
* [Scopri: {{site.data.keyword.Bluemix_local_notm}} ![icona link esterno](../icons/launch-glyph.svg)](http://www.ibm.com/cloud-computing/bluemix/hybrid/local/){: new_window}
* [Novità in {{site.data.keyword.Bluemix_notm}}](/docs/whatsnew/index.html)
* [{{site.data.keyword.Bluemix_notm}} glossario](/docs/overview/glossary/index.html)
* [Managing {{site.data.keyword.Bluemix_local_notm}} e {{site.data.keyword.Bluemix_notm}} dedicato](/docs/admin/index.html#mng)
* [Come contattare il supporto](/docs/support/index.html#getting-customer-support)
