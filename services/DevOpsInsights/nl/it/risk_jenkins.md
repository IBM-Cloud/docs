---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integrazione con i progetti Jenkins in formato libero

Dopo aver aggiunto {{site.data.keyword.DRA_full}} a una toolchain aperta e definito le politiche che monitora, puoi integrarlo con il tuo progetto Jenkins a formato libero. I progetti Jenkins a formato libero sono configurati e gestiti dall'interfaccia web Jenkins. 

Il plugin IBM Cloud DevOps per Jenkins integra i progetti Jenkins con le toolchain. Una *toolchain* è una serie di integrazioni dello strumento che supporta le attività di operazioni, sviluppo e distribuzione. La potenza collettiva di una toolchain è superiore alla somma delle relative integrazioni dello strumento. Le toolchain aperte fanno parte del servizio {{site.data.keyword.contdelivery_full}}. Per ulteriori informazioni sul servizio {{site.data.keyword.contdelivery_short}}, consulta [la sua documentazione](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html).

Dopo aver installato il plugin IBM Cloud DevOps, puoi pubblicare i risultati del test in {{site.data.keyword.DRA_short}}, aggiungere i gate di qualità automatizzati e tracciare il rischio di distribuzione. Puoi anche inviare notifiche del lavoro ad altri strumenti nella tua toolchain, come Slack e PagerDuty. Per aiutarti a tracciare le distribuzioni, la toolchain può aggiungere i messaggi di distribuzione ai commit Git e ai relativi problemi Git e JIRA. Puoi anche visualizzare le distribuzioni nella pagina delle connessioni della toolchain. 

Il plugin fornisce le azioni di post creazione e le CLI per supportare l'integrazione. {{site.data.keyword.DRA_short}} aggrega e analizza i risultati dagli strumenti di verifica di unità, di test funzionali, di copertura del codice, delle scansioni del codice di sicurezza statico per determinare se il tuo codice soddisfa le politiche predefinite nei gate nel tuo processo di distribuzione. Se il tuo codice non soddisfa o supera una politica, la distribuzione viene arrestata, per prevenire che vengano rilasciati dei rischi. Puoi utilizzare {{site.data.keyword.DRA_short}} come una rete di sicurezza per il tuo ambiente di fornitura continua, come un modo per implementare e migliorare gli standard nel tempo e come uno strumento di visualizzazione dei dati per aiutarti nella comprensione dello stato del tuo progetto.

