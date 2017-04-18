---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-4"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Informazioni sulla Fornitura continua  
{: #cd_about}  

Con {{site.data.keyword.contdelivery_full}}, puoi creare, testare e fornire applicazioni utilizzando le procedure e gli strumenti leader nel settore DevOps.
{:shortdesc}

Il servizio {{site.data.keyword.contdelivery_short}} supporta i tuoi flussi di lavoro DevOps:

 * Puoi creare [toolchain](/docs/services/ContinuousDelivery/toolchains_about.html){: new_window} DevOps integrate per abilitare le integrazioni dello strumento che supportano le tue attività di sviluppo, distribuzione e operative.

  Una toolchain è una serie integrata di strumenti che puoi utilizzare per sviluppare, costruire, distribuire, testare e gestire le applicazioni in modo collaborativo. Puoi creare toolchain che includano servizi {{site.data.keyword.Bluemix_notm}}, strumenti open source e strumenti di terzi parti, come ad esempio GitHub, PagerDuty e Slack, in modo che le attività di sviluppo e operative siano ripetibili e più facili da gestire.

 * Fornitura continua mediante [pipeline](/docs/services/ContinuousDelivery/pipeline_about.html){: new_window} automatizzate.

  Automatizza creazioni, verifiche di unità, distribuzioni e altro ancora. Crea, verifica e distribuisci in modo ripetibile con il minimo intervento umano. Tieniti pronto per il rilascio in produzione in qualsiasi momento,

 * Modifica ed esegui il push del tuo codice da qualsiasi luogo utilizzando l'[IDE basato su Web](/docs/services/ContinuousDelivery/web_ide.html){: new_window}.

  Crea, modifica, esegui e completa le attività di controllo origine in GitHub ed eseguine il debug. Passa facilmente dalla modifica del tuo codice alla sua distribuzione in produzione.

 * Migliora la qualità tramite [{{site.data.keyword.DRA_short}}](/docs/services/ContinuousDelivery/di_working.html){: new_window}.

  Comprendi le dinamiche del tuo team man mano sviluppa e fornisce il codice. Scopri come gli utenti interagiscono con la tua applicazione. Riesamina i dati per aiutarti nella gestione delle operazioni della tua applicazione.


## Disponibilità della toolchain su Bluemix Pubblico in confronto a Bluemix Dedicato
{: #public_and_dedicated}

{{site.data.keyword.Bluemix_notm}} Pubblico è una piattaforma a standard aperti e basata sul cloud per creare, eseguire e gestire le applicazioni a cui accede [http://bluemix.net ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://bluemix.net){:new_window}. {{site.data.keyword.Bluemix_notm}} Dedicato fornisce le funzionalità di {{site.data.keyword.Bluemix_notm}} in un ambiente SoftLayer dedicato collegato in modo sicuro all'ambiente {{site.data.keyword.Bluemix_notm}} Pubblico e alla tua rete. L'ambiente {{site.data.keyword.Bluemix_notm}} Dedicato della tua azienda potrebbe non contenere le stesse integrazioni dello strumento come il sito {{site.data.keyword.Bluemix_notm}} Pubblico.

Per la gestione del codice di origine e per il tracciamento del problema, {{site.data.keyword.Bluemix_notm}} Pubblico generalmente utilizza github.com. {{site.data.keyword.Bluemix_notm}} Dedicato può anche utilizzare github.com, ma normalmente utilizza {{site.data.keyword.ghe_short}} che viene installato dalla tua azienda o gestito da IBM.

{{site.data.keyword.contdelivery_short}} è disponibile su {{site.data.keyword.Bluemix_notm}} Pubblico e {{site.data.keyword.Bluemix_notm}} Dedicato. Le toolchain sono diverse a seconda se utilizzi {{site.data.keyword.contdelivery_short}} su {{site.data.keyword.Bluemix_notm}} Pubblico o {{site.data.keyword.Bluemix_notm}} Dedicato.

|Toolchain |{{site.data.keyword.Bluemix_notm}} Pubblico	|{{site.data.keyword.Bluemix_notm}} Dedicato |
|:----------|:------------------------------|:------------------|
|Integrazioni dello strumento 		|Per un elenco di integrazioni dello strumento, consulta [Configurazione delle integrazioni dello strumento](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}. 		|Le integrazioni dello strumento sono disponibili a seconda di come {{site.data.keyword.contdelivery_short}} è stato impostato nel tuo ambiente.			|
|Creazione di una toolchain da un template		|Accedi a [{{site.data.keyword.Bluemix_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://console.ng.bluemix.net/devops){:new_window}		|Accedi al tuo ambiente dedicato su {{site.data.keyword.Bluemix_notm}}.			|
|Creazione di una toolchain da un applicazione		|L'applicazione è configurata per la fornitura continua da un nuovo repository GitHub che viene popolato con il codice starter dell'applicazione. 		|L'applicazione è configurata per la fornitura continua da un nuovo repository GitHub o GitHub Enterprise che viene popolato con il codice starter dell'applicazione.		|  
|Regioni di distribuzione di Delivery pipeline		|Tutte le regioni di {{site.data.keyword.Bluemix_notm}} Pubblico sono disponibili per i lavori di distribuzione Cloud Foundry. 		|La regione di {{site.data.keyword.Bluemix_notm}} Dedicato è disponibile. Altre regioni dedicate o locali nello stesso account del cliente potrebbero essere disponibili a seconda di come {{site.data.keyword.contdelivery_short}} è stato configurato nel tuo ambiente specifico.		|
|Lavori di distribuzione di Delivery pipeline 		|Tutti i [tipi di lavoro](/docs/services/ContinuousDelivery/pipeline_about.html#deliverypipeline_jobs) sono disponibili.		|I tipi di lavoro che dipendono dai servizi {{site.data.keyword.Bluemix_notm}} non installati nell'ambiente dedicato potrebbero non essere disponibili. Ad esempio, il contenitore che crea e distribuisce i tipi di lavoro potrebbe non essere disponibile negli ambienti che non dispongono del servizio {{site.data.keyword.Bluemix_notm}} Container.	|
{: caption="Table 1. Differences between toolchains on {{site.data.keyword.Bluemix_notm}} Dedicato e {{site.data.keyword.Bluemix_notm}} Pubblico" caption-side="top"}


## Modelli toolchain
{: #templates}

Puoi utilizzare un template come punto di partenza per [creare una toolchain ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/devops/create){: new_window}. I modelli toolchain includono serie specifiche di integrazioni dello strumento che supportano le attività operative, sviluppo e distribuzione. 

**Suggerimento**: l'ambiente {{site.data.keyword.Bluemix_notm}} Dedicato della tua azienda potrebbe non contenere gli stessi modelli della toolchain del sito {{site.data.keyword.Bluemix_notm}} Pubblico. I modelli della toolchain disponibili in {{site.data.keyword.Bluemix_notm}} Pubblico e {{site.data.keyword.Bluemix_notm}} Dedicato potrebbero contenere una serie differente di integrazioni dello strumento in {{site.data.keyword.Bluemix_notm}} Dedicato.

Alcuni modelli della toolchain includono le integrazioni dello strumento come parte del servizio {{site.data.keyword.contdelivery_short}}. Se un'istanza di tale servizio non è ancora nella tua organizzazione, quando fai clic su **Crea** per creare la toolchain, il servizio viene automaticamente aggiunto senza alcun costo. Per ulteriori informazioni e termini, consulta il [Catalogo Bluemix ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/catalog/services/continuous-delivery/){:new_window}.

I modelli della toolchain dei microservizi distribuiscono un'applicazione con le API Catalogo e Ordini supportate da un negozio Cloudant. Come parte della distribuzione di un'applicazione, viene creata un'istanza del servizio Cloudant gratuita. Per ulteriori informazioni e termini, consulta il [Catalogo Bluemix ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/catalog/services/cloudant-nosql-db/){:new_window}.

|Modello |Descrizione	|
|:----------|:------------------------------|
|[Garage Method cloud-native tutorial toolchain ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fcloud-native-toolchain-tutorial){:new_window} 		|Questa toolchain illustra le procedure DevOps offerte nel metodo Garage. La toolchain è preconfigurata per la fornitura continua, il controllo dell'origine, l'automazione del test e per le operazioni e il monitoraggio automatizzati. Viene fornita con un'applicazione di esempio scritta in Node.js Express 4, che puoi ulteriormente espandere. 		|
|[Microservices toolchain with {{site.data.keyword.DRA_short}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Ftoolchain-demo){:new_window} 		|Con questa toolchain nativa nel cloud, puoi utilizzare un esempio per creare un negozio online composto da tre microservizi: un'API Catalogo, un'API Ordini e una IU che richiama entrambe le API. La toolchain è preconfigurata per la fornitura continua, il controllo dell'origine, la verifica della funzionalità, il tracciamento del problema, la modifica online e la notifica degli avvisi. 		|
|[Microservices toolchain with {{site.data.keyword.DRA_short}} (v2) ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fmicroservices-toolchain-hosted){:new_window} 		|Con questa toolchain nativa nel cloud, puoi utilizzare un esempio per creare un negozio online composto da tre microservizi: un'API Catalogo, un'API Ordini e una IU che richiama entrambe le API. La toolchain è preconfigurata per la fornitura continua, il controllo dell'origine, la verifica della funzionalità, il tracciamento del problema, la modifica online e la notifica degli avvisi. 		|
|[Secure container toolchain ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsecure-container-toolchain){:new_window} 		|Con questa toolchain, puoi sviluppare e distribuire un'applicazione del contenitore Docker sicura. Per impostazione predefinita, la toolchain utilizza un'applicazione Node.js "Hello World" di esempio ma puoi invece collegare il tuo proprio repository GitHub. La toolchain è preconfigurata per la fornitura continua con il Controllo vulnerabilità, il controllo dell'origine, il tracciamento del problema e la modifica online. 		|
|[Simple Cloud Foundry toolchain ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain){:new_window}		|Con questa toolchain, puoi sviluppare e distribuire un'applicazione Cloud Foundry. Per impostazione predefinita, questa toolchain utilizza un'applicazione Node.js "Hello world" di esempio ma puoi invece collegare il tuo proprio repository GitHub. La toolchain è preconfigurata per la fornitura continua, il controllo dell'origine, il tracciamento del problema e la modifica online.  		|
|[Simple Cloud Foundry toolchain	(v2) ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain-hosted){:new_window}	|Con questa toolchain, puoi sviluppare e distribuire un'applicazione Cloud Foundry. Per impostazione predefinita, questa toolchain clona un'applicazione Node.js "Hello world" di esempio in un repository Git ospitato da IBM, che puoi quindi modificare. La toolchain è preconfigurata per la fornitura continua, il controllo dell'origine, il tracciamento del problema e la modifica online.  		|
|[Simple Cloud Foundry toolchain with {{site.data.keyword.DRA_short}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdra-toolchain-demo){:new_window}		|Con questa toolchain nativa nel cloud, puoi utilizzare {{site.data.keyword.DRA_short}} per controllare la distribuzione di un'applicazione Cloud Foundry di esempio. Per impostazione predefinita, questa toolchain utilizza un'applicazione Node.js meteo di esempio oppure puoi collegare il tuo proprio repository GitHub.  		|
|[Simple Container toolchain ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-container-toolchain){:new_window}		|Con questa toolchain, puoi sviluppare e distribuire un'applicazione del contenitore Docker. Per impostazione predefinita, la toolchain utilizza un'applicazione Node.js "Hello World" di esempio ma puoi invece collegare il tuo proprio repository GitHub. La toolchain è preconfigurata per la fornitura continua, il controllo dell'origine, il tracciamento del problema e la modifica online.  		|
|[Delivery Insights with IBM UrbanCode Deploy ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdeliveryinsights-toolchain){:new_window}		|Con questa toolchain, puoi visualizzare le metriche di distribuzione da IBM UrbanCode Deploy. Abilita questa toolchain per comunicare con IBM UrbanCode Deploy scaricando e configurando DevOps Connect dalla pagina delle impostazioni in {{site.data.keyword.DRA_short}}. 		|
|[Deployment Risk Analytics with GitHub and Jenkins ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevopsinsights-toolchain){:new_window}		|Con questa toolchain, puoi ottenere informazioni approfondite sul tuo processo Jenkins per la distribuzione e l'integrazione continue. Puoi configurare il server Jenkins per inviare i dati a {{site.data.keyword.DRA_short}} quando i lavori sono eseguiti da Jenkins. Puoi inoltre implementare i gate di qualità per bloccare le distribuzioni basate sulle politiche. Puoi visualizzare i risultati nel dashboard Deployment Risk  in {{site.data.keyword.DRA_short}}. Se configuri un repository GitHub per indicare il repository di origine utilizzato da Jenkins, è disponibile la modifica della tracciabilità.  		|
|[Developer Insights and Team Dynamics with GitHub and JIRA ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevteaminsights-toolchain){:new_window}		|Con questa toolchain, puoi esplorare il rischio di distribuzione del tuo progetto e utilizzare l'analisi del codice sociale per comprendere i modelli dell'interazione tra gli sviluppatori. Puoi analizzare il codice di origine GitHub insieme ai problemi GitHub, JIRA o entrambi. Utilizza Developer Insights per identificare i file altamente soggetti ad errori e visualizza come il progetto sia conforme alle procedure DevOps. L'analisi del codice sociale in Team Dynamics identifica il livello di interazione tra i membri del team in modo che il team possa correggere le procedure non produttive. 		|
|[Build your own toolchain ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fempty-toolchain){:new_window}		|Questa toolchain non ha strumenti preconfigurati. Se hai già familiarità con le toolchain, puoi configurare la tua propria toolchain. 		|
{: caption="Table 2. Toolchain templates" caption-side="top"}