## Prerequisiti
{: #jenkins_prerequisites}

Devi accedere a un server in esecuzione su un progetto Jenkins.

## Creazione di una toolchain
{: #jenkins_create}

Prima di poter integrare {{site.data.keyword.DRA_short}} con un progetto Jenkins, devi creare una toolchain. 

1. Per creare una toolchain, passa alla [Pagina Crea una toolchain](https://console.ng.bluemix.net/devops/create) e segui le istruzioni in tale pagina. 

2. Dopo aver creato la toolchain, aggiungi {{site.data.keyword.DRA_short}} ad essa. Per istruzioni, consulta la [documentazione {{site.data.keyword.DRA_short}}](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html). 

## Installazione del plugin
{: #jenkins_install}

Per prima cosa, installa il plugin sul tuo server Jenkins. Apri l'interfaccia server e quindi:

1. Fai clic su **Manage Jenkins**.
2. Fai clic su **Manage Plugins**. 
3. Fai clic sulla scheda **Available**
4. Imposta un filtro per `IBM Cloud DevOps`. 
5. Seleziona IBM Cloud DevOps.
6. Fai clic su **Download now and install after restart**. 

Il plugin è disponibile dopo i riavvii del server.  

## Configurazione dei lavori Jenkins per il dashboard Deployment Risk
{: #jenkins_configure}

Dopo aver installato il plugin, puoi integrare {{site.data.keyword.DRA_short}} nel tuo progetto Jenkins. 

Segui questa procedura per utilizzare il dashboard e i gate di Deployment Risk con il tuo progetto.

1. Apri la configurazione di ogni lavoro di cui disponi, come una creazione, una verifica o una distribuzione.

2. Aggiungi un'azione di post creazione per il tipo corrispondente:

   * Per i lavori di creazione, utilizza **Publish build information to IBM Cloud DevOps**.
   
   * Per i lavori di verifica, utilizza **Publish test result to IBM Cloud DevOps**.
   
   * Per i lavori di distribuzione, utilizza **Publish deployment information to IBM Cloud DevOps**.
   
3. Completa i campi richiesti. Questi possono variare in base al tipo di lavoro. 

   * Dall'elenco **Credentials**, seleziona i tuoi ID e password {{site.data.keyword.Bluemix_notm}}. Se non sono salvati in Jenkins, fai clic su **Add** per aggiungerli e salvarli. Verifica la tua connessione con {{site.data.keyword.Bluemix_notm}} facendo clic su **Test Connection**.
   
   * Nel campo **Build Job Name**, specifica il tuo nome del lavoro di build esattamente come è in Jenkins. Se la build si verifica con il lavoro di verifica, lascia questo campo vuoto. Se il lavoro di build si verifica al di fuori di Jenkins, seleziona la casella di spunta **Builds are being done outside of Jenkins** e specifica il numero e l'URL di build.
   
   * Per l'ambiente, se le verifiche sono in esecuzione nella fase di build, seleziona solo l'ambiente di build. Se le verifiche sono in esecuzione nella fase di distribuzione, seleziona l'ambiente di distribuzione e secifica il nome dell'ambiente. Sono supportati due valori: `STAGING` e `PRODUCTION`.
   
   * Per il campo **Result File Location**, specifica l'ubicazione del file del risultato. Se il test non genera un file del risultato, lascia questo campo vuoto. Il plugin carica un file del risultato predefinito basato sullo stato del lavoro di verifica corrente.

   Queste immagini illustrano le configurazioni di esempio:
   
   ![Carica informazioni di build](images/Upload-Build-Info.png "Pubblica le informazioni di build su DRA")
   *Pubblica le informazioni di build*
   
   ![Carica il risultato del test](images/Upload-Test-Result.png "Pubblica il risultato del test su DRA")
   *Pubblica il risultato del test*
   
   ![Carica le informazioni di distribuzione](images/Upload-Deployment-Info.png "Pubblica le informazioni di distribuzione su DRA")
   *Pubblica le informazioni di distribuzione*

4. Se desideri utilizzare i gate della politica {{site.data.keyword.DRA_short}} per controllare un lavoro di distribuzione di downstream, aggiungi un'azione di post creazione, **IBM Cloud DevOps Gate**. Scegli una politica e specifica lo scopo dei risultati del test. Per consentire ai gate della politica di evitare le distribuzioni di downstream, seleziona la casella di spunta **Fail the build based on the policy rules**. La seguente immagine mostra una configurazione di esempio:

    ![Gate DevOps Insights](images/DRA-Gate.png "Gate DevOps Insights")

5. Esegui il tuo lavoro di creazione Jenkins.

6. Visualizza il dashboard Deployment Risk passando a [IBM Bluemix DevOps](https://console.ng.bluemix.net/devops), selezionando la tua toolchain e facendo clic su **DevOps Insights**.

Il dashboard Deployment Risk si basa sulla presenza di un gate dopo un lavoro di distribuzione di preparazione. Se desideri utilizzare il dashboard, assicurati di avere un gate dopo aver distribuito l'ambiente in fase di preparazione, ma prima di distribuire un ambiente di produzione.
    
## Configurazione delle notifiche
{: #jenkins_notifications}

Puoi configurare i tuoi lavori Jenkins in modo da inviare notifiche agli strumenti come Slack o PagerDuty seguendo le istruzioni nei [Documenti Bluemix](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins).
